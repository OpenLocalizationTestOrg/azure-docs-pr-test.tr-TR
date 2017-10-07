---
title: "aaaAzure geçiş API genel bakış | Microsoft Docs"
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
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="a6202-103">Kullanılabilir geçiş API'leri</span><span class="sxs-lookup"><span data-stu-id="a6202-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="a6202-104">Çalışma zamanı API'leri</span><span class="sxs-lookup"><span data-stu-id="a6202-104">Runtime APIs</span></span>

<span data-ttu-id="a6202-105">Merhaba aşağıdaki tabloda şu anda kullanılabilir tüm geçiş çalışma zamanı istemcileri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="a6202-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="a6202-106">Merhaba [ek bilgi](#additional-information) bölüm her çalışma zamanı kitaplığı hello durumu hakkında daha fazla bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="a6202-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="a6202-107">Dil/Platform</span><span class="sxs-lookup"><span data-stu-id="a6202-107">Language/Platform</span></span> | <span data-ttu-id="a6202-108">Kullanılabilir özelliği</span><span class="sxs-lookup"><span data-stu-id="a6202-108">Available feature</span></span> | <span data-ttu-id="a6202-109">İstemci paketi</span><span class="sxs-lookup"><span data-stu-id="a6202-109">Client package</span></span> | <span data-ttu-id="a6202-110">Depo</span><span class="sxs-lookup"><span data-stu-id="a6202-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a6202-111">.NET standart</span><span class="sxs-lookup"><span data-stu-id="a6202-111">.NET Standard</span></span> | <span data-ttu-id="a6202-112">Karma Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="a6202-112">Hybrid Connections</span></span> | [<span data-ttu-id="a6202-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="a6202-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="a6202-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="a6202-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="a6202-115">.NET framework</span><span class="sxs-lookup"><span data-stu-id="a6202-115">.NET Framework</span></span> | <span data-ttu-id="a6202-116">WCF Geçişi</span><span class="sxs-lookup"><span data-stu-id="a6202-116">WCF Relay</span></span> | [<span data-ttu-id="a6202-117">WindowsAzure.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="a6202-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="a6202-118">Yok</span><span class="sxs-lookup"><span data-stu-id="a6202-118">N/A</span></span> |
| <span data-ttu-id="a6202-119">Node</span><span class="sxs-lookup"><span data-stu-id="a6202-119">Node</span></span> | <span data-ttu-id="a6202-120">Karma Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="a6202-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="a6202-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="a6202-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="a6202-122">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="a6202-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="a6202-123">.NET</span><span class="sxs-lookup"><span data-stu-id="a6202-123">.NET</span></span>
<span data-ttu-id="a6202-124">birden çok çalışma zamanları Hello .NET ekosistemi vardır, bu nedenle olay hub'ları için birden çok .NET kitaplıklarına vardır.</span><span class="sxs-lookup"><span data-stu-id="a6202-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="a6202-125">Merhaba .NET standart kitaplığı hello .NET Framework kitaplığı yalnızca bir .NET Framework ortamında çalıştırılabilir .NET Core veya Merhaba, .NET Framework kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6202-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="a6202-126">.NET Framework ile ilgili daha fazla bilgi için bkz: [framework sürümlerini](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="a6202-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6202-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6202-127">Next steps</span></span>
<span data-ttu-id="a6202-128">toolearn Azure geçişi hakkında daha fazla bilgi için bu bağlantıları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="a6202-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="a6202-129">Azure Geçiş nedir?</span><span class="sxs-lookup"><span data-stu-id="a6202-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="a6202-130">Geçiş hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="a6202-130">Relay FAQ</span></span>](relay-faq.md)