---
title: "Azure Media Services hata kodları | Microsoft Docs"
description: "Konu Azure Media Services hata kodları genel bir bakış sağlar."
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
ms.openlocfilehash: 39886a955124429302609dd9d5a7c20ae7f498d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-media-services-error-codes"></a><span data-ttu-id="a419d-103">Azure Media Services hata kodları</span><span class="sxs-lookup"><span data-stu-id="a419d-103">Azure Media Services error codes</span></span>
<span data-ttu-id="a419d-104">Microsoft Azure Media Services kullanırken, Media Services desteklenmeyen Eylemler süresinin dolmasını kimlik doğrulama belirteçleri gibi sorunları bağlı olarak hizmetinden HTTP hata kodları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a419d-104">When using Microsoft Azure Media Services, you may receive HTTP error codes from the service depending on issues such as authentication tokens expiring to actions that are not supported in Media Services.</span></span> <span data-ttu-id="a419d-105">Bir listesi aşağıda verilmiştir **HTTP hata kodları** , döndürülüp döndürülmediğini Media Services ve olası nedenleri tarafından bunlar için.</span><span class="sxs-lookup"><span data-stu-id="a419d-105">The following is a list of **HTTP error codes** that may be returned by Media Services and the possible causes for them.</span></span>  

## <a name="400-bad-request"></a><span data-ttu-id="a419d-106">400 Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="a419d-106">400 Bad Request</span></span>
<span data-ttu-id="a419d-107">İstek geçersiz bilgiler içerir ve aşağıdaki nedenlerden biri reddedilemiyor:</span><span class="sxs-lookup"><span data-stu-id="a419d-107">The request contains invalid information and is rejected due to one of the following reasons:</span></span>

* <span data-ttu-id="a419d-108">Desteklenmeyen bir API sürümü belirtildi.</span><span class="sxs-lookup"><span data-stu-id="a419d-108">An unsupported API version is specified.</span></span> <span data-ttu-id="a419d-109">En güncel sürümü için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a419d-109">For the most current version, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="a419d-110">Media Services API sürümü belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="a419d-110">The API version of Media Services is not specified.</span></span> <span data-ttu-id="a419d-111">API sürümü belirtme hakkında daha fazla bilgi için bkz: [Media Services Operations REST API Başvurusu](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="a419d-111">For information on how to specify the API version, see [Media Services Operations REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="a419d-112">Media Services'e bağlanmak için .NET veya Java SDK'ları kullanıyorsanız, ne zaman deneyin ve Media Services karşı bazı eylemler gerçekleştirme API sürümü sizin için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="a419d-112">If you are using the .NET or Java SDKs to connect to Media Services, the API version is specified for you whenever you try and perform some action against Media Services.</span></span>
  > 
  > 
* <span data-ttu-id="a419d-113">Tanımlanmamış özellik belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="a419d-113">An undefined property has been specified.</span></span> <span data-ttu-id="a419d-114">Hata iletisinde özelliği adıdır.</span><span class="sxs-lookup"><span data-stu-id="a419d-114">The property name is in the error message.</span></span> <span data-ttu-id="a419d-115">Belirli bir varlık üyeleri olan özellikler belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="a419d-115">Only those properties that are members of a given entity can be specified.</span></span> <span data-ttu-id="a419d-116">Bkz: [Azure Media Services REST API Başvurusu](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) varlıkları ve özelliklerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="a419d-116">See [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) for a list of entities and their properties.</span></span>
* <span data-ttu-id="a419d-117">Geçersiz bir özellik değeri belirtildi.</span><span class="sxs-lookup"><span data-stu-id="a419d-117">An invalid property value has been specified.</span></span> <span data-ttu-id="a419d-118">Hata iletisinde özelliği adıdır.</span><span class="sxs-lookup"><span data-stu-id="a419d-118">The property name is in the error message.</span></span> <span data-ttu-id="a419d-119">Geçerli bir özellik türlerini ve değerlerini önceki bağlantısına bakın.</span><span class="sxs-lookup"><span data-stu-id="a419d-119">See the previous link for valid property types and their values.</span></span>
* <span data-ttu-id="a419d-120">Bir özellik değeri eksik ve gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a419d-120">A property value is missing and is required.</span></span>
* <span data-ttu-id="a419d-121">Belirtilen URL parçası hatalı bir değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="a419d-121">Part of the URL specified contains a bad value.</span></span>
* <span data-ttu-id="a419d-122">WriteOnce özelliği güncelleştirmek için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-122">An attempt was made to update a WriteOnce property.</span></span>
* <span data-ttu-id="a419d-123">Bir giriş varlığı belirtilmedi veya belirlenemedi birincil bir AssetFile sahip bir iş oluşturmak için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-123">An attempt was made to create a Job that has an input Asset with a primary AssetFile that was not specified or could not be determined.</span></span>
* <span data-ttu-id="a419d-124">Bir SAS Bulucu güncelleştirmek için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-124">An attempt was made to update a SAS Locator.</span></span> <span data-ttu-id="a419d-125">SAS bulucular yalnızca oluşturulan veya silinebilir.</span><span class="sxs-lookup"><span data-stu-id="a419d-125">SAS locators can only be created or deleted.</span></span> <span data-ttu-id="a419d-126">Bulucular akış güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a419d-126">Streaming locators can be updated.</span></span> <span data-ttu-id="a419d-127">Daha fazla bilgi için bkz: [Bulucular](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="a419d-127">For more information, see [Locators](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>
* <span data-ttu-id="a419d-128">Desteklenmeyen bir işlem veya sorgu gönderildi.</span><span class="sxs-lookup"><span data-stu-id="a419d-128">An unsupported operation or query was submitted.</span></span>

## <a name="401-unauthorized"></a><span data-ttu-id="a419d-129">401 Yetkisiz</span><span class="sxs-lookup"><span data-stu-id="a419d-129">401 Unauthorized</span></span>
<span data-ttu-id="a419d-130">(Bunu yetkilendirilebilir önce) istek aşağıdaki nedenlerden biri dolayısıyla doğrulanamadı:</span><span class="sxs-lookup"><span data-stu-id="a419d-130">The request could not be authenticated (before it can be authorized) due to one of the following reasons:</span></span>

* <span data-ttu-id="a419d-131">Kimlik doğrulama üstbilgisi eksik.</span><span class="sxs-lookup"><span data-stu-id="a419d-131">Missing authentication header.</span></span>
* <span data-ttu-id="a419d-132">Hatalı kimlik doğrulaması üstbilgi değeri.</span><span class="sxs-lookup"><span data-stu-id="a419d-132">Bad authentication header value.</span></span>
  * <span data-ttu-id="a419d-133">Belirtecin süresi sona erdi.</span><span class="sxs-lookup"><span data-stu-id="a419d-133">The token has expired.</span></span> 
  * <span data-ttu-id="a419d-134">Belirteç geçersiz bir imza içeriyor.</span><span class="sxs-lookup"><span data-stu-id="a419d-134">The token contains an invalid signature.</span></span>

## <a name="403-forbidden"></a><span data-ttu-id="a419d-135">403 Yasak</span><span class="sxs-lookup"><span data-stu-id="a419d-135">403 Forbidden</span></span>
<span data-ttu-id="a419d-136">İstek aşağıdaki nedenlerden biri dolayısıyla izin verilmiyor:</span><span class="sxs-lookup"><span data-stu-id="a419d-136">The request is not allowed due to one of the following reasons:</span></span>

* <span data-ttu-id="a419d-137">Media Services hesabı bulunamadı veya silinmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="a419d-137">The Media Services account cannot be found or has been deleted.</span></span>
* <span data-ttu-id="a419d-138">Media Services hesabı devre dışı bırakılır ve HTTP GET isteği türü değil.</span><span class="sxs-lookup"><span data-stu-id="a419d-138">The Media Services account is disabled and the request type is not HTTP GET.</span></span> <span data-ttu-id="a419d-139">Hizmet işlemleri de 403 bir yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="a419d-139">Service operations will return a 403 response as well.</span></span>
* <span data-ttu-id="a419d-140">Kimlik doğrulama belirteci kullanıcının kimlik bilgileri içermiyor: AccountName ve/veya Subscriptionıd.</span><span class="sxs-lookup"><span data-stu-id="a419d-140">The authentication token does not contain the user’s credential information: AccountName and/or SubscriptionId.</span></span> <span data-ttu-id="a419d-141">Azure Yönetim Portalı'nda Media Services hesabınız için medya Hizmetleri UI uzantısı'nda bu bilgileri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a419d-141">You can find this information in the Media Services UI extension for your Media Services account in the Azure Management Portal.</span></span>
* <span data-ttu-id="a419d-142">Kaynak erişilemez.</span><span class="sxs-lookup"><span data-stu-id="a419d-142">The resource cannot be accessed.</span></span>
  
  * <span data-ttu-id="a419d-143">Media Services hesabınız için kullanılabilir olmayan bir MediaProcessor kullanmak için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-143">An attempt was made to use a MediaProcessor that is not available for your Media Services account.</span></span>
  * <span data-ttu-id="a419d-144">Media Services tarafından tanımlanan bir JobTemplate güncelleştirmek için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-144">An attempt was made to update a JobTemplate defined by Media Services.</span></span>
  * <span data-ttu-id="a419d-145">Bazı diğer Media Services hesabı Bulucu üzerine yazmak için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-145">An attempt was made to overwrite some other Media Services account's Locator.</span></span>
  * <span data-ttu-id="a419d-146">Bazı diğer Media Services hesabı ContentKey üzerine yazmak için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-146">An attempt was made to overwrite some other Media Services account's ContentKey.</span></span>
* <span data-ttu-id="a419d-147">Kaynak için Media Services hesabı ulaşıldı hizmet kotasını nedeniyle oluşturulamadı.</span><span class="sxs-lookup"><span data-stu-id="a419d-147">The resource could not be created due to a service quota that was reached for the Media Services account.</span></span> <span data-ttu-id="a419d-148">Hizmeti kotaları hakkında daha fazla bilgi için bkz: [kotaları ve kısıtlamaları](media-services-quotas-and-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a419d-148">For more information on the service quotas, see [Quotas and Limitations](media-services-quotas-and-limitations.md).</span></span>

## <a name="404-not-found"></a><span data-ttu-id="a419d-149">404 Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a419d-149">404 Not Found</span></span>
<span data-ttu-id="a419d-150">İstek, aşağıdaki nedenlerin birinden dolayı bir kaynakta izin verilmiyor:</span><span class="sxs-lookup"><span data-stu-id="a419d-150">The request is not allowed on a resource due to one of the following reasons:</span></span>

* <span data-ttu-id="a419d-151">Var olmayan bir varlığı güncelleştirmek için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-151">An attempt was made to update an entity that does not exist.</span></span>
* <span data-ttu-id="a419d-152">Var olmayan bir varlığı silmek için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-152">An attempt was made to delete an entity that does not exist.</span></span>
* <span data-ttu-id="a419d-153">Var olmayan bir varlığa bağlanan bir varlık oluşturmak için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-153">An attempt was made to create an entity that links to an entity that does not exist.</span></span>
* <span data-ttu-id="a419d-154">Var olmayan bir varlık almak için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-154">An attempt was made to GET an entity that does not exist.</span></span>
* <span data-ttu-id="a419d-155">Media Services hesabıyla ilişkilendirilmemiş bir depolama hesabı belirtmek için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-155">An attempt was made to specify a storage account that is not associated with the Media Services account.</span></span>  

## <a name="409-conflict"></a><span data-ttu-id="a419d-156">409 çakışma</span><span class="sxs-lookup"><span data-stu-id="a419d-156">409 Conflict</span></span>
<span data-ttu-id="a419d-157">İstek aşağıdaki nedenlerden biri dolayısıyla izin verilmiyor:</span><span class="sxs-lookup"><span data-stu-id="a419d-157">The request is not allowed due to one of the following reasons:</span></span>

* <span data-ttu-id="a419d-158">Birden fazla AssetFile varlık içinde belirtilen ada sahip.</span><span class="sxs-lookup"><span data-stu-id="a419d-158">More than one AssetFile has the specified name within the Asset.</span></span>
* <span data-ttu-id="a419d-159">Varlık içindeki ikinci bir birincil AssetFile oluşturmak için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-159">An attempt was made to create a second primary AssetFile within the Asset.</span></span>
* <span data-ttu-id="a419d-160">Zaten kullanılan belirtilen kimliğe bir ContentKey oluşturmak için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-160">An attempt was made to create a ContentKey with the specified Id already used.</span></span>
* <span data-ttu-id="a419d-161">Zaten kullanılan belirtilen kimliğe bir Bulucu oluşturmanız için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-161">An attempt was made to create a Locator with the specified Id already used.</span></span>
* <span data-ttu-id="a419d-162">Birden fazla IngestManifestFile IngestManifest içinde belirtilen ada sahip.</span><span class="sxs-lookup"><span data-stu-id="a419d-162">More than one IngestManifestFile has the specified name within the IngestManifest.</span></span>
* <span data-ttu-id="a419d-163">Depolama şifrelenmiş varlık için ikinci bir depolama şifreleme ContentKey bağlamak için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-163">An attempt was made to link a second storage encryption ContentKey to the storage-encrypted Asset.</span></span>
* <span data-ttu-id="a419d-164">Varlık için aynı ContentKey bağlamak için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-164">An attempt was made to link the same ContentKey to the Asset.</span></span>
* <span data-ttu-id="a419d-165">Depolama kapsayıcısı eksik ya da artık varlıkla ilişkilendirilen bir varlık için bir Bulucu oluşturmanız için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-165">An attempt was made to create a locator to an Asset whose storage container is missing or is no longer associated with the Asset.</span></span>
* <span data-ttu-id="a419d-166">5 bulucular zaten kullanımda olan bir varlık için bir Bulucu oluşturmanız için girişimde bulunuldu.</span><span class="sxs-lookup"><span data-stu-id="a419d-166">An attempt was made to create a locator to an Asset which already has 5 locators in use.</span></span> <span data-ttu-id="a419d-167">(Azure depolama sınırını bir depolama kapsayıcısı üzerinde beş paylaşılan erişim ilkeleri zorunlu tutar.)</span><span class="sxs-lookup"><span data-stu-id="a419d-167">(Azure Storage enforces the limit of five shared access policies on one storage container.)</span></span>
* <span data-ttu-id="a419d-168">Bir malın depolama hesabı için bir IngestManifestAsset bağlama IngestManifest üst tarafından kullanılan depolama hesabı ile aynı değil.</span><span class="sxs-lookup"><span data-stu-id="a419d-168">Linking storage account of an Asset to an IngestManifestAsset is not the same as the storage account used by the parent IngestManifest.</span></span>  

## <a name="500-internal-server-error"></a><span data-ttu-id="a419d-169">500 İç sunucu hatası</span><span class="sxs-lookup"><span data-stu-id="a419d-169">500 Internal Server Error</span></span>
<span data-ttu-id="a419d-170">İsteğin işlenmesi sırasında Media Services işleme devam etmesini engelleyen bazı hatayla karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="a419d-170">During the processing of the request, Media Services encounters some error that prevents the processing from continuing.</span></span> <span data-ttu-id="a419d-171">Bunun nedeni, aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="a419d-171">This could be due to one of the following reasons:</span></span>

* <span data-ttu-id="a419d-172">Media Services hesabın hizmet kota bilgileri geçici olarak kullanılamadığından bir varlık veya iş oluşturma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a419d-172">Creating an Asset or Job fails because the Media Services account's service quota information is temporarily unavailable.</span></span>
* <span data-ttu-id="a419d-173">Hesabın depolama hesabı bilgilerini geçici olarak kullanılamadığından bir varlık veya IngestManifest blob depolama kapsayıcısını oluşturma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a419d-173">Creating an Asset or IngestManifest blob storage container fails because the account's storage account information is temporarily unavailable.</span></span>
* <span data-ttu-id="a419d-174">Diğer beklenmeyen hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="a419d-174">Other unexpected error.</span></span>

## <a name="503-service-unavailable"></a><span data-ttu-id="a419d-175">503 Hizmet kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="a419d-175">503 Service Unavailable</span></span>
<span data-ttu-id="a419d-176">Sunucu isteklerini almak şu anda alamıyor.</span><span class="sxs-lookup"><span data-stu-id="a419d-176">The server is currently unable to receive requests.</span></span> <span data-ttu-id="a419d-177">Bu hatanın nedeni aşırı isteklerine hizmet.</span><span class="sxs-lookup"><span data-stu-id="a419d-177">This error may be caused by excessive requests to the service.</span></span> <span data-ttu-id="a419d-178">Media Services mekanizması azaltma hizmete aşırı istekte uygulamalar için kaynak kullanımını kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="a419d-178">Media Services throttling mechanism restricts the resource usage for applications that make excessive request to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="a419d-179">Hata iletisi ve hata kodu dizesi 503 hatası aldığınız nedeni hakkında daha ayrıntılı bilgi almak için denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a419d-179">Check the error message and error code string to get more detailed information about the reason you got the 503 error.</span></span> <span data-ttu-id="a419d-180">Bu hata, azaltma her zaman gelmez.</span><span class="sxs-lookup"><span data-stu-id="a419d-180">This error does not always mean throttling.</span></span>
> 
> 

<span data-ttu-id="a419d-181">Olası durum açıklamaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a419d-181">Possible status descriptions are:</span></span>

* <span data-ttu-id="a419d-182">"Sunucu meşgul.</span><span class="sxs-lookup"><span data-stu-id="a419d-182">"Server is busy.</span></span> <span data-ttu-id="a419d-183">Bu istek türü önceki çalışmalarını birden çok {0} saniye sürdü."</span><span class="sxs-lookup"><span data-stu-id="a419d-183">Previous runs of this type of request took more than {0} seconds."</span></span>
* <span data-ttu-id="a419d-184">"Sunucu meşgul.</span><span class="sxs-lookup"><span data-stu-id="a419d-184">"Server is busy.</span></span> <span data-ttu-id="a419d-185">Birden çok saniyede {0} istekler kısıtlanan."</span><span class="sxs-lookup"><span data-stu-id="a419d-185">More than {0} requests per second can be throttled."</span></span>
* <span data-ttu-id="a419d-186">"Sunucu meşgul.</span><span class="sxs-lookup"><span data-stu-id="a419d-186">"Server is busy.</span></span> <span data-ttu-id="a419d-187">Fazlasını {0} istekleri {1} saniye içinde kısıtlanan."</span><span class="sxs-lookup"><span data-stu-id="a419d-187">More than {0} requests within {1} seconds can be throttled."</span></span>

<span data-ttu-id="a419d-188">Bu hatayı işlemeye üstel geri alma yeniden deneme mantığı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="a419d-188">To handle this error, we recommend using exponential back-off retry logic.</span></span> <span data-ttu-id="a419d-189">Ardışık hata yanıtları denemeler arasındaki aşamalı olarak uzun bekler kullanarak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a419d-189">That means using progressively longer waits between retries for consecutive error responses.</span></span>  <span data-ttu-id="a419d-190">Daha fazla bilgi için bkz: [geçici hata işleme uygulama blok](https://msdn.microsoft.com/library/hh680905.aspx).</span><span class="sxs-lookup"><span data-stu-id="a419d-190">For more information, see [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680905.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="a419d-191">Kullanıyorsanız [.Net için Azure Media Services SDK](https://github.com/Azure/azure-sdk-for-media-services/tree/master), 503 hatası için yeniden deneme mantığı SDK tarafından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="a419d-191">If you are using [Azure Media Services SDK for .Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), the retry logic for the 503 error has been implemented by the SDK.</span></span>  
> 
> 

## <a name="see-also"></a><span data-ttu-id="a419d-192">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a419d-192">See Also</span></span>
[<span data-ttu-id="a419d-193">Yönetim hata kodları medya Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="a419d-193">Media Services Management Error Codes</span></span>](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a><span data-ttu-id="a419d-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a419d-194">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a419d-195">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="a419d-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

