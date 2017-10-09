---
title: "aaaAzure Media Services hata kodları | Microsoft Docs"
description: "Merhaba konu Azure Media Services hata kodları genel bir bakış sağlar."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a><span data-ttu-id="156b6-103">Azure Media Services hata kodları</span><span class="sxs-lookup"><span data-stu-id="156b6-103">Azure Media Services error codes</span></span>
<span data-ttu-id="156b6-104">Microsoft Azure Media Services kullanırken, Media Services desteklenmez tooactions zaman aşımına uğramak kimlik doğrulama belirteçleri gibi sorunları bağlı olarak hello hizmetinden HTTP hata kodları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="156b6-104">When using Microsoft Azure Media Services, you may receive HTTP error codes from hello service depending on issues such as authentication tokens expiring tooactions that are not supported in Media Services.</span></span> <span data-ttu-id="156b6-105">Merhaba bir listesi aşağıda verilmiştir **HTTP hata kodları** , döndürülüp döndürülmediğini Media Services tarafından ve bunlar için hello olası neden olur.</span><span class="sxs-lookup"><span data-stu-id="156b6-105">hello following is a list of **HTTP error codes** that may be returned by Media Services and hello possible causes for them.</span></span>  

## <a name="400-bad-request"></a><span data-ttu-id="156b6-106">400 Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="156b6-106">400 Bad Request</span></span>
<span data-ttu-id="156b6-107">Merhaba isteği geçersiz bilgiler içeriyor ve son reddedilir nedenleri aşağıdaki hello tooone:</span><span class="sxs-lookup"><span data-stu-id="156b6-107">hello request contains invalid information and is rejected due tooone of hello following reasons:</span></span>

* <span data-ttu-id="156b6-108">Desteklenmeyen bir API sürümü belirtildi.</span><span class="sxs-lookup"><span data-stu-id="156b6-108">An unsupported API version is specified.</span></span> <span data-ttu-id="156b6-109">Merhaba en güncel sürümü için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="156b6-109">For hello most current version, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="156b6-110">Media Services Hello API sürümü belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="156b6-110">hello API version of Media Services is not specified.</span></span> <span data-ttu-id="156b6-111">Nasıl toospecify hello API sürümü hakkında daha fazla bilgi için bkz: [Media Services Operations REST API Başvurusu](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="156b6-111">For information on how toospecify hello API version, see [Media Services Operations REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="156b6-112">Merhaba .NET veya Java SDK'ları tooconnect tooMedia kullanıyorsanız, hizmetleri, hello API sürümü belirtildi sizin için ne zaman deneyin ve Media Services karşı bazı eylemler gerçekleştirme.</span><span class="sxs-lookup"><span data-stu-id="156b6-112">If you are using hello .NET or Java SDKs tooconnect tooMedia Services, hello API version is specified for you whenever you try and perform some action against Media Services.</span></span>
  > 
  > 
* <span data-ttu-id="156b6-113">Tanımlanmamış özellik belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="156b6-113">An undefined property has been specified.</span></span> <span data-ttu-id="156b6-114">Merhaba hata iletisinde Hello özelliği adıdır.</span><span class="sxs-lookup"><span data-stu-id="156b6-114">hello property name is in hello error message.</span></span> <span data-ttu-id="156b6-115">Belirli bir varlık üyeleri olan özellikler belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="156b6-115">Only those properties that are members of a given entity can be specified.</span></span> <span data-ttu-id="156b6-116">Bkz: [Azure Media Services REST API Başvurusu](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) varlıkları ve özelliklerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="156b6-116">See [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) for a list of entities and their properties.</span></span>
* <span data-ttu-id="156b6-117">Geçersiz bir özellik değeri belirtildi.</span><span class="sxs-lookup"><span data-stu-id="156b6-117">An invalid property value has been specified.</span></span> <span data-ttu-id="156b6-118">Merhaba hata iletisinde Hello özelliği adıdır.</span><span class="sxs-lookup"><span data-stu-id="156b6-118">hello property name is in hello error message.</span></span> <span data-ttu-id="156b6-119">Merhaba önceki bağlantı için geçerli özellik türleri ve değerleri bakın.</span><span class="sxs-lookup"><span data-stu-id="156b6-119">See hello previous link for valid property types and their values.</span></span>
* <span data-ttu-id="156b6-120">Bir özellik değeri eksik ve gereklidir.</span><span class="sxs-lookup"><span data-stu-id="156b6-120">A property value is missing and is required.</span></span>
* <span data-ttu-id="156b6-121">Belirtilen hello URL parçası hatalı bir değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="156b6-121">Part of hello URL specified contains a bad value.</span></span>
* <span data-ttu-id="156b6-122">Bir girişim yapıldı WriteOnce özelliği tooupdate yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-122">An attempt was made tooupdate a WriteOnce property.</span></span>
* <span data-ttu-id="156b6-123">Bir girişim yapıldı belirtilmedi veya belirlenemedi birincil bir AssetFile Giriş bir varlığı olan bir işi toocreate yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-123">An attempt was made toocreate a Job that has an input Asset with a primary AssetFile that was not specified or could not be determined.</span></span>
* <span data-ttu-id="156b6-124">Bir girişim yapıldı tooupdate bir SAS Bulucu yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-124">An attempt was made tooupdate a SAS Locator.</span></span> <span data-ttu-id="156b6-125">SAS bulucular yalnızca oluşturulan veya silinebilir.</span><span class="sxs-lookup"><span data-stu-id="156b6-125">SAS locators can only be created or deleted.</span></span> <span data-ttu-id="156b6-126">Bulucular akış güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="156b6-126">Streaming locators can be updated.</span></span> <span data-ttu-id="156b6-127">Daha fazla bilgi için bkz: [Bulucular](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="156b6-127">For more information, see [Locators](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>
* <span data-ttu-id="156b6-128">Desteklenmeyen bir işlem veya sorgu gönderildi.</span><span class="sxs-lookup"><span data-stu-id="156b6-128">An unsupported operation or query was submitted.</span></span>

## <a name="401-unauthorized"></a><span data-ttu-id="156b6-129">401 Yetkisiz</span><span class="sxs-lookup"><span data-stu-id="156b6-129">401 Unauthorized</span></span>
<span data-ttu-id="156b6-130">Hello isteği olmayan kimlik doğrulaması (bunu yetkilendirilebilir önce) son tooone hello aşağıdaki nedenlerden biri:</span><span class="sxs-lookup"><span data-stu-id="156b6-130">hello request could not be authenticated (before it can be authorized) due tooone of hello following reasons:</span></span>

* <span data-ttu-id="156b6-131">Kimlik doğrulama üstbilgisi eksik.</span><span class="sxs-lookup"><span data-stu-id="156b6-131">Missing authentication header.</span></span>
* <span data-ttu-id="156b6-132">Hatalı kimlik doğrulaması üstbilgi değeri.</span><span class="sxs-lookup"><span data-stu-id="156b6-132">Bad authentication header value.</span></span>
  * <span data-ttu-id="156b6-133">Merhaba belirtecinin süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="156b6-133">hello token has expired.</span></span> 
  * <span data-ttu-id="156b6-134">Merhaba belirteci geçersiz bir imza içeriyor.</span><span class="sxs-lookup"><span data-stu-id="156b6-134">hello token contains an invalid signature.</span></span>

## <a name="403-forbidden"></a><span data-ttu-id="156b6-135">403 Yasak</span><span class="sxs-lookup"><span data-stu-id="156b6-135">403 Forbidden</span></span>
<span data-ttu-id="156b6-136">Merhaba isteği son verilmez nedenleri aşağıdaki hello tooone:</span><span class="sxs-lookup"><span data-stu-id="156b6-136">hello request is not allowed due tooone of hello following reasons:</span></span>

* <span data-ttu-id="156b6-137">Merhaba Media Services hesabı bulunamadı veya silinmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="156b6-137">hello Media Services account cannot be found or has been deleted.</span></span>
* <span data-ttu-id="156b6-138">Merhaba Media Services hesabı devre dışı bırakılır ve HTTP GET hello istek türü değil.</span><span class="sxs-lookup"><span data-stu-id="156b6-138">hello Media Services account is disabled and hello request type is not HTTP GET.</span></span> <span data-ttu-id="156b6-139">Hizmet işlemleri de 403 bir yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="156b6-139">Service operations will return a 403 response as well.</span></span>
* <span data-ttu-id="156b6-140">Merhaba kimlik doğrulama belirteci hello kullanıcının kimlik bilgileri içermiyor: AccountName ve/veya Subscriptionıd.</span><span class="sxs-lookup"><span data-stu-id="156b6-140">hello authentication token does not contain hello user’s credential information: AccountName and/or SubscriptionId.</span></span> <span data-ttu-id="156b6-141">Media Services hesabınızı hello Azure Yönetim Portalı için hello Media Services UI uzantısı bu bilgileri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="156b6-141">You can find this information in hello Media Services UI extension for your Media Services account in hello Azure Management Portal.</span></span>
* <span data-ttu-id="156b6-142">Merhaba kaynak erişilemez.</span><span class="sxs-lookup"><span data-stu-id="156b6-142">hello resource cannot be accessed.</span></span>
  
  * <span data-ttu-id="156b6-143">Bir girişim yapıldı Media Services hesabınız için kullanılabilir olmayan bir MediaProcessor toouse yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-143">An attempt was made toouse a MediaProcessor that is not available for your Media Services account.</span></span>
  * <span data-ttu-id="156b6-144">Media Services tarafından tanımlanan bir JobTemplate tooupdate girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="156b6-144">An attempt was made tooupdate a JobTemplate defined by Media Services.</span></span>
  * <span data-ttu-id="156b6-145">Bir girişim yapıldı toooverwrite bazı diğer Media Services hesabı Bulucu yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-145">An attempt was made toooverwrite some other Media Services account's Locator.</span></span>
  * <span data-ttu-id="156b6-146">Bir girişim yapıldı bazı diğer Media Services hesabı ContentKey toooverwrite yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-146">An attempt was made toooverwrite some other Media Services account's ContentKey.</span></span>
* <span data-ttu-id="156b6-147">Merhaba kaynak hello Media Services hesabı için ulaşıldı tooa hizmet kotasını nedeniyle oluşturulamadı.</span><span class="sxs-lookup"><span data-stu-id="156b6-147">hello resource could not be created due tooa service quota that was reached for hello Media Services account.</span></span> <span data-ttu-id="156b6-148">Merhaba Hizmeti kotaları hakkında daha fazla bilgi için bkz: [kotaları ve kısıtlamaları](media-services-quotas-and-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="156b6-148">For more information on hello service quotas, see [Quotas and Limitations](media-services-quotas-and-limitations.md).</span></span>

## <a name="404-not-found"></a><span data-ttu-id="156b6-149">404 Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="156b6-149">404 Not Found</span></span>
<span data-ttu-id="156b6-150">Merhaba isteği bir kaynakta izin verilmiyor, aşağıdaki nedenlerden hello son tooone:</span><span class="sxs-lookup"><span data-stu-id="156b6-150">hello request is not allowed on a resource due tooone of hello following reasons:</span></span>

* <span data-ttu-id="156b6-151">Bir girişim yapıldı var olmayan bir varlık tooupdate yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-151">An attempt was made tooupdate an entity that does not exist.</span></span>
* <span data-ttu-id="156b6-152">Bir girişim yapıldı var olmayan bir varlık toodelete yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-152">An attempt was made toodelete an entity that does not exist.</span></span>
* <span data-ttu-id="156b6-153">Bir girişim yapıldı toocreate yok tooan varlık bağlantıları varlıkta yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-153">An attempt was made toocreate an entity that links tooan entity that does not exist.</span></span>
* <span data-ttu-id="156b6-154">Bir girişim yapıldı var olmayan bir varlık tooGET yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-154">An attempt was made tooGET an entity that does not exist.</span></span>
* <span data-ttu-id="156b6-155">Bir girişim yapıldı hello Media Services hesabı ile ilişkili olmayan bir depolama hesabı toospecify yapılan.</span><span class="sxs-lookup"><span data-stu-id="156b6-155">An attempt was made toospecify a storage account that is not associated with hello Media Services account.</span></span>  

## <a name="409-conflict"></a><span data-ttu-id="156b6-156">409 çakışma</span><span class="sxs-lookup"><span data-stu-id="156b6-156">409 Conflict</span></span>
<span data-ttu-id="156b6-157">Merhaba isteği son verilmez nedenleri aşağıdaki hello tooone:</span><span class="sxs-lookup"><span data-stu-id="156b6-157">hello request is not allowed due tooone of hello following reasons:</span></span>

* <span data-ttu-id="156b6-158">Birden fazla AssetFile hello varlık içindeki hello belirtilen ada sahip.</span><span class="sxs-lookup"><span data-stu-id="156b6-158">More than one AssetFile has hello specified name within hello Asset.</span></span>
* <span data-ttu-id="156b6-159">İkinci bir toocreate birincil girişimde bulunuldu AssetFile hello varlık içinde.</span><span class="sxs-lookup"><span data-stu-id="156b6-159">An attempt was made toocreate a second primary AssetFile within hello Asset.</span></span>
* <span data-ttu-id="156b6-160">Girişiminde bulunuldu toocreate ContentKey hello ile belirtilen kimliği zaten kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="156b6-160">An attempt was made toocreate a ContentKey with hello specified Id already used.</span></span>
* <span data-ttu-id="156b6-161">Girişiminde bulunuldu toocreate hello bulucuyla belirtilen kimliği zaten kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="156b6-161">An attempt was made toocreate a Locator with hello specified Id already used.</span></span>
* <span data-ttu-id="156b6-162">Birden fazla IngestManifestFile hello IngestManifest içinde hello belirtilen ada sahip.</span><span class="sxs-lookup"><span data-stu-id="156b6-162">More than one IngestManifestFile has hello specified name within hello IngestManifest.</span></span>
* <span data-ttu-id="156b6-163">Bir girişim yapıldı ikinci bir depolama şifreleme ContentKey toohello toolink yapılan depolama şifrelenmiş varlık.</span><span class="sxs-lookup"><span data-stu-id="156b6-163">An attempt was made toolink a second storage encryption ContentKey toohello storage-encrypted Asset.</span></span>
* <span data-ttu-id="156b6-164">Girişiminde bulunuldu toolink hello aynı ContentKey toohello varlık.</span><span class="sxs-lookup"><span data-stu-id="156b6-164">An attempt was made toolink hello same ContentKey toohello Asset.</span></span>
* <span data-ttu-id="156b6-165">Bir Bulucu tooan, depolama kapsayıcısı artık eksik veya varlık hello varlık ile ilişkili toocreate girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="156b6-165">An attempt was made toocreate a locator tooan Asset whose storage container is missing or is no longer associated with hello Asset.</span></span>
* <span data-ttu-id="156b6-166">Bir girişim yapıldı toocreate yapılan bir Bulucu tooan 5 bulucular zaten kullanımda olan varlık.</span><span class="sxs-lookup"><span data-stu-id="156b6-166">An attempt was made toocreate a locator tooan Asset which already has 5 locators in use.</span></span> <span data-ttu-id="156b6-167">(Azure depolama bir depolama kapsayıcısı üzerinde beş paylaşılan erişim ilkeleri hello sınırının zorlar.)</span><span class="sxs-lookup"><span data-stu-id="156b6-167">(Azure Storage enforces hello limit of five shared access policies on one storage container.)</span></span>
* <span data-ttu-id="156b6-168">Bir varlık tooan IngestManifestAsset depolama hesabına bağlama hello depolama hesabıyla aynı kullanılan hello hello üst IngestManifest tarafından değil.</span><span class="sxs-lookup"><span data-stu-id="156b6-168">Linking storage account of an Asset tooan IngestManifestAsset is not hello same as hello storage account used by hello parent IngestManifest.</span></span>  

## <a name="500-internal-server-error"></a><span data-ttu-id="156b6-169">500 İç sunucu hatası</span><span class="sxs-lookup"><span data-stu-id="156b6-169">500 Internal Server Error</span></span>
<span data-ttu-id="156b6-170">Merhaba hello istek işlenirken, Media Services hello işleme devam etmesini engelleyen bazı hatayla karşılaşıyor.</span><span class="sxs-lookup"><span data-stu-id="156b6-170">During hello processing of hello request, Media Services encounters some error that prevents hello processing from continuing.</span></span> <span data-ttu-id="156b6-171">Bu son olabilir nedenleri aşağıdaki hello tooone:</span><span class="sxs-lookup"><span data-stu-id="156b6-171">This could be due tooone of hello following reasons:</span></span>

* <span data-ttu-id="156b6-172">Merhaba Media Services hesabın hizmet kota bilgileri geçici olarak kullanılamadığından bir varlık veya iş oluşturma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="156b6-172">Creating an Asset or Job fails because hello Media Services account's service quota information is temporarily unavailable.</span></span>
* <span data-ttu-id="156b6-173">Merhaba hesabın depolama hesabı bilgilerini geçici olarak kullanılamadığından bir varlık veya IngestManifest blob depolama kapsayıcısını oluşturma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="156b6-173">Creating an Asset or IngestManifest blob storage container fails because hello account's storage account information is temporarily unavailable.</span></span>
* <span data-ttu-id="156b6-174">Diğer beklenmeyen hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="156b6-174">Other unexpected error.</span></span>

## <a name="503-service-unavailable"></a><span data-ttu-id="156b6-175">503 Hizmet kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="156b6-175">503 Service Unavailable</span></span>
<span data-ttu-id="156b6-176">Merhaba, şu anda işleyemiyor tooreceive istekleri sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="156b6-176">hello server is currently unable tooreceive requests.</span></span> <span data-ttu-id="156b6-177">Aşırı istekleri toohello hizmeti tarafından bu hataya neden.</span><span class="sxs-lookup"><span data-stu-id="156b6-177">This error may be caused by excessive requests toohello service.</span></span> <span data-ttu-id="156b6-178">Media Services mekanizması azaltma hello kaynak kullanımı aşırı isteği toohello hizmet uygulamalar için sınırlar.</span><span class="sxs-lookup"><span data-stu-id="156b6-178">Media Services throttling mechanism restricts hello resource usage for applications that make excessive request toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="156b6-179">Aldığınız hello nedeni hakkında daha ayrıntılı bilgi onay hello hata iletisi ve hata kodu dize tooget hello 503 hatası.</span><span class="sxs-lookup"><span data-stu-id="156b6-179">Check hello error message and error code string tooget more detailed information about hello reason you got hello 503 error.</span></span> <span data-ttu-id="156b6-180">Bu hata, azaltma her zaman gelmez.</span><span class="sxs-lookup"><span data-stu-id="156b6-180">This error does not always mean throttling.</span></span>
> 
> 

<span data-ttu-id="156b6-181">Olası durum açıklamaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="156b6-181">Possible status descriptions are:</span></span>

* <span data-ttu-id="156b6-182">"Sunucu meşgul.</span><span class="sxs-lookup"><span data-stu-id="156b6-182">"Server is busy.</span></span> <span data-ttu-id="156b6-183">Bu istek türü önceki çalışmalarını birden çok {0} saniye sürdü."</span><span class="sxs-lookup"><span data-stu-id="156b6-183">Previous runs of this type of request took more than {0} seconds."</span></span>
* <span data-ttu-id="156b6-184">"Sunucu meşgul.</span><span class="sxs-lookup"><span data-stu-id="156b6-184">"Server is busy.</span></span> <span data-ttu-id="156b6-185">Birden çok saniyede {0} istekler kısıtlanan."</span><span class="sxs-lookup"><span data-stu-id="156b6-185">More than {0} requests per second can be throttled."</span></span>
* <span data-ttu-id="156b6-186">"Sunucu meşgul.</span><span class="sxs-lookup"><span data-stu-id="156b6-186">"Server is busy.</span></span> <span data-ttu-id="156b6-187">Fazlasını {0} istekleri {1} saniye içinde kısıtlanan."</span><span class="sxs-lookup"><span data-stu-id="156b6-187">More than {0} requests within {1} seconds can be throttled."</span></span>

<span data-ttu-id="156b6-188">toohandle bu hatayı üstel geri alma yeniden deneme mantığı kullanılmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="156b6-188">toohandle this error, we recommend using exponential back-off retry logic.</span></span> <span data-ttu-id="156b6-189">Ardışık hata yanıtları denemeler arasındaki aşamalı olarak uzun bekler kullanarak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="156b6-189">That means using progressively longer waits between retries for consecutive error responses.</span></span>  <span data-ttu-id="156b6-190">Daha fazla bilgi için bkz: [geçici hata işleme uygulama blok](https://msdn.microsoft.com/library/hh680905.aspx).</span><span class="sxs-lookup"><span data-stu-id="156b6-190">For more information, see [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680905.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="156b6-191">Kullanıyorsanız [.Net için Azure Media Services SDK](https://github.com/Azure/azure-sdk-for-media-services/tree/master), hello hello 503 hatası için yeniden deneme mantığı hello SDK tarafından uygulandıktan.</span><span class="sxs-lookup"><span data-stu-id="156b6-191">If you are using [Azure Media Services SDK for .Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), hello retry logic for hello 503 error has been implemented by hello SDK.</span></span>  
> 
> 

## <a name="see-also"></a><span data-ttu-id="156b6-192">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="156b6-192">See Also</span></span>
[<span data-ttu-id="156b6-193">Yönetim hata kodları medya Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="156b6-193">Media Services Management Error Codes</span></span>](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a><span data-ttu-id="156b6-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="156b6-194">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="156b6-195">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="156b6-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

