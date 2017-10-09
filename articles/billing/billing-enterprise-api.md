---
title: aaaAzure faturalama Kurumsal API'leri | Microsoft Docs
description: "Kuruluş Azure müşterilerin toopull Tüketim verileri programlı olarak sağlayan raporlama API Hello hakkında bilgi edinin."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="42df9-103">Kurumsal müşteriler için raporlama API'leri genel bakış</span><span class="sxs-lookup"><span data-stu-id="42df9-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="42df9-104">Merhaba raporlama API'leri kuruluş Azure müşterilerin tooprogrammatically çekme kullanım ve fatura veri tercih edilen veri çözümleme araçları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="42df9-104">hello Reporting APIs enable Enterprise Azure customers tooprogrammatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-toohello-api"></a><span data-ttu-id="42df9-105">Veri erişim toohello API etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="42df9-105">Enabling data access toohello API</span></span>
* <span data-ttu-id="42df9-106">**Oluşturmak veya hello API anahtarı alıp** - günlük - Yardım altında toohello Enterprise portal ve izleme hello öğreticide raporlama API'leri.</span><span class="sxs-lookup"><span data-stu-id="42df9-106">**Generate or retrieve hello API key** - Log in toohello Enterprise portal and follow hello tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="42df9-107">Bu Yardım makalenin ilk bölümünde Hello nasıl toogenerate veya alma hello API anahtarı hello için kayıt belirtilen açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="42df9-107">hello first section under this help article explains how toogenerate or retrieve hello API key for hello specified enrollment.</span></span>
* <span data-ttu-id="42df9-108">**Merhaba API anahtarları geçirme** -hello API anahtarı kimlik doğrulaması ve yetkilendirme her çağrı için geçirilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="42df9-108">**Passing keys in hello API** - hello API key needs toobe passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="42df9-109">Merhaba aşağıdaki özellik toobe toohello HTTP üstbilgileri olması gerekiyor</span><span class="sxs-lookup"><span data-stu-id="42df9-109">hello following property needs toobe toohello HTTP headers</span></span>

|<span data-ttu-id="42df9-110">Üstbilgi anahtarı iste</span><span class="sxs-lookup"><span data-stu-id="42df9-110">Request Header Key</span></span> | <span data-ttu-id="42df9-111">Değer</span><span class="sxs-lookup"><span data-stu-id="42df9-111">Value</span></span>|
|-|-|
|<span data-ttu-id="42df9-112">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="42df9-112">Authorization</span></span>| <span data-ttu-id="42df9-113">Merhaba değer şu biçimde belirtin: **taşıyıcı {apı_key}**</span><span class="sxs-lookup"><span data-stu-id="42df9-113">Specify hello value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="42df9-114">Örnek: taşıyıcı eyr... 09</span><span class="sxs-lookup"><span data-stu-id="42df9-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="42df9-115">Tüketim API'leri</span><span class="sxs-lookup"><span data-stu-id="42df9-115">Consumption APIs</span></span>
<span data-ttu-id="42df9-116">Swagger uç nokta kullanılabilir [burada](https://consumption.azure.com/swagger/ui/index) Merhaba API'leri altında etkinleştir kolay introspection hello API ve hello özelliği toogenerate istemci SDK'ları kullanma konusunda açıklandığı [AutoRest](https://github.com/Azure/AutoRest) veya [ CodeGen swagger](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="42df9-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for hello APIs described below which should enable easy introspection of hello API and hello ability toogenerate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="42df9-117">1 Mayıs 2014 başlayan veriler bu API aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="42df9-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="42df9-118">**Yük Dengeleme ve Özet** - hello [dengelemek ve Özet API](billing-enterprise-api-balance-summary.md) aylık bakiyelerini, yeni satın alma işlemleri, Azure Marketi servis ücretleri, ayarlamalar ve fazla kullanım ücretleri bilgilerin özetini sunar.</span><span class="sxs-lookup"><span data-stu-id="42df9-118">**Balance and Summary** - hello [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="42df9-119">**Kullanım ayrıntılarını** - hello [kullanım ayrıntı API'si](billing-enterprise-api-usage-detail.md) tüketilen miktarları ve bir kayıt tarafından tahmini ücretleri günlük bir dökümü sunar.</span><span class="sxs-lookup"><span data-stu-id="42df9-119">**Usage Details** - hello [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="42df9-120">Merhaba sonuç ayrıca örnekleri, Ölçümler ve Departmanlar hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="42df9-120">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="42df9-121">Merhaba API, faturalama dönemi veya belirtilen başlangıç ve bitiş tarihi tarafından sorgulanabilir.</span><span class="sxs-lookup"><span data-stu-id="42df9-121">hello API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="42df9-122">**Market deposu ücret** - hello [Market deposu ücret API](billing-enterprise-api-marketplace-storecharge.md) hello Faturalama dönem veya (bir kez ücretleri olmayan dahil) başlangıç ve bitiş tarihleri belirtilen için hello kullanım tabanlı Market ücretleri dökümü güne göre döndürür. .</span><span class="sxs-lookup"><span data-stu-id="42df9-122">**Marketplace Store Charge** - hello [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="42df9-123">**Fiyat listesi** - hello [fiyat listesi API](billing-enterprise-api-pricesheet.md) verilen kayıt ve faturalama dönemi hello her ölçer hello geçerli hızı sunar.</span><span class="sxs-lookup"><span data-stu-id="42df9-123">**Price Sheet** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="42df9-124">Yardımcısı API'ları</span><span class="sxs-lookup"><span data-stu-id="42df9-124">Helper APIs</span></span>
 <span data-ttu-id="42df9-125">**Liste faturalama nokta** - hello [faturalama nokta API](billing-enterprise-api-billing-periods.md) Tüketim verileri hello kayıt ters kronolojik sırada belirtilen için olan nokta faturalama bir liste döndürür.</span><span class="sxs-lookup"><span data-stu-id="42df9-125">**List Billing Periods** - hello [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="42df9-126">Her dönem toohello API rota verilerini - BalanceSummary, UsageDetails, Market ücretleri ve fiyat listesi hello dört kümeleri için işaret eden bir özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="42df9-126">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="42df9-127">API yanıt kodları</span><span class="sxs-lookup"><span data-stu-id="42df9-127">API Response Codes</span></span>  
|<span data-ttu-id="42df9-128">Yanıt durum kodu</span><span class="sxs-lookup"><span data-stu-id="42df9-128">Response Status Code</span></span>|<span data-ttu-id="42df9-129">İleti</span><span class="sxs-lookup"><span data-stu-id="42df9-129">Message</span></span>|<span data-ttu-id="42df9-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="42df9-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="42df9-131">200</span><span class="sxs-lookup"><span data-stu-id="42df9-131">200</span></span>| <span data-ttu-id="42df9-132">TAMAM</span><span class="sxs-lookup"><span data-stu-id="42df9-132">OK</span></span>|<span data-ttu-id="42df9-133">Hiçbir hata</span><span class="sxs-lookup"><span data-stu-id="42df9-133">No error</span></span>|
|<span data-ttu-id="42df9-134">401</span><span class="sxs-lookup"><span data-stu-id="42df9-134">401</span></span>| <span data-ttu-id="42df9-135">Yetkilendirilmemiş</span><span class="sxs-lookup"><span data-stu-id="42df9-135">Unauthorized</span></span>| <span data-ttu-id="42df9-136">API anahtarı bulunamadı, geçersiz, vb. süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="42df9-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="42df9-137">404</span><span class="sxs-lookup"><span data-stu-id="42df9-137">404</span></span>| <span data-ttu-id="42df9-138">Kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="42df9-138">Unavailable</span></span>| <span data-ttu-id="42df9-139">Rapor uç noktası bulunamadı</span><span class="sxs-lookup"><span data-stu-id="42df9-139">Report endpoint not found</span></span>|
|<span data-ttu-id="42df9-140">400</span><span class="sxs-lookup"><span data-stu-id="42df9-140">400</span></span>| <span data-ttu-id="42df9-141">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="42df9-141">Bad Request</span></span>| <span data-ttu-id="42df9-142">Geçersiz params – tarih aralıkları EA numaralarını vb..</span><span class="sxs-lookup"><span data-stu-id="42df9-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="42df9-143">500</span><span class="sxs-lookup"><span data-stu-id="42df9-143">500</span></span>| <span data-ttu-id="42df9-144">Sunucu hatası</span><span class="sxs-lookup"><span data-stu-id="42df9-144">Server Error</span></span>| <span data-ttu-id="42df9-145">İstek işleme Unexoected hatası</span><span class="sxs-lookup"><span data-stu-id="42df9-145">Unexoected error processing request</span></span>| 









