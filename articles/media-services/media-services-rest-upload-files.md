---
title: "Dosyaları REST kullanarak bir Media Services hesabına veri yükleme | Microsoft Docs"
description: "Oluşturma ve karşıya varlıklar Media Services'e medya içeriği alma hakkında bilgi."
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
ms.openlocfilehash: 955356ffe6fc524c1528364add7e2c2a336137b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="8454c-103">Dosyaları REST kullanarak bir Media Services hesabına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="8454c-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8454c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8454c-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="8454c-105">REST</span><span class="sxs-lookup"><span data-stu-id="8454c-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="8454c-106">Portal</span><span class="sxs-lookup"><span data-stu-id="8454c-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="8454c-107">Media Services’de dijital dosyalar bir varlığa yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8454c-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="8454c-108">[Varlık](https://docs.microsoft.com/rest/api/media/operations/asset) varlık içerebilir video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkındaki meta verileri.)  Dosyaları varlığa yüklendiğinde, içeriğiniz sonraki işleme ve akışla için bulutta güvenli bir şekilde depolanır.</span><span class="sxs-lookup"><span data-stu-id="8454c-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="8454c-109">Aşağıdaki maddeler geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="8454c-109">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="8454c-110">Media Services IAssetFile.Name özelliğinin değeri, URL akış içeriğini (örneğin, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) oluştururken kullanır. Bu nedenle, yüzde kodlama izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="8454c-110">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="8454c-111">Değeri **adı** özelliği aşağıdakilerden herhangi birini içeremez [yüzde kodlama-ayrılmış karakterleri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="8454c-111">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="8454c-112">Ayrıca, yalnızca bir olabilir '.' dosya adı uzantısı için.</span><span class="sxs-lookup"><span data-stu-id="8454c-112">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="8454c-113">Adının uzunluğu 260 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8454c-113">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="8454c-114">Media Services ile işleme için desteklenen dosya boyutlarına yönelik üst sınır uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8454c-114">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="8454c-115">Dosya boyutu sınırlaması hakkında ayrıntılı bilgi için lütfen [bu konu başlığını](media-services-quotas-and-limitations.md) inceleyin.</span><span class="sxs-lookup"><span data-stu-id="8454c-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> 

<span data-ttu-id="8454c-116">Varlıklar yüklemeyle temel iş akışı, aşağıdaki bölümlere ayrılır:</span><span class="sxs-lookup"><span data-stu-id="8454c-116">The basic workflow for uploading Assets is divided into the following sections:</span></span>

* <span data-ttu-id="8454c-117">Bir varlık oluşturun</span><span class="sxs-lookup"><span data-stu-id="8454c-117">Create an Asset</span></span>
* <span data-ttu-id="8454c-118">(İsteğe bağlı) bir varlık şifrele</span><span class="sxs-lookup"><span data-stu-id="8454c-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="8454c-119">Blob depolama alanına bir dosyayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="8454c-119">Upload a file to blob storage</span></span>

<span data-ttu-id="8454c-120">AMS toplu varlıklar karşıya yüklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="8454c-120">AMS also enables you to upload assets in bulk.</span></span> <span data-ttu-id="8454c-121">Daha fazla bilgi için [bu](media-services-rest-upload-files.md#upload_in_bulk) bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="8454c-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="8454c-122">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8454c-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="8454c-123">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8454c-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="8454c-124">Media Services’e bağlanmak</span><span class="sxs-lookup"><span data-stu-id="8454c-124">Connect to Media Services</span></span>

<span data-ttu-id="8454c-125">AMS API'sine bağlanma hakkında daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile Azure Media Services API erişim](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="8454c-125">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="8454c-126">Başarıyla https://media.windows.net için bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="8454c-126">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="8454c-127">Yeni bir URI yapılan sonraki çağrılar yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8454c-127">You must make subsequent calls to the new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="8454c-128">Varlıkları yükleyin</span><span class="sxs-lookup"><span data-stu-id="8454c-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="8454c-129">Bir varlık oluşturun</span><span class="sxs-lookup"><span data-stu-id="8454c-129">Create an asset</span></span>

<span data-ttu-id="8454c-130">Bir varlık, birden çok türleri veya Media Services, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları dahil olmak üzere nesne kümeleri için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="8454c-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="8454c-131">REST API bir varlık oluşturmak için Media Services POST isteği gönderme ve istek gövdesinde Varlığınızı ilgili herhangi bir özellik bilgi yerleştirme gerekir.</span><span class="sxs-lookup"><span data-stu-id="8454c-131">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="8454c-132">Bir varlık oluşturma olduğunda belirtebilirsiniz özelliklerden birini **seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="8454c-132">One of the properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="8454c-133">**Seçenekler** bir varlığı ile oluşturulan şifreleme seçenekleri açıklayan bir numaralandırma değeridir.</span><span class="sxs-lookup"><span data-stu-id="8454c-133">**Options** is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="8454c-134">Geçerli bir değer değil değerleri bileşimini aşağıdaki listeden değerlerinden biri.</span><span class="sxs-lookup"><span data-stu-id="8454c-134">A valid value is one of the values from the list below, not a combination of values.</span></span> 

* <span data-ttu-id="8454c-135">**Hiçbiri** = **0**: şifreleme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8454c-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="8454c-136">Varsayılan değer budur.</span><span class="sxs-lookup"><span data-stu-id="8454c-136">This is the default value.</span></span> <span data-ttu-id="8454c-137">Bu seçenek kullanıldığında, içeriğinizin aktarım veya deposunda kalan korunmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8454c-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="8454c-138">Aşamalı indirme kullanarak bir MP4 iletmeyi planlıyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="8454c-138">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="8454c-139">**StorageEncrypted** = **1**: dosyalarınızın karşıya yükleme ve depolama için AES 256 bit şifreleme ile şifrelenmiş isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="8454c-139">**StorageEncrypted** = **1**: Specify if you want for your files to be encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="8454c-140">Şifrelenmiş depolama varlığınız olması durumunda, varlık teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8454c-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="8454c-141">Daha fazla bilgi için bkz: [varlık teslim ilkesini yapılandırma](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="8454c-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="8454c-142">**CommonEncryptionProtected** = **2**: ortak bir şifreleme yöntemi (örneğin, PlayReady) ile korunan dosyaları karşıya varsa belirtin.</span><span class="sxs-lookup"><span data-stu-id="8454c-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="8454c-143">**EnvelopeEncryptionProtected** = **4**: AES dosyaları ile şifrelenmiş HLS karşıya varsa belirtin.</span><span class="sxs-lookup"><span data-stu-id="8454c-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="8454c-144">Dosyaların Transform Manager tarafından kodlanmış ve şifrelenmiş olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8454c-144">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="8454c-145">Varlığınızı şifreleme kullanacaksa, oluşturmalısınız bir **ContentKey** ve aşağıdaki konuda açıklandığı gibi varlık Bağla:[bir ContentKey oluşturma](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="8454c-145">If your asset will use encryption, you must create a **ContentKey** and link it to your asset as described in the following topic:[How to create a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="8454c-146">Dosyaları varlığa yükleme sonra şifreleme özellikleri sunucusunda da güncelleştirmeniz gerektiğini unutmayın **AssetFile** aldığınız sırasında değerlerle varlık **varlık** şifreleme.</span><span class="sxs-lookup"><span data-stu-id="8454c-146">Note that after you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption.</span></span> <span data-ttu-id="8454c-147">Bunu kullanarak **birleştirme** HTTP isteği.</span><span class="sxs-lookup"><span data-stu-id="8454c-147">Do it by using the **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="8454c-148">Aşağıdaki örnek, bir varlık oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8454c-148">The following example shows how to create an asset.</span></span>

<span data-ttu-id="8454c-149">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="8454c-149">**HTTP Request**</span></span>

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

<span data-ttu-id="8454c-150">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-150">**HTTP Response**</span></span>

<span data-ttu-id="8454c-151">Başarılı olursa, aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="8454c-151">If successful, the following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="8454c-152">Bir AssetFile oluşturma</span><span class="sxs-lookup"><span data-stu-id="8454c-152">Create an AssetFile</span></span>
<span data-ttu-id="8454c-153">[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) varlığı temsil eden bir blob kapsayıcısında depolanır ses veya video dosyası.</span><span class="sxs-lookup"><span data-stu-id="8454c-153">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="8454c-154">Bir varlık dosyası her zaman bir varlıkla ilişkilidir ve bir varlığı bir veya daha çok varlık dosyaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8454c-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="8454c-155">Bir varlık dosyası nesne bir blob kapsayıcısında dijital bir dosyayla ilişkili değilse Media Services Kodlayıcısı görev başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="8454c-155">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="8454c-156">Unutmayın **AssetFile** örneği ve gerçek medya dosyası olan iki farklı nesneler.</span><span class="sxs-lookup"><span data-stu-id="8454c-156">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="8454c-157">Medya dosyasının gerçek medya içeriği içerirken AssetFile örneği medya dosyası hakkındaki meta verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="8454c-157">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="8454c-158">Bir blob kapsayıcıya bir dijital medyayı dosyanızı karşıya sonra kullanacağınız **birleştirme** (daha sonra konu başlığı altında gösterildiği gibi), ortam dosyası hakkındaki bilgilerle AssetFile güncelleştirmeye yönelik HTTP isteği.</span><span class="sxs-lookup"><span data-stu-id="8454c-158">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span> 

<span data-ttu-id="8454c-159">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="8454c-159">**HTTP Request**</span></span>

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

<span data-ttu-id="8454c-160">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-160">**HTTP Response**</span></span>

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

### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="8454c-161">AccessPolicy yazma izni olan oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="8454c-161">Creating the AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="8454c-162">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="8454c-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="8454c-163">Uzun süre boyunca kullanılmak için oluşturulan bulucu ilkeleri gibi aynı günleri / erişim izinlerini sürekli olarak kullanıyorsanız, aynı ilke kimliğini kullanmalısınız (karşıya yükleme olmayan ilkeler için).</span><span class="sxs-lookup"><span data-stu-id="8454c-163">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="8454c-164">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="8454c-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="8454c-165">Blob depolama alanına herhangi bir dosya karşıya yüklemeden önce erişim için bir varlık yazma İlkesi hakları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8454c-165">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="8454c-166">Bunu yapmak için AccessPolicies varlık kümesi için bir HTTP isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="8454c-166">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="8454c-167">Oluşturulduktan sonra bir dakika Cinsiden Süre değer tanımlama veya yanıt olarak bir 500 İç sunucu hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="8454c-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="8454c-168">AccessPolicies hakkında daha fazla bilgi için bkz: [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="8454c-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="8454c-169">Aşağıdaki örnekte bir AccessPolicy oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="8454c-169">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="8454c-170">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="8454c-170">**HTTP Request**</span></span>

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

<span data-ttu-id="8454c-171">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="8454c-171">**HTTP Request**</span></span>

    If successful, the following response is returned:

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

### <a name="get-the-upload-url"></a><span data-ttu-id="8454c-172">Karşıya yükleme URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="8454c-172">Get the Upload URL</span></span>
<span data-ttu-id="8454c-173">Gerçek yükleme URL'si almak için bir SAS Bulucu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8454c-173">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="8454c-174">Bulucular bir varlık içindeki dosyalara erişmek istediğiniz istemciler için başlangıç saatini ve bağlantı uç noktasının türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8454c-174">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="8454c-175">Farklı istemci isteklerini gereksinimlerini karşılamak belirli bir AccessPolicy ve varlık çifti için birden çok Bulucu varlık oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8454c-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="8454c-176">Her bu Bulucuyu StartTime değerinin yanı sıra AccessPolicy Dakika Cinsiden Süre değerinin bir URL kullanılabilir süreyi belirlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="8454c-176">Each of these Locators use the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="8454c-177">Daha fazla bilgi için bkz: [Bulucu](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="8454c-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="8454c-178">Bir SAS URL'si aşağıdaki biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8454c-178">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="8454c-179">Bazı dikkate alınması gereken noktalar vardır:</span><span class="sxs-lookup"><span data-stu-id="8454c-179">Some considerations apply:</span></span>

* <span data-ttu-id="8454c-180">Aynı anda belirli bir varlıkla ilişkilendirilen beşten fazla benzersiz Bulucular sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="8454c-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="8454c-181">Daha fazla bilgi için Bulucu bakın.</span><span class="sxs-lookup"><span data-stu-id="8454c-181">For more information, see Locator.</span></span>
* <span data-ttu-id="8454c-182">Dosyalarınızı hemen karşıya gerekiyorsa, geçerli tarihten önce beş dakika StartTime değeri ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8454c-182">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="8454c-183">Bu; çünkü istemci makine ve Media Services arasında eğme saat olabilir.</span><span class="sxs-lookup"><span data-stu-id="8454c-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="8454c-184">Ayrıca, StartTime değeri aşağıdaki tarih saat biçiminde olmalıdır: YYYY-MM-: ssZ (örneğin, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="8454c-184">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="8454c-185">30-40 saniyenin olması için bir Bulucu kullanılabilir olduğunda oluşturulduktan sonra gecikme.</span><span class="sxs-lookup"><span data-stu-id="8454c-185">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="8454c-186">Bu sorun, SAS URL'si ve Kaynak Konum Belirleyicisi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="8454c-186">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="8454c-187">Aşağıdaki örnek, Type özelliği (bir SAS Bulucu için "1") ve "2" isteğe bağlı kaynak konum belirleyicisi için istek gövdesinde tarafından tanımlandığı şekilde bir SAS URL'si Bulucu oluşturma gösterir.</span><span class="sxs-lookup"><span data-stu-id="8454c-187">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="8454c-188">**Yolu** döndürülen özelliği dosyanızı karşıya yüklemek için kullandığınız URL'yi içerir.</span><span class="sxs-lookup"><span data-stu-id="8454c-188">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="8454c-189">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="8454c-189">**HTTP Request**</span></span>

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

<span data-ttu-id="8454c-190">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-190">**HTTP Response**</span></span>

<span data-ttu-id="8454c-191">Başarılı olursa, şu yanıtı döndürdü:</span><span class="sxs-lookup"><span data-stu-id="8454c-191">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="8454c-192">Bir blob depolama kapsayıcısının içine bir dosyayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="8454c-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="8454c-193">Bulucu ayarlamak ve AccessPolicy olduktan sonra gerçek dosya Azure Storage REST API'lerini kullanarak bir Azure Blob Storage kapsayıcısı yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8454c-193">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="8454c-194">Blok blobları dosyaları yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8454c-194">You must upload the files as block blobs.</span></span> <span data-ttu-id="8454c-195">Sayfa bloblarını Azure Media Services tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="8454c-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="8454c-196">Bulucu karşıya yüklemek istediğiniz dosyası için dosya adı eklemelisiniz **yolu** önceki bölümde alınan değer.</span><span class="sxs-lookup"><span data-stu-id="8454c-196">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="8454c-197">Örneğin, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="8454c-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="8454c-198">.</span><span class="sxs-lookup"><span data-stu-id="8454c-198">.</span></span> <span data-ttu-id="8454c-199">.</span><span class="sxs-lookup"><span data-stu-id="8454c-199">.</span></span> <span data-ttu-id="8454c-200">.</span><span class="sxs-lookup"><span data-stu-id="8454c-200">.</span></span> 
> 
> 

<span data-ttu-id="8454c-201">Azure depolama BLOB'ları ile çalışma hakkında daha fazla bilgi için bkz: [Blob hizmeti REST API'si](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="8454c-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="8454c-202">Güncelleştirme AssetFile</span><span class="sxs-lookup"><span data-stu-id="8454c-202">Update the AssetFile</span></span>
<span data-ttu-id="8454c-203">Dosyanızı yüklediğiniz, FileAsset boyut (ve diğer) bilgi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8454c-203">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="8454c-204">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8454c-204">For example:</span></span>

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


<span data-ttu-id="8454c-205">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-205">**HTTP Response**</span></span>

<span data-ttu-id="8454c-206">Başarılı, aşağıdaki döndürülür: HTTP/1.1 204 İçerik yok</span><span class="sxs-lookup"><span data-stu-id="8454c-206">If successful, the following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="8454c-207">Bulucu ve AccessPolicy Sil</span><span class="sxs-lookup"><span data-stu-id="8454c-207">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="8454c-208">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="8454c-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="8454c-209">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-209">**HTTP Response**</span></span>

<span data-ttu-id="8454c-210">Başarılı olursa, aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="8454c-210">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="8454c-211">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="8454c-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="8454c-212">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-212">**HTTP Response**</span></span>

<span data-ttu-id="8454c-213">Başarılı olursa, aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="8454c-213">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="8454c-214"><a id="upload_in_bulk"></a>Varlıkları toplu yükleyin</span><span class="sxs-lookup"><span data-stu-id="8454c-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-the-ingestmanifest"></a><span data-ttu-id="8454c-215">IngestManifest oluşturma</span><span class="sxs-lookup"><span data-stu-id="8454c-215">Create the IngestManifest</span></span>
<span data-ttu-id="8454c-216">IngestManifest varlıklar, varlık dosyaları ve küme için alma toplu ilerlemesini belirlemek için kullanılan istatistik bilgileri kümesi için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="8454c-216">The IngestManifest is a container for a set of assets, asset files, and statistic information that can be used to determine the progress of bulk ingesting for the set.</span></span>

<span data-ttu-id="8454c-217">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="8454c-217">**HTTP Request**</span></span>

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

### <a name="create-assets"></a><span data-ttu-id="8454c-218">Varlıklar oluşturma</span><span class="sxs-lookup"><span data-stu-id="8454c-218">Create assets</span></span>
<span data-ttu-id="8454c-219">IngestManifestAsset oluşturmadan önce toplu alanını kullanarak tamamlanacak varlığı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8454c-219">Before creating the IngestManifestAsset, you need to create the Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="8454c-220">Bir varlık, birden çok türleri veya Media Services, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları dahil olmak üzere nesne kümeleri için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="8454c-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="8454c-221">REST API bir varlık oluşturmak için Microsoft Azure Media Services için bir HTTP POST isteği gönderme ve istek gövdesinde Varlığınızı ilgili herhangi bir özellik bilgi yerleştirme gerekir. Bu örnekte, varlık ile istek gövdesi dahil StorageEncrption(1) seçeneği kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8454c-221">In the REST API, creating an Asset requires sending a HTTP POST request to Microsoft Azure Media Services and placing any property information about your asset in the request body.In this example, the Asset is created using the StorageEncrption(1) option included with the request body.</span></span>

<span data-ttu-id="8454c-222">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-222">**HTTP Response**</span></span>

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

### <a name="create-the-ingestmanifestassets"></a><span data-ttu-id="8454c-223">IngestManifestAssets oluşturma</span><span class="sxs-lookup"><span data-stu-id="8454c-223">Create the IngestManifestAssets</span></span>
<span data-ttu-id="8454c-224">IngestManifestAssets toplu alma ile kullanılan varlıklar bir IngestManifest içinde temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8454c-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="8454c-225">Temel varlık bildirime bağlantı.</span><span class="sxs-lookup"><span data-stu-id="8454c-225">The basically link the asset to the manifest.</span></span> <span data-ttu-id="8454c-226">Azure Media Services IngestManifestAsset ilişkili IngestManifestFiles koleksiyonu göre dosya karşıya yükleme için dahili olarak izler.</span><span class="sxs-lookup"><span data-stu-id="8454c-226">Azure Media Services watches internally for the file upload based on IngestManifestFiles collection associated to the IngestManifestAsset.</span></span> <span data-ttu-id="8454c-227">Bu dosyalar yüklendiğinde varlık tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8454c-227">Once these files are uploaded, the asset is completed.</span></span> <span data-ttu-id="8454c-228">Bir HTTP POST isteği ile yeni bir IngestManifestAsset oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8454c-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="8454c-229">İstek gövdesinde IngestManifest kimliği ve IngestManifestAsset toplu alma için birlikte bağlanması gereken varlık kimliği içerir.</span><span class="sxs-lookup"><span data-stu-id="8454c-229">In the request body, include the IngestManifest Id and the Asset Id that the IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="8454c-230">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-230">**HTTP Response**</span></span>

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


### <a name="create-the-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="8454c-231">Her varlık için IngestManifestFiles oluşturma</span><span class="sxs-lookup"><span data-stu-id="8454c-231">Create the IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="8454c-232">Bir IngestManifestFile bir varlık için toplu alma bir parçası olarak yüklenen gerçek ses veya video blob nesneyi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8454c-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="8454c-233">Şifreleme ile ilgili varlık bir şifreleme seçeneği kullanmadığınız sürece özellik gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="8454c-233">Encryption related properties are not required unless the asset is using an encryption option.</span></span> <span data-ttu-id="8454c-234">Bu bölümde kullanılan örnek StorageEncryption daha önce oluşturulan varlığı için kullanan bir IngestManifestFile oluşturma gösterir.</span><span class="sxs-lookup"><span data-stu-id="8454c-234">The example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for the Asset previously created.</span></span>

<span data-ttu-id="8454c-235">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-235">**HTTP Response**</span></span>

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

### <a name="upload-the-files-to-blob-storage"></a><span data-ttu-id="8454c-236">Blob depolama alanına dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="8454c-236">Upload the Files to Blob Storage</span></span>
<span data-ttu-id="8454c-237">URI IngestManifest BlobStorageUriForUpload özelliği tarafından sağlanan blob depolama kapsayıcısını varlık dosyaları yükleme özellikli tüm yüksek hızlı istemci uygulamasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8454c-237">You can use any high speed client application capable of uploading the asset files to the blob storage container Uri provided by the BlobStorageUriForUpload property of the IngestManifest.</span></span> <span data-ttu-id="8454c-238">Bir önem düzeyindeki yüksek hızlı karşıya yükleme hizmeti [Aspera istendiğinde Azure uygulaması için](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="8454c-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="8454c-239">İzleyici toplu ilerleme durumunu alma</span><span class="sxs-lookup"><span data-stu-id="8454c-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="8454c-240">Toplu işlemleri için bir IngestManifest IngestManifest istatistikleri özelliğinin yoklayarak alma ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8454c-240">You can monitor the progress of bulk ingesting operations for an IngestManifest by polling the Statistics property of the IngestManifest.</span></span> <span data-ttu-id="8454c-241">Özelliği bir karmaşık tür olup [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="8454c-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="8454c-242">İstatistikleri özelliği yoklamak için IngestManifest kimliği geçirme bir HTTP GET isteği gönderin</span><span class="sxs-lookup"><span data-stu-id="8454c-242">To poll the Statistics property, submit a HTTP GET request passing the IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="8454c-243">Şifreleme için kullanılan ContentKeys oluşturma</span><span class="sxs-lookup"><span data-stu-id="8454c-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="8454c-244">Varlığınızı şifreleme kullanacaksa, varlık dosyaları oluşturmadan önce şifreleme için kullanılacak ContentKey oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8454c-244">If your asset will use encryption, you must create the ContentKey to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="8454c-245">Depolama şifrelemesi için aşağıdaki özellikleri istek gövdesinde yer alması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8454c-245">For storage encryption, the following properties should be included in the request body.</span></span>

| <span data-ttu-id="8454c-246">İstek gövdesi özelliği</span><span class="sxs-lookup"><span data-stu-id="8454c-246">Request body property</span></span> | <span data-ttu-id="8454c-247">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8454c-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8454c-248">Kimlik</span><span class="sxs-lookup"><span data-stu-id="8454c-248">Id</span></span> |<span data-ttu-id="8454c-249">Biz kendisini oluşturan ContentKey kimliği aşağıdaki biçimi kullanarak "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="8454c-249">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="8454c-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="8454c-250">ContentKeyType</span></span> |<span data-ttu-id="8454c-251">Bu içerik anahtarı için bir tamsayı olarak içerik anahtar türü budur.</span><span class="sxs-lookup"><span data-stu-id="8454c-251">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="8454c-252">Biz depolama şifrelemesi için 1 değerini geçirin.</span><span class="sxs-lookup"><span data-stu-id="8454c-252">We pass the value 1 for storage encryption.</span></span> |
| <span data-ttu-id="8454c-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="8454c-253">EncryptedContentKey</span></span> |<span data-ttu-id="8454c-254">256 bitlik (32 bayt) bir değer olan yeni bir içerik anahtarı değeri oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="8454c-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="8454c-255">Anahtar GetProtectionKeyId ve GetProtectionKey yöntemleri için bir HTTP GET isteği yürüterek Microsoft Azure Media Services'den alıyoruz depolama şifreleme X.509 sertifikası kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="8454c-255">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="8454c-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="8454c-256">ProtectionKeyId</span></span> |<span data-ttu-id="8454c-257">Bu, bizim içerik anahtarı şifrelemek için kullanılan depolama şifreleme X.509 Sertifika koruma anahtar kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="8454c-257">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span> |
| <span data-ttu-id="8454c-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="8454c-258">ProtectionKeyType</span></span> |<span data-ttu-id="8454c-259">İçerik anahtarı şifrelemek için kullanılan koruma anahtarı şifreleme türü budur.</span><span class="sxs-lookup"><span data-stu-id="8454c-259">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="8454c-260">Bu değer StorageEncryption(1) Bizim örneğimizde olur.</span><span class="sxs-lookup"><span data-stu-id="8454c-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="8454c-261">Sağlama toplamı</span><span class="sxs-lookup"><span data-stu-id="8454c-261">Checksum</span></span> |<span data-ttu-id="8454c-262">MD5 hesaplanan sağlama toplamı için içerik anahtarı.</span><span class="sxs-lookup"><span data-stu-id="8454c-262">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="8454c-263">İçerik anahtarı kimliği içerikle şifreleyerek hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="8454c-263">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="8454c-264">Kod örneği, sağlama toplamı hesaplamak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8454c-264">The example code demonstrates how to calculate the checksum.</span></span> |

<span data-ttu-id="8454c-265">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-265">**HTTP Response**</span></span>

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

### <a name="link-the-contentkey-to-the-asset"></a><span data-ttu-id="8454c-266">ContentKey varlık için bağlantı</span><span class="sxs-lookup"><span data-stu-id="8454c-266">Link the ContentKey to the Asset</span></span>
<span data-ttu-id="8454c-267">ContentKey bir HTTP POST isteği göndererek bir veya daha fazla varlıklarına ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="8454c-267">The ContentKey is associated to one or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="8454c-268">Aşağıdaki isteği örnek varlığı kimliğe göre ContentKey örnek bağlamak üzere örneğidir</span><span class="sxs-lookup"><span data-stu-id="8454c-268">The following request is an example to link the example ContentKey to the example asset by Id.</span></span>

<span data-ttu-id="8454c-269">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-269">**HTTP Response**</span></span>

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

<span data-ttu-id="8454c-270">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="8454c-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="8454c-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8454c-271">Next steps</span></span>

<span data-ttu-id="8454c-272">Karşıya yüklenen varlıklarınızı artık kodlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8454c-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="8454c-273">Daha fazla bilgi için bkz. [Varlıkları kodlama](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="8454c-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="8454c-274">Yapılandırılmış kapsayıcıya gelen dosyaya göre bir kodlama işi tetiklemek için Azure İşlevleri’ni de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8454c-274">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="8454c-275">Daha fazla bilgi için [bu örneğe](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) bakın.</span><span class="sxs-lookup"><span data-stu-id="8454c-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="8454c-276">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="8454c-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8454c-277">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="8454c-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How to Get a Media Processor]: media-services-get-media-processor.md

