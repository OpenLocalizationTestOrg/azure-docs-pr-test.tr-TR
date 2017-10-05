---
title: "Azure işlevleri Media Services ile geliştirme"
description: "Bu konu Azure işlevleri Media Services ile geliştirmeye başlamak Azure portalını kullanarak gösterilmiştir."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 51bdcb01-1846-4e1f-bd90-70020ab471b0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/21/2017
ms.author: juliako
ms.openlocfilehash: 35d539855572fef6c00de614a4e57738a8abd075
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
#<a name="develop-azure-functions-with-media-services"></a>Azure işlevleri Media Services ile geliştirme

Bu konu, Media Services'i kullanma Azure işlevleri oluşturmaya başlamak gösterilmiştir. Bu konu başlığı altında tanımlanan Azure işlevi adlı bir depolama hesabı kapsayıcısının izler **giriş** yeni MP4 dosyaları için. Bir dosya depolama kapsayıcıya bırakılan sonra blob tetikleyici işlevi yürütülür.

Keşfetmek ve Azure Media Services'i kullanma mevcut Azure işlevleri dağıtmak istiyorsanız, kullanıma [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Bu depo alma için ilgili iş akışları doğrudan blob depolama alanından blob depolama alanına kodlama ve içeriği yazma geri içeriğini göstermek için Media Services'i kullanma örnekleri içerir. Ayrıca Web kancaları ve Azure kuyrukları aracılığıyla iş bildirimleri izleme örnekleri içerir. İşlevlerinizi örneklerde göre de geliştirebilirsiniz [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) deposu. İşlevler dağıtmak için basın **Azure'a Dağıt** düğmesi.

## <a name="prerequisites"></a>Ön koşullar

- İlk işlevinizin oluşturmadan önce etkin bir Azure hesabınız olması gerekir. Bir Azure hesabınız yoksa [ücretsiz hesaplar kullanılabilir](https://azure.microsoft.com/free/).
- Azure Media Services (AMS) hesabınızdaki eylemleri gerçekleştirmek veya Media Services tarafından gönderilen olayları dinleme Azure işlevleri oluşturmak için kullanacaksanız, açıklandığı gibi bir AMS hesabının oluşturmalısınız [burada](media-services-portal-create-account.md).
- Anlayış [Azure işlevlerinin nasıl kullanılacağı](../azure-functions/functions-overview.md). Ayrıca, gözden geçirin:
    - [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-triggers-bindings.md)
    - [Azure işlevi uygulama ayarlarının nasıl yapılandırılacağı](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Dikkat edilmesi gerekenler

-  Tüketim plan altında çalışan azure işlevlerinin 5 dakika zaman aşımı sınırı yoktur.

## <a name="create-a-function-app"></a>İşlev uygulaması oluşturma

1. [Azure portalına](http://portal.azure.com) gidip Azure hesabınızla oturum açın.
2. Açıklandığı gibi işlev uygulaması oluşturma [burada](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Belirttiğiniz bir depolama hesabı **StorageConnection** ortam değişkeni, uygulamanız ile aynı bölgede olmalıdır (sonraki adıma bakın).

## <a name="configure-function-app-settings"></a>İşlev uygulaması ayarlarını yapılandır

Media Services işlevleri geliştirirken işlevlerinizi kullanılan ortam değişkenleri eklemek için kullanışlıdır. Uygulama ayarlarını yapılandırmak için uygulama ayarlarını yapılandır bağlantısına tıklayın. Daha fazla bilgi için bkz: [Azure işlevi uygulama ayarlarının nasıl yapılandırılacağı](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

Örneğin:

![Ayarlar](./media/media-services-azure-functions/media-services-azure-functions001.png)

Bu makalede, tanımlanmış işlevi, aşağıdaki ortam değişkenleri, uygulama ayarlarınızı olduğu varsayılır:

**AMSAccount** : *AMS hesabının adını* (örneğin testams)

**AMSKey** : *AMS hesap anahtarı* (örneğin IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)

**MediaServicesStorageAccountName** : *depolama hesabı adı* (örn., testamsstorage)

**MediaServicesStorageAccountKey** : *depolama hesabı anahtarı* (örn., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)

**StorageConnection** : *depolama bağlantısı* (örn., DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX = ==)

## <a name="create-a-function"></a>İşlev oluşturma

İşlev Uygulamanız dağıtıldıktan sonra onu arasında bulabilirsiniz **uygulama hizmetleri** Azure işlevleri.

1. İşlev uygulamanızı seçin ve'ı tıklatın **yeni işlev**.
2. Seçin **C#** dil ve **veri işleme** senaryo.
3. Seçin **BlobTrigger** şablonu. Bir blob hizmetine yüklendikten olduğunda bu işlev tetiklenen **giriş** kapsayıcı. **Giriş** adı belirtilen **yolu**, sonraki adımda.

    ![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. Seçtiğinizde, bundan sonra **BlobTrigger**, daha fazla bazı denetimler sayfasında görünür.

    ![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. **Oluştur**'a tıklayın. 


## <a name="files"></a>Dosyalar

Azure işlevinizi ve bu bölümde açıklanan diğer dosyaları kod dosyaları ile ilişkilidir. Varsayılan olarak, bir işlev ilişkili olduğu **function.json** ve **run.csx** (C#) dosyaları. Eklemeniz gerekir bir **project.json** dosya. Bu bölümün geri kalanında bu dosyaları tanımlarında gösterir.

![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>Function.JSON

Function.json dosyası, işlev bağlamaları ve diğer yapılandırma ayarlarını tanımlar. Çalışma zamanı izlenecek olaylar belirlemek için bu dosyaya ve verilerini geçirin ve işlev yürütülmesini veri dönmek nasıl kullanır. Daha fazla bilgi için bkz: [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Ayarlama **devre dışı** özelliğine **true** işlevi çalıştırılmasını engellemek için. 


Bir örneği burada verilmiştir **function.json** dosya.

    {
    "bindings": [
      {
        "name": "myBlob",
        "type": "blobTrigger",
        "direction": "in",
        "path": "input/{fileName}.mp4",
        "connection": "StorageConnection"
      }
    ],
    "disabled": false
    }

### <a name="projectjson"></a>Project.JSON

Project.json dosyası bağımlılıkları içerir. Bir örneği burada verilmiştir **project.json** Nuget gerekli .NET Azure Media Services'i paketlerinden içeren dosya. Sürüm numaraları, en son sürümleri onaylamanız böylece paketler için en son güncelleştirmeleri ile değişir unutmayın. 

    {
      "frameworks": {
        "net46":{
          "dependencies": {
        "windowsazure.mediaservices": "3.8.0.5",
        "windowsazure.mediaservices.extensions": "3.8.0.3"
          }
        }
       }
    }
    
### <a name="runcsx"></a>Run.csx

C# kodunu işlevinizi budur.  İşlevi izleyiciler adlı bir depolama hesabı kapsayıcısının tanımlanan **giriş** (ne yolu belirtildi olan) yeni MP4 dosyaları için. Bir dosya depolama kapsayıcıya bırakılan sonra blob tetikleyici işlevi yürütülür.
    
Bu bölümde tanımlanan örnek gösterir 

1. bir Media Services hesabına (blob bir AMS varlığa kopyalamayı tarafından) varlık alma konusunda ve 
2. bir kodlama işi göndermek için Medya Kodlayıcısı standart 's kullanan nasıl "Uyarlamalı akış" hazır.

Gerçek Hayatta senaryosunda, büyük olasılıkla iş ilerleme durumunu izlemek ve kodlanmış Varlığınızı yayımlamak istediğiniz. Daha fazla bilgi için bkz: [kullanım Azure Media Services iş bildirimleri izlemek için Web kancası](media-services-dotnet-check-job-progress-with-webhooks.md). Daha fazla örnek için bkz: [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

Tamamladıktan sonra işlevinizi tanımlama tıklatın **kaydedip çalıştırın**.

    #r "Microsoft.WindowsAzure.Storage"
    #r "Newtonsoft.Json"
    #r "System.Web"

    using System;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Net;
    using System.Threading;
    using System.Threading.Tasks;
    using System.IO;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Auth;

    private static readonly string _mediaServicesAccountName = Environment.GetEnvironmentVariable("AMSAccount");
    private static readonly string _mediaServicesAccountKey = Environment.GetEnvironmentVariable("AMSKey");

    static string _storageAccountName = Environment.GetEnvironmentVariable("MediaServicesStorageAccountName");
    static string _storageAccountKey = Environment.GetEnvironmentVariable("MediaServicesStorageAccountKey");

    private static CloudStorageAccount _destinationStorageAccount = null;

    // Field for service context.
    private static CloudMediaContext _context = null;
    private static MediaServicesCredentials _cachedCredentials = null;

    public static void Run(CloudBlockBlob myBlob, string fileName, TraceWriter log)
    {
        // NOTE that the variables {fileName} here come from the path setting in function.json
        // and are passed into the  Run method signature above. We can use this to make decisions on what type of file
        // was dropped into the input container for the function. 

        // No need to do any Retry strategy in this function, By default, the SDK calls a function up to 5 times for a 
        // given blob. If the fifth try fails, the SDK adds a message to a queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used the chached credentials to create CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy the Blob into a new Input Asset for the Job
        // ***NOTE: Ideally we would have a method to ingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with the Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with the encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify the input asset to be encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset to contain the results of the job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means the output asset is not encrypted. 
        task.OutputAssets.AddNew(fileName, AssetCreationOptions.None);

        job.Submit();
        log.Info("Job Submitted");

        }
        catch (Exception ex)
        {
        log.Error("ERROR: failed.");
        log.Info($"StackTrace : {ex.StackTrace}");
        throw ex;
        }
    }

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


    public static async Task<IAsset> CreateAssetFromBlob(CloudBlockBlob blob, string assetName, TraceWriter log){
        IAsset newAsset = null;

        try{
            Task<IAsset> copyAssetTask = CreateAssetFromBlobAsync(blob, assetName, log);
            newAsset = await copyAssetTask;
            log.Info($"Asset Copied : {newAsset.Id}");
        }
        catch(Exception ex){
            log.Info("Copy Failed");
            log.Info($"ERROR : {ex.Message}");
            throw ex;
        }

        return newAsset;
    }

    /// <summary>
    /// Creates a new asset and copies blobs from the specifed storage account.
    /// </summary>
    /// <param name="blob">The specified blob.</param>
    /// <returns>The new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference to the storage account that is associated with the Media Services account. 
        StorageCredentials mediaServicesStorageCredentials =
        new StorageCredentials(_storageAccountName, _storageAccountKey);
        _destinationStorageAccount = new CloudStorageAccount(mediaServicesStorageCredentials, false);

        // Create a new asset. 
        var asset = _context.Assets.Create(blob.Name, AssetCreationOptions.None);
        log.Info($"Created new asset {asset.Name}");

        IAccessPolicy writePolicy = _context.AccessPolicies.Create("writePolicy",
        TimeSpan.FromHours(4), AccessPermissions.Write);
        ILocator destinationLocator = _context.Locators.CreateLocator(LocatorType.Sas, asset, writePolicy);
        CloudBlobClient destBlobStorage = _destinationStorageAccount.CreateCloudBlobClient();

        // Get the destination asset container reference
        string destinationContainerName = (new Uri(destinationLocator.Path)).Segments[1];
        CloudBlobContainer assetContainer = destBlobStorage.GetContainerReference(destinationContainerName);

        try{
        assetContainer.CreateIfNotExists();
        }
        catch (Exception ex)
        {
        log.Error ("ERROR:" + ex.Message);
        }

        log.Info("Created asset.");

        // Get hold of the destination blob
        CloudBlockBlob destinationBlob = assetContainer.GetBlockBlobReference(blob.Name);

        // Copy Blob
        try
        {
        using (var stream = await blob.OpenReadAsync()) 
        {            
            await destinationBlob.UploadFromStreamAsync(stream);          
        }

        log.Info("Copy Complete.");

        var assetFile = asset.AssetFiles.Create(blob.Name);
        assetFile.ContentFileSize = blob.Properties.Length;
        assetFile.IsPrimary = true;
        assetFile.Update();
        asset.Update();
        }
        catch (Exception ex)
        {
        log.Error(ex.Message);
        log.Info (ex.StackTrace);
        log.Info ("Copy Failed.");
        throw;
        }

        destinationLocator.Delete();
        writePolicy.Delete();

        return asset;
    }
##<a name="test-your-function"></a>İşlevinizi test

İşlevinizi test etmek için bir MP4 dosyasına karşıya yüklemek gereken **giriş** bağlantı dizesinde belirtilen depolama hesabının kapsayıcı.  

## <a name="next-step"></a>Sonraki adım

Bu noktada, Media Services uygulama geliştirmeye başlamak hazırsınız. 
 
Daha fazla ayrıntı ve Azure işlevleri ve Logic Apps özel içerik oluşturma iş akışı oluşturmak üzere Azure Media Services ile kullanma tam örnekleri/çözümler için bkz: [Media Services .NET işlevleri tümleştirme örnek github'da](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Ayrıca bkz [.NET ile Media Services iş bildirimleri izlemek için kullanım Azure Kancalarını](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

