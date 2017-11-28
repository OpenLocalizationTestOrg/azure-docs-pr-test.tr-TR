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
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="f02ee-103">Varlıklar ve ilgili varlıklar Media Services .NET SDK'sı ile yönetme</span><span class="sxs-lookup"><span data-stu-id="f02ee-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f02ee-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f02ee-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="f02ee-105">REST</span><span class="sxs-lookup"><span data-stu-id="f02ee-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="f02ee-106">Bu konu, nasıl toomanage Azure Media Services gösterir .NET olan varlık.</span><span class="sxs-lookup"><span data-stu-id="f02ee-106">This topic shows how toomanage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="f02ee-107">Merhaba toplam kayıt sayısı hello en yüksek kota altında olsa bile 1 Nisan 2017 başlangıç 90 günden daha eski hesabınızda herhangi bir işi kaydının otomatik olarak, ilişkili görev kayıtlarını yanı sıra, silinir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="f02ee-108">Örneğin, 1 Nisan 2017 üzerinde 31 Aralık 2016'den daha eski hesabınızda herhangi bir işi kaydının otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="f02ee-109">Tooarchive hello iş/görevi bilgiye ihtiyacınız varsa, bu konuda açıklanan hello kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ee-109">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f02ee-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f02ee-110">Prerequisites</span></span>

<span data-ttu-id="f02ee-111">Geliştirme ortamınızı ayarlama ve açıklandığı gibi hello app.config dosyası bağlantı bilgileriyle doldurmak [.NET ile Media Services geliştirme](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="f02ee-111">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="f02ee-112">Bir varlık başvurusu alın</span><span class="sxs-lookup"><span data-stu-id="f02ee-112">Get an Asset Reference</span></span>
<span data-ttu-id="f02ee-113">Tooget başvuru tooan varolan varlık Media Services buna sık bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-113">A frequent task is tooget a reference tooan existing asset in Media Services.</span></span> <span data-ttu-id="f02ee-114">Aşağıdaki kod örneğine hello nasıl bir varlık başvurusu hello sunucuda hello varlıklar koleksiyonundan bağlam nesnesi alabileceğiniz gösterir, aşağıdaki kod örneği kullanan bir varlık kimliği hello üzerinde temel LINQ Sorgu tooget başvuru tooan varolan IAsset nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f02ee-114">hello following code example shows how you can get an asset reference from hello Assets collection on hello server context object, based on an asset Id. hello following code example uses a Linq query tooget a reference tooan existing IAsset object.</span></span>

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

## <a name="list-all-assets"></a><span data-ttu-id="f02ee-115">Tüm varlıklar listesi</span><span class="sxs-lookup"><span data-stu-id="f02ee-115">List All Assets</span></span>
<span data-ttu-id="f02ee-116">Depolama alanına sahip varlıklar Hello sayısı arttıkça, yararlı toolist olan varlıklarınızı.</span><span class="sxs-lookup"><span data-stu-id="f02ee-116">As hello number of assets you have in storage grows, it is helpful toolist your assets.</span></span> <span data-ttu-id="f02ee-117">Aşağıdaki kod örneğine hello nasıl tooiterate aracılığıyla hello varlıklar koleksiyonu hello sunucu context nesnesinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-117">hello following code example shows how tooiterate through hello Assets collection on hello server context object.</span></span> <span data-ttu-id="f02ee-118">Merhaba kod örneği, her varlık ile bazı özellik değerleri toohello konsolunda de yazar.</span><span class="sxs-lookup"><span data-stu-id="f02ee-118">With each asset, hello code example also writes some of its property values toohello console.</span></span> <span data-ttu-id="f02ee-119">Örneğin, her varlık birçok medya dosyaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="f02ee-120">Her varlık ile ilişkili tüm dosyalar çıkışı Hello kod örneğinde yazar.</span><span class="sxs-lookup"><span data-stu-id="f02ee-120">hello code example writes out all files associated with each asset.</span></span>

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

## <a name="get-a-job-reference"></a><span data-ttu-id="f02ee-121">Bir iş başvurusu alın</span><span class="sxs-lookup"><span data-stu-id="f02ee-121">Get a Job Reference</span></span>

<span data-ttu-id="f02ee-122">Media Services kod görevlerinde işleme ile çalışırken, aşağıdaki kod örneğine bir kimliği hello üzerinde göre başvuru tooan var olan bir işi nasıl tooget başvuru tooan IJob nesne hello işleri koleksiyonundan gösterir tooget genellikle gerekir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-122">When you work with processing tasks in Media Services code, you often need tooget a reference tooan existing job based on an Id. hello following code example shows how tooget a reference tooan IJob object from hello Jobs collection.</span></span>

<span data-ttu-id="f02ee-123">Uzun süre çalışan kodlama işi başlatırken tooget iş başvuru gerekir ve bir iş parçacığında toocheck hello iş durumu gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="f02ee-123">You may need tooget a job reference when starting a long-running encoding job, and need toocheck hello job status on a thread.</span></span> <span data-ttu-id="f02ee-124">Bu gibi durumlarda, bir iş parçacığından Hello yöntemi geri döndüğünde tooretrieve yenilendi başvuru tooa iş gerekir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-124">In cases like this, when hello method returns from a thread, you need tooretrieve a refreshed reference tooa job.</span></span>

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

## <a name="list-jobs-and-assets"></a><span data-ttu-id="f02ee-125">Liste işler ve varlıklar</span><span class="sxs-lookup"><span data-stu-id="f02ee-125">List Jobs and Assets</span></span>
<span data-ttu-id="f02ee-126">Önemli ilgili bir görevi ilişkili işlerini Media Services ile toolist varlıklar ' dir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-126">An important related task is toolist assets with their associated job in Media Services.</span></span> <span data-ttu-id="f02ee-127">Merhaba aşağıdaki kod örneği, nasıl gösterir toolist her IJob nesne ve daha sonra özellikleri hello iş, ilgili tüm görevler, tüm giriş varlıklar hakkında görüntüler her bir iş ve tüm varlıklar çıktı.</span><span class="sxs-lookup"><span data-stu-id="f02ee-127">hello following code example shows you how toolist each IJob object, and then for each job, it displays properties about hello job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="f02ee-128">Bu örnekteki Hello kod çok sayıda diğer görevler için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-128">hello code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="f02ee-129">Örneğin, toolist hello çıkış önceden çalıştıran bir veya daha fazla kodlama işleri varlıklarından istiyorsanız, bu kodu nasıl tooaccess hello varlıklar çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-129">For example, if you want toolist hello output assets from one or more encoding jobs that you ran previously, this code shows how tooaccess hello output assets.</span></span> <span data-ttu-id="f02ee-130">Bir başvuru tooan çıkış varlığına sahip olduğunuzda, karşıdan veya URL'leri sağlama sonra hello içerik tooother kullanıcılar veya uygulamalar'i sunabilir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-130">When you have a reference tooan output asset, you can then deliver hello content tooother users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="f02ee-131">Varlık teslim etmek için seçenekleri hakkında daha fazla bilgi için bkz: [teslim varlıklar hello .NET için Media Services SDK'sı ile](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="f02ee-131">For more information on options for delivering assets, see [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="list-all-access-policies"></a><span data-ttu-id="f02ee-132">Tüm erişim ilkeleri listesi</span><span class="sxs-lookup"><span data-stu-id="f02ee-132">List all Access Policies</span></span>
<span data-ttu-id="f02ee-133">Media Services'de bir varlık veya dosyalarından bir erişim ilkesi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ee-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="f02ee-134">Bir erişim ilkesi için bir dosya veya bir varlık (erişim hello süresi ve ne tür) hello izinleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f02ee-134">An access policy defines hello permissions for a file or an asset (what type of access, and hello duration).</span></span> <span data-ttu-id="f02ee-135">Media Services kodunuzda, genellikle bir erişim ilkesi IAccessPolicy nesneyi oluşturarak ve var olan bir varlıkla ilişkilendirme tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="f02ee-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="f02ee-136">Ardından Media Services doğrudan erişim tooassets sağlamanıza olanak veren bir ILocator nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f02ee-136">Then you create a ILocator object, which lets you provide direct access tooassets in Media Services.</span></span> <span data-ttu-id="f02ee-137">Bu belge seri eşlik hello Visual Studio projesi nasıl toocreate ve ata erişim ilkeleri ve bulucular tooassets gösteren birkaç kod örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-137">hello Visual Studio project that accompanies this documentation series contains several code examples that show how toocreate and assign access policies and locators tooassets.</span></span>

<span data-ttu-id="f02ee-138">Kod örnekteki nasıl aşağıdaki hello toolist hello sunucuda ve izinleri gösterir hello türü tüm erişim ilkeleri her ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="f02ee-138">hello following code example shows how toolist all access policies on hello server, and shows hello type of permissions associated with each.</span></span> <span data-ttu-id="f02ee-139">Başka bir kullanışlı bir yol tooview erişim ilkeleri toolist tüm ILocator hello sunucuda nesnedir ve ardından her Bulucu için onun ilişkili erişim ilkesi kendi AccessPolicy özelliğini kullanarak listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ee-139">Another useful way tooview access policies is toolist all ILocator objects on hello server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

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
    
## <a name="limit-access-policies"></a><span data-ttu-id="f02ee-140">Sınır erişim ilkeleri</span><span class="sxs-lookup"><span data-stu-id="f02ee-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="f02ee-141">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="f02ee-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="f02ee-142">Merhaba kullanması gereken her zaman kullanıyorsanız, aynı ilke kimliği hello aynı gün / erişim izinlerini, örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="f02ee-142">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="f02ee-143">Örneğin, yalnızca bir kez uygulamanızda çalıştırırsınız: koddan hello olan genel bir ilke kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ee-143">For example, you can create a generic set of policies with hello following code that would only run one time in your application.</span></span> <span data-ttu-id="f02ee-144">Daha sonra kullanmak için kimlikleri tooa günlük dosyası kaydedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f02ee-144">You can log IDs tooa log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="f02ee-145">Daha sonra kodunuzda şöyle kimlikleri varolan hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f02ee-145">Then, you can use hello existing IDs in your code like this:</span></span>

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

## <a name="list-all-locators"></a><span data-ttu-id="f02ee-146">Tüm Bulucular listesi</span><span class="sxs-lookup"><span data-stu-id="f02ee-146">List All Locators</span></span>
<span data-ttu-id="f02ee-147">Bir Bulucu sağlayan doğrudan yolu tooaccess izinleri toohello varlık birlikte bir varlık hello Bulucu'nın ilişkili erişim ilkesi tarafından tanımlandığı şekilde bir URL'dir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-147">A locator is a URL that provides a direct path tooaccess an asset, along with permissions toohello asset as defined by hello locator's associated access policy.</span></span> <span data-ttu-id="f02ee-148">Her varlık, kendi Bulucular özellikte ilişkili ILocator nesnelerinin bir koleksiyonu olabilir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="f02ee-149">Merhaba sunucu bağlamı da tüm bulucular içeren bir konum belirleyicisi koleksiyon sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-149">hello server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="f02ee-150">Merhaba aşağıdaki kod örneğinde hello sunucusundaki tüm bulucular listeler.</span><span class="sxs-lookup"><span data-stu-id="f02ee-150">hello following code example lists all locators on hello server.</span></span> <span data-ttu-id="f02ee-151">Her Bulucu için hello kimliği hello ilgili varlık ve erişim ilkesi için gösterir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-151">For each locator, it shows hello Id for hello related asset and access policy.</span></span> <span data-ttu-id="f02ee-152">Ayrıca, izinler, hello sona erme tarihi ve hello tam yolu toohello varlık hello türünü görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f02ee-152">It also displays hello type of permissions, hello expiration date, and hello full path toohello asset.</span></span>

<span data-ttu-id="f02ee-153">Bir Bulucu yolu tooan varlık yalnızca URL toohello bir temel varlık olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f02ee-153">Note that a locator path tooan asset is only a base URL toohello asset.</span></span> <span data-ttu-id="f02ee-154">bir kullanıcı veya uygulama göz doğrudan yolu tooindividual dosyaları toocreate kodunuzu hello belirli dosya yolu toohello Bulucu yolu eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-154">toocreate a direct path tooindividual files that a user or application could browse to, your code must add hello specific file path toohello locator path.</span></span> <span data-ttu-id="f02ee-155">Hakkında daha fazla bilgi için toodo buna ek olarak, bkz: hello konu [teslim varlıklar hello .NET için Media Services SDK'sı ile](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="f02ee-155">For more information on how toodo this, see hello topic [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="f02ee-156">Varlıkları büyük koleksiyonlarına numaralandırma</span><span class="sxs-lookup"><span data-stu-id="f02ee-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="f02ee-157">Varlıkları sorgulanırken ortak REST v2 sorgu sonuçları too1000 sonuçları sınırladığından aynı anda döndürülen 1000 varlıkların bir sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="f02ee-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="f02ee-158">Toouse atlama ve alma varlıklar büyük koleksiyonlarına numaralandırılırken gerekir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-158">You need toouse Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="f02ee-159">Merhaba hello içindeki tüm hello işlere aşağıdaki işlevi döngüler Media Services hesabı sağlanan.</span><span class="sxs-lookup"><span data-stu-id="f02ee-159">hello following function loops through all hello jobs in hello provided Media Services Account.</span></span> <span data-ttu-id="f02ee-160">Media Services 1000 işleri işleri koleksiyondaki döndürür.</span><span class="sxs-lookup"><span data-stu-id="f02ee-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="f02ee-161">Merhaba işlevi atlayın ve toomake emin gerçekleştirin (1000'den fazla iş hesabınızı olması durumunda), tüm işleri numaralandırılır hale getirir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-161">hello function makes use of Skip and Take toomake sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

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

## <a name="delete-an-asset"></a><span data-ttu-id="f02ee-162">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="f02ee-162">Delete an Asset</span></span>
<span data-ttu-id="f02ee-163">Aşağıdaki örnek hello bir varlığını siler.</span><span class="sxs-lookup"><span data-stu-id="f02ee-163">hello following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="f02ee-164">Bir işi Sil</span><span class="sxs-lookup"><span data-stu-id="f02ee-164">Delete a Job</span></span>
<span data-ttu-id="f02ee-165">bir iş toodelete hello hello durumu özelliğinde belirtildiği gibi hello iş durumunu denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-165">toodelete a job, you must check hello state of hello job as indicated in hello State property.</span></span> <span data-ttu-id="f02ee-166">İlk sıraya alınan, zamanlanan ya da işlem, gibi diğer bazı durumlarda işler iptal edildi ve bunlar daha sonra silinebilir tamamlandı veya iptal edilen işler silinebilir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="f02ee-167">Merhaba aşağıdaki kod örneğinde iş durumlarını denetleme ve hello durumu tamamlandı ya da iptal edildiğinde sonra silerek bir işi silmek için bir yöntemi gösterir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-167">hello following code example shows a method for deleting a job by checking job states and then deleting when hello state is finished or canceled.</span></span> <span data-ttu-id="f02ee-168">Bu kod bir başvuru tooa işi almak için bu konunun önceki bölümde hello bağlıdır: bir iş başvurusu alın.</span><span class="sxs-lookup"><span data-stu-id="f02ee-168">This code depends on hello previous section in this topic for getting a reference tooa job: Get a job reference.</span></span>

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


## <a name="delete-an-access-policy"></a><span data-ttu-id="f02ee-169">Erişim ilkesini Sil</span><span class="sxs-lookup"><span data-stu-id="f02ee-169">Delete an Access Policy</span></span>
<span data-ttu-id="f02ee-170">Merhaba aşağıdaki kod örneğinde nasıl tooget bir başvuru tooan erişim ilkesi bir ilke kimliği ve toodelete hello İlkesi sonra göre gösterir.</span><span class="sxs-lookup"><span data-stu-id="f02ee-170">hello following code example shows how tooget a reference tooan access policy based on a policy Id, and then toodelete hello policy.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="f02ee-171">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="f02ee-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f02ee-172">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="f02ee-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

