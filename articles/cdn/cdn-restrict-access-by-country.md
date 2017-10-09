---
title: "Azure CDN içeriğini ülkeye göre aaaRestrict | Microsoft Docs"
description: "Nasıl toorestrict tooyour Azure CDN içerik kullanarak erişimini izin ver hello coğrafi filtreleme özelliği hakkında bilgi edinin."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="b9793-103">Azure CDN içeriğini ülkeye göre kısıtla</span><span class="sxs-lookup"><span data-stu-id="b9793-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="b9793-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b9793-104">Overview</span></span>
<span data-ttu-id="b9793-105">Kullanıcı varsayılan olarak, içerik istediğinde, hello içerik hello kullanıcı bu istekten burada yapılan bağımsız olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="b9793-105">When a user requests your content, by default, hello content is served regardless of where hello user made this request from.</span></span> <span data-ttu-id="b9793-106">Bazı durumlarda, toorestrict erişim tooyour içerik ülkeye göre isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9793-106">In some cases, you may want toorestrict access tooyour content by country.</span></span> <span data-ttu-id="b9793-107">Bu konuda açıklanmaktadır nasıl toouse hello **coğrafi filtreleme** sipariş tooconfigure hello hizmeti tooallow veya blok erişimini ülkeye göre özelliği.</span><span class="sxs-lookup"><span data-stu-id="b9793-107">This topic explains how toouse hello **Geo-Filtering** feature in order tooconfigure hello service tooallow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9793-108">Merhaba Verizon ve Akamai ürünleri sağlamak hello aynı coğrafi filtreleme işlevselliği ancak destekledikleri arı ülke kodlarına küçük bir fark vardır.</span><span class="sxs-lookup"><span data-stu-id="b9793-108">hello Verizon and Akamai products provide hello same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="b9793-109">Adım 3'için bir bağlantı toohello farkları bakın.</span><span class="sxs-lookup"><span data-stu-id="b9793-109">See Step 3 for a link toohello differences.</span></span>


<span data-ttu-id="b9793-110">Kısıtlama, bu tür tooconfiguring dikkat edilecek noktalar hakkında bilgi için hello bkz [konuları](cdn-restrict-access-by-country.md#considerations) hello konu hello sonunda bölüm.</span><span class="sxs-lookup"><span data-stu-id="b9793-110">For information about considerations that apply tooconfiguring this type of restriction, see hello [Considerations](cdn-restrict-access-by-country.md#considerations) section at hello end of hello topic.</span></span>  

![Ülke filtreleme](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a><span data-ttu-id="b9793-112">1. adım: hello dizin yolu tanımlama</span><span class="sxs-lookup"><span data-stu-id="b9793-112">Step 1: Define hello directory path</span></span>
<span data-ttu-id="b9793-113">Uç noktanız hello portalındaki seçin ve bu özellik hello coğrafi filtreleme sekmesinde hello sol gezinti toofind bulun.</span><span class="sxs-lookup"><span data-stu-id="b9793-113">Select your endpoint within hello portal, and find hello Geo-Filtering tab on hello left-hand navigation toofind this feature.</span></span>

<span data-ttu-id="b9793-114">Bir ülke filtresi yapılandırırken hello göreli yol toohello konumu toowhich kullanıcılar izin verilen veya erişimi reddedilen belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9793-114">When configuring a country filter, you must specify hello relative path toohello location toowhich users will be allowed or denied access.</span></span> <span data-ttu-id="b9793-115">Tüm dosyaları ile coğrafi filtreleme uygulayabilirsiniz "/" veya seçili klasörler dizin yolu "/ resimler /" belirterek.</span><span class="sxs-lookup"><span data-stu-id="b9793-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="b9793-116">Ayrıca coğrafi filtreleme tooa tek dosyalı hello dosya belirterek uygulayabilirsiniz ve bırakarak hello eğik "/ resimler/şehir.PNG silebilir".</span><span class="sxs-lookup"><span data-stu-id="b9793-116">You can also apply geo-filtering tooa single file by specifying hello file, and leaving out hello trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="b9793-117">Örnek dizin yolu Filtresi:</span><span class="sxs-lookup"><span data-stu-id="b9793-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a><span data-ttu-id="b9793-118">2. adım: hello eylem tanımlama: Engelle veya izin ver</span><span class="sxs-lookup"><span data-stu-id="b9793-118">Step 2: Define hello action: block or allow</span></span>
<span data-ttu-id="b9793-119">**Engelle:** hello kullanıcılardan belirtilen ülkeler bu özyinelemeli yolundan istenen erişim tooassets izni verilmez.</span><span class="sxs-lookup"><span data-stu-id="b9793-119">**Block:** Users from hello specified countries will be denied access tooassets requested from that recursive path.</span></span> <span data-ttu-id="b9793-120">Bu konumda hiçbir diğer ülke filtreleme seçenekleri yapılandırıldıysa diğer tüm kullanıcıların erişim verilmez.</span><span class="sxs-lookup"><span data-stu-id="b9793-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="b9793-121">**İzin ver:** hello kullanıcılardan yalnızca belirtilen ülkeler bu özyinelemeli yolundan istenen erişim tooassets izin verilir.</span><span class="sxs-lookup"><span data-stu-id="b9793-121">**Allow:** Only users from hello specified countries will be allowed access tooassets requested from that recursive path.</span></span>

## <a name="step-3-define-hello-countries"></a><span data-ttu-id="b9793-122">3. adım: hello ülkelerde tanımlama</span><span class="sxs-lookup"><span data-stu-id="b9793-122">Step 3: Define hello countries</span></span>
<span data-ttu-id="b9793-123">Tooblock istediğiniz veya hello yolu için izin hello ülke seçin.</span><span class="sxs-lookup"><span data-stu-id="b9793-123">Select hello countries that you want tooblock or allow for hello path.</span></span> 

<span data-ttu-id="b9793-124">Örneğin, /Photos/Strasbourg/engelleme hello kural dosyaları dahil süzer:</span><span class="sxs-lookup"><span data-stu-id="b9793-124">For example, hello rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="b9793-125">Ülke kodu</span><span class="sxs-lookup"><span data-stu-id="b9793-125">Country codes</span></span>
<span data-ttu-id="b9793-126">Merhaba **coğrafi filtreleme** özelliği için güvenli bir dizin, bir istek izin verilen ya da engellenen ülke kodları toodefine hello ülkelerde kullanır.</span><span class="sxs-lookup"><span data-stu-id="b9793-126">hello **Geo-Filtering** feature uses country codes toodefine hello countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="b9793-127">Ülke kodu hello bulacaksınız [Azure CDN ülke kodlarına](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9793-127">You will find hello country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="b9793-128"><a id="considerations"></a>Dikkat edilecek noktalar</span><span class="sxs-lookup"><span data-stu-id="b9793-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="b9793-129">Verizon too90 dakika veya değişiklikleri tooyour ülke filtreleme yapılandırması tootake etkisi Akamai ile birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b9793-129">It may take up too90 minutes for Verizon, or a couple minutes with Akamai, for changes tooyour country filtering configuration tootake effect.</span></span>
* <span data-ttu-id="b9793-130">Bu özellik joker karakterleri desteklemez (örneğin, ' *').</span><span class="sxs-lookup"><span data-stu-id="b9793-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="b9793-131">Merhaba göreli yol ile ilişkili hello coğrafi filtreleme yapılandırması uygulanan yinelemeli olarak toothat yol olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b9793-131">hello geo-filtering configuration associated with hello relative path will be applied recursively toothat path.</span></span>
* <span data-ttu-id="b9793-132">Yalnızca bir kural uygulanan toohello olabilir aynı göreli yol (Bu noktası toohello birden fazla ülke filtre oluşturulamıyor aynı göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="b9793-132">Only one rule can be applied toohello same relative path (you cannot create multiple country filters that point toohello same relative path.</span></span> <span data-ttu-id="b9793-133">Bununla birlikte, bir klasör birden fazla ülke filtre olabilir.</span><span class="sxs-lookup"><span data-stu-id="b9793-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="b9793-134">Ülke filtreleri toohello özyinelemeli yapısı budur.</span><span class="sxs-lookup"><span data-stu-id="b9793-134">This is due toohello recursive nature of country filters.</span></span> <span data-ttu-id="b9793-135">Diğer bir deyişle, önceden yapılandırılmış bir klasörün bir alt farklı ülke filtre atanabilir.</span><span class="sxs-lookup"><span data-stu-id="b9793-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

