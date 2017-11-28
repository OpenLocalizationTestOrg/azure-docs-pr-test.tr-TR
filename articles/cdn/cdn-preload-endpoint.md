---
title: "Azure CDN uç noktasında varlıkları önceden yükleme | Microsoft Docs"
description: "Azure CDN uç noktada önbelleğe alınmış içeriği önceden yükleme hakkında bilgi edinin."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 1f2dcd9a91bb6e883cbef06373c1acd98bf8d45f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="23921-103">Azure CDN uç noktasında varlıkları önceden yükleme</span><span class="sxs-lookup"><span data-stu-id="23921-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="23921-104">Varsayılan olarak, bunlar istendiği varlıklar ilk önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="23921-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="23921-105">Bunun anlamı her bölge ilk istekten uzun sürebilir, uç sunucuların değil gerekeceğinden, içeriği önbelleğe'yı ve kaynak sunucuya istek iletmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="23921-105">This means that the first request from each region may take longer, since the edge servers will not have the content cached and will need to forward the request to the origin server.</span></span> <span data-ttu-id="23921-106">İçeriği önceden yüklerken bu ilk isabet gecikmesini önler.</span><span class="sxs-lookup"><span data-stu-id="23921-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="23921-107">Daha iyi bir müşteri deneyimi sağlamaya ek olarak, önbelleğe alınan varlıkları önceden yükleme da kaynak sunucu üzerindeki ağ trafiğini azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="23921-107">In addition to providing a better customer experience, pre-loading your cached assets can also reduce network traffic on the origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="23921-108">Varlıkları önceden yükleme büyük olayları veya kullanıcılar, yeni bir filmi sürüm veya bir yazılım güncelleştirmesi gibi çok sayıda eşzamanlı olarak kullanılabilir içeriği için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="23921-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available to a large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="23921-109">Bu öğreticide, tüm Azure CDN uç düğümlerde önbelleğe alınmış içeriği önceden yükleme aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="23921-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="23921-110">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="23921-110">Walkthrough</span></span>
1. <span data-ttu-id="23921-111">İçinde [Azure Portal](https://portal.azure.com), önceden yüklemek istediğiniz uç nokta içeren CDN profili göz atın.</span><span class="sxs-lookup"><span data-stu-id="23921-111">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span></span>  <span data-ttu-id="23921-112">Profili dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="23921-112">The profile blade opens.</span></span>
2. <span data-ttu-id="23921-113">Uç nokta listesinde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="23921-113">Click the endpoint in the list.</span></span>  <span data-ttu-id="23921-114">Uç nokta dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="23921-114">The endpoint blade opens.</span></span>
3. <span data-ttu-id="23921-115">CDN uç noktası dikey penceresinden Yükle düğmesini tıklayın.</span><span class="sxs-lookup"><span data-stu-id="23921-115">From the CDN endpoint blade, click the load button.</span></span>
   
    ![CDN uç noktası dikey penceresi](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="23921-117">Yük dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="23921-117">The Load blade opens.</span></span>
   
    ![CDN yük dikey penceresi](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="23921-119">Yüklemek istediğiniz her varlık tam yolunu girin (örn., `/pictures/kitten.png`) içinde **yolu** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="23921-119">Enter the full path of each asset you wish to load (e.g., `/pictures/kitten.png`) in the **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="23921-120">Daha fazla **yolu** birden çok varlıkların listesi oluşturmanıza izin vermek için metni girdikten sonra metin kutuları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="23921-120">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="23921-121">Üç nokta (...) düğmesini tıklatarak listeden varlıklar silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23921-121">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="23921-122">Yolları aşağıdaki uygun göreli bir URL olmalıdır [normal ifade](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="23921-122">Paths must be a relative URL that fits the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="23921-123">Tek bir dosya yolu yük `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="23921-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="23921-124">Sorgu dizesi tek bir dosyayı yükleme`@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="23921-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="23921-125">Her varlık, kendi yolu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="23921-125">Each asset must have its own path.</span></span>  <span data-ttu-id="23921-126">Ön yükleme varlıklar için joker karakter işlevi yoktur.</span><span class="sxs-lookup"><span data-stu-id="23921-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Yük düğmesi](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="23921-128">Tıklatın **yük** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="23921-128">Click the **Load** button.</span></span>
   
    ![Yük düğmesi](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="23921-130">Her CDN profili dakikada 10 yük isteklerinin bir sınırlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="23921-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="23921-131">İstek başına 50 yollara izin verilir.</span><span class="sxs-lookup"><span data-stu-id="23921-131">50 paths are allowed per request.</span></span> <span data-ttu-id="23921-132">Her yol 1024 karakterden oluşan bir yol uzunluğu sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="23921-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="23921-133">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="23921-133">See also</span></span>
* [<span data-ttu-id="23921-134">Bir Azure CDN uç noktasını temizleme</span><span class="sxs-lookup"><span data-stu-id="23921-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="23921-135">Azure CDN REST API Başvurusu - temizlemek veya bir uç nokta önceden yükleme</span><span class="sxs-lookup"><span data-stu-id="23921-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

