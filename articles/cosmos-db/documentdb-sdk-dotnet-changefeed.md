---
title: "aaaAzure DocumentDB .NET değişiklik akış işlemci SDK & kaynakları | Microsoft Docs"
description: "Değişiklik akış işlemci API ve SDK sürüm tarih, sona erme tarihlerini ve her bir hello DocumentDB .NET değişiklik akış işlemci SDK sürümü arasında yapılan değişiklikler dahil olmak üzere tüm hello hakkında öğrenin."
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: maquaran
ms.openlocfilehash: 7c001cc77f41c01445fb53328e9d99fd3d312c58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="62ddd-103">DocumentDB .NET değişiklik akış işlemci SDK: İndirme ve sürüm notları</span><span class="sxs-lookup"><span data-stu-id="62ddd-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="62ddd-104">.NET</span><span class="sxs-lookup"><span data-stu-id="62ddd-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="62ddd-105">.NET değişiklik besleme</span><span class="sxs-lookup"><span data-stu-id="62ddd-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="62ddd-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="62ddd-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="62ddd-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="62ddd-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="62ddd-108">Java</span><span class="sxs-lookup"><span data-stu-id="62ddd-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="62ddd-109">Python</span><span class="sxs-lookup"><span data-stu-id="62ddd-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="62ddd-110">REST</span><span class="sxs-lookup"><span data-stu-id="62ddd-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="62ddd-111">REST Kaynak Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="62ddd-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="62ddd-112">SQL</span><span class="sxs-lookup"><span data-stu-id="62ddd-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="62ddd-113">**SDK yükleme**</span><span class="sxs-lookup"><span data-stu-id="62ddd-113">**SDK download**</span></span></td><td>[<span data-ttu-id="62ddd-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="62ddd-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="62ddd-115">**API belgeleri**</span><span class="sxs-lookup"><span data-stu-id="62ddd-115">**API documentation**</span></span></td><td>[<span data-ttu-id="62ddd-116">Akış işlemci kitaplığı API başvuru belgeleri değiştirme</span><span class="sxs-lookup"><span data-stu-id="62ddd-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="62ddd-117">**Kullanmaya başlama**</span><span class="sxs-lookup"><span data-stu-id="62ddd-117">**Get started**</span></span></td><td>[<span data-ttu-id="62ddd-118">Merhaba DocumentDB değişiklik akış işlemci .NET SDK ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="62ddd-118">Get started with hello DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="62ddd-119">**Geçerli desteklenen çerçevelerden**</span><span class="sxs-lookup"><span data-stu-id="62ddd-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="62ddd-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="62ddd-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="62ddd-121">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="62ddd-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="62ddd-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="62ddd-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="62ddd-123">Yöntem tooobtain hello değişiklik akış işlenen kalan iş toobe tahmini eklendi.</span><span class="sxs-lookup"><span data-stu-id="62ddd-123">Added a method tooobtain an estimate of remaining work toobe processed in hello Change Feed.</span></span>
* <span data-ttu-id="62ddd-124">Uyumlu [DocumentDB .NET SDK'sı](documentdb-sdk-dotnet.md) sürümleri 1.13.2 ve üstü.</span><span class="sxs-lookup"><span data-stu-id="62ddd-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="62ddd-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="62ddd-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="62ddd-126">GA SDK'SI</span><span class="sxs-lookup"><span data-stu-id="62ddd-126">GA SDK</span></span>
* <span data-ttu-id="62ddd-127">Uyumlu [DocumentDB .NET SDK'sı](documentdb-sdk-dotnet.md) sürümleri 1.14.1 ve aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="62ddd-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="62ddd-128">Yayın & sona erme tarihleri</span><span class="sxs-lookup"><span data-stu-id="62ddd-128">Release & Retirement dates</span></span>
<span data-ttu-id="62ddd-129">Microsoft sağlayacaktır bildirim en az **12 ay** sipariş toosmooth hello geçiş tooa sürümü daha yeni/desteklenen bir SDK'yı devre dışı bırakmadan önce.</span><span class="sxs-lookup"><span data-stu-id="62ddd-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="62ddd-130">Yeni özellikler ve işlevsellik ve en iyi duruma getirme toohello geçerli ekleneceği yalnızca SDK, bu nedenle önerilir, her zaman yükseltme toohello en son SDK sürümünün olabildiğince erken.</span><span class="sxs-lookup"><span data-stu-id="62ddd-130">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="62ddd-131">Tüm istek tooCosmos devre dışı bırakılan bir SDK'sını kullanarak DB hello hizmeti tarafından reddedilir.</span><span class="sxs-lookup"><span data-stu-id="62ddd-131">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="62ddd-132">Sürüm</span><span class="sxs-lookup"><span data-stu-id="62ddd-132">Version</span></span> | <span data-ttu-id="62ddd-133">Sürüm tarihi</span><span class="sxs-lookup"><span data-stu-id="62ddd-133">Release Date</span></span> | <span data-ttu-id="62ddd-134">Sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="62ddd-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="62ddd-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="62ddd-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="62ddd-136">13 Ağustos 2017</span><span class="sxs-lookup"><span data-stu-id="62ddd-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="62ddd-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="62ddd-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="62ddd-138">07 Temmuz 2017</span><span class="sxs-lookup"><span data-stu-id="62ddd-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="62ddd-139">SSS</span><span class="sxs-lookup"><span data-stu-id="62ddd-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="62ddd-140">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="62ddd-140">See also</span></span>
<span data-ttu-id="62ddd-141">toolearn Cosmos DB hakkında daha fazla bilgi görmek [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmet sayfası.</span><span class="sxs-lookup"><span data-stu-id="62ddd-141">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

