---
title: "Azure CDN önbelleğe alma davranışını sorgu dizeleriyle - Premium aaaControl | Microsoft Docs"
description: "Azure CDN sorgu dizesini önbelleğe alma denetimleri nasıl sorgu dizeleri içerdiğinde önbelleğe toobe dosyalarıdır."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="976ae-103">Denetim Azure CDN önbelleğe alma davranışını sorgu dizeleriyle - Premium</span><span class="sxs-lookup"><span data-stu-id="976ae-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="976ae-104">Standart</span><span class="sxs-lookup"><span data-stu-id="976ae-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="976ae-105">Verizon'dan Azure CDN Premium</span><span class="sxs-lookup"><span data-stu-id="976ae-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="976ae-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="976ae-106">Overview</span></span>
<span data-ttu-id="976ae-107">Sorgu dizeleri içerdiğinde önbelleğe toobe nasıl dosyalarıdır denetimleri önbelleğe alma sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="976ae-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="976ae-108">Merhaba standart ve Premium CDN ürünler sağlar hello aynı sorgu dizesini önbelleğe alma işlevselliği, ancak hello kullanıcı arabirimi farklıdır.</span><span class="sxs-lookup"><span data-stu-id="976ae-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="976ae-109">Merhaba arabirimi için bu belgede açıklanan **verizon'dan Azure CDN Premium**.</span><span class="sxs-lookup"><span data-stu-id="976ae-109">This document describes hello interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="976ae-110">İle sorgu dizesi önbelleğe alma için **akamai'den Azure CDN standart** ve **verizon'dan Azure CDN standart**, bkz: [CDN önbelleğe alma davranışını denetleme, sorgu dizeleri içeren istekleri](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="976ae-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="976ae-111">Üç modu kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="976ae-111">Three modes are available:</span></span>

* <span data-ttu-id="976ae-112">**Standart önbellek**: hello varsayılan mod budur.</span><span class="sxs-lookup"><span data-stu-id="976ae-112">**standard-cache**:  This is hello default mode.</span></span>  <span data-ttu-id="976ae-113">Merhaba CDN kenar düğümüne hello sorgu dizesi hello ilk istek ve önbellek hello varlık hello istek sahibi toohello kaynaktan geçer.</span><span class="sxs-lookup"><span data-stu-id="976ae-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="976ae-114">Merhaba önbelleğe alınan varlık süresi doluncaya kadar hello kenar düğümden sunulan tüm istekler bu varlık için hello sorgu dizesi göz ardı eder.</span><span class="sxs-lookup"><span data-stu-id="976ae-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="976ae-115">**Hayır-cache**: Bu modda, hello CDN kenar düğümüne sorgu dizeleri içeren istekleri önbelleğe alınmaz.</span><span class="sxs-lookup"><span data-stu-id="976ae-115">**no-cache**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="976ae-116">Merhaba kenar düğümüne hello varlık doğrudan hello kaynaktan alır ve her istek ile toohello istek sahibi geçirir.</span><span class="sxs-lookup"><span data-stu-id="976ae-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="976ae-117">**Önbellek benzersiz**: Bu mod, kendi önbelleği ile benzersiz bir varlık olarak bir sorgu dizesi her bir istekle değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="976ae-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="976ae-118">Örneğin, yanıt için bir istek için hello kaynaktan hello *foo.ashx?q=bar* o aynı sorgu dizesi ile sonraki önbellekler için döndürülen ve hello kenar düğümüne önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="976ae-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="976ae-119">Bir istek için *foo.ashx?q=somethingelse* toolive kendi süresiyle ayrı bir varlık olarak önbelleğe alınması.</span><span class="sxs-lookup"><span data-stu-id="976ae-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="976ae-120">Sorgu dizesini önbelleğe alma premium CDN profili ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="976ae-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="976ae-121">Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="976ae-121">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="976ae-123">Merhaba CDN Yönetim Portalı açar.</span><span class="sxs-lookup"><span data-stu-id="976ae-123">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="976ae-124">Merhaba üzerine getirin **HTTP büyük** sekmesini ve ardından hello üzerine getirin **önbellek ayarları** çıkma.</span><span class="sxs-lookup"><span data-stu-id="976ae-124">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="976ae-125">Tıklayın **sorgu dizesi önbelleğe alma**.</span><span class="sxs-lookup"><span data-stu-id="976ae-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="976ae-126">Sorgu dizesini önbelleğe alma seçenekleri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="976ae-126">Query string caching options are displayed.</span></span>
   
    ![CDN sorgu dizesini önbelleğe alma seçenekleri](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="976ae-128">Seçiminizi yaptıktan sonra hello tıklatın **güncelleştirme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="976ae-128">After making your selection, click hello **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="976ae-129">Merhaba kayıt toopropagate hello CDN aracılığıyla süredir yararlanırken hello ayarları değişiklikleri hemen görünür olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="976ae-129">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="976ae-130"><b>Verizon'dan Azure CDN</b> profilleri için yayma işlemi genellikle 90 dakika içinde tamamlanır ancak bazı durumlarda daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="976ae-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

