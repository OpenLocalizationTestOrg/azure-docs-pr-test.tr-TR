---
title: "Azure CDN uç aaaPurge | Microsoft Docs"
description: "Tüm toopurge nasıl önbelleğe öğrenin Azure CDN uç noktasından içerik."
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
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="29da9-103">Bir Azure CDN uç noktasını temizleme</span><span class="sxs-lookup"><span data-stu-id="29da9-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="29da9-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="29da9-104">Overview</span></span>
<span data-ttu-id="29da9-105">Merhaba varlığın yaşam süresi (TTL) süresi doluncaya kadar azure CDN uç düğümleri varlıklar önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="29da9-105">Azure CDN edge nodes will cache assets until hello asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="29da9-106">Bir istemci hello kenar düğümden hello varlık istediğinde hello varlığın TTL dolduktan sonra hello kenar düğümüne hello varlık tooserve hello istemci isteği yeni güncelleştirilmiş bir kopyasını almak ve yenileme hello önbellek depolamak.</span><span class="sxs-lookup"><span data-stu-id="29da9-106">After hello asset's TTL expires, when a client requests hello asset from hello edge node, hello edge node will retrieve a new updated copy of hello asset tooserve hello client request and store refresh hello cache.</span></span>

<span data-ttu-id="29da9-107">varlıklarınızı her güncelleştirin ve bunları yeni URL'ler olarak yayımlamak tooversion Hello en iyi yöntem toomake kullanıcılarınızın her zaman en yeni kopyasını varlıklarınızı hello Al emin olur.</span><span class="sxs-lookup"><span data-stu-id="29da9-107">hello best practice toomake sure your users always obtain hello latest copy of your assets is tooversion your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="29da9-108">CDN hemen hello sonraki istemci istekleri için yeni varlıklar hello alır.</span><span class="sxs-lookup"><span data-stu-id="29da9-108">CDN will immediately retrieve hello new assets for hello next client requests.</span></span>  <span data-ttu-id="29da9-109">Bazen toopurge önbelleğe alınmış içeriği tüm kenar düğümlerinden ve tüm tooretrieve yeni güncelleştirilmiş varlıklar zorlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29da9-109">Sometimes you may wish toopurge cached content from all edge nodes and force them all tooretrieve new updated assets.</span></span>  <span data-ttu-id="29da9-110">Bu tooupdates tooyour web uygulaması veya yanlış bilgiler içeren tooquickly güncelleştirme varlıklar olabilir.</span><span class="sxs-lookup"><span data-stu-id="29da9-110">This might be due tooupdates tooyour web application, or tooquickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="29da9-111">Temizleme, hello yalnızca temizler, Not önbelleğe alınmış içeriği hello CDN uç sunucularda.</span><span class="sxs-lookup"><span data-stu-id="29da9-111">Note that purging only clears hello cached content on hello CDN edge servers.</span></span>  <span data-ttu-id="29da9-112">Proxy sunucuları ve yerel tarayıcı önbellekleri gibi tüm aşağı akış önbellekleri önbelleğe alınmış kopyasını hello dosyasının hala tutabilir.</span><span class="sxs-lookup"><span data-stu-id="29da9-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of hello file.</span></span>  <span data-ttu-id="29da9-113">Önemli tooremember olduğundan bu yaşam süresi bir dosyanın ayarlandığında.</span><span class="sxs-lookup"><span data-stu-id="29da9-113">It's important tooremember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="29da9-114">Bir aşağı akış istemci toorequest hello en son sürümünü dosyanızı güncelleştirmeniz her zaman benzersiz bir ad verip tarafından ya da yararlanarak zorlayabilirsiniz [sorgu dizesi önbelleğe alma](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="29da9-114">You can force a downstream client toorequest hello latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="29da9-115">Bu öğreticide, bir uç nokta tüm kenar düğümlerinden varlıklar temizleme aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="29da9-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="29da9-116">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="29da9-116">Walkthrough</span></span>
1. <span data-ttu-id="29da9-117">Merhaba, [Azure Portal](https://portal.azure.com), toopurge istediğiniz hello bitiş noktası içeren toohello CDN profili göz atın.</span><span class="sxs-lookup"><span data-stu-id="29da9-117">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopurge.</span></span>
2. <span data-ttu-id="29da9-118">Merhaba CDN profili dikey penceresinden hello Temizleme düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="29da9-118">From hello CDN profile blade, click hello purge button.</span></span>
   
    ![CDN profili dikey penceresi](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="29da9-120">Merhaba temizleme dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="29da9-120">hello Purge blade opens.</span></span>
   
    ![CDN temizleme dikey penceresi](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="29da9-122">Dikey penceresinde Hello üzerinde temizlemek, hello URL açılır gelen toopurge istediğiniz hello hizmeti adresi seçin.</span><span class="sxs-lookup"><span data-stu-id="29da9-122">On hello Purge blade, select hello service address you wish toopurge from hello URL dropdown.</span></span>
   
    ![Form Temizle](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="29da9-124">Merhaba tıklayarak da toohello temizleme dikey alabilirsiniz **Temizleme** hello CDN uç noktası dikey düğmesi.</span><span class="sxs-lookup"><span data-stu-id="29da9-124">You can also get toohello Purge blade by clicking hello **Purge** button on hello CDN endpoint blade.</span></span>  <span data-ttu-id="29da9-125">Bu durumda, hello **URL** alan hello hizmeti adresi bu belirli uç ile önceden doldurulmuş haldedir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="29da9-125">In that case, hello **URL** field will be pre-populated with hello service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="29da9-126">Hangi varlıkları kenar düğümleri hello gelen toopurge istediğiniz seçin.</span><span class="sxs-lookup"><span data-stu-id="29da9-126">Select what assets you wish toopurge from hello edge nodes.</span></span>  <span data-ttu-id="29da9-127">Tüm varlıklar tooclear isterseniz hello tıklatın **Tümünü Temizle** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="29da9-127">If you wish tooclear all assets, click hello **Purge all** checkbox.</span></span>  <span data-ttu-id="29da9-128">Aksi takdirde, her varlık türü hello yolunu toopurge hello istediğiniz **yolu** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="29da9-128">Otherwise, type hello path of each asset you wish toopurge in hello **Path** textbox.</span></span> <span data-ttu-id="29da9-129">Merhaba yolunda aşağıdaki biçimleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="29da9-129">Below formats are supported in hello path.</span></span>
    1. <span data-ttu-id="29da9-130">**Tek URL Temizleme**: temizleme tek varlığı ile veya olmadan hello dosya uzantısı, örneğin, hello tam URL belirterek`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="29da9-130">**Single URL purge**: Purge individual asset by specifying hello full URL, with or without hello file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="29da9-131">**Joker Temizleme**: yıldız işareti (\*) joker karakter olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="29da9-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="29da9-132">Tüm klasörleri, alt klasörler ve dosyaları bir uç nokta altında Temizleme `/*` hello yolu veya arkasından hello klasörünü belirterek tüm alt klasörleri ve belirli bir klasör altındaki dosyalar Temizleme `/*`, örn.,`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="29da9-132">Purge all folders, sub-folders and files under an endpoint with `/*` in hello path or purge all sub-folders and files under a specific folder by specifying hello folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="29da9-133">Bu joker temizleme akamai'den Azure CDN tarafından şu anda desteklenmiyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="29da9-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="29da9-134">**Kök etki alanı Temizleme**: hello endpoint hello yolundaki "/" ile temizleme hello kökü.</span><span class="sxs-lookup"><span data-stu-id="29da9-134">**Root domain purge**: Purge hello root of hello endpoint with "/" in hello path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="29da9-135">Yollar için temizleme belirtilmeli ve hello şunları sığacak göreli bir URL olmalıdır [normal ifade](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="29da9-135">Paths must be specified for purge and must be a relative URL that fit hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="29da9-136">**Tümünü Temizle** ve **joker Temizleme** tarafından desteklenmeyen **akamai'den Azure CDN** şu anda.</span><span class="sxs-lookup"><span data-stu-id="29da9-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="29da9-137">Tek URL temizleme`@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="29da9-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="29da9-138">Sorgu dizesi`@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="29da9-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="29da9-139">Joker Temizleme `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="29da9-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="29da9-140">Daha fazla **yolu** kutularındaki metin tooallow girdikten sonra görünür toobuild birden çok varlıkların listesi.</span><span class="sxs-lookup"><span data-stu-id="29da9-140">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="29da9-141">Merhaba üç nokta (...) düğmesini tıklatarak varlıklar hello listesinden silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29da9-141">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="29da9-142">Merhaba tıklatın **Temizleme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="29da9-142">Click hello **Purge** button.</span></span>
   
    ![Düğme Temizle](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="29da9-144">Temizleme istekleri almak yaklaşık 2-3 dakika tooprocess ile **verizon'dan Azure CDN** (standart ve Premium) ve yaklaşık 7 dakika ile **akamai'den Azure CDN**.</span><span class="sxs-lookup"><span data-stu-id="29da9-144">Purge requests take approximately 2-3 minutes tooprocess with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="29da9-145">Azure CDN 50 eş zamanlı istekleri herhangi bir anda temizleme bir sınıra sahiptir.</span><span class="sxs-lookup"><span data-stu-id="29da9-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="29da9-146">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="29da9-146">See also</span></span>
* [<span data-ttu-id="29da9-147">Azure CDN uç noktasında varlıkları önceden yükleme</span><span class="sxs-lookup"><span data-stu-id="29da9-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="29da9-148">Azure CDN REST API Başvurusu - temizlemek veya bir uç nokta önceden yükleme</span><span class="sxs-lookup"><span data-stu-id="29da9-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

