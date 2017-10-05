---
title: "Azure Service Bus Mesajlaşma örnekleri genel bakış | Microsoft Docs"
description: "Service Bus örnekleri her bağlantılarla Mesajlaşma açıklar"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0b420343-2d2a-4c65-98f1-ee0e39ef55c8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: sethm
ms.openlocfilehash: 0cf21ea9a820de0396b54dd26a625a046de39291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-messaging-samples"></a><span data-ttu-id="dfd93-103">Service Bus Mesajlaşma örnekleri</span><span class="sxs-lookup"><span data-stu-id="dfd93-103">Service Bus messaging samples</span></span>

<span data-ttu-id="dfd93-104">Service Bus Mesajlaşma örnekleri anahtar özelliklerini göstermek [Service Bus Mesajlaşma](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="dfd93-104">The Service Bus messaging samples demonstrate key features in [Service Bus messaging](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="dfd93-105">Şu anda iki yerde örnekleri bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dfd93-105">Currently, you can find the samples in two places:</span></span>

- <span data-ttu-id="dfd93-106">[Service Bus Mesajlaşma örnekler Github'da](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet): örnekler, GitHub üzerinde barındırılan yeni kümesi.</span><span class="sxs-lookup"><span data-stu-id="dfd93-106">[Service Bus messaging samples on GitHub](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet): a newer set of samples, hosted on GitHub.</span></span> <span data-ttu-id="dfd93-107">Bkz: [Benioku dosyasını](https://github.com/Azure/azure-service-bus/blob/master/samples/DotNet/Microsoft.ServiceBus.Messaging/README.md) bu .NET örnekleri açıklamaları için depodaki.</span><span class="sxs-lookup"><span data-stu-id="dfd93-107">See the [readme file](https://github.com/Azure/azure-service-bus/blob/master/samples/DotNet/Microsoft.ServiceBus.Messaging/README.md) in the repo for descriptions of these .NET samples.</span></span> <span data-ttu-id="dfd93-108">Örnekler sürekli olarak güncelleştirilir, kontrol geri genellikle güncelleştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="dfd93-108">The samples are continuously updated, so check back often for updates.</span></span>
- <span data-ttu-id="dfd93-109">[MSDN örnekleri sayfasını](https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=5): MSDN kod Galerisi'nden Canlı eski örnekleri.</span><span class="sxs-lookup"><span data-stu-id="dfd93-109">[MSDN samples page](https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=5): older samples that live in the MSDN code gallery.</span></span> <span data-ttu-id="dfd93-110">Bu örnekler çalışmaya olsa da korunmaz ve göre geçerli önerilen programlama uygulamalarını güncel olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="dfd93-110">Although these samples still work, they are not maintained and may be outdated with respect to current recommended programming practices.</span></span>
 
## <a name="service-bus-explorer"></a><span data-ttu-id="dfd93-111">Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="dfd93-111">Service Bus Explorer</span></span>

<span data-ttu-id="dfd93-112">Ayrıca, [hizmet veri yolu Gezgini](https://github.com/paolosalvatori/ServiceBusExplorer) Service Bus hizmeti ad alanına bağlanmak ve mesajlaşma varlıkları kolayca yönetmenize olanak tanıyan GitHub üzerinde barındırılan bir örnek.</span><span class="sxs-lookup"><span data-stu-id="dfd93-112">In addition, the [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer) is a sample hosted on GitHub that enables you to connect to a Service Bus service namespace and easily manage messaging entities.</span></span> <span data-ttu-id="dfd93-113">Aracı içeri/dışarı aktarma işlevleri gibi gelişmiş özellikler ve test Mesajlaşma varlıkları ve geçiş hizmetleri olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="dfd93-113">The tool provides advanced features such as import/export functionality, and the ability to test messaging entities and relay services.</span></span> <span data-ttu-id="dfd93-114">Üzerinde tam hizmet veri yolu Gezgini kaynak ve belgeleri bulabilirsiniz [GitHub](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="dfd93-114">You can find the full Service Bus Explorer source and documentation on [GitHub](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfd93-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dfd93-115">Next steps</span></span>

<span data-ttu-id="dfd93-116">Örnek konumları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dfd93-116">Sample locations are here:</span></span>

- [<span data-ttu-id="dfd93-117">GitHub örnekleri</span><span class="sxs-lookup"><span data-stu-id="dfd93-117">GitHub samples</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples)
- [<span data-ttu-id="dfd93-118">Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="dfd93-118">Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer)

<span data-ttu-id="dfd93-119">Hizmet veri yolu kavramsal genel bakış için aşağıdaki konulara bakın.</span><span class="sxs-lookup"><span data-stu-id="dfd93-119">See the following topics for conceptual overviews of Service Bus.</span></span>

* [<span data-ttu-id="dfd93-120">Service Bus mesajlaşma hizmetine genel bakış</span><span class="sxs-lookup"><span data-stu-id="dfd93-120">Service Bus messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="dfd93-121">Service Bus mimarisi</span><span class="sxs-lookup"><span data-stu-id="dfd93-121">Service Bus architecture</span></span>](service-bus-architecture.md)
* [<span data-ttu-id="dfd93-122">Service Bus ile ilgili temel bilgiler</span><span class="sxs-lookup"><span data-stu-id="dfd93-122">Service Bus fundamentals</span></span>](service-bus-fundamentals-hybrid-solutions.md)

