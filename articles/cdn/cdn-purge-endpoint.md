---
title: "Bir Azure CDN uç noktasını temizleme | Microsoft Docs"
description: "Bir Azure CDN uç noktasından tüm önbelleğe alınmış içeriği temizlenecek öğrenin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: b035c232bb58d653960190d4974cc3789d55a51d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="11cd3-103">Bir Azure CDN uç noktasını temizleme</span><span class="sxs-lookup"><span data-stu-id="11cd3-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="11cd3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="11cd3-104">Overview</span></span>
<span data-ttu-id="11cd3-105">Varlığın yaşam süresi (TTL) süresi doluncaya kadar azure CDN uç düğümleri varlıklar önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="11cd3-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="11cd3-106">Bir istemci kenar düğümden varlık istediğinde varlığın TTL süresi dolduğunda, kenar düğümüne istemci isteği sunmak için varlığı yeni güncelleştirilmiş bir kopyasını alır ve depolama önbelleği yenileyin.</span><span class="sxs-lookup"><span data-stu-id="11cd3-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span></span>

<span data-ttu-id="11cd3-107">Kullanıcılarınızın her zaman en yeni kopyasını varlıklarınızı Al emin olmak için en iyi uygulama varlıklarınızı her bir güncelleştirme sürümüdür ve bunları yeni URL'ler olarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11cd3-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="11cd3-108">CDN hemen sonraki istemci istekleri için yeni varlıklar alır.</span><span class="sxs-lookup"><span data-stu-id="11cd3-108">CDN will immediately retrieve the new assets for the next client requests.</span></span>  <span data-ttu-id="11cd3-109">Bazen önbelleğe alınmış içeriği tüm kenar düğümlerinden temizlemek ve bunları tüm yeni güncelleştirilmiş varlıklar almak için zorlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11cd3-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span></span>  <span data-ttu-id="11cd3-110">Bu, web uygulamanızı veya hızlı bir şekilde yanlış bilgiler içeren güncelleştirme varlıklar güncelleştirmeleri nedeniyle olabilir.</span><span class="sxs-lookup"><span data-stu-id="11cd3-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="11cd3-111">Temizleme, CDN uç sunucularda önbelleğe alınmış içeriği yalnızca temizler olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="11cd3-111">Note that purging only clears the cached content on the CDN edge servers.</span></span>  <span data-ttu-id="11cd3-112">Proxy sunucuları ve yerel tarayıcı önbellekleri gibi tüm aşağı akış önbellekleri yine dosyayı önbelleğe alınmış bir kopyasını tutabilir.</span><span class="sxs-lookup"><span data-stu-id="11cd3-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span></span>  <span data-ttu-id="11cd3-113">Bir dosyanın yaşam süresi ayarladığınızda unutmamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="11cd3-113">It's important to remember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="11cd3-114">Dosyanızı en son sürümünü güncelleştirmeniz her zaman benzersiz bir ad verip tarafından ya da yararlanarak istemek için bir aşağı akış istemci zorlayabilirsiniz [sorgu dizesi önbelleğe alma](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="11cd3-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="11cd3-115">Bu öğreticide, bir uç nokta tüm kenar düğümlerinden varlıklar temizleme aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="11cd3-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="11cd3-116">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="11cd3-116">Walkthrough</span></span>
1. <span data-ttu-id="11cd3-117">İçinde [Azure Portal](https://portal.azure.com), temizlemek istediğiniz uç nokta içeren CDN profili göz atın.</span><span class="sxs-lookup"><span data-stu-id="11cd3-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span></span>
2. <span data-ttu-id="11cd3-118">CDN profili dikey penceresinden Temizleme düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="11cd3-118">From the CDN profile blade, click the purge button.</span></span>
   
    ![CDN profili dikey penceresi](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="11cd3-120">Temizleme dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="11cd3-120">The Purge blade opens.</span></span>
   
    ![CDN temizleme dikey penceresi](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="11cd3-122">Temizleme dikey penceresinde, URL aşağı açılır listeden temizlemek istediğiniz hizmeti adresi seçin.</span><span class="sxs-lookup"><span data-stu-id="11cd3-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span></span>
   
    ![Form Temizle](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="11cd3-124">Tıklayarak temizleme dikey penceresine alabilirsiniz **Temizleme** CDN uç noktası dikey düğmesi.</span><span class="sxs-lookup"><span data-stu-id="11cd3-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span></span>  <span data-ttu-id="11cd3-125">Bu durumda, **URL** alan, belirli bir uç hizmeti adresiyle önceden doldurulmuş haldedir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="11cd3-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="11cd3-126">Edge düğümlerden temizlemek istediğiniz hangi varlıkları seçin.</span><span class="sxs-lookup"><span data-stu-id="11cd3-126">Select what assets you wish to purge from the edge nodes.</span></span>  <span data-ttu-id="11cd3-127">Tüm varlıklar temizlemek isterseniz, tıklatın **Tümünü Temizle** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="11cd3-127">If you wish to clear all assets, click the **Purge all** checkbox.</span></span>  <span data-ttu-id="11cd3-128">Aksi takdirde, temizlemek istediğiniz her varlık yolunu yazın **yolu** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="11cd3-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span></span> <span data-ttu-id="11cd3-129">Yolu biçimleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="11cd3-129">Below formats are supported in the path.</span></span>
    1. <span data-ttu-id="11cd3-130">**Tek URL Temizleme**: temizleme tek varlığı ile veya olmadan dosya uzantısı, örneğin, tam URL belirterek`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="11cd3-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="11cd3-131">**Joker Temizleme**: yıldız işareti (\*) joker karakter olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="11cd3-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="11cd3-132">Tüm klasörleri, alt klasörler ve dosyaları bir uç nokta altında Temizleme `/*` yolunu veya temizleme tüm alt klasörleri ve klasör belirterek belirli bir klasör altındaki dosyalar ve ardından `/*`, örn.,`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="11cd3-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="11cd3-133">Bu joker temizleme akamai'den Azure CDN tarafından şu anda desteklenmiyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="11cd3-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="11cd3-134">**Kök etki alanı Temizleme**: kök yolundaki "/" ile uç noktasının Temizle.</span><span class="sxs-lookup"><span data-stu-id="11cd3-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="11cd3-135">Yollar için temizleme belirtilmeli ve şunları sığacak göreli bir URL olmalıdır [normal ifade](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="11cd3-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="11cd3-136">**Tümünü Temizle** ve **joker Temizleme** tarafından desteklenmeyen **akamai'den Azure CDN** şu anda.</span><span class="sxs-lookup"><span data-stu-id="11cd3-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="11cd3-137">Tek URL temizleme`@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="11cd3-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="11cd3-138">Sorgu dizesi`@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="11cd3-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="11cd3-139">Joker Temizleme `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="11cd3-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="11cd3-140">Daha fazla **yolu** birden çok varlıkların listesi oluşturmanıza izin vermek için metni girdikten sonra metin kutuları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="11cd3-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="11cd3-141">Üç nokta (...) düğmesini tıklatarak listeden varlıklar silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11cd3-141">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="11cd3-142">Tıklatın **Temizleme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="11cd3-142">Click the **Purge** button.</span></span>
   
    ![Düğme Temizle](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="11cd3-144">Temizleme istekleri almak yaklaşık 2-3 ile işlemek için dakika **verizon'dan Azure CDN** (standart ve Premium) ve yaklaşık 7 dakika ile **akamai'den Azure CDN**.</span><span class="sxs-lookup"><span data-stu-id="11cd3-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="11cd3-145">Azure CDN 50 eş zamanlı istekleri herhangi bir anda temizleme bir sınıra sahiptir.</span><span class="sxs-lookup"><span data-stu-id="11cd3-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="11cd3-146">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="11cd3-146">See also</span></span>
* [<span data-ttu-id="11cd3-147">Azure CDN uç noktasında varlıkları önceden yükleme</span><span class="sxs-lookup"><span data-stu-id="11cd3-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="11cd3-148">Azure CDN REST API Başvurusu - temizlemek veya bir uç nokta önceden yükleme</span><span class="sxs-lookup"><span data-stu-id="11cd3-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

