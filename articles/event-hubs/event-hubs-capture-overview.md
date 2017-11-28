---
title: "Azure olay hub'ları yakalama aaaOverview | Microsoft Docs"
description: "Olay hub'ları yakalama telemetri verilerini yakalama"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="c7cbb-103">Azure Event Hubs yakalama</span><span class="sxs-lookup"><span data-stu-id="c7cbb-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="c7cbb-104">Azure olay hub'ları yakalama sağlar, olay hub'ları tooan veri akış tooautomatically teslim hello [Azure Blob Depolama](https://azure.microsoft.com/services/storage/blobs/) veya [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) hello ile tercih ettiğiniz hesabına esneklik eklenen bir kez veya boyut aralığı belirterek.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-104">Azure Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooan [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with hello added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="c7cbb-105">Yakalama kurduğunuzda ayardır hızlı ve bunu ölçeklendirir otomatik olarak Event Hubs ile hiçbir yönetim maliyetleri toorun [üretilen iş birimleri](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="c7cbb-105">Setting up Capture is fast, there are no administrative costs toorun it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="c7cbb-106">Olay hub'ları yakalama akış verileri Azure'da hello en kolay yolu tooload ve toofocus veri işleme yerine veri yakalamayı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-106">Event Hubs Capture is hello easiest way tooload streaming data into Azure, and enables you toofocus on data processing rather than on data capture.</span></span>

<span data-ttu-id="c7cbb-107">Toplu işlem tabanlı ardışık düzen üzerinde aynı akış hello ve olay hub'ları yakalama tooprocess gerçek zamanlı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-107">Event Hubs Capture enables you tooprocess real-time and batch-based pipelines on hello same stream.</span></span> <span data-ttu-id="c7cbb-108">Bu, zaman içinde gereksinimlerinizi ile büyümesine çözümleri oluşturmanıza anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="c7cbb-109">Toplu işlem tabanlı sistemleriyle bugün gelecekteki gerçek zamanlı işleme doğru bir göz oluşturmakta olduğunuz ya tooadd etkin yolunuzda tooan varolan gerçek zamanlı çözümü istiyor da olsanız, olay hub'ları yakalama daha kolay veri akış ile çalışma hale getirir.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want tooadd an efficient cold path tooan existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="c7cbb-110">Olay hub'ları yakalama nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="c7cbb-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="c7cbb-111">Olay hub'ları telemetri giriş, benzer tooa dağıtılmış günlük bir bekletme süresi dayanıklı arabellek olur.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar tooa distributed log.</span></span> <span data-ttu-id="c7cbb-112">Olay hub'ın anahtar tooscaling Hello olduğu hello [bölümlenmiş tüketici modelinin](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="c7cbb-112">hello key tooscaling in Event Hubs is hello [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="c7cbb-113">Her bölüm veri bağımsız bir parçasıdır ve bağımsız olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="c7cbb-114">Bu verileri kapalı eskir zamanla hello yapılandırılabilir saklama dönemi temel.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-114">Over time this data ages off, based on hello configurable retention period.</span></span> <span data-ttu-id="c7cbb-115">Sonuç olarak, belirli olay hub'ı hiçbir zaman "dolu." alır</span><span class="sxs-lookup"><span data-stu-id="c7cbb-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="c7cbb-116">Olay hub'ları yakalama, toospecify kendi Azure Blob Depolama hesabı ve kapsayıcı ya da kullanılan toostore hello yakalanan verileri Azure Data Lake Store hesabını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-116">Event Hubs Capture enables you toospecify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used toostore hello captured data.</span></span> <span data-ttu-id="c7cbb-117">Bu hesapları hello olabilir aynı bölgede olay hub'ınızı ya da başka bir bölgede hello olay hub'ları yakalama özelliği toohello esnekliğini ekleme.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-117">These accounts can be in hello same region as your event hub or in another region, adding toohello flexibility of hello Event Hubs Capture feature.</span></span>

<span data-ttu-id="c7cbb-118">Yakalanan verileri yazılmış [Apache Avro] [ Apache Avro] biçimi: satır içi şeması ile zengin veri yapılarını sağlar compact, hızlı ve ikili biçimi.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="c7cbb-119">Bu biçim hello Hadoop ekosistemi, akış analizi ve Azure Data Factory yaygın olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-119">This format is widely used in hello Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="c7cbb-120">Avro ile çalışma hakkında daha fazla bilgi, bu makalenin sonraki bölümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="c7cbb-121">Pencereleme yakalama</span><span class="sxs-lookup"><span data-stu-id="c7cbb-121">Capture windowing</span></span>

<span data-ttu-id="c7cbb-122">Olay hub'ları yakalama pencere yakalanıyor toocontrol yukarı tooset sağlar.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-122">Event Hubs Capture enables you tooset up a window toocontrol capturing.</span></span> <span data-ttu-id="c7cbb-123">Bu, en küçük boyut ve zaman yapılandırma İlkesi'yle "yakalama işlemi, ilk tetikleyici karşılaşılan nedenleri hello yani ilk WINS," penceredir.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-123">This window is a minimum size and time configuration with a "first wins policy," meaning that hello first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="c7cbb-124">On beş dakikalık varsa, 100 MB Yakalama penceresinin ve 1 MB saniye başına hello boyutu penceresi Tetikleyicileri hello zaman penceresi önce gönderin.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, hello size window triggers before hello time window.</span></span> <span data-ttu-id="c7cbb-125">Her bölüm bağımsız olarak yakalar ve tamamlanan blok blobu, yakalama, başlangıç sırasında hangi hello yakalama aralığı karşılaşıldı hello süredir adlı yazar.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-125">Each partition captures independently and writes a completed block blob at hello time of capture, named for hello time at which hello capture interval was encountered.</span></span> <span data-ttu-id="c7cbb-126">Merhaba depolama adlandırma kuralı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c7cbb-126">hello storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a><span data-ttu-id="c7cbb-127">Toothroughput birimleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="c7cbb-127">Scaling toothroughput units</span></span>

<span data-ttu-id="c7cbb-128">Olay hub'ları trafiği tarafından denetlenir [üretilen iş birimleri](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="c7cbb-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="c7cbb-129">Tek bir işleme birimi, ikinci veya 1000 olayları giriş ve çıkış miktarı iki kez saniyede başına 1 MB sağlar.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="c7cbb-130">Standart olay hub'ları 1-20 işleme birimleri ile yapılandırılabilir ve daha fazla satın alma ile kota artırma [destek isteği][support request].</span><span class="sxs-lookup"><span data-stu-id="c7cbb-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="c7cbb-131">Kullanım, satın alınan işleme birimlerine ötesinde kısıtlanır.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="c7cbb-132">Olay hub'ları yakalama verileri doğrudan hello İç olay hub'ları depolama biriminden, işleme birimi çıkış kotaları atlayarak ve akış analizi veya Spark gibi diğer işleme okuyucular için çıkış kaydetme kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-132">Event Hubs Capture copies data directly from hello internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="c7cbb-133">Olay hub'ları yakalama yapılandırdıktan sonra ilk olay gönderdiğinizde, otomatik olarak çalışır ve çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="c7cbb-134">hiçbir veri olduğunda toomake hello işlemin çalıştığını, aşağı akış işleme tooknow için olay hub'ları daha kolaydır boş dosyaları yazar.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-134">toomake it easier for your downstream processing tooknow that hello process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="c7cbb-135">Bu işlem, tahmin edilebilir tempoyla ve toplu işlemciler besleyebilecek işaret sunar.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="c7cbb-136">Olay hub'ları yakalama ayarlama</span><span class="sxs-lookup"><span data-stu-id="c7cbb-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="c7cbb-137">Yakalama hello kullanarak hello olay hub'ı oluşturma zamanında yapılandırabilirsiniz [Azure portal](https://portal.azure.com), veya Azure Resource Manager şablonları kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-137">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="c7cbb-138">Daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="c7cbb-138">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="c7cbb-139">Olay hub'ları hello Azure portal kullanarak yakalama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c7cbb-139">Enable Event Hubs Capture using hello Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="c7cbb-140">Bir event hub ile Event Hubs ad alanı oluşturmak ve bir Azure Resource Manager şablonu kullanarak yakalamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c7cbb-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a><span data-ttu-id="c7cbb-141">Yakalanan hello dosyaları keşfetme ve Avro ile çalışma</span><span class="sxs-lookup"><span data-stu-id="c7cbb-141">Exploring hello captured files and working with Avro</span></span>

<span data-ttu-id="c7cbb-142">Olay hub'ları yakalama Avro biçiminde hello yapılandırılmış zaman penceresi belirtildiği gibi dosyalar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-142">Event Hubs Capture creates files in Avro format, as specified on hello configured time window.</span></span> <span data-ttu-id="c7cbb-143">Bu dosyaları gibi herhangi bir aracı görüntüleyebilirsiniz [Azure Storage Gezgini][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="c7cbb-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="c7cbb-144">İndirebilirsiniz hello dosyaları yerel olarak toowork bunlar üzerinde.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-144">You can download hello files locally toowork on them.</span></span>

<span data-ttu-id="c7cbb-145">Olay hub'ları yakalama tarafından üretilen hello dosyaları Avro şemasının aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c7cbb-145">hello files produced by Event Hubs Capture have hello following Avro schema:</span></span>

![][3]

<span data-ttu-id="c7cbb-146">Kolay bir yolu tooexplore Avro dosyalarının olduğu hello kullanarak [Avro Araçları] [ Avro Tools] Apache gelen jar.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-146">An easy way tooexplore Avro files is by using hello [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="c7cbb-147">Bu jar indirdikten sonra komutu aşağıdaki hello çalıştırarak belirli bir Avro dosya hello şeması görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c7cbb-147">After downloading this jar, you can see hello schema of a specific Avro file by running hello following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="c7cbb-148">Bu komut döndürür</span><span class="sxs-lookup"><span data-stu-id="c7cbb-148">This command returns</span></span>

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

<span data-ttu-id="c7cbb-149">Avro araçları tooconvert hello dosya tooJSON biçimini kullanın ve başka bir işlem gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-149">You can also use Avro Tools tooconvert hello file tooJSON format and perform other processing.</span></span>

<span data-ttu-id="c7cbb-150">daha gelişmiş işleme, karşıdan yüklenip Avro için tercih ettiğiniz platformun tooperform.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-150">tooperform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="c7cbb-151">Bu yazma Hello anda uygulamaları C, C++, C için kullanılabilir olduğundan\#, Java, NodeJS, Perl, PHP, Python ve Ruby.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-151">At hello time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="c7cbb-152">Apache Avro için tam Başlarken kılavuzları sahip [Java] [ Java] ve [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="c7cbb-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="c7cbb-153">Ayrıca, hello okuyabilirsiniz [olay hub'ları yakalama ile çalışmaya başlama](event-hubs-capture-python.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-153">You can also read hello [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="c7cbb-154">Olay hub'ları yakalama nasıl doludur</span><span class="sxs-lookup"><span data-stu-id="c7cbb-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="c7cbb-155">Olay hub'ları yakalama ölçülen benzer şekilde toothroughput birimler: saatlik giderleri olarak.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-155">Event Hubs Capture is metered similarly toothroughput units: as an hourly charge.</span></span> <span data-ttu-id="c7cbb-156">Merhaba ücret orantılı toohello hello ad alanı için satın alınan işleme birimi sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-156">hello charge is directly proportional toohello number of throughput units purchased for hello namespace.</span></span> <span data-ttu-id="c7cbb-157">Üretilen iş birimleri artırılır ve azaltılır gibi olay hub'ları yakalama ölçümler artırın ve performans eşleşen tooprovide azaltın.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease tooprovide matching performance.</span></span> <span data-ttu-id="c7cbb-158">Merhaba ölçümler dağıtımınızla oluşur.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-158">hello meters occur in tandem.</span></span> <span data-ttu-id="c7cbb-159">Fiyatlandırma ayrıntıları için bkz: [Event Hubs fiyatlandırması](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="c7cbb-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c7cbb-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7cbb-160">Next steps</span></span>

<span data-ttu-id="c7cbb-161">Olay hub'ları yakalama hello en kolay yolu tooget Azure içine verilerdir.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-161">Event Hubs Capture is hello easiest way tooget data into Azure.</span></span> <span data-ttu-id="c7cbb-162">Azure Data Lake, Azure Data Factory ve Azure Hdınsight kullanarak toplu işleme gerçekleştirebilir ve herhangi bir ölçekte tanıdık Araçlar ve seçtiğiniz platformlar kullanarak diğer analytics gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7cbb-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="c7cbb-163">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c7cbb-163">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="c7cbb-164">Gönderme ve alma olayları kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c7cbb-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="c7cbb-165">[Event Hubs kullanan bir örnek uygulamanın][sample application that uses Event Hubs] tamamı</span><span class="sxs-lookup"><span data-stu-id="c7cbb-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="c7cbb-166">[Event Hubs'a genel bakış][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="c7cbb-166">[Event Hubs overview][Event Hubs overview]</span></span>

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
