---
title: "aaaDevelop Media Services ile Azure işlevleri"
description: "Bu konu, nasıl Azure portal ile Media Services'i kullanarak Azure işlevleri geliştirme toostart hello gösterir."
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
ms.openlocfilehash: 3b2c2fb498fea399c862dfbdb63033d06cabf6d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#<a name="develop-azure-functions-with-media-services"></a>Azure işlevleri Media Services ile geliştirme

Bu konuda tooget Media Services'i kullanma Azure işlevleri oluşturma ile çalışmaya nasıl gösterilmektedir. Hello Azure Bu konu başlığı altında tanımlanan işlevi izler adlı bir depolama hesabı kapsayıcısının **giriş** yeni MP4 dosyaları için. Bir dosya hello depolama kapsayıcıya bırakılan sonra hello blob tetikleyici hello işlevi yürütülür.

Tooexplore istediğiniz ve Azure Media Services'i kullanma mevcut Azure işlevleri dağıtırsanız, kullanıma [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration). Bu depo, Media Services tooshow iş akışları ilgili tooingesting doğrudan blob depolama alanından tooblob depolama kodlama ve içeriği yazma geri içerik kullanma örnekleri içerir. Ayrıca nasıl toomonitor iş Web kancaları ve Azure kuyruklar üzerinden bildirimleri örnekleri içerir. İşlevlerinizi hello hello örneklerde göre de geliştirebilirsiniz [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration) deposu. toodeploy hello İşlevler, basın hello **tooAzure dağıtmak** düğmesi.

## <a name="prerequisites"></a>Ön koşullar

- İlk işlevinizin oluşturmadan önce toohave etkin bir Azure hesabı gerekir. Bir Azure hesabınız yoksa [ücretsiz hesaplar kullanılabilir](https://azure.microsoft.com/free/).
- Azure Media Services (AMS) hesabınızdaki eylemleri gerçekleştirmek ya da Media Services tarafından gönderilen tooevents dinleme toocreate Azure işlevleri kullanacaksanız açıklandığı gibi bir AMS hesabının oluşturmalısınız [burada](media-services-portal-create-account.md).
- Anlayış [nasıl toouse Azure işlevleri](../azure-functions/functions-overview.md). Ayrıca, gözden geçirin:
    - [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-triggers-bindings.md)
    - [Nasıl tooconfigure Azure işlevi uygulama ayarları](../azure-functions/functions-how-to-use-azure-function-app-settings.md)
    
## <a name="considerations"></a>Dikkat edilmesi gerekenler

-  Merhaba tüketim plan altında çalışan azure işlevlerinin 5 dakika zaman aşımı sınırı yoktur.

## <a name="create-a-function-app"></a>İşlev uygulaması oluşturma

1. Toohello Git [Azure portal](http://portal.azure.com) ve Azure hesabınız ile oturum açın.
2. Açıklandığı gibi işlev uygulaması oluşturma [burada](../azure-functions/functions-create-function-app-portal.md).

>[!NOTE]
> Hello belirttiğiniz bir depolama hesabı **StorageConnection** ortam değişkeni hello olmalıdır (Merhaba sonraki adıma bakın), uygulamanızın aynı bölgede.

## <a name="configure-function-app-settings"></a>İşlev uygulaması ayarlarını yapılandır

Media Services işlevleri geliştirme işlevlerinizi kullanılan kullanışlı tooadd ortam değişkenleri olur. tooconfigure uygulama ayarları, hello uygulama ayarlarını yapılandır bağlantısını tıklatın. Daha fazla bilgi için bkz: [nasıl tooconfigure Azure işlevi uygulama ayarları](../azure-functions/functions-how-to-use-azure-function-app-settings.md). 

Örneğin:

![Ayarlar](./media/media-services-azure-functions/media-services-azure-functions001.png)

Bu makalede, tanımlanan hello işlevi uygulama ayarlarınızı ortam değişkenleri aşağıdaki hello olduğu varsayılır:

**AMSAccount** : *AMS hesabının adını* (örneğin testams)

**AMSKey** : *AMS hesap anahtarı* (örneğin IHOySnH + XX3LGPfraE5fKPl0EnzvEPKkOPKCr59aiMM =)

**MediaServicesStorageAccountName** : *depolama hesabı adı* (örn., testamsstorage)

**MediaServicesStorageAccountKey** : *depolama hesabı anahtarı* (örn., xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXXX ==)

**StorageConnection** : *depolama bağlantısı* (örn., DefaultEndpointsProtocol = https; AccountName = testamsstorage; AccountKey xx7RN7mvpcipkuXvn5g7jwxnKh5MwYQ/awZAzkSIxQA8tmCtn93rqobjgjt41Wb0zwTZWeWQHY5kSZF0XXXXX = ==)

## <a name="create-a-function"></a>İşlev oluşturma

İşlev Uygulamanız dağıtıldıktan sonra onu arasında bulabilirsiniz **uygulama hizmetleri** Azure işlevleri.

1. İşlev uygulamanızı seçin ve'ı tıklatın **yeni işlev**.
2. Merhaba seçin **C#** dil ve **veri işleme** senaryo.
3. Seçin **BlobTrigger** şablonu. Blob hello karşıya olduğunda bu işlev tetiklenen **giriş** kapsayıcı. Merhaba **giriş** adı hello belirtilen **yolu**, hello sonraki adımda.

    ![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions004.png)

4. Seçtiğinizde, bundan sonra **BlobTrigger**, daha fazla bazı denetimler hello sayfasında görünür.

    ![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions005.png)

4. **Oluştur**'a tıklayın. 


## <a name="files"></a>Dosyalar

Azure işlevinizi ve bu bölümde açıklanan diğer dosyaları kod dosyaları ile ilişkilidir. Varsayılan olarak, bir işlev ilişkili olduğu **function.json** ve **run.csx** (C#) dosyaları. Tooadd ihtiyacınız olacak bir **project.json** dosya. Bu bölümde Hello kalan hello tanımlarını bu dosyalar için gösterir.

![Dosyaları](./media/media-services-azure-functions/media-services-azure-functions003.png)

### <a name="functionjson"></a>Function.JSON

Merhaba function.json dosyası hello işlev bağlamaları ve diğer yapılandırma ayarlarını tanımlar. Bu dosya toodetermine hello olayları toomonitor ve yürütme toopass verisine ve dönüş verileri nasıl işlev Hello çalışma zamanı kullanır. Daha fazla bilgi için bkz: [Azure işlevleri HTTP ve Web kancası bağlamaları](../azure-functions/functions-reference.md#function-code).

>[!NOTE]
>Set hello **devre dışı** özelliği çok**true** çalıştırılmasını tooprevent hello işlevi. 


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

Merhaba project.json dosyası bağımlılıkları içerir. Bir örneği burada verilmiştir **project.json** gerekli hello .NET Azure Media Services içeren dosyası Nuget'ten paketler. Hello en son sürümleri onaylamalısınız şekilde hello sürüm numaraları toohello paketleri, en son güncelleştirmeleri ile değiştirmek olduğunu unutmayın. 

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

Bu hello C# işlevinizi kodudur.  Merhaba işlevi adlı bir depolama hesabı kapsayıcısının izleyiciler tanımlanan **giriş** (ne hello yolunda belirtilen olan) yeni MP4 dosyaları için. Bir dosya hello depolama kapsayıcıya bırakılan sonra hello blob tetikleyici hello işlevi yürütülür.
    
Bu bölümde tanımlanan hello örnek gösterir 

1. nasıl tooingest bir varlığa bir medya hizmetleri hesabı (bir blobu bir AMS varlığa kopyalamayı göre) ve 
2. nasıl toosubmit Medya Kodlayıcısı standart 's "Uyarlamalı akış" kullanan bir kodlama işi hazır.

Merhaba gerçek hayatta senaryosunda, büyük olasılıkla tootrack ilerleyişini istediğiniz ve kodlanmış Varlığınızı yayımlayın. Daha fazla bilgi için bkz: [kullanım Azure Web Kancalarını toomonitor Media Services iş bildirimleri](media-services-dotnet-check-job-progress-with-webhooks.md). Daha fazla örnek için bkz: [medya Hizmetleri Azure işlevleri](https://github.com/Azure-Samples/media-services-dotnet-functions-integration).  

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
        // NOTE that hello variables {fileName} here come from hello path setting in function.json
        // and are passed into hello  Run method signature above. We can use this toomake decisions on what type of file
        // was dropped into hello input container for hello function. 

        // No need toodo any Retry strategy in this function, By default, hello SDK calls a function up too5 times for a 
        // given blob. If hello fifth try fails, hello SDK adds a message tooa queue named webjobs-blobtrigger-poison.

        log.Info($"C# Blob trigger function processed: {fileName}.mp4");
        log.Info($"Using Azure Media Services account : {_mediaServicesAccountName}");


        try
        {
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(
                _mediaServicesAccountName,
                _mediaServicesAccountKey);

        // Used hello chached credentials toocreate CloudMediaContext.
        _context = new CloudMediaContext(_cachedCredentials);

        // Step 1:  Copy hello Blob into a new Input Asset for hello Job
        // ***NOTE: Ideally we would have a method tooingest a Blob directly here somehow. 
        // using code from this sample - https://azure.microsoft.com/en-us/documentation/articles/media-services-copying-existing-blob/

        StorageCredentials mediaServicesStorageCredentials =
            new StorageCredentials(_storageAccountName, _storageAccountKey);

        IAsset newAsset = CreateAssetFromBlob(myBlob, fileName, log).GetAwaiter().GetResult();

        // Step 2: Create an Encoding Job

        // Declare a new encoding job with hello Standard encoder
        IJob job = _context.Jobs.Create("Azure Function - MES Job");

        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Create a task with hello encoding details, using a custom preset
        ITask task = job.Tasks.AddNew("Encode with Adaptive Streaming",
            processor,
            "Adaptive Streaming",
            TaskOptions.None); 

        // Specify hello input asset toobe encoded.
        task.InputAssets.Add(newAsset);

        // Add an output asset toocontain hello results of hello job. 
        // This output is specified as AssetCreationOptions.None, which 
        // means hello output asset is not encrypted. 
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
    /// Creates a new asset and copies blobs from hello specifed storage account.
    /// </summary>
    /// <param name="blob">hello specified blob.</param>
    /// <returns>hello new asset.</returns>
    public static async Task<IAsset> CreateAssetFromBlobAsync(CloudBlockBlob blob, string assetName, TraceWriter log)
    {
         //Get a reference toohello storage account that is associated with hello Media Services account. 
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

        // Get hello destination asset container reference
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

        // Get hold of hello destination blob
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

tootest, işlevi bir MP4 dosyası hello tooupload gerek **giriş** hello bağlantı dizesinde belirtilen depolama hesabının hello kapsayıcı.  

## <a name="next-step"></a>Sonraki adım

Bu noktada, Media Services uygulama geliştirme hazır toostart var. 
 
Daha fazla ayrıntı ve Azure işlevleri ve Logic Apps ile Azure Media Services toocreate özel içerik oluşturma iş akışı kullanarak tam örnekleri/çözümleri için hello bkz [Media Services .NET işlevleri tümleştirme örnek github'da](https://github.com/Azure-Samples/media-services-dotnet-functions-integration)

Ayrıca bkz [kullanım Azure Web Kancalarını toomonitor Media Services .NET ile bildirimleri iş](media-services-dotnet-check-job-progress-with-webhooks.md). 

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

