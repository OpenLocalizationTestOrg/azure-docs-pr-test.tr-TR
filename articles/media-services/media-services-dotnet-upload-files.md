---
title: ".NET kullanarak Media Services hesabı aaaUpload dosyalarıyla | Microsoft Docs"
description: "Oluşturma ve varlıklar karşıya tooget medya medya Hizmetleri içine nasıl içerik öğrenin."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c9c86380-9395-4db8-acea-507c52066f73
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/12/2017
ms.author: juliako
ms.openlocfilehash: 11c8a359b09efe04b54490fd48ac0cd7c366f8b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-net"></a><span data-ttu-id="e8d82-103">.NET kullanarak bir Media Services hesabına dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="e8d82-103">Upload files into a Media Services account using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e8d82-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e8d82-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="e8d82-105">REST</span><span class="sxs-lookup"><span data-stu-id="e8d82-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="e8d82-106">Portal</span><span class="sxs-lookup"><span data-stu-id="e8d82-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="e8d82-107">Media Services’de, dijital dosyalar bir varlığa yüklenir (veya alınır).</span><span class="sxs-lookup"><span data-stu-id="e8d82-107">In Media Services, you upload (or ingest) your digital files into an asset.</span></span> <span data-ttu-id="e8d82-108">Merhaba **varlık** varlık içerebilir video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkında hello meta veriler.)  Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır.</span><span class="sxs-lookup"><span data-stu-id="e8d82-108">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="e8d82-109">Merhaba varlık Hello dosyalarında çağrılır **varlık dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="e8d82-109">hello files in hello asset are called **Asset Files**.</span></span> <span data-ttu-id="e8d82-110">Merhaba **AssetFile** örneği ve hello gerçek medya dosyası olan iki farklı nesneler.</span><span class="sxs-lookup"><span data-stu-id="e8d82-110">hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="e8d82-111">Merhaba medya dosyası hello gerçek medya içeriği içerirken hello AssetFile örneği hello medya dosyası hakkındaki meta verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-111">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

> [!NOTE]
> <span data-ttu-id="e8d82-112">ilgili önemli noktalar aşağıdaki hello Uygula:</span><span class="sxs-lookup"><span data-stu-id="e8d82-112">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="e8d82-113">Media Services URL'leri içeriği (örneğin, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) akış Merhaba oluştururken hello hello IAssetFile.Name özellik değerini kullanır Bu nedenle, yüzde kodlama izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="e8d82-113">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="e8d82-114">Merhaba hello değerini **adı** özelliği hello aşağıdakilerden herhangi birini içeremez [yüzde kodlama-ayrılmış karakterleri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="e8d82-114">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="e8d82-115">Ayrıca, yalnızca bir olabilir '.' hello dosya adı uzantısı için.</span><span class="sxs-lookup"><span data-stu-id="e8d82-115">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="e8d82-116">Merhaba hello adının uzunluğu 260 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="e8d82-116">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="e8d82-117">Media Services işlemek için desteklenen bir toohello en büyük dosya boyutu sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="e8d82-117">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="e8d82-118">Lütfen bakın [bu](media-services-quotas-and-limitations.md) hello dosya boyutu sınırlaması hakkında ayrıntılı bilgi için konu.</span><span class="sxs-lookup"><span data-stu-id="e8d82-118">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> * <span data-ttu-id="e8d82-119">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="e8d82-119">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="e8d82-120">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="e8d82-120">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="e8d82-121">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-121">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>
> 

<span data-ttu-id="e8d82-122">Varlıklar oluşturduğunuzda, şifreleme seçenekleri aşağıdaki hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8d82-122">When you create assets, you can specify hello following encryption options.</span></span> 

* <span data-ttu-id="e8d82-123">**Hiçbiri**: Şifreleme kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="e8d82-123">**None** - No encryption is used.</span></span> <span data-ttu-id="e8d82-124">Merhaba varsayılan değer budur.</span><span class="sxs-lookup"><span data-stu-id="e8d82-124">This is hello default value.</span></span> <span data-ttu-id="e8d82-125">Bu seçenek kullanıldığında, içeriğinizin aktarım veya deposunda kalan korunmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-125">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
  <span data-ttu-id="e8d82-126">Aşamalı indirme kullanarak toodeliver bir MP4 planlıyorsanız, bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-126">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="e8d82-127">**CommonEncryption** -zaten şifrelenmiş ve ortak şifreleme veya PlayReady DRM (örneğin, ile korunan kesintisiz akış PlayReady DRM) ile korunan içerik yüklüyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-127">**CommonEncryption** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="e8d82-128">**EnvelopeEncrypted** – AES ile şifrelenmiş HLS yüklüyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-128">**EnvelopeEncrypted** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="e8d82-129">Hello dosyaları gerekir alınan kodlanmış ve Transform Manager tarafından şifrelenmiş olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-129">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>
* <span data-ttu-id="e8d82-130">**StorageEncrypted** - Temizle içeriğinizi yerel olarak AES 256 bit şifreleme kullanarak şifreler ve tooAzure depolanır depolama şifrelenen yükler.</span><span class="sxs-lookup"><span data-stu-id="e8d82-130">**StorageEncrypted** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="e8d82-131">Depolama şifrelemesi ile korunan varlıklar otomatik olarak şifrelenmemiş ve bir şifrelenmiş dosya sistemi önceki tooencoding ve yeni bir çıkış varlığı olarak geri isteğe bağlı olarak yeniden şifrelenmiş önceki toouploading yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-131">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="e8d82-132">Depolama şifrelemesinin birincil kullanım durumu hello yüksek kaliteli giriş medya dosyalarınızın güçlü şifrelemeyle diskte rest toosecure istediğiniz durumdur.</span><span class="sxs-lookup"><span data-stu-id="e8d82-132">hello primary use case for Storage Encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>
  
    <span data-ttu-id="e8d82-133">Media Services değil üzerinden dijital hak Yöneticisi (DRM) gibi hat varlıklarınızı için disk üzerinde depolama şifreleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8d82-133">Media Services provides on-disk storage encryption for your assets, not over-the-wire like Digital Rights Manager (DRM).</span></span>
  
    <span data-ttu-id="e8d82-134">Şifrelenmiş depolama varlığınız olması durumunda, varlık teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-134">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="e8d82-135">Daha fazla bilgi için bkz: [varlık teslim ilkesini yapılandırma](media-services-dotnet-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="e8d82-135">For more information see [Configuring asset delivery policy](media-services-dotnet-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="e8d82-136">Varlık toobe ile şifrelenmiş için belirtirseniz bir **CommonEncrypted** seçeneği veya bir **EnvelopeEncypted** seçeneği, varlıkla tooassociate gerekir bir **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="e8d82-136">If you specify for your asset toobe encrypted with a **CommonEncrypted** option, or an **EnvelopeEncypted** option, you will need tooassociate your asset with a **ContentKey**.</span></span> <span data-ttu-id="e8d82-137">Daha fazla bilgi için bkz: [nasıl toocreate bir ContentKey](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="e8d82-137">For more information, see [How toocreate a ContentKey](media-services-dotnet-create-contentkey.md).</span></span> 

<span data-ttu-id="e8d82-138">Varlık toobe ile şifrelenmiş için belirtirseniz bir **StorageEncrypted** seçeneği, .NET oluşturacak için Media Services SDK'sı hello bir **StorateEncrypted** **ContentKey** için varlık.</span><span class="sxs-lookup"><span data-stu-id="e8d82-138">If you specify for your asset toobe encrypted with a **StorageEncrypted** option, hello Media Services SDK for .NET will create a **StorateEncrypted** **ContentKey** for your asset.</span></span>

<span data-ttu-id="e8d82-139">Bu konu, nasıl toouse medya hizmetleri gösterir Media Services .NET SDK uzantıları tooupload dosyalarıyla Media Services varlık yanı sıra .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e8d82-139">This topic shows how toouse Media Services .NET SDK as well as Media Services .NET SDK extensions tooupload files into a Media Services asset.</span></span>

## <a name="upload-a-single-file-with-media-services-net-sdk"></a><span data-ttu-id="e8d82-140">Media Services .NET SDK'sı ile tek bir dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="e8d82-140">Upload a single file with Media Services .NET SDK</span></span>
<span data-ttu-id="e8d82-141">Aşağıdaki örnek kodu Hello .NET SDK'sı tooupload tek bir dosya kullanır.</span><span class="sxs-lookup"><span data-stu-id="e8d82-141">hello sample code below uses .NET SDK tooupload a single file.</span></span> <span data-ttu-id="e8d82-142">Merhaba AccessPolicy ve Bulucu oluşturulur ve hello karşıya yükleme işlevi tarafından yok.</span><span class="sxs-lookup"><span data-stu-id="e8d82-142">hello AccessPolicy and Locator are created and destroyed by hello Upload function.</span></span> 


        static public IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
                Console.WriteLine("File does not exist.");
                return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, assetCreationOptions);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }


## <a name="upload-multiple-files-with-media-services-net-sdk"></a><span data-ttu-id="e8d82-143">Media Services .NET SDK'sı ile birden çok dosya karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="e8d82-143">Upload multiple files with Media Services .NET SDK</span></span>
<span data-ttu-id="e8d82-144">kodun gösterdiği nasıl aşağıdaki hello toocreate bir varlık ve birden çok dosya karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="e8d82-144">hello following code shows how toocreate an asset and upload multiple files.</span></span>

<span data-ttu-id="e8d82-145">Merhaba kod aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="e8d82-145">hello code does hello following:</span></span>

* <span data-ttu-id="e8d82-146">Merhaba önceki adımda tanımlanan hello CreateEmptyAsset yöntemi kullanarak boş bir varlık oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e8d82-146">Creates an empty asset using hello CreateEmptyAsset method defined in hello previous step.</span></span>
* <span data-ttu-id="e8d82-147">Oluşturur bir **AccessPolicy** hello izinler ve erişim toohello varlık süresini tanımlayan örnek.</span><span class="sxs-lookup"><span data-stu-id="e8d82-147">Creates an **AccessPolicy** instance that defines hello permissions and duration of access toohello asset.</span></span>
* <span data-ttu-id="e8d82-148">Oluşturur bir **Bulucu** erişim toohello varlık sağlar örneği.</span><span class="sxs-lookup"><span data-stu-id="e8d82-148">Creates a **Locator** instance that provides access toohello asset.</span></span>
* <span data-ttu-id="e8d82-149">Oluşturur bir **BlobTransferClient** örneği.</span><span class="sxs-lookup"><span data-stu-id="e8d82-149">Creates a **BlobTransferClient** instance.</span></span> <span data-ttu-id="e8d82-150">Bu tür Azure BLOB'hello üzerinde çalıştığı bir istemci temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e8d82-150">This type represents a client that operates on hello Azure blobs.</span></span> <span data-ttu-id="e8d82-151">Bu örnekte hello istemci toomonitor hello karşıya yükleme işlemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-151">In this example we use hello client toomonitor hello upload progress.</span></span> 
* <span data-ttu-id="e8d82-152">Merhaba belirtilen dizindeki dosyaları aracılığıyla numaralandırır ve oluşturan bir **AssetFile** her dosya için örneği.</span><span class="sxs-lookup"><span data-stu-id="e8d82-152">Enumerates through files in hello specified directory and creates an **AssetFile** instance for each file.</span></span>
* <span data-ttu-id="e8d82-153">Karşıya dosya hello kullanarak Media Services hello **UploadAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e8d82-153">Uploads hello files into Media Services using hello **UploadAsync** method.</span></span> 

> [!NOTE]
> <span data-ttu-id="e8d82-154">Merhaba çağrıları engellemediğini ve paralel olarak karşıya yüklenen hello dosyaların hello UploadAsync yöntemi tooensure kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-154">Use hello UploadAsync method tooensure that hello calls are not blocking and hello files are uploaded in parallel.</span></span>
> 
> 

        static public IAsset CreateAssetAndUploadMultipleFiles(AssetCreationOptions assetCreationOptions, string folderPath)
        {
            var assetName = "UploadMultipleFiles_" + DateTime.UtcNow.ToString();

            IAsset asset = _context.Assets.Create(assetName, assetCreationOptions);

            var accessPolicy = _context.AccessPolicies.Create(assetName, TimeSpan.FromDays(30),
                                                                AccessPermissions.Write | AccessPermissions.List);

            var locator = _context.Locators.CreateLocator(LocatorType.Sas, asset, accessPolicy);

            var blobTransferClient = new BlobTransferClient();
            blobTransferClient.NumberOfConcurrentTransfers = 20;
            blobTransferClient.ParallelTransferThreadCount = 20;

            blobTransferClient.TransferProgressChanged += blobTransferClient_TransferProgressChanged;

            var filePaths = Directory.EnumerateFiles(folderPath);

            Console.WriteLine("There are {0} files in {1}", filePaths.Count(), folderPath);

            if (!filePaths.Any())
            {
                throw new FileNotFoundException(String.Format("No files in directory, check folderPath: {0}", folderPath));
            }

            var uploadTasks = new List<Task>();
            foreach (var filePath in filePaths)
            {
                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                Console.WriteLine("Created assetFile {0}", assetFile.Name);

                // It is recommended toovalidate AccestFiles before upload. 
                Console.WriteLine("Start uploading of {0}", assetFile.Name);
                uploadTasks.Add(assetFile.UploadAsync(filePath, blobTransferClient, locator, CancellationToken.None));
            }

            Task.WaitAll(uploadTasks.ToArray());
            Console.WriteLine("Done uploading hello files");

            blobTransferClient.TransferProgressChanged -= blobTransferClient_TransferProgressChanged;

            locator.Delete();
            accessPolicy.Delete();

            return asset;
        }

    static void  blobTransferClient_TransferProgressChanged(object sender, BlobTransferProgressChangedEventArgs e)
    {
        if (e.ProgressPercentage > 4) // Avoid startup jitter, as hello upload tasks are added.
        {
            Console.WriteLine("{0}% upload competed for {1}.", e.ProgressPercentage, e.LocalFile);
        }
    }



<span data-ttu-id="e8d82-155">Çok sayıda varlıklar karşıya yüklenirken hello aşağıdakileri göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="e8d82-155">When uploading a large number of assets, consider hello following.</span></span>

* <span data-ttu-id="e8d82-156">Yeni bir **CloudMediaContext** iş parçacığı başına nesne.</span><span class="sxs-lookup"><span data-stu-id="e8d82-156">Create a new **CloudMediaContext** object per thread.</span></span> <span data-ttu-id="e8d82-157">Merhaba **CloudMediaContext** sınıfı iş parçacığı içinde korumalı değil.</span><span class="sxs-lookup"><span data-stu-id="e8d82-157">hello **CloudMediaContext** class is not thread safe.</span></span>
* <span data-ttu-id="e8d82-158">2 tooa daha yüksek değer 5 gibi hello varsayılan değerinden NumberOfConcurrentTransfers artırın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-158">Increase NumberOfConcurrentTransfers from hello default value of 2 tooa higher value like 5.</span></span> <span data-ttu-id="e8d82-159">Bu özelliği ayarlamak etkiler tüm örneklerini **CloudMediaContext**.</span><span class="sxs-lookup"><span data-stu-id="e8d82-159">Setting this property affects all instances of **CloudMediaContext**.</span></span> 
* <span data-ttu-id="e8d82-160">ParallelTransferThreadCount 10 hello varsayılan değeri koruyun.</span><span class="sxs-lookup"><span data-stu-id="e8d82-160">Keep ParallelTransferThreadCount at hello default value of 10.</span></span>

## <span data-ttu-id="e8d82-161"><a id="ingest_in_bulk"></a>Varlıklar Media Services .NET SDK kullanarak toplu alma</span><span class="sxs-lookup"><span data-stu-id="e8d82-161"><a id="ingest_in_bulk"></a>Ingesting Assets in Bulk using Media Services .NET SDK</span></span>
<span data-ttu-id="e8d82-162">Büyük varlık dosyaları karşıya yükleme varlık oluşturma sırasında bir performans sorunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-162">Uploading large asset files can be a bottleneck during asset creation.</span></span> <span data-ttu-id="e8d82-163">Varlıklar toplu ya da "Toplu alma" alanını, varlık oluşturma hello karşıya yükleme işleminden kesilmesi içerir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-163">Ingesting Assets in Bulk or “Bulk Ingesting”, involves decoupling asset creation from hello upload process.</span></span> <span data-ttu-id="e8d82-164">toouse bir toplu ingesting yaklaşım hello varlık ve ilişkili dosyalarını açıklayan bir bildirimi (IngestManifest) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e8d82-164">toouse a bulk ingesting approach, create a manifest (IngestManifest) that describes hello asset and its associated files.</span></span> <span data-ttu-id="e8d82-165">Ardından, seçim tooupload hello ilişkili dosyaları toohello bildirim blob kapsayıcısının hello karşıya yükleme yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-165">Then use hello upload method of your choice tooupload hello associated files toohello manifest’s blob container.</span></span> <span data-ttu-id="e8d82-166">Microsoft Azure Media Services ile Merhaba bildirimini ilişkili hello blob kapsayıcısı izler.</span><span class="sxs-lookup"><span data-stu-id="e8d82-166">Microsoft Azure Media Services watches hello blob container associated with hello manifest.</span></span> <span data-ttu-id="e8d82-167">Bir dosyayı karşıya yüklenen toohello blob kapsayıcısı olduğunda, Microsoft Azure Media Services hello varlık oluşturma (IngestManifestAsset) hello bildiriminde hello varlık hello yapılandırmasına dayalı tamamlar.</span><span class="sxs-lookup"><span data-stu-id="e8d82-167">Once a file is uploaded toohello blob container, Microsoft Azure Media Services completes hello asset creation based on hello configuration of hello asset in hello manifest (IngestManifestAsset).</span></span>

<span data-ttu-id="e8d82-168">toocreate yeni IngestManifest hello hello CloudMediaContext IngestManifests koleksiyonunda tarafından sunulan hello Create yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-168">toocreate a new IngestManifest call hello Create method exposed by hello IngestManifests collection on hello CloudMediaContext.</span></span> <span data-ttu-id="e8d82-169">Bu yöntem, sağladığınız hello bildirim adıyla yeni IngestManifest oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e8d82-169">This method will create a new IngestManifest with hello manifest name you provide.</span></span>

    IIngestManifest manifest = context.IngestManifests.Create(name);

<span data-ttu-id="e8d82-170">Merhaba toplu IngestManifest ile ilişkilendirilecek hello varlıklar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e8d82-170">Create hello assets that will be associated with hello bulk IngestManifest.</span></span> <span data-ttu-id="e8d82-171">Toplu alma için hello varlık üzerinde istenen hello şifreleme seçeneklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-171">Configure hello desired encryption options on hello asset for bulk ingesting.</span></span>

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

<span data-ttu-id="e8d82-172">Bir IngestManifestAsset toplu alma için bir toplu IngestManifest bir varlık ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-172">An IngestManifestAsset associates an Asset with a bulk IngestManifest for bulk ingesting.</span></span> <span data-ttu-id="e8d82-173">Ayrıca, hello her varlık yapacak AssetFiles ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-173">It also associates hello AssetFiles that will make up each Asset.</span></span> <span data-ttu-id="e8d82-174">toocreate bir IngestManifestAsset hello sunucu içeriğine hello Create yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-174">toocreate an IngestManifestAsset, use hello Create method on hello server context.</span></span>

<span data-ttu-id="e8d82-175">Merhaba aşağıdaki örnek toohello toplu daha önce oluşturduğunuz hello iki varlıklar ilişkilendirmek ekleme iki yeni IngestManifestAssets bildirim alma gösterir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-175">hello following example demonstrates adding two new IngestManifestAssets that associate hello two assets previously created toohello bulk ingest manifest.</span></span> <span data-ttu-id="e8d82-176">Her IngestManifestAsset toplu alma sırasında yüklenecek dosyaları her varlık için bir dizi de ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-176">Each IngestManifestAsset also associates a set of files that will be uploaded for each asset during bulk ingesting.</span></span>  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

<span data-ttu-id="e8d82-177">Merhaba varlık dosyaları toohello blob depolama kapsayıcısını hello tarafından sağlanan URI karşıya yükleme özellikli tüm yüksek hızlı istemci uygulaması kullanabilirsiniz **IIngestManifest.BlobStorageUriForUpload** hello IngestManifest özelliği.</span><span class="sxs-lookup"><span data-stu-id="e8d82-177">You can use any high speed client application capable of uploading hello asset files toohello blob storage container URI provided by hello **IIngestManifest.BlobStorageUriForUpload** property of hello IngestManifest.</span></span> <span data-ttu-id="e8d82-178">Bir önem düzeyindeki yüksek hızlı karşıya yükleme hizmeti [Aspera istendiğinde Azure uygulaması için](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span><span class="sxs-lookup"><span data-stu-id="e8d82-178">One notable high speed upload service is [Aspera On Demand for Azure Application](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6).</span></span> <span data-ttu-id="e8d82-179">Aşağıdaki kod örneğine hello gösterildiği gibi tooupload hello varlıklar dosyaları da kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8d82-179">You can also write code tooupload hello assets files as shown in hello following code example.</span></span>

    static void UploadBlobFile(string destBlobURI, string filename)
    {
        Task copytask = new Task(() =>
        {
            var storageaccount = new CloudStorageAccount(new StorageCredentials(_storageAccountName, _storageAccountKey), true);
            CloudBlobClient blobClient = storageaccount.CreateCloudBlobClient();
            CloudBlobContainer blobContainer = blobClient.GetContainerReference(destBlobURI);

            string[] splitfilename = filename.Split('\\');
            var blob = blobContainer.GetBlockBlobReference(splitfilename[splitfilename.Length - 1]);

            using (var stream = System.IO.File.OpenRead(filename))
                blob.UploadFromStream(stream);

            lock (consoleWriteLock)
            {
                Console.WriteLine("Upload for {0} completed.", filename);
            }
        });

        copytask.Start();
    }

<span data-ttu-id="e8d82-180">Bu konuda kullanılan hello örnek hello varlık dosyaları karşıya yükleme için hello kodu aşağıdaki kod örneğine hello gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-180">hello code for uploading hello asset files for hello sample used in this topic is shown in hello following code example.</span></span>

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


<span data-ttu-id="e8d82-181">İle ilişkili tüm varlıklar için toplu hello alma hello ilerlemesini belirlemek bir **IngestManifest** hello hello istatistikleri özelliği yoklayarak **IngestManifest**.</span><span class="sxs-lookup"><span data-stu-id="e8d82-181">You can determine hello progress of hello bulk ingesting for all assets associated with an **IngestManifest** by polling hello Statistics property of hello **IngestManifest**.</span></span> <span data-ttu-id="e8d82-182">Sipariş tooupdate ilerleme durumu bilgileri yeni bir kullanmalısınız **CloudMediaContext** her zaman hello istatistikleri özelliği yoklamak.</span><span class="sxs-lookup"><span data-stu-id="e8d82-182">In order tooupdate progress information, you must use a new **CloudMediaContext** each time you poll hello Statistics property.</span></span>

<span data-ttu-id="e8d82-183">Merhaba aşağıdaki örnekte bir IngestManifest tarafından yoklama gösterir, **kimliği**.</span><span class="sxs-lookup"><span data-stu-id="e8d82-183">hello following example demonstrates polling an IngestManifest by its **Id**.</span></span>

    static void MonitorBulkManifest(string manifestID)
    {
       bool bContinue = true;
       while (bContinue)
       {
          CloudMediaContext context = GetContext();
          IIngestManifest manifest = context.IngestManifests.Where(m => m.Id == manifestID).FirstOrDefault();

          if (manifest != null)
          {
             lock(consoleWriteLock)
             {
                Console.WriteLine("\nWaiting on all file uploads.");
                Console.WriteLine("PendingFilesCount  : {0}", manifest.Statistics.PendingFilesCount);
                Console.WriteLine("FinishedFilesCount : {0}", manifest.Statistics.FinishedFilesCount);
                Console.WriteLine("{0}% complete.\n", (float)manifest.Statistics.FinishedFilesCount / (float)(manifest.Statistics.FinishedFilesCount + manifest.Statistics.PendingFilesCount) * 100);

                if (manifest.Statistics.PendingFilesCount == 0)
                {
                   Console.WriteLine("Completed\n");
                   bContinue = false;
                }
             }

             if (manifest.Statistics.FinishedFilesCount < manifest.Statistics.PendingFilesCount)
                Thread.Sleep(60000);
          }
          else // Manifest is null
             bContinue = false;
       }
    }



## <a name="upload-files-using-net-sdk-extensions"></a><span data-ttu-id="e8d82-184">.NET SDK uzantıları kullanarak dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="e8d82-184">Upload files using .NET SDK Extensions</span></span>
<span data-ttu-id="e8d82-185">tek bir tooupload nasıl dosya .NET SDK uzantıları kullanarak Hello örnekte gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-185">hello example below shows how tooupload a single file using .NET SDK Extensions.</span></span> <span data-ttu-id="e8d82-186">Bu durumda hello **CreateFromFile** yöntemi kullanılır, ancak hello zaman uyumsuz sürümü de kullanılabilir (**CreateFromFileAsync**).</span><span class="sxs-lookup"><span data-stu-id="e8d82-186">In this case hello **CreateFromFile** method is used, but hello asynchronous version is also available (**CreateFromFileAsync**).</span></span> <span data-ttu-id="e8d82-187">Merhaba **CreateFromFile** yöntemi hello dosya adı, şifreleme seçeneği ve bir geri çağırma sırası tooreport hello içinde karşıya hello dosya ilerlemesini belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8d82-187">hello **CreateFromFile** method lets you specify hello file name, encryption option, and a callback in order tooreport hello upload progress of hello file.</span></span>

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

<span data-ttu-id="e8d82-188">Merhaba aşağıdaki örnek UploadFile işlevi çağırır ve depolama şifrelemesi hello varlık oluşturma seçeneği olarak belirtir.</span><span class="sxs-lookup"><span data-stu-id="e8d82-188">hello following example calls UploadFile function and specifies storage encryption as hello asset creation option.</span></span>  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a><span data-ttu-id="e8d82-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8d82-189">Next steps</span></span>

<span data-ttu-id="e8d82-190">Karşıya yüklenen varlıklarınızı artık kodlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8d82-190">You can now encode your uploaded assets.</span></span> <span data-ttu-id="e8d82-191">Daha fazla bilgi için bkz. [Varlıkları kodlama](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="e8d82-191">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="e8d82-192">Azure işlevleri tootrigger yapılandırılmış hello kapsayıcısında ulaşan bir dosyayı temel bir kodlama işi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8d82-192">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="e8d82-193">Daha fazla bilgi için [bu örneğe](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) bakın.</span><span class="sxs-lookup"><span data-stu-id="e8d82-193">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="e8d82-194">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="e8d82-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e8d82-195">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="e8d82-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="e8d82-196">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="e8d82-196">Next step</span></span>
<span data-ttu-id="e8d82-197">Bir varlığı karşıya yüklediğiniz göre tooMedia Hizmetleri Git toohello [nasıl tooGet medya işlemcisi] [ How tooGet a Media Processor] konu.</span><span class="sxs-lookup"><span data-stu-id="e8d82-197">Now that you have uploaded an asset tooMedia Services, go toohello [How tooGet a Media Processor][How tooGet a Media Processor] topic.</span></span>

[How tooGet a Media Processor]: media-services-get-media-processor.md

