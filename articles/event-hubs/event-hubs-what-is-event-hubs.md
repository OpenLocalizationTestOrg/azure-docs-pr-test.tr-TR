---
title: "aaaWhat Azure Event hubs ve neden kullanın | Microsoft Docs"
description: "Genel bakış ve giriş tooAzure Event Hubs - bulut ölçekli telemetri alım Web siteleri, uygulamalar ve cihazlar"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="534a7-103">Event Hubs nedir?</span><span class="sxs-lookup"><span data-stu-id="534a7-103">What is Event Hubs?</span></span>

<span data-ttu-id="534a7-104">Azure Event Hubs saniyede milyonlarca olay alıp işleyebilen, ölçeklenebilirlik yüzeyi yüksek bir veri akışı platformu ve olay alma hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="534a7-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="534a7-105">Event Hubs dağıtılan yazılımlar ve cihazlar tarafından oluşturulan olayları, verileri ve telemetrileri işleyebilir ve depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="534a7-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="534a7-106">Veri tooan olay hub'ı dönüştürülebilir ve herhangi bir gerçek zamanlı analiz sağlayıcısı veya toplu işlem/depolama bağdaştırıcısı kullanılarak saklanan gönderdi.</span><span class="sxs-lookup"><span data-stu-id="534a7-106">Data sent tooan event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="534a7-107">Merhaba özelliği tooprovide ile [yayımlama-abonelik özellikleri](https://msdn.microsoft.com/library/aa560414.aspx) düşük gecikme ile ve büyük ölçekte olay hub'ları "on Rampa" Merhaba büyük veriler için görevi görür.</span><span class="sxs-lookup"><span data-stu-id="534a7-107">With hello ability tooprovide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as hello "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="534a7-108">Event Hubs’ı neden kullanmalıyım?</span><span class="sxs-lookup"><span data-stu-id="534a7-108">Why use Event Hubs?</span></span>

<span data-ttu-id="534a7-109">Event Hubs olay ve telemetri işleme özellikler onu özellikle aşağıdaki durumlar için yararlı hale getirir:</span><span class="sxs-lookup"><span data-stu-id="534a7-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="534a7-110">Uygulama izleme</span><span class="sxs-lookup"><span data-stu-id="534a7-110">Application instrumentation</span></span>
* <span data-ttu-id="534a7-111">Kullanıcı deneyimi veya iş akışı işleme</span><span class="sxs-lookup"><span data-stu-id="534a7-111">User experience or workflow processing</span></span>
* <span data-ttu-id="534a7-112">Nesnelerin İnterneti (IoT) senaryoları</span><span class="sxs-lookup"><span data-stu-id="534a7-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="534a7-113">Örneğin, Event Hubs mobil uygulamalarda davranış izleme, web gruplarından trafik bilgileri alma, konsol oyunlarında oyun içi olay yakalama veya sanayi makinelerinden ya da bağlı taşıtlardan telemetri verileri toplama olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="534a7-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="534a7-114">Azure Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="534a7-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="534a7-115">Merhaba olay hub'ın çözüm mimarilerinde oynadığı genel rol olan hello "ön adlandırılırlar kapı" bir olay ardışık düzeni için bir *olay yutucu*.</span><span class="sxs-lookup"><span data-stu-id="534a7-115">hello common role that Event Hubs plays in solution architectures is hello "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="534a7-116">Bir olay yutucu, bir bileşeni ya da olay yayımcıları ile olay tüketicileri toodecouple hello hello üretimini ilgili olayların olay akışının üretimini arasındaki bulunur service ' dir.</span><span class="sxs-lookup"><span data-stu-id="534a7-116">An event ingestor is a component or service that sits between event publishers and event consumers toodecouple hello production of an event stream from hello consumption of those events.</span></span> <span data-ttu-id="534a7-117">Merhaba aşağıdaki şekilde bu mimari gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="534a7-117">hello following figure depicts this architecture:</span></span>

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="534a7-119">Event Hubs, ileti akışı işleme olanağı sağlar ancak geleneksel kurumsal mesajlaşmadan farklı özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="534a7-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="534a7-120">Event Hubs özellikleri, yüksek işleme ve olay işleme senaryoları üzerine inşa edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="534a7-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="534a7-121">Bu nedenle, Event Hubs farklıdır [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) Mesajlaşma ve bazı kullanılabilir hello özelliklerini uygulamıyor [Service Bus Mesajlaşma](/azure/service-bus-messaging/) konuları gibi varlıklar.</span><span class="sxs-lookup"><span data-stu-id="534a7-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of hello capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="534a7-122">Event Hubs özellikleri</span><span class="sxs-lookup"><span data-stu-id="534a7-122">Event Hubs features</span></span>

<span data-ttu-id="534a7-123">Olay hub'ları temel öğeleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="534a7-123">Event Hubs contains hello following key elements:</span></span>

- <span data-ttu-id="534a7-124">[**Olay üreticileri/yayımcıları**](event-hubs-features.md#event-publishers): tooan event hub'ı veri gönderen bir varlık.</span><span class="sxs-lookup"><span data-stu-id="534a7-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data tooan event hub.</span></span> <span data-ttu-id="534a7-125">Olay AMQP 1.0 veya HTTPS üzerinden yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="534a7-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="534a7-126">[**Yakalama**](event-hubs-features.md#capture): bir Azure Blob storage hesabında depolamak ve toocapture olay hub'ın veri akış sağlar.</span><span class="sxs-lookup"><span data-stu-id="534a7-126">[**Capture**](event-hubs-features.md#capture): Enables you toocapture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="534a7-127">[**Bölümler**](event-hubs-features.md#partitions): etkinleştirir, her tüketici tooonly okuma belirli alt ya da bölümü hello olay akışı.</span><span class="sxs-lookup"><span data-stu-id="534a7-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer tooonly read a specific subset, or partition, of hello event stream.</span></span>
- <span data-ttu-id="534a7-128">[**SAS belirteci**](event-hubs-features.md#sas-tokens): tanımlar ve hello olay yayımcısı kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="534a7-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates hello event publisher.</span></span>
- <span data-ttu-id="534a7-129">[**Olay tüketicileri**](event-hubs-features.md#event-consumers): Bir olay hub'ından olay verilerini okuyan bir varlıktır.</span><span class="sxs-lookup"><span data-stu-id="534a7-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="534a7-130">Olay tüketicileri AMQP 1.0 üzerinden bağlanır.</span><span class="sxs-lookup"><span data-stu-id="534a7-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="534a7-131">[**Tüketici grupları**](event-hubs-features.md#consumer-groups): hello olay akışının ayrı bir görünümle uygulama, bu tüketicileri tooact bağımsız olarak etkinleştirme her birden çok sağlar.</span><span class="sxs-lookup"><span data-stu-id="534a7-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of hello event stream, enabling those consumers tooact independently.</span></span>
- <span data-ttu-id="534a7-132">[**İşleme birimleri**](event-hubs-features.md#capacity): Önceden satın alınan kapasite birimleridir.</span><span class="sxs-lookup"><span data-stu-id="534a7-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="534a7-133">Tek bir bölüm en fazla 1 işleme biriminden oluşan ölçeğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="534a7-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="534a7-134">Bunlar ve diğer Event Hubs özellikleri hakkında teknik ayrıntılar için bkz: Merhaba [olay hub'ları özelliklere genel bakış](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="534a7-134">For technical details about these and other Event Hubs features, see hello [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="534a7-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="534a7-135">Next steps</span></span>

<span data-ttu-id="534a7-136">Event Hubs ayrıntılı fiyatlandırma bilgileri için bkz. [Event Hubs Fiyatlandırması](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="534a7-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="534a7-137">Event Hubs hakkında daha fazla bilgi için bağlantılar aşağıdaki hello ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="534a7-137">For more information about Event Hubs, visit hello following links:</span></span>

* <span data-ttu-id="534a7-138">[Event Hubs öğreticisi](event-hubs-dotnet-standard-getstarted-send.md) ile çalışmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="534a7-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="534a7-139">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="534a7-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="534a7-140">Event Hubs kullanan örnek uygulamalar</span><span class="sxs-lookup"><span data-stu-id="534a7-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

