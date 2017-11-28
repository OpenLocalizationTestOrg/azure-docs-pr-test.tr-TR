---
title: "aaaAvailability ve Azure Event Hubs tutarlılık | Microsoft Docs"
description: "Nasıl tooprovide hello en büyük miktarda kullanılabilirlik ve Azure Event Hubs kullanarak tutarlılık bölümler."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="157d7-103">Kullanılabilirlik ve Event Hubs tutarlılığı</span><span class="sxs-lookup"><span data-stu-id="157d7-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="157d7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="157d7-104">Overview</span></span>
<span data-ttu-id="157d7-105">Azure Event Hubs kullanan bir [modeli bölümleme](event-hubs-features.md#partitions) tooimprove kullanılabilirlik ve tek olay hub'ı içinde paralelleştirme.</span><span class="sxs-lookup"><span data-stu-id="157d7-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) tooimprove availability and parallelization within a single event hub.</span></span> <span data-ttu-id="157d7-106">Örneğin, dört bölüm bir event hub varsa ve bu bölümler birini bir yük dengeleme işlemi bir sunucu tooanother gelen taşınır, hala gönderebilir ve diğer üç bölümlerden alırsınız.</span><span class="sxs-lookup"><span data-stu-id="157d7-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server tooanother in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="157d7-107">Ayrıca, daha fazla bölümlemeye sahip olmak toohave sağlar, toplam verimliliği artırma, veri işleme daha fazla eşzamanlı okuyucu.</span><span class="sxs-lookup"><span data-stu-id="157d7-107">Additionally, having more partitions enables you toohave more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="157d7-108">Bölümlendirme ve dağıtılmış bir sistemde sıralama hello etkilerini anlama, çözüm tasarımı önemli bir yönüdür.</span><span class="sxs-lookup"><span data-stu-id="157d7-108">Understanding hello implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="157d7-109">Bkz hello sıralama ve kullanılabilirlik arasındaki hello dengelemeyi açıklayan toohelp [CAP Teoremi](https://en.wikipedia.org/wiki/CAP_theorem), Brewer'ın Teoremi olarak da bilinir.</span><span class="sxs-lookup"><span data-stu-id="157d7-109">toohelp explain hello trade-off between ordering and availability, see hello [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="157d7-110">Bu Teoremi tutarlılık, kullanılabilirlik ve bölüm dayanıklılık arasında hello seçim açıklanır.</span><span class="sxs-lookup"><span data-stu-id="157d7-110">This theorem discusses hello choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="157d7-111">Brewer'ın Teoremi tutarlılık ve kullanılabilirlik gibi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="157d7-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="157d7-112">Dayanıklılık bölüm: Merhaba bölümünde hata olduğunda bile verileri işlerken veri işleme sistem toocontinue özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="157d7-112">Partition tolerance: hello ability of a data processing system toocontinue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="157d7-113">Kullanılabilirlik: başarısız olmayan düğüm makul bir süre (ile bir hata veya zaman aşımı) içinde makul bir yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="157d7-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="157d7-114">Tutarlılık: Okuma tooreturn hello en son yazma belirli bir istemcinin garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="157d7-114">Consistency: a read is guaranteed tooreturn hello most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="157d7-115">Bölüm dayanıklılık</span><span class="sxs-lookup"><span data-stu-id="157d7-115">Partition tolerance</span></span>
<span data-ttu-id="157d7-116">Olay hub'ları bölümlenmiş veri modeli üzerine inşa edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="157d7-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="157d7-117">Kurulum sırasında olay hub'ınıza hello bölüm sayısı yapılandırabilirsiniz ancak bu değer daha sonra değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="157d7-117">You can configure hello number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="157d7-118">Bölümler Event Hubs ile kullanmalısınız olduğundan toomake uygulamanız için kullanılabilirlik ve tutarlılık hakkındaki kararınızı sahip.</span><span class="sxs-lookup"><span data-stu-id="157d7-118">Since you must use partitions with Event Hubs, you have toomake a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="157d7-119">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="157d7-119">Availability</span></span>
<span data-ttu-id="157d7-120">Merhaba en basit yolu tooget kullanmaya olay hub'ları olan toouse hello varsayılan davranışı.</span><span class="sxs-lookup"><span data-stu-id="157d7-120">hello simplest way tooget started with Event Hubs is toouse hello default behavior.</span></span> <span data-ttu-id="157d7-121">Yeni bir oluşturursanız `EventHubClient` nesne ve hello kullan `Send` yöntemi, olayları olay hub'ınızdaki bölümler arasında otomatik olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="157d7-121">If you create a new `EventHubClient` object and use hello `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="157d7-122">Bu davranış hello büyük miktarda zaman verir.</span><span class="sxs-lookup"><span data-stu-id="157d7-122">This behavior allows for hello greatest amount of up time.</span></span>

<span data-ttu-id="157d7-123">Bu model hello en fazla çalışma zamanını gerektirir kullanım durumları için tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="157d7-123">For use cases that require hello maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="157d7-124">Tutarlılık</span><span class="sxs-lookup"><span data-stu-id="157d7-124">Consistency</span></span>
<span data-ttu-id="157d7-125">Bazı senaryolarda, olayların hello sıralama önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="157d7-125">In some scenarios, hello ordering of events can be important.</span></span> <span data-ttu-id="157d7-126">Örneğin, arka uç sistem tooprocess delete komutu önce güncelleştirme komutu isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="157d7-126">For example, you may want your back-end system tooprocess an update command before a delete command.</span></span> <span data-ttu-id="157d7-127">Bu örnekte, bir olayda hello bölüm anahtarı ayarlayın veya kullanın bir `PartitionSender` nesne tooonly belirli bölüm olayları tooa gönderin.</span><span class="sxs-lookup"><span data-stu-id="157d7-127">In this instance, you can either set hello partition key on an event, or use a `PartitionSender` object tooonly send events tooa certain partition.</span></span> <span data-ttu-id="157d7-128">Bu olaylar hello bölümünden okurken bunlar sırayla okunduğu sağlar.</span><span class="sxs-lookup"><span data-stu-id="157d7-128">Doing so ensures that when these events are read from hello partition, they are read in order.</span></span>

<span data-ttu-id="157d7-129">Bu yapılandırma ile gönderdiğiniz hello belirli bölüm toowhich kullanılamıyorsa, bir hata yanıtı alırsınız göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="157d7-129">With this configuration, keep in mind that if hello particular partition toowhich you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="157d7-130">Bir benzeşim tooa tek bölüm yoksa bir karşılaştırma noktası olarak hello Event Hubs hizmeti, olay toohello sonraki kullanılabilir bölüm gönderir.</span><span class="sxs-lookup"><span data-stu-id="157d7-130">As a point of comparison, if you do not have an affinity tooa single partition, hello Event Hubs service sends your event toohello next available partition.</span></span>

<span data-ttu-id="157d7-131">Sıralama, ayrıca çalışma zamanı, en üst düzeye çıkarma sırasında bir olası çözüm tooensure tooaggregate olayları, olay işleme uygulama bir parçası olarak olacaktır.</span><span class="sxs-lookup"><span data-stu-id="157d7-131">One possible solution tooensure ordering, while also maximizing up time, would be tooaggregate events as part of your event processing application.</span></span> <span data-ttu-id="157d7-132">Bu en kolay yolu tooaccomplish hello toostamp özel sıra sayısı özelliği ile bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="157d7-132">hello easiest way tooaccomplish this is toostamp your event with a custom sequence number property.</span></span> <span data-ttu-id="157d7-133">koddan hello bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="157d7-133">hello following code shows an example:</span></span>

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="157d7-134">Bu örnek, olay tooone hello kullanılabilir bölümlerinin olay hub'ınıza gönderir ve uygulamanızdan hello karşılık gelen sıra numarasını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="157d7-134">This example sends your event tooone of hello available partitions in your event hub, and sets hello corresponding sequence number from your application.</span></span> <span data-ttu-id="157d7-135">Bu çözüm, işleme uygulamanız tarafından tutulan durumu toobe gerektirir ancak büyük olasılıkla toobe kullanılabilir olduğu bir uç nokta, Gönderenler sağlar.</span><span class="sxs-lookup"><span data-stu-id="157d7-135">This solution requires state toobe kept by your processing application, but gives your senders an endpoint that is more likely toobe available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="157d7-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="157d7-136">Next steps</span></span>
<span data-ttu-id="157d7-137">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="157d7-137">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="157d7-138">Olay hub hizmetine genel bakış</span><span class="sxs-lookup"><span data-stu-id="157d7-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="157d7-139">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="157d7-139">Create an event hub</span></span>](event-hubs-create.md)
