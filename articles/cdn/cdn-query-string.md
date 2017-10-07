---
title: "Azure CDN önbelleğe alma davranışını sorgu dizeleriyle aaaControl | Microsoft Docs"
description: "Azure CDN sorgu dizesini önbelleğe alma denetimleri nasıl sorgu dizeleri içerdiğinde önbelleğe toobe dosyalarıdır."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="3c38a-103">Denetim Azure CDN önbelleğe alma davranışını sorgu dizeleriyle etkinleştirmek</span><span class="sxs-lookup"><span data-stu-id="3c38a-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c38a-104">Standart</span><span class="sxs-lookup"><span data-stu-id="3c38a-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="3c38a-105">Verizon'dan Azure CDN Premium</span><span class="sxs-lookup"><span data-stu-id="3c38a-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="3c38a-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3c38a-106">Overview</span></span>
<span data-ttu-id="3c38a-107">Sorgu dizeleri içerdiğinde önbelleğe toobe nasıl dosyalarıdır denetimleri önbelleğe alma sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="3c38a-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c38a-108">Merhaba standart ve Premium CDN ürünler sağlar hello aynı sorgu dizesini önbelleğe alma işlevselliği, ancak hello kullanıcı arabirimi farklıdır.</span><span class="sxs-lookup"><span data-stu-id="3c38a-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="3c38a-109">Merhaba arabirimi için bu belgede açıklanan **akamai'den Azure CDN standart** ve **verizon'dan Azure CDN standart**.</span><span class="sxs-lookup"><span data-stu-id="3c38a-109">This document describes hello interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="3c38a-110">İle sorgu dizesi önbelleğe alma için **verizon'dan Azure CDN Premium**, bkz: [CDN önbelleğe alma davranışını denetleme istekleri sorgu dizeleriyle - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="3c38a-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="3c38a-111">Üç modu kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="3c38a-111">Three modes are available:</span></span>

* <span data-ttu-id="3c38a-112">**Sorgu dizelerini yoksayabilir**: hello varsayılan mod budur.</span><span class="sxs-lookup"><span data-stu-id="3c38a-112">**Ignore query strings**:  This is hello default mode.</span></span>  <span data-ttu-id="3c38a-113">Merhaba CDN kenar düğümüne hello sorgu dizesi hello ilk istek ve önbellek hello varlık hello istek sahibi toohello kaynaktan geçer.</span><span class="sxs-lookup"><span data-stu-id="3c38a-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="3c38a-114">Merhaba önbelleğe alınan varlık süresi doluncaya kadar hello kenar düğümden sunulan tüm istekler bu varlık için hello sorgu dizesi göz ardı eder.</span><span class="sxs-lookup"><span data-stu-id="3c38a-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="3c38a-115">**Sorgu dizeleri içeren URL için önbelleğe almayı atla**: Bu modda, hello CDN kenar düğümüne sorgu dizeleri içeren istekleri önbelleğe alınmaz.</span><span class="sxs-lookup"><span data-stu-id="3c38a-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="3c38a-116">Merhaba kenar düğümüne hello varlık doğrudan hello kaynaktan alır ve her istek ile toohello istek sahibi geçirir.</span><span class="sxs-lookup"><span data-stu-id="3c38a-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="3c38a-117">**Her benzersiz URL'yi önbelleğe**: Bu mod, kendi önbelleği ile benzersiz bir varlık olarak bir sorgu dizesi her bir istekle değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="3c38a-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="3c38a-118">Örneğin, yanıt için bir istek için hello kaynaktan hello *foo.ashx?q=bar* o aynı sorgu dizesi ile sonraki önbellekler için döndürülen ve hello kenar düğümüne önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="3c38a-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="3c38a-119">Bir istek için *foo.ashx?q=somethingelse* toolive kendi süresiyle ayrı bir varlık olarak önbelleğe alınması.</span><span class="sxs-lookup"><span data-stu-id="3c38a-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="3c38a-120">Sorgu dizesini önbelleğe alma standart CDN profili ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="3c38a-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="3c38a-121">Merhaba CDN profili dikey penceresinden toomanage istediğiniz hello CDN uç noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3c38a-121">From hello CDN profile blade, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![CDN profili dikey uç noktaları](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="3c38a-123">Merhaba CDN uç noktası dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="3c38a-123">hello CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="3c38a-124">Merhaba tıklatın **yapılandırma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3c38a-124">Click hello **Configure** button.</span></span>
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="3c38a-126">Merhaba CDN yapılandırma dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="3c38a-126">hello CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="3c38a-127">Merhaba bir ayar seçin **sorgu dizesini önbelleğe alma davranışı** açılır.</span><span class="sxs-lookup"><span data-stu-id="3c38a-127">Select a setting from hello **Query string caching behavior** dropdown.</span></span>
   
    ![CDN sorgu dizesini önbelleğe alma seçenekleri](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="3c38a-129">Seçiminizi yaptıktan sonra hello tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3c38a-129">After making your selection, click hello **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c38a-130">Merhaba kayıt toopropagate hello CDN aracılığıyla süredir yararlanırken hello ayarları değişiklikleri hemen görünür olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="3c38a-130">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="3c38a-131"><b>Akamai'den Azure CDN</b> profilleri için yayma işlemi genellikle bir dakika içinde tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="3c38a-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="3c38a-132"><b>Verizon'dan Azure CDN</b> profilleri için yayma işlemi genellikle 90 dakika içinde tamamlanır ancak bazı durumlarda daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="3c38a-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

