---
title: "Azure CDN içeriğini ülkeye göre kısıtla | Microsoft Docs"
description: "Erişim coğrafi filtreleme özelliğini kullanarak, Azure CDN içeriğine erişimi kısıtlamak öğrenin."
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
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="6963e-103">Azure CDN içeriğini ülkeye göre kısıtla</span><span class="sxs-lookup"><span data-stu-id="6963e-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="6963e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6963e-104">Overview</span></span>
<span data-ttu-id="6963e-105">Kullanıcı varsayılan olarak, içerik istediğinde, içerik kullanıcı bu istekten burada yapılan bağımsız olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="6963e-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="6963e-106">Bazı durumlarda, içeriğinizi ülkeye göre erişimi sınırlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6963e-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="6963e-107">Bu konuda nasıl kullanılacağı açıklanmaktadır **coğrafi filtreleme** izin vermek veya ülkeye göre erişimi engellemek için bu hizmeti yapılandırmak için özellik.</span><span class="sxs-lookup"><span data-stu-id="6963e-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6963e-108">Verizon ve Akamai ürünleri aynı coğrafi filtreleme işlevselliği sağlar ancak destekledikleri arı ülke kodlarına küçük bir fark vardır.</span><span class="sxs-lookup"><span data-stu-id="6963e-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="6963e-109">Adım 3 farklar bağlantısına bakın.</span><span class="sxs-lookup"><span data-stu-id="6963e-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="6963e-110">Bu tür bir kısıtlama yapılandırma için geçerli konuları hakkında daha fazla bilgi için bkz: [konuları](cdn-restrict-access-by-country.md#considerations) konunun sonunda bölüm.</span><span class="sxs-lookup"><span data-stu-id="6963e-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![Ülke filtreleme](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="6963e-112">1. adım: dizin yolu tanımlama</span><span class="sxs-lookup"><span data-stu-id="6963e-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="6963e-113">Uç noktanız portalındaki seçin ve bu özelliği bulmak için sol gezinti coğrafi filtreleme sekmesini bulun.</span><span class="sxs-lookup"><span data-stu-id="6963e-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="6963e-114">Bir ülke filtresi yapılandırırken, kullanıcılar izin verilen ya da erişim reddedildi konumunun göreli yolunu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6963e-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="6963e-115">Tüm dosyaları ile coğrafi filtreleme uygulayabilirsiniz "/" veya seçili klasörler dizin yolu "/ resimler /" belirterek.</span><span class="sxs-lookup"><span data-stu-id="6963e-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="6963e-116">Ayrıca coğrafi filtreleme tek bir dosyaya dosyasını belirtmek ve eğik bırakarak uygulayabilirsiniz "/ resimler/şehir.PNG silebilir".</span><span class="sxs-lookup"><span data-stu-id="6963e-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="6963e-117">Örnek dizin yolu Filtresi:</span><span class="sxs-lookup"><span data-stu-id="6963e-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="6963e-118">2. adım: eylem tanımlama: Engelle veya izin ver</span><span class="sxs-lookup"><span data-stu-id="6963e-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="6963e-119">**Engelle:** belirtilen ülkelerin kullanıcılardan izni verilmez erişim o özyinelemeli yolundan istenen varlıklar için.</span><span class="sxs-lookup"><span data-stu-id="6963e-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="6963e-120">Bu konumda hiçbir diğer ülke filtreleme seçenekleri yapılandırıldıysa diğer tüm kullanıcıların erişim verilmez.</span><span class="sxs-lookup"><span data-stu-id="6963e-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="6963e-121">**İzin ver:** yalnızca belirtilen ülkelerin kullanıcılardan, özyinelemeli yolundan istenen varlıklarına erişimine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6963e-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="6963e-122">3. adım: ülkelerin tanımlama</span><span class="sxs-lookup"><span data-stu-id="6963e-122">Step 3: Define the countries</span></span>
<span data-ttu-id="6963e-123">Engellemek veya yolu için izin vermek istediğiniz ülkelerin seçin.</span><span class="sxs-lookup"><span data-stu-id="6963e-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="6963e-124">Örneğin, /Photos/Strasbourg/engelleme kuralı dosyaları dahil süzer:</span><span class="sxs-lookup"><span data-stu-id="6963e-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="6963e-125">Ülke kodu</span><span class="sxs-lookup"><span data-stu-id="6963e-125">Country codes</span></span>
<span data-ttu-id="6963e-126">**Coğrafi filtreleme** özelliği, bir istek izin verilen ya da güvenli bir dizin için engellenen ülkelerin tanımlamak için ülke kodlarına kullanır.</span><span class="sxs-lookup"><span data-stu-id="6963e-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="6963e-127">Ülke kodu bulacaksınız [Azure CDN ülke kodlarına](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="6963e-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="6963e-128"><a id="considerations"></a>Dikkat edilecek noktalar</span><span class="sxs-lookup"><span data-stu-id="6963e-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="6963e-129">Verizon veya Akamai, birkaç dakika yapılandırmasının devreye girmesi için filtreleme ülkeniz değişiklikleri 90 dakikaya kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="6963e-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="6963e-130">Bu özellik joker karakterleri desteklemez (örneğin, ' *').</span><span class="sxs-lookup"><span data-stu-id="6963e-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="6963e-131">Göreli yol ile ilişkili coğrafi filtreleme yapılandırması yol uygulanan yinelemeli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6963e-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="6963e-132">Yalnızca bir kural (noktası aynı göreli yolu için birden fazla ülke filtre oluşturulamıyor. aynı göreli yol uygulanabilir</span><span class="sxs-lookup"><span data-stu-id="6963e-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="6963e-133">Bununla birlikte, bir klasör birden fazla ülke filtre olabilir.</span><span class="sxs-lookup"><span data-stu-id="6963e-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="6963e-134">Ülke filtreleri özyinelemeli doğası nedeniyle budur.</span><span class="sxs-lookup"><span data-stu-id="6963e-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="6963e-135">Diğer bir deyişle, önceden yapılandırılmış bir klasörün bir alt farklı ülke filtre atanabilir.</span><span class="sxs-lookup"><span data-stu-id="6963e-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

