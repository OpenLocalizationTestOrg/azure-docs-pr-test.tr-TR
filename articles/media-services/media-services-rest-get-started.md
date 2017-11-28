---
title: "aaaGet başlatılan REST kullanarak isteğe bağlı içerik göndermeye | Microsoft Docs"
description: "Bu öğretici, REST API kullanarak Azure Media Services ile bir üzerinde isteğe bağlı içerik teslim uygulaması gerçekleştirilmesinin hello adım adım anlatılmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="df7de-103">REST kullanarak isteğe bağlı içerik göndermeye başlama</span><span class="sxs-lookup"><span data-stu-id="df7de-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="df7de-104">Bu hızlı başlangıç Azure Media Services (AMS) REST API'lerini kullanarak bir isteğe bağlı video (VoD) içerik teslim uygulaması gerçekleştirilmesinin hello adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="df7de-104">This quickstart walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="df7de-105">Başlangıç Öğreticisi hello temel Media Services iş akışı, hello en genel programlama nesnelerini ve Media Services geliştirmek için gereken görevleri tanıtır.</span><span class="sxs-lookup"><span data-stu-id="df7de-105">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="df7de-106">Başlangıç Öğreticisi Hello tamamlandığında mümkün toostream olması veya aşamalı olarak örnek bir medya dosyasını karşıya kodlanmış ve yüklenen indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df7de-106">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="df7de-107">Merhaba aşağıdaki görüntüde bazılarını hello en yaygın olarak kullanılan nesneler hello Media Services OData modelde VoD uygulamaları geliştirirken gösterir.</span><span class="sxs-lookup"><span data-stu-id="df7de-107">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="df7de-108">Merhaba görüntü tooview boyutu tam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="df7de-108">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="df7de-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="df7de-109">Prerequisites</span></span>
<span data-ttu-id="df7de-110">Merhaba aşağıdaki önkoşullar REST API'leri ile Media Services ile geliştirme gerekli toostart bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="df7de-110">hello following prerequisites are required toostart developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="df7de-111">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="df7de-111">An Azure account.</span></span> <span data-ttu-id="df7de-112">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df7de-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="df7de-113">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="df7de-113">A Media Services account.</span></span> <span data-ttu-id="df7de-114">bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="df7de-114">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="df7de-115">Nasıl anlayış toodevelop Media Services REST API ile.</span><span class="sxs-lookup"><span data-stu-id="df7de-115">Understanding of how toodevelop with Media Services REST API.</span></span> <span data-ttu-id="df7de-116">Daha fazla bilgi için bkz: [Media Services REST API genel bakış](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="df7de-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="df7de-117">HTTP istekleri ve yanıtları göndermek tercih ettiğiniz bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="df7de-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="df7de-118">Bu öğretici kullanır [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="df7de-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="df7de-119">Bu hızlı başlangıcı görevleri aşağıdaki hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="df7de-119">hello following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="df7de-120">Akış uç noktası (hello Azure portal kullanarak) başlatın.</span><span class="sxs-lookup"><span data-stu-id="df7de-120">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="df7de-121">REST API'si ile toohello Media Services hesabına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="df7de-121">Connect toohello Media Services account with REST API.</span></span>
3. <span data-ttu-id="df7de-122">Yeni bir varlık oluşturun ve REST API ile video dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="df7de-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="df7de-123">Merhaba kaynak dosyayı Uyarlamalı bit hızlı MP4 dosyaları REST API ile kodlayın.</span><span class="sxs-lookup"><span data-stu-id="df7de-123">Encode hello source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="df7de-124">Merhaba varlığı yayımlayın ve get akış ve aşamalı indirme URL'lerini REST API ile.</span><span class="sxs-lookup"><span data-stu-id="df7de-124">Publish hello asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="df7de-125">İçeriğinizi oynatın.</span><span class="sxs-lookup"><span data-stu-id="df7de-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="df7de-126">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="df7de-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="df7de-127">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="df7de-127">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="df7de-128">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="df7de-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="df7de-129">Bu konuda kullanılan AMS REST varlıklar hakkında daha fazla ayrıntı için bkz: [Azure Media Services REST API Başvurusu](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="df7de-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="df7de-130">Ayrıca bkz [Azure Media Services kavramları](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="df7de-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="df7de-131">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="df7de-132">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="df7de-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="df7de-133">Akış uç noktaları Hello Azure portal kullanarak Başlat</span><span class="sxs-lookup"><span data-stu-id="df7de-133">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="df7de-134">Merhaba en sık karşılaşılan senaryolardan biri, video bit hızı Uyarlamalı akış iletmektir Azure Media Services ile çalışırken.</span><span class="sxs-lookup"><span data-stu-id="df7de-134">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="df7de-135">Media Services, bit hızı Uyarlamalı MP4 kodlanmış içeriğinizi Media Services (MPEG DASH, HLS, kesintisiz akış) tam zamanında tarafından önceden paketlenmiş toostore kalmadan desteklenen akış biçimlerinde toodeliver sağlayan dinamik paketleme sağlar Bu akış biçimlerine her da sürümleri.</span><span class="sxs-lookup"><span data-stu-id="df7de-135">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="df7de-136">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="df7de-136">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="df7de-137">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="df7de-137">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="df7de-138">toostart akış uç Merhaba, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="df7de-138">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="df7de-139">Merhaba oturum açma [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="df7de-139">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="df7de-140">Hello Ayarları penceresinde, akış uç noktaları'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="df7de-140">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="df7de-141">Merhaba varsayılan akış uç noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="df7de-141">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="df7de-142">Merhaba varsayılan akış uç noktası AYRINTILAR penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="df7de-142">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="df7de-143">Merhaba başlangıç simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="df7de-143">Click hello Start icon.</span></span>
5. <span data-ttu-id="df7de-144">Merhaba Kaydet düğmesine toosave değişikliklerinizi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="df7de-144">Click hello Save button toosave your changes.</span></span>

## <span data-ttu-id="df7de-145"><a id="connect"></a>REST API'si ile toohello Media Services hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="df7de-145"><a id="connect"></a>Connect toohello Media Services account with REST API</span></span>

<span data-ttu-id="df7de-146">Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="df7de-146">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="df7de-147">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="df7de-147">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="df7de-148">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="df7de-148">You must make subsequent calls toohello new URI.</span></span>

<span data-ttu-id="df7de-149">Örneğin, tooconnect çalışıyorsanız, sonra hello aşağıdaki var:</span><span class="sxs-lookup"><span data-stu-id="df7de-149">For example, if after trying tooconnect, you got hello following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="df7de-150">Sonraki API çağrıları toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-150">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="df7de-151"><a id="upload"></a>Yeni bir varlık oluşturun ve REST API ile video dosyası yükleyin</span><span class="sxs-lookup"><span data-stu-id="df7de-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="df7de-152">Media Services’de dijital dosyalar bir varlığa yüklenir.</span><span class="sxs-lookup"><span data-stu-id="df7de-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="df7de-153">Merhaba **varlık** varlık içerebilir video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkında hello meta veriler.)  Hello varlığa Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır.</span><span class="sxs-lookup"><span data-stu-id="df7de-153">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="df7de-154">Bir varlık oluşturma varlık oluşturma seçeneklerden olduğunda tooprovide sahip hello değerlerinden biri.</span><span class="sxs-lookup"><span data-stu-id="df7de-154">One of hello values that you have tooprovide when creating an asset is asset creation options.</span></span> <span data-ttu-id="df7de-155">Merhaba **seçenekleri** bir varlığı ile oluşturulan hello şifreleme seçenekleri açıklayan bir numaralandırma değeri bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="df7de-155">hello **Options** property is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="df7de-156">Geçerli bir değer değil Bu listeden bir değerler birleşimi aşağıdaki hello listeden hello değerlerinden biri:</span><span class="sxs-lookup"><span data-stu-id="df7de-156">A valid value is one of hello values from hello list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="df7de-157">**Hiçbiri** = **0** -şifreleme kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="df7de-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="df7de-158">Bu seçenek kullanıldığında, içeriğinizin aktarım veya deposunda kalan korunmaz.</span><span class="sxs-lookup"><span data-stu-id="df7de-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="df7de-159">Aşamalı indirme kullanarak toodeliver bir MP4 planlıyorsanız, bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="df7de-159">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="df7de-160">**StorageEncrypted** = **1** - Temizle içeriğinizi yerel olarak AES 256 bit şifreleme kullanarak şifreler ve tooAzure depolanır depolama şifrelenen yükler.</span><span class="sxs-lookup"><span data-stu-id="df7de-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="df7de-161">Depolama şifrelemesi ile korunan varlıklar otomatik olarak şifrelenmemiş ve bir şifrelenmiş dosya sistemi önceki tooencoding ve yeni bir çıkış varlığı olarak geri isteğe bağlı olarak yeniden şifrelenmiş önceki toouploading yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="df7de-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="df7de-162">Depolama şifrelemesinin birincil kullanım durumu hello yüksek kaliteli giriş medya dosyalarınızı REST güçlü şifrelemeyle diskte toosecure istediğiniz durumdur.</span><span class="sxs-lookup"><span data-stu-id="df7de-162">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="df7de-163">**CommonEncryptionProtected** = **2** -zaten şifrelenmiş ve ortak şifreleme veya PlayReady DRM (örneğin, ile korunan kesintisiz akış PlayReady DRM) ile korunan içerik yüklüyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="df7de-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="df7de-164">**EnvelopeEncryptionProtected** = **4** – AES ile şifrelenmiş HLS yüklüyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="df7de-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="df7de-165">Merhaba dosyaları kodlanmış ve Transform Manager tarafından şifrelenmiş gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-165">hello files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="df7de-166">Bir varlık oluşturun</span><span class="sxs-lookup"><span data-stu-id="df7de-166">Create an asset</span></span>
<span data-ttu-id="df7de-167">Bir varlık, birden çok türleri veya Media Services, video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları dahil olmak üzere nesne kümeleri için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="df7de-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="df7de-168">REST API bir varlık oluşturma, posta gönderme gerektirir hello tooMedia Hizmetleri isteyin ve hello istek gövdesinde Varlığınızı ilgili herhangi bir özellik bilgi yerleştirme.</span><span class="sxs-lookup"><span data-stu-id="df7de-168">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="df7de-169">örnekte gösterildiği nasıl aşağıdaki hello toocreate bir varlık.</span><span class="sxs-lookup"><span data-stu-id="df7de-169">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="df7de-170">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-170">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="df7de-171">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-171">**HTTP Response**</span></span>

<span data-ttu-id="df7de-172">Başarılı olursa, hello aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="df7de-172">If successful, hello following is returned:</span></span>

    HTTP/1.1 201 Created
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
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="df7de-173">Bir AssetFile oluşturma</span><span class="sxs-lookup"><span data-stu-id="df7de-173">Create an AssetFile</span></span>
<span data-ttu-id="df7de-174">Merhaba [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) varlığı temsil eden bir blob kapsayıcısında depolanır ses veya video dosyası.</span><span class="sxs-lookup"><span data-stu-id="df7de-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="df7de-175">Bir varlık dosyası her zaman bir varlıkla ilişkilidir ve bir varlığı bir veya daha çok AssetFiles içerebilir.</span><span class="sxs-lookup"><span data-stu-id="df7de-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="df7de-176">bir varlık dosyası nesne bir blob kapsayıcısında dijital bir dosyayla ilişkili değilse hello Media Services Kodlayıcısı görev başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="df7de-176">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="df7de-177">Bir blob kapsayıcıya bir dijital medyayı dosyanızı karşıya sonra hello kullanın **birleştirme** medya dosyanızın (Merhaba konunun ilerleyen bölümlerinde gösterildiği gibi) hakkında bilgi içeren HTTP isteği tooupdate hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="df7de-177">After you upload your digital media file into a blob container, you use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span>

<span data-ttu-id="df7de-178">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-178">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="df7de-179">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-179">**HTTP Response**</span></span>

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


### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="df7de-180">Yazma izni olan Hello AccessPolicy oluşturma</span><span class="sxs-lookup"><span data-stu-id="df7de-180">Creating hello AccessPolicy with write permission</span></span>
<span data-ttu-id="df7de-181">Blob depolama alanına herhangi bir dosya karşıya yüklemeden önce hello erişim ilkesi hakları tooan varlık yazmak için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="df7de-181">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="df7de-182">bir HTTP isteği toohello AccessPolicies varlık sonrası toodo ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="df7de-182">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="df7de-183">Oluşturulduktan sonra bir dakika Cinsiden Süre değer tanımlama veya yanıt olarak bir 500 İç sunucu hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="df7de-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="df7de-184">AccessPolicies hakkında daha fazla bilgi için bkz: [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="df7de-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="df7de-185">örnekte gösterildiği nasıl aşağıdaki hello toocreate bir AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="df7de-185">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="df7de-186">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-186">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="df7de-187">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-187">**HTTP Response**</span></span>

<span data-ttu-id="df7de-188">Başarılı olursa, yanıt aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="df7de-188">If successful, hello following response is returned:</span></span>

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
    X-Powered-By: ASP.NET
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

### <a name="get-hello-upload-url"></a><span data-ttu-id="df7de-189">Merhaba karşıya yükleme URL'si Al</span><span class="sxs-lookup"><span data-stu-id="df7de-189">Get hello Upload URL</span></span>

<span data-ttu-id="df7de-190">tooreceive gerçek karşıya yükleme URL'si Merhaba, SAS Bulucu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="df7de-190">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="df7de-191">Bulucular bir varlık tooaccess dosyalarında istediğiniz istemciler için hello başlangıç saati ve bağlantı uç noktasının türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="df7de-191">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="df7de-192">İstekleri ve gereksinimlerini verilen AccessPolicy ve varlık çifti toohandle farklı bir istemci için birden çok Bulucu varlık oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df7de-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="df7de-193">Her bu Bulucuyu hello StartTime değerinin yanı sıra hello AccessPolicy toodetermine hello süreyi bir URL kullanılabilir hello Dakika Cinsiden Süre değerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="df7de-193">Each of these Locators uses hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="df7de-194">Daha fazla bilgi için bkz: [Bulucu](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="df7de-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="df7de-195">Bir SAS URL'si biçimi aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="df7de-195">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="df7de-196">Bazı dikkate alınması gereken noktalar vardır:</span><span class="sxs-lookup"><span data-stu-id="df7de-196">Some considerations apply:</span></span>

* <span data-ttu-id="df7de-197">Aynı anda belirli bir varlıkla ilişkilendirilen beşten fazla benzersiz Bulucular sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="df7de-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="df7de-198">Daha fazla bilgi için Bulucu bakın.</span><span class="sxs-lookup"><span data-stu-id="df7de-198">For more information, see Locator.</span></span>
* <span data-ttu-id="df7de-199">Dosyalarınızı hemen tooupload gerekiyorsa, StartTime değeri toofive dakika hello geçerli saati önce ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-199">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="df7de-200">Bu; çünkü istemci makine ve Media Services arasında eğme saat olabilir.</span><span class="sxs-lookup"><span data-stu-id="df7de-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="df7de-201">Ayrıca, StartTime değeriniz tarih saat biçiminde aşağıdaki hello olmalıdır: YYYY-MM-: ssZ (örneğin, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="df7de-201">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="df7de-202">30-40 saniyenin olabilir bir Bulucu kullanılabilir olmasından toowhen oluşturulduktan sonra gecikme.</span><span class="sxs-lookup"><span data-stu-id="df7de-202">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="df7de-203">Bu sorun tooboth SAS URL'si ve Kaynak Konum Belirleyicisi geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="df7de-203">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="df7de-204">SAS hakkında daha fazla bilgi için bkz: bulucular [bu](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu.</span><span class="sxs-lookup"><span data-stu-id="df7de-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="df7de-205">Aşağıdaki örneğine hello nasıl toocreate bir SAS URL'si tarafından tanımlanan Bulucu, hello hello istek gövdesindeki (bir SAS Bulucu için "1") ve bir isteğe bağlı kaynak Bulucu için "2" Type özelliği gösterir.</span><span class="sxs-lookup"><span data-stu-id="df7de-205">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="df7de-206">Merhaba **yolu** döndürülen özelliği içeren hello URL dosyanızı tooupload kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-206">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="df7de-207">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-207">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="df7de-208">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-208">**HTTP Response**</span></span>

<span data-ttu-id="df7de-209">Başarılı olursa, yanıt aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="df7de-209">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="df7de-210">Bir blob depolama kapsayıcısının içine bir dosyayı karşıya yüklemek</span><span class="sxs-lookup"><span data-stu-id="df7de-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="df7de-211">Merhaba AccessPolicy ve Bulucu kümesi oluşturduktan sonra hello gerçek hello Azure Storage REST API'leri kullanılarak karşıya yüklenen tooan Azure blob depolama kapsayıcısını dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="df7de-211">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure blob storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="df7de-212">Blok blobları hello dosyalarını yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-212">You must upload hello files as block blobs.</span></span> <span data-ttu-id="df7de-213">Sayfa bloblarını Azure Media Services tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="df7de-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="df7de-214">Merhaba dosya adı eklemelisiniz hello dosya için tooupload toohello Bulucu istediğiniz **yolu** hello önceki bölümde alınan değer.</span><span class="sxs-lookup"><span data-stu-id="df7de-214">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="df7de-215">Örneğin, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="df7de-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="df7de-216">.</span><span class="sxs-lookup"><span data-stu-id="df7de-216">.</span></span> <span data-ttu-id="df7de-217">.</span><span class="sxs-lookup"><span data-stu-id="df7de-217">.</span></span> <span data-ttu-id="df7de-218">.</span><span class="sxs-lookup"><span data-stu-id="df7de-218">.</span></span>
>
>

<span data-ttu-id="df7de-219">Azure depolama BLOB'ları ile çalışma hakkında daha fazla bilgi için bkz: [Blob hizmeti REST API'si](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="df7de-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="df7de-220">Merhaba AssetFile güncelleştir</span><span class="sxs-lookup"><span data-stu-id="df7de-220">Update hello AssetFile</span></span>
<span data-ttu-id="df7de-221">Dosyanızı yüklediğiniz, hello FileAsset boyut (ve diğer) bilgi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="df7de-221">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="df7de-222">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="df7de-222">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="df7de-223">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-223">**HTTP Response**</span></span>

<span data-ttu-id="df7de-224">Başarılı olursa, hello aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="df7de-224">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="df7de-225">Merhaba Bulucu ve AccessPolicy Sil</span><span class="sxs-lookup"><span data-stu-id="df7de-225">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="df7de-226">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="df7de-227">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-227">**HTTP Response**</span></span>

<span data-ttu-id="df7de-228">Başarılı olursa, hello aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="df7de-228">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="df7de-229">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="df7de-230">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-230">**HTTP Response**</span></span>

<span data-ttu-id="df7de-231">Başarılı olursa, hello aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="df7de-231">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="df7de-232"><a id="encode"></a>Merhaba kaynak dosya bit hızı Uyarlamalı MP4 dosyaları kümesine kodlayın</span><span class="sxs-lookup"><span data-stu-id="df7de-232"><a id="encode"></a>Encode hello source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="df7de-233">Önce varlıklar Media Services, medya içine olarak kodlanmış alma, filigran, biçimini ve benzeri, sonra tooclients teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="df7de-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="df7de-234">Bu etkinlikler zamanlanmış ve birden fazla arka plan rol örnekleri tooensure yüksek performans ve kullanılabilirlik karşı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="df7de-234">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="df7de-235">Bu etkinliklere işler adı verilir ve her bir iş hello varlık dosyası üzerinde asıl işi hello atomik görevlerin oluşur (daha fazla bilgi için bkz: [iş](/rest/api/media/services/job), [görev](/rest/api/media/services/task) açıklamaları).</span><span class="sxs-lookup"><span data-stu-id="df7de-235">These activities are called Jobs and each Job is composed of atomic Tasks that do hello actual work on hello Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="df7de-236">Ne zaman daha önce belirtildiği gibi Azure Media Services bir hello en yaygın senaryolar ile çalışma bit hızı Uyarlamalı tooyour istemcileri akış iletmektir.</span><span class="sxs-lookup"><span data-stu-id="df7de-236">As was mentioned earlier, when working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="df7de-237">Media Services dinamik olarak paketini bit hızı Uyarlamalı MP4 dosyaları kümesini biçimleri aşağıdaki hello birine: HTTP canlı akışı (HLS), kesintisiz akış, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="df7de-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="df7de-238">bölümden hello nasıl toocreate bir kodlama içeren bir işi görev gösterir.</span><span class="sxs-lookup"><span data-stu-id="df7de-238">hello following section shows how toocreate a job that contains one encoding task.</span></span> <span data-ttu-id="df7de-239">Merhaba görev tootranscode hello Ara dosyayı Uyarlamalı bit hızlı MP4s kullanarak bir kümesini **Medya Kodlayıcısı standart**.</span><span class="sxs-lookup"><span data-stu-id="df7de-239">hello task specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="df7de-240">Merhaba bölümü de nasıl toomonitor hello işleme ilerleyişini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="df7de-240">hello section also shows how toomonitor hello job processing progress.</span></span> <span data-ttu-id="df7de-241">Merhaba iş tamamlandıktan sonra gerekli tooget erişim tooyour varlıklar mümkün toocreate bulucular olacaktır.</span><span class="sxs-lookup"><span data-stu-id="df7de-241">When hello job is complete, you would be able toocreate locators that are needed tooget access tooyour assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="df7de-242">Medya işlemcisi Al</span><span class="sxs-lookup"><span data-stu-id="df7de-242">Get a media processor</span></span>
<span data-ttu-id="df7de-243">Media Services'de medya işlemcisi kodlama, biçimini dönüştürme, şifreleme veya şifresi çözme medya içeriği gibi ek olarak, belirli işleme görevi işleyen bir bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="df7de-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="df7de-244">Bu öğreticide gösterilen görev kodlama hello, biz toouse hello Medya Kodlayıcısı standart adımıdır.</span><span class="sxs-lookup"><span data-stu-id="df7de-244">For hello encoding task shown in this tutorial, we are going toouse hello Media Encoder Standard.</span></span>

<span data-ttu-id="df7de-245">Aşağıdaki kod istekleri hello Kodlayıcı'nın kimliği hello.</span><span class="sxs-lookup"><span data-stu-id="df7de-245">hello following code requests hello encoder's id.</span></span>

<span data-ttu-id="df7de-246">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="df7de-247">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-247">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="df7de-248">Bir iş oluşturma</span><span class="sxs-lookup"><span data-stu-id="df7de-248">Create a job</span></span>
<span data-ttu-id="df7de-249">Her iş sahip olabilir veya tooaccomplish, işleme hello türüne bağlı olarak daha fazla görev istiyor.</span><span class="sxs-lookup"><span data-stu-id="df7de-249">Each Job can have one or more Tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="df7de-250">Merhaba REST API, işler ve bunların ilgili görevleri aşağıdaki iki yöntemden biriyle oluşturabilirsiniz: görevler, satır içi olarak tanımlanan OData toplu işlemin veya iş varlıkları hello görevleri gezinti özelliği üzerinden olabilir.</span><span class="sxs-lookup"><span data-stu-id="df7de-250">Through hello REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through hello Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="df7de-251">Merhaba Media Services SDK'sı toplu işleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="df7de-251">hello Media Services SDK uses batch processing.</span></span> <span data-ttu-id="df7de-252">Ancak, bu konudaki hello kod örnekleri hello okunabilir olması için satır içi olarak tanımlanan görevlerdir.</span><span class="sxs-lookup"><span data-stu-id="df7de-252">However, for hello readability of hello code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="df7de-253">Toplu işleme hakkında daha fazla bilgi için bkz: [açık veri Protokolü (OData) toplu işleme](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="df7de-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="df7de-254">Aşağıdaki örneğine hello nasıl toocreate ve sonrası bir görev bir işle tooencode bir video belirli çözümleme ve kalite ayarlama gösterir.</span><span class="sxs-lookup"><span data-stu-id="df7de-254">hello following example shows you how toocreate and post a Job with one Task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="df7de-255">bir belge bölümü aşağıdaki hello tüm hello hello listesini içeren [görev hazır](http://msdn.microsoft.com/library/mt269960) hello Medya Kodlayıcısı standart işlemcisi tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="df7de-255">hello following documentation section contains hello list of all hello [task presets](http://msdn.microsoft.com/library/mt269960) supported by hello Media Encoder Standard processor.</span></span>  

<span data-ttu-id="df7de-256">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-256">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="df7de-257">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-257">**HTTP Response**</span></span>

<span data-ttu-id="df7de-258">Başarılı olursa, yanıt aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="df7de-258">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="df7de-259">Tüm iş isteği birkaç önemli nokta toonote vardır:</span><span class="sxs-lookup"><span data-stu-id="df7de-259">There are a few important things toonote in any Job request:</span></span>

* <span data-ttu-id="df7de-260">TaskBody özellikleri değişmez değer XML toodefine hello sayısı giriş ya da görev hello tarafından kullanılan çıkış varlıklar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-260">TaskBody properties MUST use literal XML toodefine hello number of input, or output assets that are used by hello Task.</span></span> <span data-ttu-id="df7de-261">Merhaba görev konu hello XML Merhaba XML şema tanımı içerir.</span><span class="sxs-lookup"><span data-stu-id="df7de-261">hello Task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="df7de-262">Her iç Hello TaskBody tanımı, değer <inputAsset> ve <outputAsset> JobInputAsset(value) veya JobOutputAsset(value) ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-262">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="df7de-263">Bir görev, birden fazla çıkış varlığına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="df7de-263">A task can have multiple output assets.</span></span> <span data-ttu-id="df7de-264">Bir JobOutputAsset(x) yalnızca bir kez bir görevin bir İşte bir çıkış olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="df7de-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="df7de-265">Bir görev bir giriş varlık JobInputAsset veya JobOutputAsset belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df7de-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="df7de-266">Görevler bir döngü oluşturmuyor gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="df7de-267">tooJobInputAsset veya JobOutputAsset geçirmek hello değer parametresi için bir varlık hello dizin değeri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="df7de-267">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an Asset.</span></span> <span data-ttu-id="df7de-268">Merhaba gerçek bir varlıklar hello iş varlık tanımı hello InputMediaAssets ve OutputMediaAssets Gezinti özellikleri tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="df7de-268">hello actual Assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="df7de-269">Media Services üzerinde OData v3 oluşturulduğundan, tek tek varlıkları InputMediaAssets hello ve OutputMediaAssets gezinti özelliği koleksiyonlar aracılığıyla başvurulan bir "__metadata: URI" ad-değer çifti.</span><span class="sxs-lookup"><span data-stu-id="df7de-269">Because Media Services is built on OData v3, hello individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="df7de-270">InputMediaAssets tooone ya da daha fazla varlıklar Media Services ile oluşturduğunuz eşler.</span><span class="sxs-lookup"><span data-stu-id="df7de-270">InputMediaAssets maps tooone or more Assets you have created in Media Services.</span></span> <span data-ttu-id="df7de-271">OutputMediaAssets hello sistem tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="df7de-271">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="df7de-272">Var olan bir varlık başvuru değil.</span><span class="sxs-lookup"><span data-stu-id="df7de-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="df7de-273">OutputMediaAssets hello assetName özniteliği kullanılarak adlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="df7de-273">OutputMediaAssets can be named using hello assetName attribute.</span></span> <span data-ttu-id="df7de-274">Bu öznitelik yok sonra hello hello OutputMediaAsset adıdır hello ne olursa olsun hello iç metin değeri <outputAsset> öğesidir hello iş adı değeri veya hello iş kimliği değeri (durumda hello Name özelliği tanımlanmadı burada hello) soneki.</span><span class="sxs-lookup"><span data-stu-id="df7de-274">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="df7de-275">AssetName için bir değer ayarlarsanız, örneğin, çok "Örnek" sonra hello OutputMediaAsset özelliğinin ayarlanması adı çok "Sample".</span><span class="sxs-lookup"><span data-stu-id="df7de-275">For example, if you set a value for assetName too"Sample", then hello OutputMediaAsset Name property would be set too"Sample".</span></span> <span data-ttu-id="df7de-276">AssetName için bir değer ayarlı değil, ancak hello iş adı ayarlama ancak, çok "NewJob" sonra hello OutputMediaAsset adı "JobOutputAsset (değer) _NewJob" olacaktır.</span><span class="sxs-lookup"><span data-stu-id="df7de-276">However, if you did not set a value for assetName, but did set hello job name too"NewJob", then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="df7de-277">Aşağıdaki örnek hello nasıl tooset hello assetName özniteliği gösterir:</span><span class="sxs-lookup"><span data-stu-id="df7de-277">hello following example shows how tooset hello assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="df7de-278">tooenable görev zincirleme:</span><span class="sxs-lookup"><span data-stu-id="df7de-278">tooenable task chaining:</span></span>

  * <span data-ttu-id="df7de-279">Bir işi en az iki görev olmalıdır</span><span class="sxs-lookup"><span data-stu-id="df7de-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="df7de-280">Merhaba işteki başka bir görev çıktısını girişi olan en az bir görev olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-280">There must be at least one task whose input is output of another task in hello job.</span></span>

<span data-ttu-id="df7de-281">Daha fazla bilgi için [hello Media Services REST API ile bir kodlama işi oluşturma](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="df7de-281">For more information see, [Creating an Encoding Job with hello Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="df7de-282">Devam eden işlem İzleyicisi</span><span class="sxs-lookup"><span data-stu-id="df7de-282">Monitor Processing Progress</span></span>
<span data-ttu-id="df7de-283">Hello aşağıdaki örnekte gösterildiği gibi hello durum özelliğini kullanarak hello iş durumu alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df7de-283">You can retrieve hello Job status by using hello State property, as shown in hello following example.</span></span>

<span data-ttu-id="df7de-284">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="df7de-285">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-285">**HTTP Response**</span></span>

<span data-ttu-id="df7de-286">Başarılı olursa, yanıt aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="df7de-286">If successful, hello following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="df7de-287">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="df7de-287">Cancel a job</span></span>
<span data-ttu-id="df7de-288">Media Services CancelJob işlevi hello çalışan iş toocancel sağlar.</span><span class="sxs-lookup"><span data-stu-id="df7de-288">Media Services allows you toocancel running jobs through hello CancelJob function.</span></span> <span data-ttu-id="df7de-289">Bu çağrı denerseniz toocancel bir iş durumu iptal edildiğinde, iptal etme, hata 400 hata kodunu döndürür veya tamamlanmış.</span><span class="sxs-lookup"><span data-stu-id="df7de-289">This call returns a 400 error code if you try toocancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="df7de-290">örnekte gösterildiği nasıl aşağıdaki hello toocall CancelJob.</span><span class="sxs-lookup"><span data-stu-id="df7de-290">hello following example shows how toocall CancelJob.</span></span>

<span data-ttu-id="df7de-291">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="df7de-292">Başarılı olursa, 204 yanıt kodu ile ileti gövdesi yok döndürülür.</span><span class="sxs-lookup"><span data-stu-id="df7de-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="df7de-293">URL kodlama hello iş kimliği gerekir (normalde nb:jid:UUID: somevalue) içinde bir parametre tooCancelJob geçirilirken.</span><span class="sxs-lookup"><span data-stu-id="df7de-293">You must URL-encode hello job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter tooCancelJob.</span></span>
>
>

### <a name="get-hello-output-asset"></a><span data-ttu-id="df7de-294">Merhaba çıkış varlığı edinme</span><span class="sxs-lookup"><span data-stu-id="df7de-294">Get hello output asset</span></span>
<span data-ttu-id="df7de-295">Merhaba aşağıdaki kod toorequest hello varlık kimliği nasıl çıktısını gösterir</span><span class="sxs-lookup"><span data-stu-id="df7de-295">hello following code shows how toorequest hello output asset Id.</span></span>

<span data-ttu-id="df7de-296">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="df7de-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="df7de-297">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="df7de-297">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <span data-ttu-id="df7de-298"><a id="publish_get_urls"></a>Merhaba varlığı yayımlayın ve get akış ve aşamalı indirme URL'lerini REST API'si</span><span class="sxs-lookup"><span data-stu-id="df7de-298"><a id="publish_get_urls"></a>Publish hello asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="df7de-299">toostream veya indirme bir varlık, ilk çok "bir Bulucu oluşturarak yayımlamadan".</span><span class="sxs-lookup"><span data-stu-id="df7de-299">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="df7de-300">Bulucular hello varlıkta bulunan erişim toofiles sağlar.</span><span class="sxs-lookup"><span data-stu-id="df7de-300">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="df7de-301">Media Services iki tür Bulucuyu destekler: OnDemandOrigin bulucuları, kullanılan toostream medya (örneğin, MPEG DASH, HLS veya kesintisiz akış) ve erişim imzası (SAS) bulucular kullanılan toodownload medya dosyaları.</span><span class="sxs-lookup"><span data-stu-id="df7de-301">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files.</span></span> <span data-ttu-id="df7de-302">SAS hakkında daha fazla bilgi için bkz: bulucular [bu](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogu.</span><span class="sxs-lookup"><span data-stu-id="df7de-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="df7de-303">Merhaba bulucuları oluşturduktan sonra kullanılan toostream veya dosyalarınızı karşıdan hello URL'leri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df7de-303">Once you create hello locators, you can build hello URLs that are used toostream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="df7de-304">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="df7de-304">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="df7de-305">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="df7de-305">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="df7de-306">Bir akış URL'si kesintisiz akış biçimini izleyen hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="df7de-306">A streaming URL for Smooth Streaming has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="df7de-307">HLS akış URL'sini biçimini izleyen hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="df7de-307">A streaming URL for HLS has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="df7de-308">MPEG DASH bir akış URL'si biçimi aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="df7de-308">A streaming URL for MPEG DASH has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="df7de-309">Bir SAS kullanılan URL toodownload dosyaları biçimini izleyen hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="df7de-309">A SAS URL used toodownload files has hello following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="df7de-310">Bu bölümde, nasıl tooperform hello aşağıdaki gerekli çok "varlıklarınızı yayımlamak" görevler gösterir.</span><span class="sxs-lookup"><span data-stu-id="df7de-310">This section shows how tooperform hello following tasks necessary too"publish" your assets.</span></span>  

* <span data-ttu-id="df7de-311">Okuma izni olan Hello AccessPolicy oluşturma</span><span class="sxs-lookup"><span data-stu-id="df7de-311">Creating hello AccessPolicy with read permission</span></span>
* <span data-ttu-id="df7de-312">İçerik indirme için bir SAS URL'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="df7de-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="df7de-313">İçerik akışı için bir kaynak URL'sini oluşturma</span><span class="sxs-lookup"><span data-stu-id="df7de-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-hello-accesspolicy-with-read-permission"></a><span data-ttu-id="df7de-314">Okuma izni olan Hello AccessPolicy oluşturma</span><span class="sxs-lookup"><span data-stu-id="df7de-314">Creating hello AccessPolicy with read permission</span></span>
<span data-ttu-id="df7de-315">İndirme veya hiçbir medya içeriği akış önce ilk olarak okuma izinlerine sahip bir AccessPolicy tanımlamak ve hello türünü belirten hello uygun Bulucu varlık oluşturma teslim mekanizması istemcileriniz için tooenable istiyor.</span><span class="sxs-lookup"><span data-stu-id="df7de-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create hello appropriate Locator entity that specifies hello type of delivery mechanism you want tooenable for your clients.</span></span> <span data-ttu-id="df7de-316">Kullanılabilir hello özellikleri hakkında daha fazla bilgi için bkz: [AccessPolicy varlık özellikleri](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="df7de-316">For more information on hello properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="df7de-317">Aşağıdaki örnek hello nasıl toospecify hello AccessPolicy belirli bir varlık için Okuma izinleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="df7de-317">hello following example shows how toospecify hello AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="df7de-318">Başarılı olursa, oluşturduğunuz hello AccessPolicy varlık açıklayan 201 başarı kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="df7de-318">If successful, a 201 success code is returned describing hello AccessPolicy entity that you created.</span></span> <span data-ttu-id="df7de-319">Ardından hello AccessPolicy kimliği hello (örneğin, bir çıkış varlığı) toodeliver toocreate hello Bulucu varlık istediğiniz hello dosyasını içeren hello varlık varlık kimliği ile birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df7de-319">You then use hello AccessPolicy Id along with hello Asset Id of hello asset that contains hello file you want toodeliver(such as an output asset) toocreate hello Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="df7de-320">Bu temel iş akışı olan hello (Bu konuda daha önce açıklanan) bir varlık alma, bir dosyayı karşıya yüklemeyi aynıdır.</span><span class="sxs-lookup"><span data-stu-id="df7de-320">This basic workflow is hello same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="df7de-321">Ayrıca, sizin (veya istemcileriniz) tooaccess ihtiyacınız varsa dosyaları, dosyalarınızı hemen yükleme gibi, StartTime değeri toofive dakika önce hello geçerli saati ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="df7de-321">Also, like uploading files, if you (or your clients) need tooaccess your files immediately, set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="df7de-322">Bu eylem gereklidir çünkü hello istemci ve Media Services arasında eğme saat olabilir.</span><span class="sxs-lookup"><span data-stu-id="df7de-322">This action is necessary because there may be clock skew between hello client and Media Services.</span></span> <span data-ttu-id="df7de-323">Merhaba StartTime değeri, DateTime biçimi aşağıdaki hello olmalıdır: YYYY-MM-: ssZ (örneğin, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="df7de-323">hello StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="df7de-324">İçerik indirme için bir SAS URL'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="df7de-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="df7de-325">koddan hello nasıl tooget kullanılan toodownload bir medya dosyasını olabilir bir URL oluşturulduğunu ve daha önce karşıya gösterir.</span><span class="sxs-lookup"><span data-stu-id="df7de-325">hello following code shows how tooget a URL that can be used toodownload a media file created and uploaded previously.</span></span> <span data-ttu-id="df7de-326">Merhaba AccessPolicy izinler kümesi okuma ve tooa SAS indirme URL'si hello Bulucu yol gösteriyor.</span><span class="sxs-lookup"><span data-stu-id="df7de-326">hello AccessPolicy has read permissions set and hello Locator path refers tooa SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="df7de-327">Başarılı olursa, yanıt aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="df7de-327">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="df7de-328">döndürülen hello **yolu** özelliği hello SAS URL içerir.</span><span class="sxs-lookup"><span data-stu-id="df7de-328">hello returned **Path** property contains hello SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="df7de-329">Şifrelenmiş depolama içeriği yüklerseniz, el ile işlemeden önce şifresini veya gerekir depolama şifre çözme MediaProcessor işleme görev toooutput içinde hello Temizle tooan OutputAsset dosyalarında işlenir ve bu varlığından karşıdan hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="df7de-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use hello Storage Decryption MediaProcessor in a processing task toooutput processed files in hello clear tooan OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="df7de-330">İşlem hakkında daha fazla bilgi için bkz: hello Media Services REST API ile bir kodlama işi oluşturma.</span><span class="sxs-lookup"><span data-stu-id="df7de-330">For more information on processing, see Creating an Encoding Job with hello Media Services REST API.</span></span> <span data-ttu-id="df7de-331">Ayrıca, oluşturulduktan sonra SAS URL Bulucular güncelleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="df7de-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="df7de-332">Örneğin, yeniden kullanamazsınız güncelleştirilmiş StartTime değerle aynı Bulucu hello.</span><span class="sxs-lookup"><span data-stu-id="df7de-332">For example, you cannot reuse hello same Locator with an updated StartTime value.</span></span> <span data-ttu-id="df7de-333">Bu SAS URL'leri oluşturulur hello nedeniyle yoludur.</span><span class="sxs-lookup"><span data-stu-id="df7de-333">This is because of hello way SAS URLs are created.</span></span> <span data-ttu-id="df7de-334">Bir Bulucu süresi dolduktan sonra karşıdan tooaccess bir varlık istiyorsanız, yeni bir StartTime ile yeni bir tane oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-334">If you want tooaccess an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="df7de-335">Dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="df7de-335">Download files</span></span>
<span data-ttu-id="df7de-336">Merhaba AccessPolicy ve Bulucu kümesi oluşturduktan sonra hello Azure Storage REST API'leri kullanarak dosyaları indirebilir.</span><span class="sxs-lookup"><span data-stu-id="df7de-336">Once you have hello AccessPolicy and Locator set, you can download files using hello Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="df7de-337">Merhaba dosya adı eklemelisiniz hello dosya için toodownload toohello Bulucu istediğiniz **yolu** hello önceki bölümde alınan değer.</span><span class="sxs-lookup"><span data-stu-id="df7de-337">You must add hello file name for hello file you want toodownload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="df7de-338">Örneğin, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="df7de-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="df7de-339">.</span><span class="sxs-lookup"><span data-stu-id="df7de-339">.</span></span> <span data-ttu-id="df7de-340">.</span><span class="sxs-lookup"><span data-stu-id="df7de-340">.</span></span> <span data-ttu-id="df7de-341">.</span><span class="sxs-lookup"><span data-stu-id="df7de-341">.</span></span>
>
>

<span data-ttu-id="df7de-342">Azure depolama BLOB'ları ile çalışma hakkında daha fazla bilgi için bkz: [Blob hizmeti REST API'si](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="df7de-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="df7de-343">Daha önce gerçekleştirdiğiniz iş kodlama hello (Uyarlamalı MP4 kümesine kodlama) sonucunda aşamalı olarak indirebilirsiniz birden çok MP4 dosyaları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="df7de-343">As a result of hello encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="df7de-344">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="df7de-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="df7de-345">İçerik akışı için bir akış URL'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="df7de-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="df7de-346">kodun gösterdiği nasıl aşağıdaki hello toocreate akış URL'si Bulucusu:</span><span class="sxs-lookup"><span data-stu-id="df7de-346">hello following code shows how toocreate a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="df7de-347">Başarılı olursa, yanıt aşağıdaki hello verilir:</span><span class="sxs-lookup"><span data-stu-id="df7de-347">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="df7de-348">toostream bir akış medya oynatıcı kesintisiz akış kaynak URL, kesintisiz akış bildirim dosyası, ardından "/ bildirimi" Merhaba hello adıyla hello Path özelliği eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="df7de-348">toostream a Smooth Streaming origin URL in a streaming media player, you must append hello Path property with hello name of hello Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="df7de-349">toostream HLS, ekleme (format = m3u8-aapl) hello sonra "/ bildirimi".</span><span class="sxs-lookup"><span data-stu-id="df7de-349">toostream HLS, append (format=m3u8-aapl) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="df7de-350">toostream MPEG DASH ekleme (biçim mpd zaman csf =) hello sonra "/ bildirimi".</span><span class="sxs-lookup"><span data-stu-id="df7de-350">toostream MPEG DASH, append (format=mpd-time-csf) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="df7de-351"><a id="play"></a>İçeriğinizi oynatma</span><span class="sxs-lookup"><span data-stu-id="df7de-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="df7de-352">toostream video, kullandığınız [Azure Media Services Oynatıcısı](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="df7de-352">toostream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="df7de-353">tootest aşamalı indirmek için bir URL (örneğin, IE, Chrome, Safari) bir tarayıcıya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="df7de-353">tootest progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="df7de-354">Sonraki Adımlar: Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="df7de-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="df7de-355">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="df7de-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
