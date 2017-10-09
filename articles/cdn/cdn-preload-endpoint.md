---
title: "Azure CDN uç noktasında aaaPre yük varlıkları | Microsoft Docs"
description: "Nasıl toopre yük Azure CDN uç noktada önbelleğe alınmış içeriği öğrenin."
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
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="58376-103">Azure CDN uç noktasında varlıkları önceden yükleme</span><span class="sxs-lookup"><span data-stu-id="58376-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="58376-104">Varsayılan olarak, bunlar istendiği varlıklar ilk önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="58376-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="58376-105">Bunun anlamı hello ilk istek her bölgesinden uzun sürebilir, hello uç sunucuların değil gerekeceğinden hello içeriği önbelleğe ve tooforward hello istek toohello kaynak sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="58376-105">This means that hello first request from each region may take longer, since hello edge servers will not have hello content cached and will need tooforward hello request toohello origin server.</span></span> <span data-ttu-id="58376-106">İçeriği önceden yüklerken bu ilk isabet gecikmesini önler.</span><span class="sxs-lookup"><span data-stu-id="58376-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="58376-107">Ayrıca tooproviding önbelleğe alınmış varlıkları önceden yükleme daha iyi bir müşteri deneyimi hello kaynak sunucu üzerindeki ağ trafiğini azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="58376-107">In addition tooproviding a better customer experience, pre-loading your cached assets can also reduce network traffic on hello origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="58376-108">İçerik, kullanıcılar, yeni bir filmi sürüm veya bir yazılım güncelleştirmesi gibi çok sayıda eşzamanlı olarak kullanılabilir tooa olur veya varlıkları önceden yükleme büyük olaylar için yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="58376-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available tooa large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="58376-109">Bu öğreticide, tüm Azure CDN uç düğümlerde önbelleğe alınmış içeriği önceden yükleme aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="58376-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="58376-110">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="58376-110">Walkthrough</span></span>
1. <span data-ttu-id="58376-111">Merhaba, [Azure Portal](https://portal.azure.com), toopre yük istediğiniz hello bitiş noktası içeren toohello CDN profili göz atın.</span><span class="sxs-lookup"><span data-stu-id="58376-111">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopre-load.</span></span>  <span data-ttu-id="58376-112">Hello profili dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="58376-112">hello profile blade opens.</span></span>
2. <span data-ttu-id="58376-113">Merhaba listesinde Hello uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="58376-113">Click hello endpoint in hello list.</span></span>  <span data-ttu-id="58376-114">Merhaba uç nokta dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="58376-114">hello endpoint blade opens.</span></span>
3. <span data-ttu-id="58376-115">Merhaba CDN uç noktası dikey penceresinden hello yükle düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="58376-115">From hello CDN endpoint blade, click hello load button.</span></span>
   
    ![CDN uç noktası dikey penceresi](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="58376-117">Merhaba yük dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="58376-117">hello Load blade opens.</span></span>
   
    ![CDN yük dikey penceresi](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="58376-119">Merhaba tam yolunu girin tooload istediğiniz her varlık (örn., `/pictures/kitten.png`) hello içinde **yolu** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="58376-119">Enter hello full path of each asset you wish tooload (e.g., `/pictures/kitten.png`) in hello **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="58376-120">Daha fazla **yolu** kutularındaki metin tooallow girdikten sonra görünür toobuild birden çok varlıkların listesi.</span><span class="sxs-lookup"><span data-stu-id="58376-120">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="58376-121">Merhaba üç nokta (...) düğmesini tıklatarak varlıklar hello listesinden silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58376-121">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="58376-122">Yollar hello aşağıdaki uygun göreli bir URL olmalıdır [normal ifade](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="58376-122">Paths must be a relative URL that fits hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="58376-123">Tek bir dosya yolu yük `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="58376-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="58376-124">Sorgu dizesi tek bir dosyayı yükleme`@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="58376-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="58376-125">Her varlık, kendi yolu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="58376-125">Each asset must have its own path.</span></span>  <span data-ttu-id="58376-126">Ön yükleme varlıklar için joker karakter işlevi yoktur.</span><span class="sxs-lookup"><span data-stu-id="58376-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Yük düğmesi](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="58376-128">Merhaba tıklatın **yük** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="58376-128">Click hello **Load** button.</span></span>
   
    ![Yük düğmesi](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="58376-130">Her CDN profili dakikada 10 yük isteklerinin bir sınırlama yoktur.</span><span class="sxs-lookup"><span data-stu-id="58376-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="58376-131">İstek başına 50 yollara izin verilir.</span><span class="sxs-lookup"><span data-stu-id="58376-131">50 paths are allowed per request.</span></span> <span data-ttu-id="58376-132">Her yol 1024 karakterden oluşan bir yol uzunluğu sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="58376-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="58376-133">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="58376-133">See also</span></span>
* [<span data-ttu-id="58376-134">Bir Azure CDN uç noktasını temizleme</span><span class="sxs-lookup"><span data-stu-id="58376-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="58376-135">Azure CDN REST API Başvurusu - temizlemek veya bir uç nokta önceden yükleme</span><span class="sxs-lookup"><span data-stu-id="58376-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

