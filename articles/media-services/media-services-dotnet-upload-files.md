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
# <a name="upload-files-into-a-media-services-account-using-net"></a>.NET kullanarak bir Media Services hesabına dosya yükleme
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

Media Services’de, dijital dosyalar bir varlığa yüklenir (veya alınır). Merhaba **varlık** varlık içerebilir video, ses, görüntüler, küçük resim koleksiyonları, metin parçaları ve kapalı açıklamalı alt yazı dosyaları (ve bu dosyalar hakkında hello meta veriler.)  Hello dosyalar yüklendiğinde, içeriğiniz sonraki işleme ve akışla için hello bulutta güvenli bir şekilde depolanır.

Merhaba varlık Hello dosyalarında çağrılır **varlık dosyaları**. Merhaba **AssetFile** örneği ve hello gerçek medya dosyası olan iki farklı nesneler. Merhaba medya dosyası hello gerçek medya içeriği içerirken hello AssetFile örneği hello medya dosyası hakkındaki meta verileri içerir.

> [!NOTE]
> ilgili önemli noktalar aşağıdaki hello Uygula:
> 
> * Media Services URL'leri içeriği (örneğin, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) akış Merhaba oluştururken hello hello IAssetFile.Name özellik değerini kullanır Bu nedenle, yüzde kodlama izin verilmiyor. Merhaba hello değerini **adı** özelliği hello aşağıdakilerden herhangi birini içeremez [yüzde kodlama-ayrılmış karakterleri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Ayrıca, yalnızca bir olabilir '.' hello dosya adı uzantısı için.
> * Merhaba hello adının uzunluğu 260 karakterden uzun olmamalıdır.
> * Media Services işlemek için desteklenen bir toohello en büyük dosya boyutu sınırı yoktur. Lütfen bakın [bu](media-services-quotas-and-limitations.md) hello dosya boyutu sınırlaması hakkında ayrıntılı bilgi için konu.
> * Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.
> 

Varlıklar oluşturduğunuzda, şifreleme seçenekleri aşağıdaki hello belirtebilirsiniz. 

* **Hiçbiri**: Şifreleme kullanılmaz. Merhaba varsayılan değer budur. Bu seçenek kullanıldığında, içeriğinizin aktarım veya deposunda kalan korunmadığını unutmayın.
  Aşamalı indirme kullanarak toodeliver bir MP4 planlıyorsanız, bu seçeneği kullanın. 
* **CommonEncryption** -zaten şifrelenmiş ve ortak şifreleme veya PlayReady DRM (örneğin, ile korunan kesintisiz akış PlayReady DRM) ile korunan içerik yüklüyorsanız bu seçeneği kullanın.
* **EnvelopeEncrypted** – AES ile şifrelenmiş HLS yüklüyorsanız bu seçeneği kullanın. Hello dosyaları gerekir alınan kodlanmış ve Transform Manager tarafından şifrelenmiş olduğunu unutmayın.
* **StorageEncrypted** - Temizle içeriğinizi yerel olarak AES 256 bit şifreleme kullanarak şifreler ve tooAzure depolanır depolama şifrelenen yükler. Depolama şifrelemesi ile korunan varlıklar otomatik olarak şifrelenmemiş ve bir şifrelenmiş dosya sistemi önceki tooencoding ve yeni bir çıkış varlığı olarak geri isteğe bağlı olarak yeniden şifrelenmiş önceki toouploading yerleştirilir. Depolama şifrelemesinin birincil kullanım durumu hello yüksek kaliteli giriş medya dosyalarınızın güçlü şifrelemeyle diskte rest toosecure istediğiniz durumdur.
  
    Media Services değil üzerinden dijital hak Yöneticisi (DRM) gibi hat varlıklarınızı için disk üzerinde depolama şifreleme sağlar.
  
    Şifrelenmiş depolama varlığınız olması durumunda, varlık teslim ilkesini yapılandırmanız gerekir. Daha fazla bilgi için bkz: [varlık teslim ilkesini yapılandırma](media-services-dotnet-configure-asset-delivery-policy.md).

Varlık toobe ile şifrelenmiş için belirtirseniz bir **CommonEncrypted** seçeneği veya bir **EnvelopeEncypted** seçeneği, varlıkla tooassociate gerekir bir **ContentKey**. Daha fazla bilgi için bkz: [nasıl toocreate bir ContentKey](media-services-dotnet-create-contentkey.md). 

Varlık toobe ile şifrelenmiş için belirtirseniz bir **StorageEncrypted** seçeneği, .NET oluşturacak için Media Services SDK'sı hello bir **StorateEncrypted** **ContentKey** için varlık.

Bu konu, nasıl toouse medya hizmetleri gösterir Media Services .NET SDK uzantıları tooupload dosyalarıyla Media Services varlık yanı sıra .NET SDK.

## <a name="upload-a-single-file-with-media-services-net-sdk"></a>Media Services .NET SDK'sı ile tek bir dosyayı karşıya yükleme
Aşağıdaki örnek kodu Hello .NET SDK'sı tooupload tek bir dosya kullanır. Merhaba AccessPolicy ve Bulucu oluşturulur ve hello karşıya yükleme işlevi tarafından yok. 


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


## <a name="upload-multiple-files-with-media-services-net-sdk"></a>Media Services .NET SDK'sı ile birden çok dosya karşıya yükleme
kodun gösterdiği nasıl aşağıdaki hello toocreate bir varlık ve birden çok dosya karşıya yükleme.

Merhaba kod aşağıdaki hello:

* Merhaba önceki adımda tanımlanan hello CreateEmptyAsset yöntemi kullanarak boş bir varlık oluşturur.
* Oluşturur bir **AccessPolicy** hello izinler ve erişim toohello varlık süresini tanımlayan örnek.
* Oluşturur bir **Bulucu** erişim toohello varlık sağlar örneği.
* Oluşturur bir **BlobTransferClient** örneği. Bu tür Azure BLOB'hello üzerinde çalıştığı bir istemci temsil eder. Bu örnekte hello istemci toomonitor hello karşıya yükleme işlemini kullanın. 
* Merhaba belirtilen dizindeki dosyaları aracılığıyla numaralandırır ve oluşturan bir **AssetFile** her dosya için örneği.
* Karşıya dosya hello kullanarak Media Services hello **UploadAsync** yöntemi. 

> [!NOTE]
> Merhaba çağrıları engellemediğini ve paralel olarak karşıya yüklenen hello dosyaların hello UploadAsync yöntemi tooensure kullanın.
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



Çok sayıda varlıklar karşıya yüklenirken hello aşağıdakileri göz önünde bulundurun.

* Yeni bir **CloudMediaContext** iş parçacığı başına nesne. Merhaba **CloudMediaContext** sınıfı iş parçacığı içinde korumalı değil.
* 2 tooa daha yüksek değer 5 gibi hello varsayılan değerinden NumberOfConcurrentTransfers artırın. Bu özelliği ayarlamak etkiler tüm örneklerini **CloudMediaContext**. 
* ParallelTransferThreadCount 10 hello varsayılan değeri koruyun.

## <a id="ingest_in_bulk"></a>Varlıklar Media Services .NET SDK kullanarak toplu alma
Büyük varlık dosyaları karşıya yükleme varlık oluşturma sırasında bir performans sorunu olabilir. Varlıklar toplu ya da "Toplu alma" alanını, varlık oluşturma hello karşıya yükleme işleminden kesilmesi içerir. toouse bir toplu ingesting yaklaşım hello varlık ve ilişkili dosyalarını açıklayan bir bildirimi (IngestManifest) oluşturun. Ardından, seçim tooupload hello ilişkili dosyaları toohello bildirim blob kapsayıcısının hello karşıya yükleme yöntemini kullanın. Microsoft Azure Media Services ile Merhaba bildirimini ilişkili hello blob kapsayıcısı izler. Bir dosyayı karşıya yüklenen toohello blob kapsayıcısı olduğunda, Microsoft Azure Media Services hello varlık oluşturma (IngestManifestAsset) hello bildiriminde hello varlık hello yapılandırmasına dayalı tamamlar.

toocreate yeni IngestManifest hello hello CloudMediaContext IngestManifests koleksiyonunda tarafından sunulan hello Create yöntemini çağırın. Bu yöntem, sağladığınız hello bildirim adıyla yeni IngestManifest oluşturur.

    IIngestManifest manifest = context.IngestManifests.Create(name);

Merhaba toplu IngestManifest ile ilişkilendirilecek hello varlıklar oluşturun. Toplu alma için hello varlık üzerinde istenen hello şifreleme seçeneklerini yapılandırın.

    // Create hello assets that will be associated with this bulk ingest manifest
    IAsset destAsset1 = _context.Assets.Create(name + "_asset_1", AssetCreationOptions.None);
    IAsset destAsset2 = _context.Assets.Create(name + "_asset_2", AssetCreationOptions.None);

Bir IngestManifestAsset toplu alma için bir toplu IngestManifest bir varlık ilişkilendirir. Ayrıca, hello her varlık yapacak AssetFiles ilişkilendirir. toocreate bir IngestManifestAsset hello sunucu içeriğine hello Create yöntemini kullanın.

Merhaba aşağıdaki örnek toohello toplu daha önce oluşturduğunuz hello iki varlıklar ilişkilendirmek ekleme iki yeni IngestManifestAssets bildirim alma gösterir. Her IngestManifestAsset toplu alma sırasında yüklenecek dosyaları her varlık için bir dizi de ilişkilendirir.  

    string filename1 = _singleInputMp4Path;
    string filename2 = _primaryFilePath;
    string filename3 = _singleInputFilePath;

    IIngestManifestAsset bulkAsset1 =  manifest.IngestManifestAssets.Create(destAsset1, new[] { filename1 });
    IIngestManifestAsset bulkAsset2 =  manifest.IngestManifestAssets.Create(destAsset2, new[] { filename2, filename3 });

Merhaba varlık dosyaları toohello blob depolama kapsayıcısını hello tarafından sağlanan URI karşıya yükleme özellikli tüm yüksek hızlı istemci uygulaması kullanabilirsiniz **IIngestManifest.BlobStorageUriForUpload** hello IngestManifest özelliği. Bir önem düzeyindeki yüksek hızlı karşıya yükleme hizmeti [Aspera istendiğinde Azure uygulaması için](https://datamarket.azure.com/application/2cdbc511-cb12-4715-9871-c7e7fbbb82a6). Aşağıdaki kod örneğine hello gösterildiği gibi tooupload hello varlıklar dosyaları da kod yazabilirsiniz.

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

Bu konuda kullanılan hello örnek hello varlık dosyaları karşıya yükleme için hello kodu aşağıdaki kod örneğine hello gösterilir.

    UploadBlobFile(manifest.BlobStorageUriForUpload, filename1);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename2);
    UploadBlobFile(manifest.BlobStorageUriForUpload, filename3);


İle ilişkili tüm varlıklar için toplu hello alma hello ilerlemesini belirlemek bir **IngestManifest** hello hello istatistikleri özelliği yoklayarak **IngestManifest**. Sipariş tooupdate ilerleme durumu bilgileri yeni bir kullanmalısınız **CloudMediaContext** her zaman hello istatistikleri özelliği yoklamak.

Merhaba aşağıdaki örnekte bir IngestManifest tarafından yoklama gösterir, **kimliği**.

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



## <a name="upload-files-using-net-sdk-extensions"></a>.NET SDK uzantıları kullanarak dosyaları karşıya yükleme
tek bir tooupload nasıl dosya .NET SDK uzantıları kullanarak Hello örnekte gösterilir. Bu durumda hello **CreateFromFile** yöntemi kullanılır, ancak hello zaman uyumsuz sürümü de kullanılabilir (**CreateFromFileAsync**). Merhaba **CreateFromFile** yöntemi hello dosya adı, şifreleme seçeneği ve bir geri çağırma sırası tooreport hello içinde karşıya hello dosya ilerlemesini belirtmenize olanak sağlar.

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

Merhaba aşağıdaki örnek UploadFile işlevi çağırır ve depolama şifrelemesi hello varlık oluşturma seçeneği olarak belirtir.  

    var asset = UploadFile(@"C:\VideoFiles\BigBuckBunny.mp4", AssetCreationOptions.StorageEncrypted);

## <a name="next-steps"></a>Sonraki adımlar

Karşıya yüklenen varlıklarınızı artık kodlayabilirsiniz. Daha fazla bilgi için bkz. [Varlıkları kodlama](media-services-portal-encode.md).

Azure işlevleri tootrigger yapılandırılmış hello kapsayıcısında ulaşan bir dosyayı temel bir kodlama işi de kullanabilirsiniz. Daha fazla bilgi için [bu örneğe](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ) bakın.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Sonraki adım
Bir varlığı karşıya yüklediğiniz göre tooMedia Hizmetleri Git toohello [nasıl tooGet medya işlemcisi] [ How tooGet a Media Processor] konu.

[How tooGet a Media Processor]: media-services-get-media-processor.md

