---
title: "Azure geçiş API genel bakış | Microsoft Docs"
description: "Kullanılabilir Azure geçiş API'larının genel bakış"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 8d93a0344adc3b0b7617f3a7d85124142d7a7555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="a8589-103">Kullanılabilir geçiş API'leri</span><span class="sxs-lookup"><span data-stu-id="a8589-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="a8589-104">Çalışma zamanı API'leri</span><span class="sxs-lookup"><span data-stu-id="a8589-104">Runtime APIs</span></span>

<span data-ttu-id="a8589-105">Aşağıdaki tabloda şu anda kullanılabilir tüm geçiş çalışma zamanı istemcileri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="a8589-105">The following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="a8589-106">[Ek bilgi](#additional-information) bölüm her çalışma zamanı kitaplığı durumu hakkında daha fazla bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="a8589-106">The [additional information](#additional-information) section contains more information about the status of each runtime library.</span></span>

| <span data-ttu-id="a8589-107">Dil/Platform</span><span class="sxs-lookup"><span data-stu-id="a8589-107">Language/Platform</span></span> | <span data-ttu-id="a8589-108">Kullanılabilir özelliği</span><span class="sxs-lookup"><span data-stu-id="a8589-108">Available feature</span></span> | <span data-ttu-id="a8589-109">İstemci paketi</span><span class="sxs-lookup"><span data-stu-id="a8589-109">Client package</span></span> | <span data-ttu-id="a8589-110">Depo</span><span class="sxs-lookup"><span data-stu-id="a8589-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a8589-111">.NET standart</span><span class="sxs-lookup"><span data-stu-id="a8589-111">.NET Standard</span></span> | <span data-ttu-id="a8589-112">Karma Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="a8589-112">Hybrid Connections</span></span> | [<span data-ttu-id="a8589-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="a8589-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="a8589-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="a8589-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="a8589-115">.NET framework</span><span class="sxs-lookup"><span data-stu-id="a8589-115">.NET Framework</span></span> | <span data-ttu-id="a8589-116">WCF Geçişi</span><span class="sxs-lookup"><span data-stu-id="a8589-116">WCF Relay</span></span> | [<span data-ttu-id="a8589-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="a8589-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="a8589-118">Yok</span><span class="sxs-lookup"><span data-stu-id="a8589-118">N/A</span></span> |
| <span data-ttu-id="a8589-119">Node</span><span class="sxs-lookup"><span data-stu-id="a8589-119">Node</span></span> | <span data-ttu-id="a8589-120">Karma Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="a8589-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="a8589-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="a8589-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="a8589-122">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="a8589-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="a8589-123">.NET</span><span class="sxs-lookup"><span data-stu-id="a8589-123">.NET</span></span>
<span data-ttu-id="a8589-124">Birden çok çalışma zamanları .NET ekosistemi vardır, bu nedenle olay hub'ları için birden çok .NET kitaplıklarına vardır.</span><span class="sxs-lookup"><span data-stu-id="a8589-124">The .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="a8589-125">.NET standart kitaplığı, .NET Framework kitaplığı yalnızca bir .NET Framework ortamında çalıştırılabilir .NET Core veya .NET Framework kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8589-125">The .NET Standard library can be run using either .NET Core or the .NET Framework, while the .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="a8589-126">.NET Framework ile ilgili daha fazla bilgi için bkz: [framework sürümlerini](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="a8589-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8589-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8589-127">Next steps</span></span>
<span data-ttu-id="a8589-128">Azure geçişi hakkında daha fazla bilgi için bu bağlantıları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="a8589-128">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="a8589-129">Azure Geçiş nedir?</span><span class="sxs-lookup"><span data-stu-id="a8589-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="a8589-130">Geçiş hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="a8589-130">Relay FAQ</span></span>](relay-faq.md)