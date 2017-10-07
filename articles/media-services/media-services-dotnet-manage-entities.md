---
title: "aaaManaging varlıklar ve Media Services .NET SDK'sı ile ilgili varlıklar"
description: "Nasıl toomanage varlıklar ve ilişkili varlıklarla .NET için Media Services SDK'sı hello öğrenin."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 59a8543ffc6f7f30da2c67a6fcae09bc46da7a52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a>Varlıklar ve ilgili varlıklar Media Services .NET SDK'sı ile yönetme
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

Bu konu, nasıl toomanage Azure Media Services gösterir .NET olan varlık. 

>[!NOTE]
> Merhaba toplam kayıt sayısı hello en yüksek kota altında olsa bile 1 Nisan 2017 başlangıç 90 günden daha eski hesabınızda herhangi bir işi kaydının otomatik olarak, ilişkili görev kayıtlarını yanı sıra, silinir. Örneğin, 1 Nisan 2017 üzerinde 31 Aralık 2016'den daha eski hesabınızda herhangi bir işi kaydının otomatik olarak silinir. Tooarchive hello iş/görevi bilgiye ihtiyacınız varsa, bu konuda açıklanan hello kodu kullanabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md). 

## <a name="get-an-asset-reference"></a>Bir varlık başvurusu alın
Tooget başvuru tooan varolan varlık Media Services buna sık bir görevdir. Aşağıdaki kod örneğine hello nasıl bir varlık başvurusu hello sunucuda hello varlıklar koleksiyonundan bağlam nesnesi alabileceğiniz gösterir, aşağıdaki kod örneği kullanan bir varlık kimliği hello üzerinde temel LINQ Sorgu tooget başvuru tooan varolan IAsset nesnesi.

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query tooget an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference hello asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a>Tüm varlıklar listesi
Depolama alanına sahip varlıklar Hello sayısı arttıkça, yararlı toolist olan varlıklarınızı. Aşağıdaki kod örneğine hello nasıl tooiterate aracılığıyla hello varlıklar koleksiyonu hello sunucu context nesnesinde gösterir. Merhaba kod örneği, her varlık ile bazı özellik değerleri toohello konsolunda de yazar. Örneğin, her varlık birçok medya dosyaları içerebilir. Her varlık ile ilişkili tüm dosyalar çıkışı Hello kod örneğinde yazar.

    static void ListAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display hello collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display hello files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="get-a-job-reference"></a>Bir iş başvurusu alın

Media Services kod görevlerinde işleme ile çalışırken, aşağıdaki kod örneğine bir kimliği hello üzerinde göre başvuru tooan var olan bir işi nasıl tooget başvuru tooan IJob nesne hello işleri koleksiyonundan gösterir tooget genellikle gerekir.

Uzun süre çalışan kodlama işi başlatırken tooget iş başvuru gerekir ve bir iş parçacığında toocheck hello iş durumu gerekiyor. Bu gibi durumlarda, bir iş parçacığından Hello yöntemi geri döndüğünde tooretrieve yenilendi başvuru tooa iş gerekir.

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query tooget an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return hello job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a>Liste işler ve varlıklar
Önemli ilgili bir görevi ilişkili işlerini Media Services ile toolist varlıklar ' dir. Merhaba aşağıdaki kod örneği, nasıl gösterir toolist her IJob nesne ve daha sonra özellikleri hello iş, ilgili tüm görevler, tüm giriş varlıklar hakkında görüntüler her bir iş ve tüm varlıklar çıktı. Bu örnekteki Hello kod çok sayıda diğer görevler için yararlı olabilir. Örneğin, toolist hello çıkış önceden çalıştıran bir veya daha fazla kodlama işleri varlıklarından istiyorsanız, bu kodu nasıl tooaccess hello varlıklar çıktısını gösterir. Bir başvuru tooan çıkış varlığına sahip olduğunuzda, karşıdan veya URL'leri sağlama sonra hello içerik tooother kullanıcılar veya uygulamalar'i sunabilir. 

Varlık teslim etmek için seçenekleri hakkında daha fazla bilgi için bkz: [teslim varlıklar hello .NET için Media Services SDK'sı ile](media-services-deliver-streaming-content.md).

    // List all jobs on hello server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display hello collection of jobs on hello server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display hello associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display hello list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display hello list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="list-all-access-policies"></a>Tüm erişim ilkeleri listesi
Media Services'de bir varlık veya dosyalarından bir erişim ilkesi tanımlayabilirsiniz. Bir erişim ilkesi için bir dosya veya bir varlık (erişim hello süresi ve ne tür) hello izinleri tanımlar. Media Services kodunuzda, genellikle bir erişim ilkesi IAccessPolicy nesneyi oluşturarak ve var olan bir varlıkla ilişkilendirme tanımlarsınız. Ardından Media Services doğrudan erişim tooassets sağlamanıza olanak veren bir ILocator nesnesi oluşturun. Bu belge seri eşlik hello Visual Studio projesi nasıl toocreate ve ata erişim ilkeleri ve bulucular tooassets gösteren birkaç kod örnekleri içerir.

Kod örnekteki nasıl aşağıdaki hello toolist hello sunucuda ve izinleri gösterir hello türü tüm erişim ilkeleri her ile ilişkili. Başka bir kullanışlı bir yol tooview erişim ilkeleri toolist tüm ILocator hello sunucuda nesnedir ve ardından her Bulucu için onun ilişkili erişim ilkesi kendi AccessPolicy özelliğini kullanarak listeleyebilirsiniz.

    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
    
## <a name="limit-access-policies"></a>Sınır erişim ilkeleri 

>[!NOTE]
> Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için). Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri. 

Örneğin, yalnızca bir kez uygulamanızda çalıştırırsınız: koddan hello olan genel bir ilke kümesi oluşturabilirsiniz. Daha sonra kullanmak için kimlikleri tooa günlük dosyası kaydedebilirsiniz:

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

Daha sonra kodunuzda şöyle kimlikleri varolan hello kullanabilirsiniz:

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get hello standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get hello existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("hello locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a>Tüm Bulucular listesi
Bir Bulucu sağlayan doğrudan yolu tooaccess izinleri toohello varlık birlikte bir varlık hello Bulucu'nın ilişkili erişim ilkesi tarafından tanımlandığı şekilde bir URL'dir. Her varlık, kendi Bulucular özellikte ilişkili ILocator nesnelerinin bir koleksiyonu olabilir. Merhaba sunucu bağlamı da tüm bulucular içeren bir konum belirleyicisi koleksiyon sahiptir.

Merhaba aşağıdaki kod örneğinde hello sunucusundaki tüm bulucular listeler. Her Bulucu için hello kimliği hello ilgili varlık ve erişim ilkesi için gösterir. Ayrıca, izinler, hello sona erme tarihi ve hello tam yolu toohello varlık hello türünü görüntüler.

Bir Bulucu yolu tooan varlık yalnızca URL toohello bir temel varlık olduğuna dikkat edin. bir kullanıcı veya uygulama göz doğrudan yolu tooindividual dosyaları toocreate kodunuzu hello belirli dosya yolu toohello Bulucu yolu eklemeniz gerekir. Hakkında daha fazla bilgi için toodo buna ek olarak, bkz: hello konu [teslim varlıklar hello .NET için Media Services SDK'sı ile](media-services-deliver-streaming-content.md).

    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // hello locator path is hello base or parent path (with included permissions) tooaccess  
            // hello media content of an asset. toocreate a full URL tooa specific media file, take 
            // hello locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a>Varlıkları büyük koleksiyonlarına numaralandırma
Varlıkları sorgulanırken ortak REST v2 sorgu sonuçları too1000 sonuçları sınırladığından aynı anda döndürülen 1000 varlıkların bir sınırı yoktur. Toouse atlama ve alma varlıklar büyük koleksiyonlarına numaralandırılırken gerekir. 

Merhaba hello içindeki tüm hello işlere aşağıdaki işlevi döngüler Media Services hesabı sağlanan. Media Services 1000 işleri işleri koleksiyondaki döndürür. Merhaba işlevi atlayın ve toomake emin gerçekleştirin (1000'den fazla iş hesabınızı olması durumunda), tüm işleri numaralandırılır hale getirir.

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in hello Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

## <a name="delete-an-asset"></a>Bir varlığı silme
Aşağıdaki örnek hello bir varlığını siler.

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a>Bir işi Sil
bir iş toodelete hello hello durumu özelliğinde belirtildiği gibi hello iş durumunu denetlemeniz gerekir. İlk sıraya alınan, zamanlanan ya da işlem, gibi diğer bazı durumlarda işler iptal edildi ve bunlar daha sonra silinebilir tamamlandı veya iptal edilen işler silinebilir.

Merhaba aşağıdaki kod örneğinde iş durumlarını denetleme ve hello durumu tamamlandı ya da iptal edildiğinde sonra silerek bir işi silmek için bir yöntemi gösterir. Bu kod bir başvuru tooa işi almak için bu konunun önceki bölümde hello bağlıdır: bir iş başvurusu alın.

    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync toodo async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }


## <a name="delete-an-access-policy"></a>Erişim ilkesini Sil
Merhaba aşağıdaki kod örneğinde nasıl tooget bir başvuru tooan erişim ilkesi bir ilke kimliği ve toodelete hello İlkesi sonra göre gösterir.

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // toodelete a specific access policy, get a reference toohello policy.  
        // based on hello policy Id passed toohello method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

