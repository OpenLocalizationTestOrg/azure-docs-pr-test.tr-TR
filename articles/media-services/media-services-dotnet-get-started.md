---
title: "aaaGet başlatılan .NET kullanarak isteğe bağlı içerik göndermeye | Microsoft Docs"
description: "Bu öğreticide hello .NET kullanarak Azure Media Services ile bir üzerinde isteğe bağlı içerik teslim uygulaması gerçekleştirilmesinin adımları açıklanmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 388b8928-9aa9-46b1-b60a-a918da75bd7b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 4ca9394bd581e1d9062e5a008a410b2c058e017e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="3b735-103">.NET SDK kullanarak isteğe bağlı içerik göndermeye başlama</span><span class="sxs-lookup"><span data-stu-id="3b735-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="3b735-104">Bu öğreticide, hello Azure Media Services .NET SDK kullanarak Azure Media Services (AMS) uygulaması ile temel bir isteğe bağlı video (VoD) içerik teslim hizmeti uygulamanın hello adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3b735-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b735-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3b735-105">Prerequisites</span></span>

<span data-ttu-id="3b735-106">Merhaba, gerekli toocomplete hello öğretici şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3b735-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="3b735-107">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="3b735-107">An Azure account.</span></span> <span data-ttu-id="3b735-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3b735-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3b735-109">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="3b735-109">A Media Services account.</span></span> <span data-ttu-id="3b735-110">bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="3b735-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="3b735-111">.NET framework 4.0 veya sonraki sürümü.</span><span class="sxs-lookup"><span data-stu-id="3b735-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="3b735-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3b735-112">Visual Studio.</span></span>

<span data-ttu-id="3b735-113">Bu öğretici hello aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="3b735-113">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="3b735-114">Akış uç noktası (hello Azure portal kullanarak) başlatın.</span><span class="sxs-lookup"><span data-stu-id="3b735-114">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="3b735-115">Visual Studio projesi oluşturun ve yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3b735-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="3b735-116">Toohello Media Services hesabına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="3b735-116">Connect toohello Media Services account.</span></span>
2. <span data-ttu-id="3b735-117">Bir video dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3b735-117">Upload a video file.</span></span>
3. <span data-ttu-id="3b735-118">Merhaba kaynak dosya bit hızı Uyarlamalı MP4 dosyaları kümesine kodlayın.</span><span class="sxs-lookup"><span data-stu-id="3b735-118">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="3b735-119">Merhaba varlık ve get akış ve aşamalı indirme URL'leri yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="3b735-119">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="3b735-120">İçeriğinizi oynatın.</span><span class="sxs-lookup"><span data-stu-id="3b735-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="3b735-121">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3b735-121">Overview</span></span>
<span data-ttu-id="3b735-122">Bu öğreticide hello .NET için Azure Media Services (AMS) SDK kullanarak isteğe bağlı video (VoD) içerik teslim uygulaması gerçekleştirilmesinin adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3b735-122">This tutorial walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="3b735-123">Başlangıç Öğreticisi hello temel Media Services iş akışı, hello en genel programlama nesnelerini ve Media Services geliştirmek için gereken görevleri tanıtır.</span><span class="sxs-lookup"><span data-stu-id="3b735-123">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="3b735-124">Başlangıç Öğreticisi Hello tamamlandığında mümkün toostream olması veya aşamalı olarak örnek bir medya dosyasını karşıya kodlanmış ve yüklenen indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b735-124">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="3b735-125">AMS modeli</span><span class="sxs-lookup"><span data-stu-id="3b735-125">AMS model</span></span>

<span data-ttu-id="3b735-126">Merhaba aşağıdaki görüntüde bazılarını hello en yaygın olarak kullanılan nesneler hello Media Services OData modelde VoD uygulamaları geliştirirken gösterir.</span><span class="sxs-lookup"><span data-stu-id="3b735-126">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="3b735-127">Merhaba görüntü tooview boyutu tam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3b735-127">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="3b735-128">Merhaba tüm model görüntüleyebilirsiniz [burada](https://media.windows.net/API/$metadata?api-version=2.15).</span><span class="sxs-lookup"><span data-stu-id="3b735-128">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="3b735-129">Akış uç noktaları Hello Azure portal kullanarak Başlat</span><span class="sxs-lookup"><span data-stu-id="3b735-129">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="3b735-130">Merhaba en sık karşılaşılan senaryolardan biri, video bit hızı Uyarlamalı akış iletmektir Azure Media Services ile çalışırken.</span><span class="sxs-lookup"><span data-stu-id="3b735-130">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="3b735-131">Media Services, bit hızı Uyarlamalı MP4 kodlanmış içeriğinizi Media Services (MPEG DASH, HLS, kesintisiz akış) tam zamanında tarafından önceden paketlenmiş toostore kalmadan desteklenen akış biçimlerinde toodeliver sağlayan dinamik paketleme sağlar Bu akış biçimlerine her da sürümleri.</span><span class="sxs-lookup"><span data-stu-id="3b735-131">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="3b735-132">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="3b735-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="3b735-133">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="3b735-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="3b735-134">toostart akış uç Merhaba, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3b735-134">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="3b735-135">Merhaba oturum açma [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3b735-135">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3b735-136">Hello Ayarları penceresinde, akış uç noktaları'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3b735-136">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="3b735-137">Merhaba varsayılan akış uç noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3b735-137">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="3b735-138">Merhaba varsayılan akış uç noktası AYRINTILAR penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3b735-138">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="3b735-139">Merhaba başlangıç simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3b735-139">Click hello Start icon.</span></span>
5. <span data-ttu-id="3b735-140">Merhaba Kaydet düğmesine toosave değişikliklerinizi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3b735-140">Click hello Save button toosave your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3b735-141">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3b735-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="3b735-142">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3b735-142">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="3b735-143">Yeni bir klasör oluşturun (klasör herhangi bir yerde olabilir yerel diskinize) ve tooencode ve akış istediğiniz veya aşamalı indirmek bir .mp4 dosyasını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3b735-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="3b735-144">Bu örnekte "C:\VideoFiles" yolu hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3b735-144">In this example, hello "C:\VideoFiles" path is used.</span></span>

## <a name="connect-toohello-media-services-account"></a><span data-ttu-id="3b735-145">Toohello Media Services hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="3b735-145">Connect toohello Media Services account</span></span>

<span data-ttu-id="3b735-146">Media Services .NET ile kullanırken hello kullanmalısınız **CloudMediaContext** çoğu Media Services programlama görevlerinin sınıfı: tooMedia Services hesabına bağlanma; oluşturma, güncelleştirme, erişme ve hello aşağıdaki silme nesneleri: varlıklar, varlık dosyaları, işler, erişim ilkeleri, bulucular vb..</span><span class="sxs-lookup"><span data-stu-id="3b735-146">When using Media Services with .NET, you must use hello **CloudMediaContext** class for most Media Services programming tasks: connecting tooMedia Services account; creating, updating, accessing, and deleting hello following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="3b735-147">Koddan hello ile Merhaba varsayılan Program sınıfının üzerine.</span><span class="sxs-lookup"><span data-stu-id="3b735-147">Overwrite hello default Program class with hello following code.</span></span> <span data-ttu-id="3b735-148">Merhaba kod tooread hello bağlantı hello App.config dosyasından değerleri nasıl ve ne göstermektedir toocreate hello **CloudMediaContext** sipariş tooconnect tooMedia nesnesinde Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="3b735-148">hello code demonstrates how tooread hello connection values from hello App.config file and how toocreate hello **CloudMediaContext** object in order tooconnect tooMedia Services.</span></span> <span data-ttu-id="3b735-149">Daha fazla bilgi için bkz: [toohello Media Services API bağlanma](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="3b735-149">For more information, see [connecting toohello Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="3b735-150">Sahip olduğunuz emin tooupdate hello dosya adı ve yolu toowhere medya dosyanızın olun.</span><span class="sxs-lookup"><span data-stu-id="3b735-150">Make sure tooupdate hello file name and path toowhere you have your media file.</span></span>

<span data-ttu-id="3b735-151">Merhaba **ana** işlevi açıklanacak olan yöntemleri çağırır bu bölümün sonraki kısımlarında.</span><span class="sxs-lookup"><span data-stu-id="3b735-151">hello **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="3b735-152">Tanımları tüm hello işlevler için eklenene kadar derleme hataları alma.</span><span class="sxs-lookup"><span data-stu-id="3b735-152">You will be getting compilation errors until you add definitions for all hello functions.</span></span>

    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
        try
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Add calls toomethods defined in this section.
            // Make sure tooupdate hello file name and path toowhere you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse hello XML error message in hello Media Services response and create a new
            // exception with its content.
            exception = MediaServicesExceptionParser.Parse(exception);

            Console.Error.WriteLine(exception.Message);
        }
        finally
        {
            Console.ReadLine();
        }
        }
    }

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="3b735-153">Yeni varlık oluşturma ve video dosyası yükleme</span><span class="sxs-lookup"><span data-stu-id="3b735-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="3b735-154">Media Services’de, dijital dosyalar bir varlığa yüklenir (veya alınır).</span><span class="sxs-lookup"><span data-stu-id="3b735-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="3b735-155">Merhaba **varlık** varlık içerebilir video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve hello meta verileri bu dosyalar hakkında.)  Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır.</span><span class="sxs-lookup"><span data-stu-id="3b735-155">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span> <span data-ttu-id="3b735-156">Merhaba varlık Hello dosyalarında çağrılır **varlık dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="3b735-156">hello files in hello asset are called **Asset Files**.</span></span>

<span data-ttu-id="3b735-157">Merhaba **UploadFile** çağrıları tanımlanan yöntemi **CreateFromFile** (.NET SDK uzantılarında tanımlanmıştır).</span><span class="sxs-lookup"><span data-stu-id="3b735-157">hello **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="3b735-158">**CreateFromFile** hangi hello belirtilen kaynak dosyasının yüklendiği yeni bir varlık oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3b735-158">**CreateFromFile** creates a new asset into which hello specified source file is uploaded.</span></span>

<span data-ttu-id="3b735-159">Merhaba **CreateFromFile** yöntemi alır **AssetCreationOptions** olanak sağlayan, hello aşağıdaki varlık oluşturma seçeneklerden birini belirtin:</span><span class="sxs-lookup"><span data-stu-id="3b735-159">hello **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of hello following asset creation options:</span></span>

* <span data-ttu-id="3b735-160">**Hiçbiri**: Şifreleme kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="3b735-160">**None** - No encryption is used.</span></span> <span data-ttu-id="3b735-161">Merhaba varsayılan değer budur.</span><span class="sxs-lookup"><span data-stu-id="3b735-161">This is hello default value.</span></span> <span data-ttu-id="3b735-162">Bu seçeneği kullandığınızda, içeriğinizin aktarım sırasında ve depolama alanında beklerken korunmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3b735-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="3b735-163">Aşamalı indirme kullanarak toodeliver bir MP4 planlıyorsanız, bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b735-163">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="3b735-164">**StorageEncrypted** -bu seçenek tooencrypt Temizle içeriğinizi tooAzure depolanır depolama şifrelenen yükler Gelişmiş Şifreleme Standardı (AES)-256 bit şifreleme kullanarak yerel olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b735-164">**StorageEncrypted** - Use this option tooencrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="3b735-165">Depolama şifrelemesi ile korunan varlıklar otomatik olarak şifrelenmemiş ve bir şifrelenmiş dosya sistemi önceki tooencoding ve yeni bir çıkış varlığı olarak geri isteğe bağlı olarak yeniden şifrelenmiş önceki toouploading yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3b735-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="3b735-166">Depolama şifrelemesinin birincil kullanım durumu hello yüksek kaliteli giriş medya dosyalarınızı REST güçlü şifrelemeyle diskte toosecure istediğiniz durumdur.</span><span class="sxs-lookup"><span data-stu-id="3b735-166">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="3b735-167">**CommonEncryptionProtected**: Zaten Ortak Şifreleme veya PlayReady DRM ile şifrelenip korunan bir içerik (örneğin, PlayReady DRM ile korunan Kesintisiz Akış) yüklüyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b735-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="3b735-168">**EnvelopeEncryptionProtected**: AES ile şifrelenmiş HLS yüklüyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b735-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="3b735-169">Hello dosyaları gerekir alınan kodlanmış ve Transform Manager tarafından şifrelenmiş olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3b735-169">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="3b735-170">Merhaba **CreateFromFile** yöntemi de bir geri çağırma sırası tooreport hello karşıya yükleme sürüyor hello dosyasının belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b735-170">hello **CreateFromFile** method also lets you specify a callback in order tooreport hello upload progress of hello file.</span></span>

<span data-ttu-id="3b735-171">Aşağıdaki örneğine hello belirttiğimiz **hiçbiri** hello varlık seçenekleri için.</span><span class="sxs-lookup"><span data-stu-id="3b735-171">In hello following example, we specify **None** for hello asset options.</span></span>

<span data-ttu-id="3b735-172">Yöntem toohello Program sınıfına aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3b735-172">Add hello following method toohello Program class.</span></span>

    static public IAsset UploadFile(string fileName, AssetCreationOptions options)
    {
        IAsset inputAsset = _context.Assets.CreateFromFile(
            fileName,
            options,
            (af, p) =>
            {
                Console.WriteLine("Uploading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Asset {0} created.", inputAsset.Id);

        return inputAsset;
    }


## <a name="encode-hello-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="3b735-173">Merhaba kaynak dosya bit hızı Uyarlamalı MP4 dosyaları kümesine kodlayın</span><span class="sxs-lookup"><span data-stu-id="3b735-173">Encode hello source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="3b735-174">Varlıklar Media Services'e alındıktan sonra medya olabilir kodlanmış biçimini, filigran vb. tooclients teslim edilmeden önce.</span><span class="sxs-lookup"><span data-stu-id="3b735-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="3b735-175">Bu etkinlikler zamanlanmış ve birden fazla arka plan rol örnekleri tooensure yüksek performans ve kullanılabilirlik karşı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3b735-175">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="3b735-176">Bu etkinliklere işler adı verilir ve her bir iş hello varlık dosyası üzerinde asıl işi hello atomik görevlerin oluşur.</span><span class="sxs-lookup"><span data-stu-id="3b735-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do hello actual work on hello Asset file.</span></span>

<span data-ttu-id="3b735-177">Azure Media Services ile çalışırken, daha önce belirtildiği gibi hello en sık karşılaşılan senaryolardan biri, bit hızı Uyarlamalı tooyour istemcileri akış iletmektir.</span><span class="sxs-lookup"><span data-stu-id="3b735-177">As was mentioned earlier, when working with Azure Media Services, one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="3b735-178">Media Services dinamik olarak paketini bit hızı Uyarlamalı MP4 dosyaları kümesini biçimleri aşağıdaki hello birine: HTTP canlı akışı (HLS), kesintisiz akış ve MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="3b735-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="3b735-179">tootake avantajı dinamik paketleme, tooencode veya kodlamasını Ara (kaynak) dosyanızı Uyarlamalı bit hızlı MP4 veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesine ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="3b735-179">tootake advantage of dynamic packaging, you need tooencode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="3b735-180">koddan hello nasıl toosubmit bir kodlama işi gösterir.</span><span class="sxs-lookup"><span data-stu-id="3b735-180">hello following code shows how toosubmit an encoding job.</span></span> <span data-ttu-id="3b735-181">Merhaba iş tootranscode hello Ara dosyayı Uyarlamalı bit hızlı MP4s kullanarak kümesi belirten bir görev içerir **Medya Kodlayıcısı standart**.</span><span class="sxs-lookup"><span data-stu-id="3b735-181">hello job contains one task that specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="3b735-182">tamamlanana kadar hello kod hello iş ve bekler gönderir.</span><span class="sxs-lookup"><span data-stu-id="3b735-182">hello code submits hello job and waits until it is completed.</span></span>

<span data-ttu-id="3b735-183">Merhaba işi tamamlandığında, mümkün toostream varlığınız olması veya kodlama dönüştürmenin sonucu olarak oluşturulan MP4 dosyalarını aşamalı indirmek.</span><span class="sxs-lookup"><span data-stu-id="3b735-183">Once hello job is completed, you would be able toostream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="3b735-184">Yöntem toohello Program sınıfına aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3b735-184">Add hello following method toohello Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task tootranscode hello specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit hello job and wait until it is completed.
        job.Submit();

        job = job.StartExecutionProgressTask(
            j =>
            {
                Console.WriteLine("Job state: {0}", j.State);
                Console.WriteLine("Job progress: {0:0.##}%", j.GetOverallProgress());
            },
            CancellationToken.None).Result;

        Console.WriteLine("Transcoding job finished.");

        IAsset outputAsset = job.OutputMediaAssets[0];

        return outputAsset;
    }

## <a name="publish-hello-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="3b735-185">Merhaba varlığı yayımlayın, akış ve aşamalı indirme URL'lerini alın</span><span class="sxs-lookup"><span data-stu-id="3b735-185">Publish hello asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="3b735-186">toostream veya indirme bir varlık, ilk çok "bir Bulucu oluşturarak yayımlamadan".</span><span class="sxs-lookup"><span data-stu-id="3b735-186">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="3b735-187">Bulucular hello varlıkta bulunan erişim toofiles sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b735-187">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="3b735-188">Media Services iki tür Bulucuyu destekler: OnDemandOrigin bulucuları, kullanılan toostream medya (örneğin, MPEG DASH, HLS veya kesintisiz akış) ve erişim imzası (SAS) bulucular kullanılan toodownload medya dosyaları (SAS bulucular bakın hakkındadahafazlabilgi[bu](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span><span class="sxs-lookup"><span data-stu-id="3b735-188">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="3b735-189">URL biçimleri hakkında bazı ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="3b735-189">Some details about URL formats</span></span>

<span data-ttu-id="3b735-190">Merhaba bulucuları oluşturduktan sonra kullanılan toostream olması veya dosyalarınızı karşıdan hello URL'leri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b735-190">After you create hello locators, you can build hello URLs that would be used toostream or download your files.</span></span> <span data-ttu-id="3b735-191">Bu öğreticide Hello örnek uygun tarayıcılarda yapıştırabilirsiniz URL'leri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="3b735-191">hello sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="3b735-192">Bu bölümde yalnızca farklı biçimlerin neye benzediğini gösteren kısa örnekler verilir.</span><span class="sxs-lookup"><span data-stu-id="3b735-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-hello-following-format"></a><span data-ttu-id="3b735-193">MPEG DASH bir akış URL'si biçimi aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3b735-193">A streaming URL for MPEG DASH has hello following format:</span></span>

<span data-ttu-id="3b735-194">{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="3b735-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-hello-following-format"></a><span data-ttu-id="3b735-195">HLS akış URL'sini biçimini izleyen hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3b735-195">A streaming URL for HLS has hello following format:</span></span>

<span data-ttu-id="3b735-196">{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="3b735-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-hello-following-format"></a><span data-ttu-id="3b735-197">Bir akış URL'si kesintisiz akış biçimini izleyen hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3b735-197">A streaming URL for Smooth Streaming has hello following format:</span></span>

<span data-ttu-id="3b735-198">{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="3b735-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-toodownload-files-has-hello-following-format"></a><span data-ttu-id="3b735-199">Bir SAS kullanılan URL toodownload dosyaları biçimini izleyen hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3b735-199">A SAS URL used toodownload files has hello following format:</span></span>

<span data-ttu-id="3b735-200">{blob kapsayıcısı adı}/{varlık adı}/{dosya adı}/{SAS imzası}</span><span class="sxs-lookup"><span data-stu-id="3b735-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="3b735-201">Media Services .NET SDK uzantıları, yayımlanmış varlık dönüş URL'leri Merhaba biçimlendirilmiş kullanışlı yardımcı yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b735-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for hello published asset.</span></span>

<span data-ttu-id="3b735-202">Merhaba aşağıdaki kodu kullanan .NET SDK uzantıları toocreate bulucular ve tooget akış ve aşamalı indirme URL'lerini.</span><span class="sxs-lookup"><span data-stu-id="3b735-202">hello following code uses .NET SDK Extensions toocreate locators and tooget streaming and progressive download URLs.</span></span> <span data-ttu-id="3b735-203">Merhaba kod ayrıca nasıl toodownload dosyaları tooa yerel klasörü gösterir.</span><span class="sxs-lookup"><span data-stu-id="3b735-203">hello code also shows how toodownload files tooa local folder.</span></span>

<span data-ttu-id="3b735-204">Yöntem toohello Program sınıfına aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3b735-204">Add hello following method toohello Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish hello output asset by creating an Origin locator for adaptive streaming,
        // and a SAS locator for progressive download.

        _context.Locators.Create(
            LocatorType.OnDemandOrigin,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));

        _context.Locators.Create(
            LocatorType.Sas,
            asset,
            AccessPermissions.Read,
            TimeSpan.FromDays(30));


        IEnumerable<IAssetFile> mp4AssetFiles = asset
                .AssetFiles
                .ToList()
                .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Get hello Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and hello Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get hello URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  hello streaming URLs.
        Console.WriteLine("Use hello following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display hello URLs for progressive download.
        Console.WriteLine("Use hello following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download hello output asset tooa local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files tooa local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="3b735-205">İçeriğiniz oynatarak test etme</span><span class="sxs-lookup"><span data-stu-id="3b735-205">Test by playing your content</span></span>

<span data-ttu-id="3b735-206">Merhaba önceki bölümde tanımlanan hello programı çalıştırdığınızda benzer toohello aşağıdaki hello konsol penceresinde görüntülenir URL'leri hello.</span><span class="sxs-lookup"><span data-stu-id="3b735-206">Once you run hello program defined in hello previous section, hello URLs similar toohello following will be displayed in hello console window.</span></span>

<span data-ttu-id="3b735-207">Uyarlamalı akış URL'leri:</span><span class="sxs-lookup"><span data-stu-id="3b735-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="3b735-208">Kesintisiz Akış</span><span class="sxs-lookup"><span data-stu-id="3b735-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="3b735-209">HLS</span><span class="sxs-lookup"><span data-stu-id="3b735-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="3b735-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="3b735-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="3b735-211">Aşamalı indirme URL'leri (ses ve video).</span><span class="sxs-lookup"><span data-stu-id="3b735-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="3b735-212">toostream videonuz URL'nizi hello URL'si metin kutusuna hello yapıştırın [Azure Media Services Oynatıcısı](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="3b735-212">toostream your video, paste your URL in hello URL textbox in hello [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="3b735-213">tootest aşamalı indirmek için bir URL (örneğin, Internet Explorer, Chrome veya Safari) bir tarayıcıya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="3b735-213">tootest progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="3b735-214">Daha fazla bilgi için aşağıdaki konularda hello bakın:</span><span class="sxs-lookup"><span data-stu-id="3b735-214">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="3b735-215">İçeriğinizi mevcut oynatıcılarda oynatma</span><span class="sxs-lookup"><span data-stu-id="3b735-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="3b735-216">Video oynatıcı uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="3b735-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="3b735-217">DASH.js ile bir MPEG-DASH Uyarlamalı Akış Videosunu bir HTML5 Uygulamasına ekleme</span><span class="sxs-lookup"><span data-stu-id="3b735-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="3b735-218">Örnek indirme</span><span class="sxs-lookup"><span data-stu-id="3b735-218">Download sample</span></span>
<span data-ttu-id="3b735-219">Merhaba aşağıdaki kod örneği, bu öğreticide oluşturduğunuz hello kodunu içerir: [örnek](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="3b735-219">hello following code sample contains hello code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b735-220">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3b735-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3b735-221">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="3b735-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
