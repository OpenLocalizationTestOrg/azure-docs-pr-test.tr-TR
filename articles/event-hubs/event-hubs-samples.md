---
title: "Azure Event Hubs örnekleri | Microsoft Docs"
description: "Azure Event Hubs örnekleri"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ae9fbd97a1747d8f14c561f247a0973bb11fd039
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-samples"></a><span data-ttu-id="ed8a1-103">Olay hub'ları örnekleri</span><span class="sxs-lookup"><span data-stu-id="ed8a1-103">Event Hubs samples</span></span> 

<span data-ttu-id="ed8a1-104">Azure Event Hubs örnekleri kümesi anahtar özelliklerini gösteren [Azure Event Hubs](/azure/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="ed8a1-104">The set of Azure Event Hubs samples demonstrates key features in [Azure Event Hubs](/azure/event-hubs/).</span></span> <span data-ttu-id="ed8a1-105">Bu makalede, kategorilere ayırır ve her için bağlantılar ile birlikte kullanılabilir örnekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ed8a1-105">This article categorizes and describes the samples available, with links to each.</span></span>

<span data-ttu-id="ed8a1-106">Bu yazma zaman Event Hubs örnekleri birkaç farklı yerlerde bulunur:</span><span class="sxs-lookup"><span data-stu-id="ed8a1-106">At the time of this writing, Event Hubs samples are located in several different places:</span></span>

- [<span data-ttu-id="ed8a1-107">MSDN Geliştirici kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="ed8a1-107">MSDN developer code samples</span></span>](https://code.msdn.microsoft.com/site/search?query=event%20hubs&f%5B0%5D.Value=event%20hubs&f%5B0%5D.Type=SearchText&ac=5)
- [<span data-ttu-id="ed8a1-108">GitHub</span><span class="sxs-lookup"><span data-stu-id="ed8a1-108">GitHub</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="ed8a1-109">.NET Framework'ün farklı sürümleri hakkında daha fazla bilgi için bkz: [çerçeveler ve hedefleri](/dotnet/articles/standard/frameworks).</span><span class="sxs-lookup"><span data-stu-id="ed8a1-109">For more information about different versions of the .NET Framework, see [Frameworks and Targets](/dotnet/articles/standard/frameworks).</span></span>

<span data-ttu-id="ed8a1-110">Daha fazla örnekleri olacaktır zamanla eklenir, böylece geri burada sık Güncelleştirmeleri denetle.</span><span class="sxs-lookup"><span data-stu-id="ed8a1-110">More samples will be added over time, so check back here frequently for updates.</span></span>

## <a name="net-standard"></a><span data-ttu-id="ed8a1-111">.NET standart</span><span class="sxs-lookup"><span data-stu-id="ed8a1-111">.NET Standard</span></span>

<span data-ttu-id="ed8a1-112">Aşağıdaki örnekleri kullanarak olayları alıp göndermek nasıl ekleyebileceğiniz gösterilmektedir [Event Hubs istemcisi](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) için [.NET standart Kitaplığı](/dotnet/articles/standard/library).</span><span class="sxs-lookup"><span data-stu-id="ed8a1-112">The following samples demonstrate how to send and receive events using the [Event Hubs client](https://github.com/Azure/azure-event-hubs-dotnet/blob/master/readme.md) for the [.NET Standard library](/dotnet/articles/standard/library).</span></span>

### <a name="send-events"></a><span data-ttu-id="ed8a1-113">Olayları gönderme</span><span class="sxs-lookup"><span data-stu-id="ed8a1-113">Send events</span></span> 

<span data-ttu-id="ed8a1-114">[Göndermeye başlamak](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) örnek olayları bir event hub'ına gönderir .NET Core konsol uygulamasının nasıl yazılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ed8a1-114">The [Get started sending](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) sample shows how to write a .NET Core console application that sends events to an event hub.</span></span>

### <a name="receive-events"></a><span data-ttu-id="ed8a1-115">Olayları alma</span><span class="sxs-lookup"><span data-stu-id="ed8a1-115">Receive events</span></span> 

<span data-ttu-id="ed8a1-116">[İle olay işleyicisi konağı almaya başlamak](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) olay işleyicisi konağı kullanarak bir event hub iletileri alan bir .NET Core konsol uygulaması örnektir.</span><span class="sxs-lookup"><span data-stu-id="ed8a1-116">The [Get started receiving with the Event Processor Host](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) sample is a .NET Core console application that receives messages from an event hub using the Event Processor Host.</span></span>

## <a name="net-framework"></a><span data-ttu-id="ed8a1-117">.NET framework</span><span class="sxs-lookup"><span data-stu-id="ed8a1-117">.NET Framework</span></span>   

<span data-ttu-id="ed8a1-118">Bu örnekler çeşitli hedefleme Azure Event Hubs özelliklerini göstermek [.NET Framework Kitaplığı](/dotnet/framework/index).</span><span class="sxs-lookup"><span data-stu-id="ed8a1-118">These samples demonstrate various other features of Azure Event Hubs, targeting the [.NET Framework library](/dotnet/framework/index).</span></span>
 
### <a name="notify-users-of-events-received"></a><span data-ttu-id="ed8a1-119">Alınan olayların kullanıcıları bildir</span><span class="sxs-lookup"><span data-stu-id="ed8a1-119">Notify users of events received</span></span>

<span data-ttu-id="ed8a1-120">[AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) örnek algılayıcılar veya diğer sistemler alınan veri kullanıcılarına bildirir.</span><span class="sxs-lookup"><span data-stu-id="ed8a1-120">The [AppToNotifyUsers](https://github.com/Azure-Samples/event-hubs-dotnet-user-notifications) sample notifies users of data received from sensors or other systems.</span></span>

### <a name="get-started-with-event-hubs"></a><span data-ttu-id="ed8a1-121">Event Hubs kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="ed8a1-121">Get started with Event Hubs</span></span> 

<span data-ttu-id="ed8a1-122">[Olay hub'ları Başlarken](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) örnek olay hub'ları, bir olay hub'ı oluşturma, olay hub'ına olayları göndermek ve kullanarak olayları kullanma gibi temel özelliklerini gösteren [olay işleyicisi konağı](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) .</span><span class="sxs-lookup"><span data-stu-id="ed8a1-122">The [Event Hubs Getting Started](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097) sample demonstrates the basic capabilities of Event Hubs, such as how to create an event hub, send events to an event hub, and consume events using the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>

### <a name="scale-out-event-processing"></a><span data-ttu-id="ed8a1-123">Olay işleme çıkışı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="ed8a1-123">Scale out event processing</span></span> 

<span data-ttu-id="ed8a1-124">[Olay işleme genişletme](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) örnek nasıl kullanılacağını gösteren [olay işleyicisi konağı](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) olay hub'ları akış tüketiminin iş yükünü dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="ed8a1-124">The [Scale out event processing](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3) sample demonstrates how to use the [Event Processor Host](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) to distribute the workload of Event Hubs stream consumption.</span></span> <span data-ttu-id="ed8a1-125">Nasıl uygulandığını gösterir **EventProcessor** ve **EventProcessorFactory** olay akışının yönetilecek nesneleri.</span><span class="sxs-lookup"><span data-stu-id="ed8a1-125">It shows how to implement the **EventProcessor** and **EventProcessorFactory** objects to manage the event stream.</span></span> 

###  <a name="pull-data-from-sql-into-an-event-hub"></a><span data-ttu-id="ed8a1-126">Bir olay hub'ına SQL'den veri çekme</span><span class="sxs-lookup"><span data-stu-id="ed8a1-126">Pull data from SQL into an event hub</span></span>

<span data-ttu-id="ed8a1-127">[Çekme SQL veri](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) örnek bir SQL tablosundan veri çekmek ve aşağı akış analitik uygulamalarında bir girdi olarak kullanmak için bir olay hub'ına anında nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="ed8a1-127">The [Pulling SQL data](https://github.com/Azure-Samples/event-hubs-dotnet-import-from-sql) sample shows how to pull data from a SQL table and push it to an event hub, to use as an input in downstream analytical applications.</span></span>

### <a name="pull-web-data-into-an-event-hub"></a><span data-ttu-id="ed8a1-128">Bir olay hub'ına Web veri çekme</span><span class="sxs-lookup"><span data-stu-id="ed8a1-128">Pull web data into an event hub</span></span> 

<span data-ttu-id="ed8a1-129">[Web'den veri içeri aktarma](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) örnek verileri (örneğin, departman taşıma'nın trafiği bilgi akış) ortak akışları çekmek ve bir event hub'ına anında nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="ed8a1-129">The [Import data from the web](https://github.com/Azure-Samples/event-hubs-dotnet-importfromweb) sample shows how to pull data from public feeds (such as the Department of Transportation's traffic information feed) and push it to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed8a1-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ed8a1-130">Next steps</span></span>

<span data-ttu-id="ed8a1-131">.NET Framework sürümleri hakkında daha fazla bilgi için aşağıdaki bağlantıları ziyaret ederek öğrenin:</span><span class="sxs-lookup"><span data-stu-id="ed8a1-131">Learn more about .NET Framework versions by visiting the following links:</span></span>

- [<span data-ttu-id="ed8a1-132">Çerçeveler ve hedefler</span><span class="sxs-lookup"><span data-stu-id="ed8a1-132">Frameworks and targets</span></span>](/dotnet/articles/standard/frameworks)
- [<span data-ttu-id="ed8a1-133">.NET framework 4.6 ve 4.5</span><span class="sxs-lookup"><span data-stu-id="ed8a1-133">.NET Framework 4.6 and 4.5</span></span>](/dotnet/framework/index)

<span data-ttu-id="ed8a1-134">Aşağıdaki makalelerde Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ed8a1-134">You can learn more about Event Hubs in the following articles:</span></span>

- [<span data-ttu-id="ed8a1-135">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="ed8a1-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="ed8a1-136">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ed8a1-136">Create an event hub</span></span>](event-hubs-create.md)
- [<span data-ttu-id="ed8a1-137">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="ed8a1-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)