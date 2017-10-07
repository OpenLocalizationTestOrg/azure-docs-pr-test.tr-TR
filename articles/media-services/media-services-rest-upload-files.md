---
title: "REST kullanarak Media Services hesabı aaaUpload dosyalarıyla | Microsoft Docs"
description: "Oluşturma ve varlıklar karşıya tooget medya medya Hizmetleri içine nasıl içerik öğrenin."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="da2c6-103">Dosyaları REST kullanarak bir Media Services hesabına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="da2c6-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da2c6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="da2c6-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="da2c6-105">REST</span><span class="sxs-lookup"><span data-stu-id="da2c6-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="da2c6-106">Portal</span><span class="sxs-lookup"><span data-stu-id="da2c6-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="da2c6-107">Media Services’de dijital dosyalar bir varlığa yüklenir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="da2c6-108">Merhaba [varlık](https://docs.microsoft.com/rest/api/media/operations/asset) varlık içerebilir video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkında hello meta veriler.)  Hello varlığa Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır.</span><span class="sxs-lookup"><span data-stu-id="da2c6-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="da2c6-109">ilgili önemli noktalar aşağıdaki hello Uygula:</span><span class="sxs-lookup"><span data-stu-id="da2c6-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="da2c6-110">Media Services URL'leri içeriği (örneğin, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) akış Merhaba oluştururken hello hello IAssetFile.Name özellik değerini kullanır Bu nedenle, yüzde kodlama izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="da2c6-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="da2c6-111">Merhaba hello değerini **adı** özelliği hello aşağıdakilerden herhangi birini içeremez [yüzde kodlama-ayrılmış karakterleri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="da2c6-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="da2c6-112">Ayrıca, yalnızca bir olabilir '.' hello dosya adı uzantısı için.</span><span class="sxs-lookup"><span data-stu-id="da2c6-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="da2c6-113">Merhaba hello adının uzunluğu 260 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="da2c6-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="da2c6-114">Media Services işlemek için desteklenen bir toohello en büyük dosya boyutu sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="da2c6-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="da2c6-115">Lütfen bakın [bu](media-services-quotas-and-limitations.md) hello dosya boyutu sınırlaması hakkında ayrıntılı bilgi için konu.</span><span class="sxs-lookup"><span data-stu-id="da2c6-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="da2c6-116">Varlıklar yüklemeyle hello temel iş akışı aşağıdaki bölümlerde hello ayrılır:</span><span class="sxs-lookup"><span data-stu-id="da2c6-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="da2c6-117">Bir varlık oluşturun</span><span class="sxs-lookup"><span data-stu-id="da2c6-117">Create an Asset</span></span>
* <span data-ttu-id="da2c6-118">(İsteğe bağlı) bir varlık şifrele</span><span class="sxs-lookup"><span data-stu-id="da2c6-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="da2c6-119">Bir dosya tooblob depolama yükleme</span><span class="sxs-lookup"><span data-stu-id="da2c6-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="da2c6-120">AMS ayrıca tooupload varlıklar toplu sağlar.</span><span class="sxs-lookup"><span data-stu-id="da2c6-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="da2c6-121">Daha fazla bilgi için [bu](media-services-rest-upload-files.md#upload_in_bulk) bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="da2c6-122">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="da2c6-123">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="da2c6-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="da2c6-124">TooMedia Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="da2c6-124">Connect tooMedia Services</span></span>

<span data-ttu-id="da2c6-125">Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="da2c6-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="da2c6-126">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="da2c6-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="da2c6-127">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="da2c6-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="da2c6-128">Varlıkları yükleyin</span><span class="sxs-lookup"><span data-stu-id="da2c6-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="da2c6-129">Bir varlık oluşturun</span><span class="sxs-lookup"><span data-stu-id="da2c6-129">Create an asset</span></span>

<span data-ttu-id="da2c6-130">Bir varlık, birden çok türleri veya Media Services, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları dahil olmak üzere nesne kümeleri için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="da2c6-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="da2c6-131">REST API bir varlık oluşturma, posta gönderme gerektirir hello tooMedia Hizmetleri isteyin ve hello istek gövdesinde Varlığınızı ilgili herhangi bir özellik bilgi yerleştirme.</span><span class="sxs-lookup"><span data-stu-id="da2c6-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="da2c6-132">Bir varlık oluşturma olduğunda belirtebilirsiniz hello özelliklerinden biri **seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="da2c6-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="da2c6-133">**Seçenekler** bir varlığı ile oluşturulan hello şifreleme seçenekleri açıklayan bir numaralandırma değeridir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="da2c6-134">Geçerli bir değer hello listesinde aşağıdaki değerleri olmayan bir birleşimini hello değerlerinden biri.</span><span class="sxs-lookup"><span data-stu-id="da2c6-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="da2c6-135">**Hiçbiri** = **0**: şifreleme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="da2c6-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="da2c6-136">Merhaba varsayılan değer budur.</span><span class="sxs-lookup"><span data-stu-id="da2c6-136">This is hello default value.</span></span> <span data-ttu-id="da2c6-137">Bu seçenek kullanıldığında, içeriğinizin aktarım veya deposunda kalan korunmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="da2c6-138">Aşamalı indirme kullanarak toodeliver bir MP4 planlıyorsanız, bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="da2c6-139">**StorageEncrypted** = **1**: karşıya yükleme ve depolama için AES 256 bit şifreleme ile şifrelenmiş, dosyaları toobe için isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="da2c6-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="da2c6-140">Şifrelenmiş depolama varlığınız olması durumunda, varlık teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="da2c6-141">Daha fazla bilgi için bkz: [varlık teslim ilkesini yapılandırma](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="da2c6-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="da2c6-142">**CommonEncryptionProtected** = **2**: ortak bir şifreleme yöntemi (örneğin, PlayReady) ile korunan dosyaları karşıya varsa belirtin.</span><span class="sxs-lookup"><span data-stu-id="da2c6-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="da2c6-143">**EnvelopeEncryptionProtected** = **4**: AES dosyaları ile şifrelenmiş HLS karşıya varsa belirtin.</span><span class="sxs-lookup"><span data-stu-id="da2c6-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="da2c6-144">Hello dosyaları gerekir alınan kodlanmış ve Transform Manager tarafından şifrelenmiş olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="da2c6-145">Varlığınızı şifreleme kullanacaksa, oluşturmalısınız bir **ContentKey** ve izleyen konu hello açıklandığı gibi tooyour varlık Bağla:[nasıl toocreate bir ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="da2c6-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="da2c6-146">Merhaba varlığa hello dosyaları karşıya yükleme sonra tooupdate hello şifreleme özellikleri hello gerektiğini unutmayın **AssetFile** varlık hello sırasında aldığınız hello değerlerle **varlık** şifreleme.</span><span class="sxs-lookup"><span data-stu-id="da2c6-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="da2c6-147">Bunu hello kullanarak **birleştirme** HTTP isteği.</span><span class="sxs-lookup"><span data-stu-id="da2c6-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="da2c6-148">örnekte gösterildiği nasıl aşağıdaki hello toocreate bir varlık.</span><span class="sxs-lookup"><span data-stu-id="da2c6-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="da2c6-149">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="da2c6-149">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

<span data-ttu-id="da2c6-150">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-150">**HTTP Response**</span></span>

<span data-ttu-id="da2c6-151">Başarılı olursa, hello aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="da2c6-151">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="da2c6-152">Bir AssetFile oluşturma</span><span class="sxs-lookup"><span data-stu-id="da2c6-152">Create an AssetFile</span></span>
<span data-ttu-id="da2c6-153">Merhaba [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) varlığı temsil eden bir blob kapsayıcısında depolanır ses veya video dosyası.</span><span class="sxs-lookup"><span data-stu-id="da2c6-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="da2c6-154">Bir varlık dosyası her zaman bir varlıkla ilişkilidir ve bir varlığı bir veya daha çok varlık dosyaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="da2c6-155">bir varlık dosyası nesne bir blob kapsayıcısında dijital bir dosyayla ilişkili değilse hello Media Services Kodlayıcısı görev başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="da2c6-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="da2c6-156">Bu hello Not **AssetFile** örneği ve hello gerçek medya dosyası olan iki farklı nesneler.</span><span class="sxs-lookup"><span data-stu-id="da2c6-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="da2c6-157">Merhaba medya dosyası hello gerçek medya içeriği içerirken hello AssetFile örneği hello medya dosyası hakkındaki meta verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="da2c6-158">Bir blob kapsayıcıya bir dijital medyayı dosyanızı karşıya sonra hello kullanacağı **birleştirme** medya dosyanızın (Merhaba konunun ilerleyen bölümlerinde gösterildiği gibi) hakkında bilgi içeren HTTP isteği tooupdate hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="da2c6-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="da2c6-159">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="da2c6-159">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="da2c6-160">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-160">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="da2c6-161">Merhaba AccessPolicy yazma izni olan oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="da2c6-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="da2c6-162">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="da2c6-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="da2c6-163">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="da2c6-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="da2c6-164">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="da2c6-165">Blob depolama alanına herhangi bir dosya karşıya yüklemeden önce hello erişim ilkesi hakları tooan varlık yazmak için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="da2c6-166">bir HTTP isteği toohello AccessPolicies varlık sonrası toodo ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="da2c6-167">Oluşturulduktan sonra bir dakika Cinsiden Süre değer tanımlama veya yanıt olarak bir 500 İç sunucu hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="da2c6-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="da2c6-168">AccessPolicies hakkında daha fazla bilgi için bkz: [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="da2c6-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="da2c6-169">örnekte gösterildiği nasıl aşağıdaki hello toocreate bir AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="da2c6-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="da2c6-170">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="da2c6-170">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="da2c6-171">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="da2c6-171">**HTTP Request**</span></span>

    If successful, hello following response is returned:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-hello-upload-url"></a><span data-ttu-id="da2c6-172">Merhaba karşıya yükleme URL'si Al</span><span class="sxs-lookup"><span data-stu-id="da2c6-172">Get hello Upload URL</span></span>
<span data-ttu-id="da2c6-173">tooreceive gerçek karşıya yükleme URL'si Merhaba, SAS Bulucu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="da2c6-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="da2c6-174">Bulucular bir varlık tooaccess dosyalarında istediğiniz istemciler için hello başlangıç saati ve bağlantı uç noktasının türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="da2c6-175">İstekleri ve gereksinimlerini verilen AccessPolicy ve varlık çifti toohandle farklı bir istemci için birden çok Bulucu varlık oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2c6-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="da2c6-176">Her bu Bulucuyu hello StartTime değerinin yanı sıra hello AccessPolicy toodetermine hello süreyi bir URL kullanılabilir hello Dakika Cinsiden Süre değerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="da2c6-177">Daha fazla bilgi için bkz: [Bulucu](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="da2c6-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="da2c6-178">Bir SAS URL'si biçimi aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="da2c6-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="da2c6-179">Bazı dikkate alınması gereken noktalar vardır:</span><span class="sxs-lookup"><span data-stu-id="da2c6-179">Some considerations apply:</span></span>

* <span data-ttu-id="da2c6-180">Aynı anda belirli bir varlıkla ilişkilendirilen beşten fazla benzersiz Bulucular sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="da2c6-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="da2c6-181">Daha fazla bilgi için Bulucu bakın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-181">For more information, see Locator.</span></span>
* <span data-ttu-id="da2c6-182">Dosyalarınızı hemen tooupload gerekiyorsa, StartTime değeri toofive dakika hello geçerli saati önce ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="da2c6-183">Bu; çünkü istemci makine ve Media Services arasında eğme saat olabilir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="da2c6-184">Ayrıca, StartTime değeriniz tarih saat biçiminde aşağıdaki hello olmalıdır: YYYY-MM-: ssZ (örneğin, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="da2c6-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="da2c6-185">30-40 saniyenin olabilir bir Bulucu kullanılabilir olmasından toowhen oluşturulduktan sonra gecikme.</span><span class="sxs-lookup"><span data-stu-id="da2c6-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="da2c6-186">Bu sorun tooboth SAS URL'si ve Kaynak Konum Belirleyicisi geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="da2c6-187">Aşağıdaki örneğine hello nasıl toocreate bir SAS URL'si tarafından tanımlanan Bulucu, hello hello istek gövdesindeki (bir SAS Bulucu için "1") ve bir isteğe bağlı kaynak Bulucu için "2" Type özelliği gösterir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="da2c6-188">Merhaba **yolu** döndürülen özelliği içeren hello URL dosyanızı tooupload kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="da2c6-189">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="da2c6-189">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

<span data-ttu-id="da2c6-190">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-190">**HTTP Response**</span></span>

<span data-ttu-id="da2c6-191">Başarılı olursa, yanıt aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="da2c6-191">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="da2c6-192">Bir blob depolama kapsayıcısının içine bir dosyayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="da2c6-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="da2c6-193">Merhaba AccessPolicy ve Bulucu kümesi oluşturduktan sonra hello gerçek hello Azure Storage REST API'leri kullanılarak karşıya yüklenen tooan Azure Blob Storage kapsayıcısına dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="da2c6-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="da2c6-194">Blok blobları hello dosyalarını yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="da2c6-195">Sayfa bloblarını Azure Media Services tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="da2c6-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="da2c6-196">Merhaba dosya adı eklemelisiniz hello dosya için tooupload toohello Bulucu istediğiniz **yolu** hello önceki bölümde alınan değer.</span><span class="sxs-lookup"><span data-stu-id="da2c6-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="da2c6-197">Örneğin, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="da2c6-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="da2c6-198">.</span><span class="sxs-lookup"><span data-stu-id="da2c6-198">.</span></span> <span data-ttu-id="da2c6-199">.</span><span class="sxs-lookup"><span data-stu-id="da2c6-199">.</span></span> <span data-ttu-id="da2c6-200">.</span><span class="sxs-lookup"><span data-stu-id="da2c6-200">.</span></span> 
> 
> 

<span data-ttu-id="da2c6-201">Azure depolama BLOB'ları ile çalışma hakkında daha fazla bilgi için bkz: [Blob hizmeti REST API'si](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="da2c6-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="da2c6-202">Merhaba AssetFile güncelleştir</span><span class="sxs-lookup"><span data-stu-id="da2c6-202">Update hello AssetFile</span></span>
<span data-ttu-id="da2c6-203">Dosyanızı yüklediğiniz, hello FileAsset boyut (ve diğer) bilgi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="da2c6-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="da2c6-204">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="da2c6-204">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="da2c6-205">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-205">**HTTP Response**</span></span>

<span data-ttu-id="da2c6-206">Başarılı, hello aşağıdaki döndürülür: HTTP/1.1 204 İçerik yok</span><span class="sxs-lookup"><span data-stu-id="da2c6-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="da2c6-207">Merhaba Bulucu ve AccessPolicy Sil</span><span class="sxs-lookup"><span data-stu-id="da2c6-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="da2c6-208">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="da2c6-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="da2c6-209">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-209">**HTTP Response**</span></span>

<span data-ttu-id="da2c6-210">Başarılı olursa, hello aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="da2c6-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="da2c6-211">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="da2c6-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="da2c6-212">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-212">**HTTP Response**</span></span>

<span data-ttu-id="da2c6-213">Başarılı olursa, hello aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="da2c6-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="da2c6-214"><a id="upload_in_bulk"></a>Varlıkları toplu yükleyin</span><span class="sxs-lookup"><span data-stu-id="da2c6-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="da2c6-215">Merhaba IngestManifest oluşturma</span><span class="sxs-lookup"><span data-stu-id="da2c6-215">Create hello IngestManifest</span></span>
<span data-ttu-id="da2c6-216">Merhaba IngestManifest varlıklar, varlık dosyaları ve olabilir istatistik bilgileri kümesi için bir kapsayıcıdır toodetermine hello ilerlemesini, toplu alma hello kümesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="da2c6-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="da2c6-217">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="da2c6-217">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="da2c6-218">Varlıklar oluşturma</span><span class="sxs-lookup"><span data-stu-id="da2c6-218">Create assets</span></span>
<span data-ttu-id="da2c6-219">Merhaba IngestManifestAsset oluşturmadan önce toocreate hello toplu alanını kullanarak tamamlanacak varlık gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="da2c6-220">Bir varlık, birden çok türleri veya Media Services, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları dahil olmak üzere nesne kümeleri için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="da2c6-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="da2c6-221">Hello REST API'da, bir varlık oluşturmak için bir HTTP POST isteği tooMicrosoft Azure Media Services gönderme ve hello istek gövdesinde Varlığınızı ilgili herhangi bir özellik bilgi yerleştirme gerekir. Bu örnekte, hello varlık hello istek gövdesi dahil hello StorageEncrption(1) seçeneği kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="da2c6-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="da2c6-222">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-222">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="da2c6-223">Merhaba IngestManifestAssets oluşturma</span><span class="sxs-lookup"><span data-stu-id="da2c6-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="da2c6-224">IngestManifestAssets toplu alma ile kullanılan varlıklar bir IngestManifest içinde temsil eder.</span><span class="sxs-lookup"><span data-stu-id="da2c6-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="da2c6-225">Merhaba temelde hello varlık toohello bildirimi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="da2c6-226">Azure Media Services IngestManifestFiles ilişkili koleksiyon toohello IngestManifestAsset üzerinde temel hello dosya karşıya yükleme için dahili olarak izler.</span><span class="sxs-lookup"><span data-stu-id="da2c6-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="da2c6-227">Bu dosyalar yüklendiğinde hello varlık tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="da2c6-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="da2c6-228">Bir HTTP POST isteği ile yeni bir IngestManifestAsset oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2c6-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="da2c6-229">Merhaba istek gövdesinde hello IngestManifest kimliği ve hello varlık kimliği IngestManifestAsset toplu alma için birlikte bağlanması gereken bu hello içerir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="da2c6-230">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-230">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="da2c6-231">Merhaba IngestManifestFiles her varlık için oluşturma</span><span class="sxs-lookup"><span data-stu-id="da2c6-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="da2c6-232">Bir IngestManifestFile bir varlık için toplu alma bir parçası olarak yüklenen gerçek ses veya video blob nesneyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="da2c6-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="da2c6-233">Şifreleme ile ilgili bir şifreleme seçeneği hello varlık kullanmadığınız sürece özellikler gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="da2c6-234">Bu bölümde kullanılan hello örnek StorageEncryption varlık daha önce oluşturduğunuz Merhaba kullanan bir IngestManifestFile oluşturma gösterir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="da2c6-235">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-235">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="da2c6-236">Merhaba dosyaları tooBlob depolama karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="da2c6-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="da2c6-237">Merhaba varlık dosyaları toohello blob depolama kapsayıcısını hello hello IngestManifest BlobStorageUriForUpload özelliği tarafından sağlanan URI karşıya yükleme özellikli tüm yüksek hızlı istemci uygulamasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2c6-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="da2c6-238">Bir önem düzeyindeki yüksek hızlı karşıya yükleme hizmeti [Aspera istendiğinde Azure uygulaması için](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="da2c6-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="da2c6-239">İzleyici toplu ilerleme durumunu alma</span><span class="sxs-lookup"><span data-stu-id="da2c6-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="da2c6-240">Toplu işlemleri için bir IngestManifest hello IngestManifest hello istatistikleri özelliği yoklayarak alındıktan hello ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2c6-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="da2c6-241">Özelliği bir karmaşık tür olup [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="da2c6-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="da2c6-242">toopoll hello istatistikleri özelliği hello IngestManifest kimliği geçirme bir HTTP GET isteği gönder</span><span class="sxs-lookup"><span data-stu-id="da2c6-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="da2c6-243">Şifreleme için kullanılan ContentKeys oluşturma</span><span class="sxs-lookup"><span data-stu-id="da2c6-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="da2c6-244">Varlığınızı şifreleme kullanacaksa, varlık dosyaları hello oluşturmadan önce şifreleme için kullanılan hello ContentKey toobe oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="da2c6-245">Depolama şifrelemesi için hello aşağıdaki özellikleri hello istek gövdesinde yer alması gerekir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="da2c6-246">İstek gövdesi özelliği</span><span class="sxs-lookup"><span data-stu-id="da2c6-246">Request body property</span></span> | <span data-ttu-id="da2c6-247">Açıklama</span><span class="sxs-lookup"><span data-stu-id="da2c6-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="da2c6-248">Kimlik</span><span class="sxs-lookup"><span data-stu-id="da2c6-248">Id</span></span> |<span data-ttu-id="da2c6-249">Merhaba biz oluşturan ContentKey kimliği kendisini izleyen hello kullanarak biçimi, "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="da2c6-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="da2c6-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="da2c6-250">ContentKeyType</span></span> |<span data-ttu-id="da2c6-251">Bu içerik anahtarı için bir tamsayı olarak hello içerik anahtar türü budur.</span><span class="sxs-lookup"><span data-stu-id="da2c6-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="da2c6-252">Biz depolama şifrelemesi için 1 hello değeri geçirin.</span><span class="sxs-lookup"><span data-stu-id="da2c6-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="da2c6-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="da2c6-253">EncryptedContentKey</span></span> |<span data-ttu-id="da2c6-254">256 bitlik (32 bayt) bir değer olan yeni bir içerik anahtarı değeri oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="da2c6-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="da2c6-255">başlangıç anahtarı hello GetProtectionKeyId ve GetProtectionKey yöntemleri için bir HTTP GET isteği yürüterek Microsoft Azure Media Services'den alıyoruz hello depolama şifreleme X.509 sertifikası kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="da2c6-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="da2c6-256">ProtectionKeyId</span></span> |<span data-ttu-id="da2c6-257">Bu olduğu hello koruma anahtar kimliği için kullanılan tooencrypt edildi hello depolama şifreleme X.509 sertifikası bizim içerik anahtarı.</span><span class="sxs-lookup"><span data-stu-id="da2c6-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="da2c6-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="da2c6-258">ProtectionKeyType</span></span> |<span data-ttu-id="da2c6-259">Bu hello şifreleme için kullanılan tooencrypt hello içerik anahtar: hello koruma anahtarı türüdür.</span><span class="sxs-lookup"><span data-stu-id="da2c6-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="da2c6-260">Bu değer StorageEncryption(1) Bizim örneğimizde olur.</span><span class="sxs-lookup"><span data-stu-id="da2c6-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="da2c6-261">Sağlama toplamı</span><span class="sxs-lookup"><span data-stu-id="da2c6-261">Checksum</span></span> |<span data-ttu-id="da2c6-262">Merhaba MD5 hello içerik anahtarı için hesaplanan sağlama.</span><span class="sxs-lookup"><span data-stu-id="da2c6-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="da2c6-263">Merhaba içerik anahtarı kimliği içerikle hello şifreleyerek hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="da2c6-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="da2c6-264">Merhaba örnek kodu nasıl toocalculate hello sağlama toplamı gösterir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="da2c6-265">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-265">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="da2c6-266">Bağlantı hello ContentKey toohello varlık</span><span class="sxs-lookup"><span data-stu-id="da2c6-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="da2c6-267">Merhaba ContentKey ilişkili tooone ya da daha fazla varlıklar bir HTTP POST isteği göndermektir.</span><span class="sxs-lookup"><span data-stu-id="da2c6-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="da2c6-268">Merhaba aşağıdaki isteği olan bir örnek toolink hello örnek ContentKey toohello örnek varlığı kimliğe göre</span><span class="sxs-lookup"><span data-stu-id="da2c6-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="da2c6-269">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-269">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="da2c6-270">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="da2c6-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="da2c6-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="da2c6-271">Next steps</span></span>

<span data-ttu-id="da2c6-272">Karşıya yüklenen varlıklarınızı artık kodlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2c6-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="da2c6-273">Daha fazla bilgi için bkz. [Varlıkları kodlama](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="da2c6-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="da2c6-274">Azure işlevleri tootrigger yapılandırılmış hello kapsayıcısında ulaşan bir dosyayı temel bir kodlama işi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da2c6-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="da2c6-275">Daha fazla bilgi için [bu örneğe](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) bakın.</span><span class="sxs-lookup"><span data-stu-id="da2c6-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="da2c6-276">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="da2c6-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="da2c6-277">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="da2c6-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

