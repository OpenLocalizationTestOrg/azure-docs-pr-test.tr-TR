---
title: ".NET kullanarak isteğe bağlı içerik göndermeye başlama | Microsoft Belgeleri"
description: "Bu öğreticide, .NET’i kullanarak Azure Media Services ile isteğe bağlı bir içerik teslim uygulaması gerçekleştirilmesinin adımları açıklanmaktadır."
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
ms.openlocfilehash: f0be787ba1ccee067fb1d7e6a6554be32f886089
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-net-sdk"></a><span data-ttu-id="e86f5-103">.NET SDK kullanarak isteğe bağlı içerik göndermeye başlama</span><span class="sxs-lookup"><span data-stu-id="e86f5-103">Get started with delivering content on demand using .NET SDK</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="e86f5-104">Bu öğretici, Azure Media Services .NET SDK'sı kullanarak Azure Media Services (AMS) uygulaması ile temel bir İsteğe Bağlı Video (VoD) içerik teslim hizmeti uygulamanın adımlarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="e86f5-104">This tutorial walks you through the steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using the Azure Media Services .NET SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e86f5-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e86f5-105">Prerequisites</span></span>

<span data-ttu-id="e86f5-106">Öğreticiyi tamamlamak için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="e86f5-106">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="e86f5-107">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="e86f5-107">An Azure account.</span></span> <span data-ttu-id="e86f5-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e86f5-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e86f5-109">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="e86f5-109">A Media Services account.</span></span> <span data-ttu-id="e86f5-110">Bir Media Services hesabı oluşturmak için bkz. [Media Services hesabı oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="e86f5-110">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="e86f5-111">.NET framework 4.0 veya sonraki sürümü.</span><span class="sxs-lookup"><span data-stu-id="e86f5-111">.NET Framework 4.0 or later.</span></span>
* <span data-ttu-id="e86f5-112">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e86f5-112">Visual Studio.</span></span>

<span data-ttu-id="e86f5-113">Bu öğretici aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="e86f5-113">This tutorial includes the following tasks:</span></span>

1. <span data-ttu-id="e86f5-114">Akış uç noktalarını başlatın (Azure portalını kullanarak).</span><span class="sxs-lookup"><span data-stu-id="e86f5-114">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="e86f5-115">Visual Studio projesi oluşturun ve yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-115">Create and configure a Visual Studio project.</span></span>
3. <span data-ttu-id="e86f5-116">Media Services hesabına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-116">Connect to the Media Services account.</span></span>
2. <span data-ttu-id="e86f5-117">Bir video dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e86f5-117">Upload a video file.</span></span>
3. <span data-ttu-id="e86f5-118">Kaynak dosyayı uyarlamalı bit hızlı bir MP4 dosyaları grubuna kodlayın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-118">Encode the source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="e86f5-119">Varlığı yayımlayın, akış ve aşamalı indirme URL’lerini alın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-119">Publish the asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="e86f5-120">İçeriğinizi oynatın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-120">Play your content.</span></span>

## <a name="overview"></a><span data-ttu-id="e86f5-121">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e86f5-121">Overview</span></span>
<span data-ttu-id="e86f5-122">Bu öğreticide, .NET için Azure Media Services (AMS) SDK’sını kullanarak bir İsteğe Bağlı Video (VoD) içerik teslim uygulaması gerçekleştirilmesinin adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e86f5-122">This tutorial walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) SDK for .NET.</span></span>

<span data-ttu-id="e86f5-123">Öğretici, temel Media Services iş akışını ve Media Services geliştirmek için gereken en genel programlama nesnelerini ve görevleri tanıtır.</span><span class="sxs-lookup"><span data-stu-id="e86f5-123">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="e86f5-124">Öğreticiyi tamamladığınızda, yükleyip kodlayarak ardından indirdiğiniz örnek bir medya dosyasını akışla aktarabilecek veya aşamalı olarak indirebileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e86f5-124">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

### <a name="ams-model"></a><span data-ttu-id="e86f5-125">AMS modeli</span><span class="sxs-lookup"><span data-stu-id="e86f5-125">AMS model</span></span>

<span data-ttu-id="e86f5-126">Aşağıdaki resimde Media Services OData modeliyle VoD uygulamaları geliştirirken en sık kullanılan nesnelerin bazıları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-126">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="e86f5-127">Resmi tam boyutlu görüntülemek için tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-127">Click the image to view it full size.</span></span>  

<a href="./media/media-services-dotnet-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-dotnet-get-started/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="e86f5-128">Modelin tamamını [buradan](https://media.windows.net/API/$metadata?api-version=2.15) görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e86f5-128">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="e86f5-129">Azure portal ile akış uç noktalarını başlatma</span><span class="sxs-lookup"><span data-stu-id="e86f5-129">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="e86f5-130">Azure Media Services ile çalışırken en sık karşılaşılan senaryolardan biri bit hızı uyarlamalı akış iletmektir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-130">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="e86f5-131">Media Services, bu akış biçimlerinin her birinin önceden paketlenmiş sürümlerini depolamanıza gerek kalmadan, uyarlamalı bit hızı MP4 ile kodlanmış içeriğinizi Media Services tarafından desteklenen akış biçimlerinde (MPEG DASH, HLS, Kesintisiz Akış) tam vaktinde göndermenize olanak tanıyan dinamik paketleme özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-131">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="e86f5-132">AMS hesabınız oluşturulduğunda hesabınıza **Durdurulmuş** durumda bir **varsayılan** akış uç noktası eklenir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="e86f5-133">İçerik akışını başlatmak ve dinamik paketleme ile dinamik şifrelemeden yararlanmak için içerik akışı yapmak istediğiniz akış uç noktasının **Çalışıyor** durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="e86f5-134">Akış uç noktasını başlatmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="e86f5-134">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="e86f5-135">[Azure portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-135">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e86f5-136">Ayarlar penceresinde, Akış uç noktaları'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-136">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="e86f5-137">Varsayılan akış uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-137">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="e86f5-138">VARSAYILAN AKIŞ UÇ NOKTASI AYRINTILARI penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-138">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="e86f5-139">Başlat simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-139">Click the Start icon.</span></span>
5. <span data-ttu-id="e86f5-140">Yaptığınız değişiklikleri kaydetmek için Kaydet düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-140">Click the Save button to save your changes.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e86f5-141">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e86f5-141">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="e86f5-142">Geliştirme ortamınızı kurun ve app.config dosyanızı [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md) bölümünde açıklandığı gibi bağlantı bilgileriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="e86f5-142">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="e86f5-143">Yeni bir klasör oluşturun (yerel sürücünüzün herhangi bir yerinde) ve kodlayıp akışla aktarmak veya aşamalı indirmek istediğiniz bir .mp4 dosyasını buraya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-143">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="e86f5-144">Bu örnekte "C:\VideoFiles" yolu kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e86f5-144">In this example, the "C:\VideoFiles" path is used.</span></span>

## <a name="connect-to-the-media-services-account"></a><span data-ttu-id="e86f5-145">Media Services hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="e86f5-145">Connect to the Media Services account</span></span>

<span data-ttu-id="e86f5-146">.NET ile Media Services’i kullanırken, Media Services programlama görevlerinin çoğu için **CloudMediaContext** sınıfını kullanmalısınız: Media Services hesabına bağlanma; şu nesneleri oluşturma, güncelleştirme, silme ve bunlara erişme: varlıklar, varlık dosyaları, işler, erişim ilkeleri, bulucular vb.</span><span class="sxs-lookup"><span data-stu-id="e86f5-146">When using Media Services with .NET, you must use the **CloudMediaContext** class for most Media Services programming tasks: connecting to Media Services account; creating, updating, accessing, and deleting the following objects: assets, asset files, jobs, access policies, locators, etc.</span></span>

<span data-ttu-id="e86f5-147">Varsayılan Program sınıfının üzerine aşağıdaki kodu yazın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-147">Overwrite the default Program class with the following code.</span></span> <span data-ttu-id="e86f5-148">Kod, bağlantı değerlerinin App.config dosyasından nasıl okunacağını ve Media Services’e bağlanmak amacıyla **CloudMediaContext** nesnesinin nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-148">The code demonstrates how to read the connection values from the App.config file and how to create the **CloudMediaContext** object in order to connect to Media Services.</span></span> <span data-ttu-id="e86f5-149">Daha fazla bilgi için bkz. [Media Services API'sine bağlanma](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="e86f5-149">For more information, see [connecting to the Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

<span data-ttu-id="e86f5-150">Dosya adını ve yolunu medya dosyanıza göre güncelleştirmeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-150">Make sure to update the file name and path to where you have your media file.</span></span>

<span data-ttu-id="e86f5-151">**Ana** işlev, bu bölümün sonraki kısımlarında açıklanacak olan yöntemleri çağırır.</span><span class="sxs-lookup"><span data-stu-id="e86f5-151">The **Main** function calls methods that will be defined further in this section.</span></span>

> [!NOTE]
> <span data-ttu-id="e86f5-152">Tüm işlevler için tanım ekleyene kadar derleme hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e86f5-152">You will be getting compilation errors until you add definitions for all the functions.</span></span>

    class Program
    {
        // Read values from the App.config file.
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

            // Add calls to methods defined in this section.
            // Make sure to update the file name and path to where you have your media file.
            IAsset inputAsset =
            UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.None);

            IAsset encodedAsset =
            EncodeToAdaptiveBitrateMP4s(inputAsset, AssetCreationOptions.None);

            PublishAssetGetURLs(encodedAsset);
        }
        catch (Exception exception)
        {
            // Parse the XML error message in the Media Services response and create a new
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

## <a name="create-a-new-asset-and-upload-a-video-file"></a><span data-ttu-id="e86f5-153">Yeni varlık oluşturma ve video dosyası yükleme</span><span class="sxs-lookup"><span data-stu-id="e86f5-153">Create a new asset and upload a video file</span></span>

<span data-ttu-id="e86f5-154">Media Services’de, dijital dosyalar bir varlığa yüklenir (veya alınır).</span><span class="sxs-lookup"><span data-stu-id="e86f5-154">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="e86f5-155">**Varlık** varlığı video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkındaki meta veriler) içerebilir.  Dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla aktarma faaliyetleri için güvenli bir şekilde bulutta depolanmış olur.</span><span class="sxs-lookup"><span data-stu-id="e86f5-155">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks, and closed caption files (and the metadata about these files.)  Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> <span data-ttu-id="e86f5-156">Varlık içindeki dosyalara **Varlık Dosyaları** adı verilir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-156">The files in the asset are called **Asset Files**.</span></span>

<span data-ttu-id="e86f5-157">Aşağıda tanımlanan **UploadFile** yöntemi, **CreateFromFile** yöntemini (.NET SDK Uzantılarında tanımlanmıştır) çağırır.</span><span class="sxs-lookup"><span data-stu-id="e86f5-157">The **UploadFile** method defined below calls **CreateFromFile** (defined in .NET SDK Extensions).</span></span> <span data-ttu-id="e86f5-158">**CreateFromFile**, belirtilen kaynak dosyasının yüklendiği yeni bir varlık oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e86f5-158">**CreateFromFile** creates a new asset into which the specified source file is uploaded.</span></span>

<span data-ttu-id="e86f5-159">**CreateFromFile** yöntemi, aşağıdaki varlık oluşturma seçeneklerden birini belirtmenize olanak sağlayan **AssetCreationOptions**’ı alır:</span><span class="sxs-lookup"><span data-stu-id="e86f5-159">The **CreateFromFile** method takes **AssetCreationOptions** which lets you specify one of the following asset creation options:</span></span>

* <span data-ttu-id="e86f5-160">**Hiçbiri**: Şifreleme kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="e86f5-160">**None** - No encryption is used.</span></span> <span data-ttu-id="e86f5-161">Varsayılan değer budur.</span><span class="sxs-lookup"><span data-stu-id="e86f5-161">This is the default value.</span></span> <span data-ttu-id="e86f5-162">Bu seçeneği kullandığınızda, içeriğinizin aktarım sırasında ve depolama alanında beklerken korunmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-162">Note that when using this option, your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="e86f5-163">Aşamalı indirme kullanarak bir MP4 iletmeyi planlıyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-163">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="e86f5-164">**StorageEncrypted**: Temiz içeriğinizi yerel olarak Gelişmiş Şifreleme Standardı (AES) 256 bit şifreleme kullanarak şifrelemek için bu seçeneği kullanın. Şifrelenen içerik ardından Azure Storage’a yüklenerek bekleme durumunda depolanır.</span><span class="sxs-lookup"><span data-stu-id="e86f5-164">**StorageEncrypted** - Use this option to encrypt your clear content locally using Advanced Encryption Standard (AES)-256 bit encryption, which then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="e86f5-165">Depolama Şifrelemesi ile korunan varlıklar, kodlamadan önce otomatik olarak şifrelenerek şifrelenmiş bir dosya sistemine yerleştirilir ve yeni bir çıktı varlığı şeklinde geri yüklenmeden önce isteğe bağlı olarak yeniden şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-165">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="e86f5-166">Depolama Şifrelemesinin birincil kullanım nedeni, yüksek kaliteli girdi medya dosyalarınızın güvenliğini güçlü şifrelemeyle diskte bekleyen konumda sağlamak istediğiniz durumdur.</span><span class="sxs-lookup"><span data-stu-id="e86f5-166">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="e86f5-167">**CommonEncryptionProtected**: Zaten Ortak Şifreleme veya PlayReady DRM ile şifrelenip korunan bir içerik (örneğin, PlayReady DRM ile korunan Kesintisiz Akış) yüklüyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-167">**CommonEncryptionProtected** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="e86f5-168">**EnvelopeEncryptionProtected**: AES ile şifrelenmiş HLS yüklüyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-168">**EnvelopeEncryptionProtected** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="e86f5-169">Dosyaların Transform Manager tarafından kodlanmış ve şifrelenmiş olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-169">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

<span data-ttu-id="e86f5-170">**CreateFromFile** yöntemi, dosyanın yükleme durumunu bildirmek üzere bir geri çağırma belirtmenize de olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e86f5-170">The **CreateFromFile** method also lets you specify a callback in order to report the upload progress of the file.</span></span>

<span data-ttu-id="e86f5-171">Aşağıdaki örnekte, varlık seçeneği olarak **Hiçbiri** belirliyoruz.</span><span class="sxs-lookup"><span data-stu-id="e86f5-171">In the following example, we specify **None** for the asset options.</span></span>

<span data-ttu-id="e86f5-172">Program sınıfına aşağıdaki yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e86f5-172">Add the following method to the Program class.</span></span>

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


## <a name="encode-the-source-file-into-a-set-of-adaptive-bitrate-mp4-files"></a><span data-ttu-id="e86f5-173">Kaynak dosyayı uyarlamalı bit hızlı bir MP4 dosyaları grubuna kodlama</span><span class="sxs-lookup"><span data-stu-id="e86f5-173">Encode the source file into a set of adaptive bitrate MP4 files</span></span>
<span data-ttu-id="e86f5-174">Varlıklar Media Services’e alındıktan sonra medyaya, istemcilere teslim edilmeden önce kodlama, biçimini değiştirme, filigran ekleme ve benzeri işlemler uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-174">After ingesting assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="e86f5-175">Bu etkinlikler, yüksek performans ve kullanılabilirlik sağlamak için birden fazla arka plan rol örneğinde zamanlanır ve çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="e86f5-175">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="e86f5-176">Bu etkinliklere İşler adı verilir ve her bir İş, Varlık dosyası üzerinde asıl işi yapan atomik Görevlerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="e86f5-176">These activities are called Jobs, and each Job is composed of atomic Tasks that do the actual work on the Asset file.</span></span>

<span data-ttu-id="e86f5-177">Daha önce belirtildiği gibi, Azure Media Services ile çalışırken en sık karşılaşılan senaryolardan biri, istemcilerinize bit hızı uyarlamalı akış iletmektir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-177">As was mentioned earlier, when working with Azure Media Services, one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="e86f5-178">Media Services, bit hızı uyarlamalı bir MP4 dosyaları kümesini dinamik olarak şu biçimlerden birine paketleyebilir: HTTP Canlı Akışı (HLS), Kesintisiz Akış ve MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="e86f5-178">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span>

<span data-ttu-id="e86f5-179">Dinamik paketlemeden yararlanmak için, ara (kaynak) dosyanızı bit hızı uyarlamalı bir MP4 veya Kesintisiz Akış dosyaları kümesine kodlamanız veya dosyanın kodlamasını dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-179">To take advantage of dynamic packaging, you need to encode or transcode your mezzanine (source) file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span>  

<span data-ttu-id="e86f5-180">Aşağıdaki kod, bir kodlama işinin nasıl gönderileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-180">The following code shows how to submit an encoding job.</span></span> <span data-ttu-id="e86f5-181">İş, ara dosyayı **Medya Kodlayıcı Standart**’ını kullanarak bir grup bit hızı uyarlamalı MP4’e kodlamasını dönüştüren bir görev içerir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-181">The job contains one task that specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="e86f5-182">Kod işi gönderir ve tamamlanana kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="e86f5-182">The code submits the job and waits until it is completed.</span></span>

<span data-ttu-id="e86f5-183">İş tamamlandığında varlığınızı akışla aktarabilir veya kodlama dönüştürmenin sonucu olarak oluşturulan MP4 dosyalarını aşamalı indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e86f5-183">Once the job is completed, you would be able to stream your asset or progressively download MP4 files that were created as a result of transcoding.</span></span>

<span data-ttu-id="e86f5-184">Program sınıfına aşağıdaki yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e86f5-184">Add the following method to the Program class.</span></span>

    static public IAsset EncodeToAdaptiveBitrateMP4s(IAsset asset, AssetCreationOptions options)
    {

        // Prepare a job with a single task to transcode the specified asset
        // into a multi-bitrate asset.

        IJob job = _context.Jobs.CreateWithSingleTask(
            "Media Encoder Standard",
            "Adaptive Streaming",
            asset,
            "Adaptive Bitrate MP4",
            options);

        Console.WriteLine("Submitting transcoding job...");


        // Submit the job and wait until it is completed.
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

## <a name="publish-the-asset-and-get-urls-for-streaming-and-progressive-download"></a><span data-ttu-id="e86f5-185">Varlığı yayımlayıp akış ve aşamalı indirme URL’lerini alma</span><span class="sxs-lookup"><span data-stu-id="e86f5-185">Publish the asset and get URLs for streaming and progressive download</span></span>

<span data-ttu-id="e86f5-186">Bir varlığı akışla aktarmak veya indirmek için söz konusu varlığı önce bir bulucu oluşturarak “yayımlamak” gerekir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-186">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="e86f5-187">Bulucular varlıkta bulunan dosyalara erişim imkanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e86f5-187">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="e86f5-188">Media Services, iki tür bulucuyu destekler: Medyayı akışla aktarmak (örneğin MPEG DASH, HLS veya Kesintisiz Akış) için kullanılan OnDemandOrigin bulucuları ve medya dosyalarını indirmek için kullanılan Erişim İmzası (SAS) bulucuları (SAS bulucuları hakkında daha fazla bilgi için [bu](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog sayfasına bakın).</span><span class="sxs-lookup"><span data-stu-id="e86f5-188">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files (for more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog).</span></span>

### <a name="some-details-about-url-formats"></a><span data-ttu-id="e86f5-189">URL biçimleri hakkında bazı ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="e86f5-189">Some details about URL formats</span></span>

<span data-ttu-id="e86f5-190">Bulucuları oluşturduktan sonra, dosyalarınızı akışla aktarmak veya indirmek için kullanılacak URL'leri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e86f5-190">After you create the locators, you can build the URLs that would be used to stream or download your files.</span></span> <span data-ttu-id="e86f5-191">Bu öğreticideki örnek, uygun tarayıcılara yapıştırabileceğiniz URL'ler oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="e86f5-191">The sample in this tutorial will output URLs that you can paste in appropriate browsers.</span></span> <span data-ttu-id="e86f5-192">Bu bölümde yalnızca farklı biçimlerin neye benzediğini gösteren kısa örnekler verilir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-192">This section just gives short examples of what different formats look like.</span></span>

#### <a name="a-streaming-url-for-mpeg-dash-has-the-following-format"></a><span data-ttu-id="e86f5-193">MPEG DASH’e ilişkin bir akış URL'si aşağıdaki biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e86f5-193">A streaming URL for MPEG DASH has the following format:</span></span>

<span data-ttu-id="e86f5-194">{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest**(format=mpd-time-csf)**</span><span class="sxs-lookup"><span data-stu-id="e86f5-194">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=mpd-time-csf)**</span></span>

#### <a name="a-streaming-url-for-hls-has-the-following-format"></a><span data-ttu-id="e86f5-195">HLS’ye ilişkin bir akış URL'si aşağıdaki biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e86f5-195">A streaming URL for HLS has the following format:</span></span>

<span data-ttu-id="e86f5-196">{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest**(format=m3u8-aapl)**</span><span class="sxs-lookup"><span data-stu-id="e86f5-196">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest**(format=m3u8-aapl)**</span></span>

#### <a name="a-streaming-url-for-smooth-streaming-has-the-following-format"></a><span data-ttu-id="e86f5-197">Kesintisiz Akışa ilişkin bir akış URL'si aşağıdaki biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e86f5-197">A streaming URL for Smooth Streaming has the following format:</span></span>

<span data-ttu-id="e86f5-198">{akış uç noktası adı-media services hesabı adı}.streaming.mediaservices.windows.net/{konum kimliği}/{dosya adı}.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="e86f5-198">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>


#### <a name="a-sas-url-used-to-download-files-has-the-following-format"></a><span data-ttu-id="e86f5-199">Dosya indirmek için kullanılan bir SAS URL'si aşağıdaki biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e86f5-199">A SAS URL used to download files has the following format:</span></span>

<span data-ttu-id="e86f5-200">{blob kapsayıcısı adı}/{varlık adı}/{dosya adı}/{SAS imzası}</span><span class="sxs-lookup"><span data-stu-id="e86f5-200">{blob container name}/{asset name}/{file name}/{SAS signature}</span></span>

<span data-ttu-id="e86f5-201">Media Services .NET SDK uzantıları, yayımlanan varlık için biçimlendirilmiş URL'ler döndüren kullanışlı yardımcı yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e86f5-201">Media Services .NET SDK extensions provide convenient helper methods that return formatted URLs for the published asset.</span></span>

<span data-ttu-id="e86f5-202">Aşağıdaki kod, .NET SDK Uzantıları kullanarak bulucu oluşturur, akış ve aşamalı indirme URL'leri alır.</span><span class="sxs-lookup"><span data-stu-id="e86f5-202">The following code uses .NET SDK Extensions to create locators and to get streaming and progressive download URLs.</span></span> <span data-ttu-id="e86f5-203">Kod ayrıca yerel bir klasöre nasıl dosya indirileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-203">The code also shows how to download files to a local folder.</span></span>

<span data-ttu-id="e86f5-204">Program sınıfına aşağıdaki yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e86f5-204">Add the following method to the Program class.</span></span>

    static public void PublishAssetGetURLs(IAsset asset)
    {
        // Publish the output asset by creating an Origin locator for adaptive streaming,
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

        // Get the Smooth Streaming, HLS and MPEG-DASH URLs for adaptive streaming,
        // and the Progressive Download URL.
        Uri smoothStreamingUri = asset.GetSmoothStreamingUri();
        Uri hlsUri = asset.GetHlsUri();
        Uri mpegDashUri = asset.GetMpegDashUri();

        // Get the URls for progressive download for each MP4 file that was generated as a result
        // of encoding.
        List<Uri> mp4ProgressiveDownloadUris = mp4AssetFiles.Select(af => af.GetSasUri()).ToList();


        // Display  the streaming URLs.
        Console.WriteLine("Use the following URLs for adaptive streaming: ");
        Console.WriteLine(smoothStreamingUri);
        Console.WriteLine(hlsUri);
        Console.WriteLine(mpegDashUri);
        Console.WriteLine();

        // Display the URLs for progressive download.
        Console.WriteLine("Use the following URLs for progressive download.");
        mp4ProgressiveDownloadUris.ForEach(uri => Console.WriteLine(uri + "\n"));
        Console.WriteLine();

        // Download the output asset to a local folder.
        string outputFolder = "job-output";
        if (!Directory.Exists(outputFolder))
        {
            Directory.CreateDirectory(outputFolder);
        }

        Console.WriteLine();
        Console.WriteLine("Downloading output asset files to a local folder...");
        asset.DownloadToFolder(
            outputFolder,
            (af, p) =>
            {
                Console.WriteLine("Downloading '{0}' - Progress: {1:0.##}%", af.Name, p.Progress);
            });

        Console.WriteLine("Output asset files available at '{0}'.", Path.GetFullPath(outputFolder));
    }

## <a name="test-by-playing-your-content"></a><span data-ttu-id="e86f5-205">İçeriğiniz oynatarak test etme</span><span class="sxs-lookup"><span data-stu-id="e86f5-205">Test by playing your content</span></span>

<span data-ttu-id="e86f5-206">Önceki bölümde tanımlanan programı çalıştırdığınızda konsol penceresinde aşağıdakine benzer URL'ler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e86f5-206">Once you run the program defined in the previous section, the URLs similar to the following will be displayed in the console window.</span></span>

<span data-ttu-id="e86f5-207">Uyarlamalı akış URL'leri:</span><span class="sxs-lookup"><span data-stu-id="e86f5-207">Adaptive streaming URLs:</span></span>

<span data-ttu-id="e86f5-208">Kesintisiz Akış</span><span class="sxs-lookup"><span data-stu-id="e86f5-208">Smooth Streaming</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="e86f5-209">HLS</span><span class="sxs-lookup"><span data-stu-id="e86f5-209">HLS</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="e86f5-210">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="e86f5-210">MPEG DASH</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)

<span data-ttu-id="e86f5-211">Aşamalı indirme URL'leri (ses ve video).</span><span class="sxs-lookup"><span data-stu-id="e86f5-211">Progressive download URLs (audio and video).</span></span>

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


<span data-ttu-id="e86f5-212">Videonuzun akışını yapmak için URL'nizi [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)'daki URL metin kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-212">To stream your video, paste your URL in the URL textbox in the [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="e86f5-213">Aşamalı indirmeyi test etmek için bir tarayıcıya (örneğin Internet Explorer, Chrome veya Safari) bir URL yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e86f5-213">To test progressive download, paste a URL into a browser (for example, Internet Explorer, Chrome, or Safari).</span></span>

<span data-ttu-id="e86f5-214">Daha fazla bilgi edinmek için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="e86f5-214">For more information, see the following topics:</span></span>

- [<span data-ttu-id="e86f5-215">İçeriğinizi mevcut oynatıcılarda oynatma</span><span class="sxs-lookup"><span data-stu-id="e86f5-215">Playing your content with existing players</span></span>](media-services-playback-content-with-existing-players.md)
- [<span data-ttu-id="e86f5-216">Video oynatıcı uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="e86f5-216">Develop video player applications</span></span>](media-services-develop-video-players.md)
- [<span data-ttu-id="e86f5-217">DASH.js ile bir MPEG-DASH Uyarlamalı Akış Videosunu bir HTML5 Uygulamasına ekleme</span><span class="sxs-lookup"><span data-stu-id="e86f5-217">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>](media-services-embed-mpeg-dash-in-html5.md)

## <a name="download-sample"></a><span data-ttu-id="e86f5-218">Örnek indirme</span><span class="sxs-lookup"><span data-stu-id="e86f5-218">Download sample</span></span>
<span data-ttu-id="e86f5-219">Aşağıdaki kod örneği, bu öğreticide oluşturduğunuz kodu içerir: [örnek](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="e86f5-219">The following code sample contains the code that you created in this tutorial: [sample](https://azure.microsoft.com/documentation/samples/media-services-dotnet-on-demand-encoding-with-media-encoder-standard/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e86f5-220">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e86f5-220">Next Steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e86f5-221">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="e86f5-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]



<!-- Anchors. -->


<!-- URLs. -->
[Web Platform Installer]: http://go.microsoft.com/fwlink/?linkid=255386
[Portal]: http://manage.windowsazure.com/
