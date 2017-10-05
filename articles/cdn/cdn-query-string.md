---
title: "Azure CDN önbelleğe alma davranışını sorgu dizeleriyle denetleme | Microsoft Docs"
description: "Azure CDN sorgu dizesini önbelleğe alma dosyaları nasıl sorgu dizeleri içerdiğinde önbelleğe alınacağını kontrol eder."
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
ms.openlocfilehash: 8d79626fa8516f226a82d3dac693c2033904c91d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="112b9-103">Denetim Azure CDN önbelleğe alma davranışını sorgu dizeleriyle etkinleştirmek</span><span class="sxs-lookup"><span data-stu-id="112b9-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="112b9-104">Standart</span><span class="sxs-lookup"><span data-stu-id="112b9-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="112b9-105">Verizon'dan Azure CDN Premium</span><span class="sxs-lookup"><span data-stu-id="112b9-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="112b9-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="112b9-106">Overview</span></span>
<span data-ttu-id="112b9-107">Sorgu dizesini dosyaları nasıl sorgu dizeleri içerdiğinde önbelleğe alınacağını denetimleri önbelleğe alma.</span><span class="sxs-lookup"><span data-stu-id="112b9-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="112b9-108">Standart ve Premium CDN ürünleri için önbelleğe alma işlevinin aynı sorgu dizesi sağlasa da, kullanıcı arabirimi farklıdır.</span><span class="sxs-lookup"><span data-stu-id="112b9-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="112b9-109">Arabirim için bu belgede açıklanan **akamai'den Azure CDN standart** ve **verizon'dan Azure CDN standart**.</span><span class="sxs-lookup"><span data-stu-id="112b9-109">This document describes the interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="112b9-110">İle sorgu dizesi önbelleğe alma için **verizon'dan Azure CDN Premium**, bkz: [CDN önbelleğe alma davranışını denetleme istekleri sorgu dizeleriyle - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="112b9-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="112b9-111">Üç modu kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="112b9-111">Three modes are available:</span></span>

* <span data-ttu-id="112b9-112">**Sorgu dizelerini yoksayabilir**: Bu varsayılan moddur.</span><span class="sxs-lookup"><span data-stu-id="112b9-112">**Ignore query strings**:  This is the default mode.</span></span>  <span data-ttu-id="112b9-113">CDN kenar düğümüne sorgu dizesi istek sahibi kaynağa ilk istek ve önbellek varlık geçer.</span><span class="sxs-lookup"><span data-stu-id="112b9-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="112b9-114">Önbelleğe alınan varlık süresi doluncaya kadar kenar düğümden sunulan tüm istekler bu varlık için sorgu dizesi göz ardı eder.</span><span class="sxs-lookup"><span data-stu-id="112b9-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="112b9-115">**Sorgu dizeleri içeren URL için önbelleğe almayı atla**: Bu modda, CDN kenar düğümüne sorgu dizeleri içeren istekleri önbelleğe alınmaz.</span><span class="sxs-lookup"><span data-stu-id="112b9-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="112b9-116">Kenar düğümüne doğrudan kaynaktan varlığı alır ve bunu her istek ile istek sahibi geçirir.</span><span class="sxs-lookup"><span data-stu-id="112b9-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="112b9-117">**Her benzersiz URL'yi önbelleğe**: Bu mod, kendi önbelleği ile benzersiz bir varlık olarak bir sorgu dizesi her bir istekle değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="112b9-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="112b9-118">Örneğin, bir istek için başlangıç yanıttan *foo.ashx?q=bar* o aynı sorgu dizesi ile sonraki önbellekler için döndürülen ve kenar düğümüne önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="112b9-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="112b9-119">Bir istek için *foo.ashx?q=somethingelse* canlı bir ayrı varlık kendi süresiyle önbelleğe alınması.</span><span class="sxs-lookup"><span data-stu-id="112b9-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="112b9-120">Sorgu dizesini önbelleğe alma standart CDN profili ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="112b9-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="112b9-121">CDN profili dikey penceresinden, yönetmek istediğiniz CDN uç noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="112b9-121">From the CDN profile blade, click the CDN endpoint you wish to manage.</span></span>
   
    ![CDN profili dikey uç noktaları](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="112b9-123">CDN uç noktası dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="112b9-123">The CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="112b9-124">Tıklatın **yapılandırma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="112b9-124">Click the **Configure** button.</span></span>
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="112b9-126">CDN yapılandırma dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="112b9-126">The CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="112b9-127">Bir ayar seçin **sorgu dizesini önbelleğe alma davranışı** açılır.</span><span class="sxs-lookup"><span data-stu-id="112b9-127">Select a setting from the **Query string caching behavior** dropdown.</span></span>
   
    ![CDN sorgu dizesini önbelleğe alma seçenekleri](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="112b9-129">Seçiminizi yaptıktan sonra tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="112b9-129">After making your selection, click the **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="112b9-130">Kaydın yayılması zaman yararlanırken ayar değişiklikleri hemen görünür olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="112b9-130">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="112b9-131"><b>Akamai'den Azure CDN</b> profilleri için yayma işlemi genellikle bir dakika içinde tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="112b9-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="112b9-132"><b>Verizon'dan Azure CDN</b> profilleri için yayma işlemi genellikle 90 dakika içinde tamamlanır ancak bazı durumlarda daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="112b9-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

