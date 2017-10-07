---
title: "aaaPersist iş ve görev çıktısını tooAzure depolama hello dosyası kuralları kitaplığı için .NET - Azure Batch | Microsoft Docs"
description: ".NET toopersist toplu görev için toouse Azure toplu işlem dosyası kuralları kitaplığı ve proje çıktı tooAzure depolama ve görünüm hello hello Azure portal çıktısında nasıl kalıcı öğrenin."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="082c7-103">İşi Sürdür ve .NET toopersist için hello toplu iş dosyası kuralları kitaplığı ile verileri tooAzure depolama görev</span><span class="sxs-lookup"><span data-stu-id="082c7-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="082c7-104">Tek yönlü toopersist görev verilerdir toouse hello [.NET için Azure toplu işlem dosyası kuralları Kitaplığı][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="082c7-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="082c7-105">Merhaba dosyası kuralları Kitaplığı görev çıktısını depolamak hello işlemini basitleştirir veri tooAzure depolama ve onu alınıyor.</span><span class="sxs-lookup"><span data-stu-id="082c7-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="082c7-106">Merhaba dosyası kuralları Kitaplığı'nda görev ve istemci kodu kullanabilirsiniz &mdash; görev kodu kalıcı dosyaları için ve istemci kodu toolist ve bunları almak.</span><span class="sxs-lookup"><span data-stu-id="082c7-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="082c7-107">Görev kodunuzu da hello kitaplığı tooretrieve hello çıkış Yukarı Akış görevlerin gibi kullanabilirsiniz bir [görev bağımlılıkları](batch-task-dependencies.md) senaryo.</span><span class="sxs-lookup"><span data-stu-id="082c7-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="082c7-108">tooretrieve çıkış dosyaları hello dosyası kuralları kitaplığı ile belirli iş ya da görev için hello dosyaları amacı ve kimliği listeleyerek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="082c7-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="082c7-109">Tooknow hello adlar veya konumlar hello dosyaların gerekmez.</span><span class="sxs-lookup"><span data-stu-id="082c7-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="082c7-110">Örneğin, belirli bir görev için tüm ara dosyaları hello dosyası kuralları kitaplığı toolist kullanın veya belirli bir iş için Önizleme dosya almak.</span><span class="sxs-lookup"><span data-stu-id="082c7-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="082c7-111">Merhaba Batch hizmeti API'si 2017-05-01 sürümünden başlayarak, görevler ve hello sanal makine yapılandırması ile oluşturulan havuzu çalışan iş yöneticisi görevleri için kalıcı çıkış veri tooAzure depolama destekler.</span><span class="sxs-lookup"><span data-stu-id="082c7-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="082c7-112">Merhaba Batch hizmeti API'si bir görev oluşturur ve bir alternatif toohello dosyası kuralları kitaplık olarak hizmet veren hello kodu ve çıkış basit yol toopersist sağlar.</span><span class="sxs-lookup"><span data-stu-id="082c7-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="082c7-113">Görevinizi çalıştıran tooupdate Merhaba uygulaması gerek kalmadan, Batch istemci uygulamaları toopersist çıkış değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="082c7-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="082c7-114">Daha fazla bilgi için bkz: [hello Batch hizmeti API'si ile görev veri tooAzure depolama kalıcı](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="082c7-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="082c7-115">Merhaba dosyası kuralları kitaplığı toopersist görev çıktısını kullandığınızda?</span><span class="sxs-lookup"><span data-stu-id="082c7-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="082c7-116">Azure Batch birden fazla tek yönlü toopersist görev çıktısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="082c7-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="082c7-117">Merhaba dosyası kuralları en iyi uygun toothese senaryolar verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="082c7-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="082c7-118">Merhaba kod göreviniz hello dosyası kuralları kitaplığı kullanarak toopersist dosyaları çalıştığını Merhaba uygulaması için kolayca değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="082c7-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="082c7-119">Merhaba görev çalışmaya devam ederken toostream veri tooAzure depolama istiyor.</span><span class="sxs-lookup"><span data-stu-id="082c7-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="082c7-120">Merhaba bulut hizmet yapılandırması veya hello sanal makine yapılandırması ile oluşturulan havuzlarından toopersist veri istiyor.</span><span class="sxs-lookup"><span data-stu-id="082c7-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="082c7-121">İstemci uygulamanız veya diğer görevler hello gereksinimlerini toolocate iş ve Görev çıkış dosyalarını Kimliğine göre veya amacına göre yükleyin.</span><span class="sxs-lookup"><span data-stu-id="082c7-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="082c7-122">Hello Azure portal tooview Görev çıkış istiyor.</span><span class="sxs-lookup"><span data-stu-id="082c7-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="082c7-123">Senaryonuz Yukarıda listelenenler farklıysa, farklı bir yaklaşım tooconsider gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="082c7-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="082c7-124">Kalıcı görev çıktısı için diğer seçenekleri hakkında daha fazla bilgi için bkz: [kalan iş ve görev çıktısını tooAzure depolama](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="082c7-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="082c7-125">Merhaba toplu iş dosyası kuralları standart nedir?</span><span class="sxs-lookup"><span data-stu-id="082c7-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="082c7-126">Merhaba [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) hello hedef kapsayıcılarını ve çıktı dosyalarınızı yazılır blob yolları toowhich bir adlandırma şeması sağlar.</span><span class="sxs-lookup"><span data-stu-id="082c7-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="082c7-127">Dosyaları kalıcı tooAzure toohello standart dosya kurallarına uyması depolama hello Azure portalında görüntülenmek için otomatik olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="082c7-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="082c7-128">Hello portal hello adlandırma kuralı farkındadır ve bu nedenle tooit uyması dosyaları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="082c7-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="082c7-129">Hello dosyası kuralları kitaplığı .NET için depolama kapsayıcıları ve Görev çıkış dosyalarını toohello standart dosya kurallarına göre otomatik olarak adlandırır.</span><span class="sxs-lookup"><span data-stu-id="082c7-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="082c7-130">Merhaba dosyası kuralları kitaplığı toojob kimliği, görev kimliği veya amaca göre yöntemleri tooquery çıktı dosyalarını Azure storage'da de sağlar.</span><span class="sxs-lookup"><span data-stu-id="082c7-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="082c7-131">.NET dışında bir dil ile geliştiriyorsanız, uygulamanızda kendiniz hello dosyası kuralları standart uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="082c7-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="082c7-132">Daha fazla bilgi için bkz: [hello toplu iş dosyası kuralları standardı hakkında](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="082c7-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="082c7-133">Bir Azure depolama hesabı tooyour toplu işlem hesabı Bağla</span><span class="sxs-lookup"><span data-stu-id="082c7-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="082c7-134">toopersist çıkış veri tooAzure Hello dosyası kuralları kitaplığı kullanarak depolama, ilk Azure Storage hesabı tooyour toplu işlem hesabı bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="082c7-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="082c7-135">Henüz yapmadıysanız, bir depolama hesabı tooyour toplu işlem hesabı hello kullanarak bağlantı [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="082c7-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="082c7-136">Tooyour Batch hesabında hello Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="082c7-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="082c7-137">Altında **ayarları**seçin **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="082c7-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="082c7-138">Batch hesabınızla ilişkili bir depolama hesabı zaten yoksa tıklatın **depolama hesabı (hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="082c7-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="082c7-139">Aboneliğiniz için hello listesinden bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="082c7-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="082c7-140">En iyi performans için hello olan bir Azure depolama hesabı kullanmak aynı bölgede hello toplu işlem hesabı görevlerinizi çalıştırdığı.</span><span class="sxs-lookup"><span data-stu-id="082c7-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="082c7-141">Çıktı verilerini Sürdür</span><span class="sxs-lookup"><span data-stu-id="082c7-141">Persist output data</span></span>

<span data-ttu-id="082c7-142">toopersist iş ve görev çıktı verilerini hello dosyası kuralları kitaplığıyla, Azure Storage'da kapsayıcı oluşturma ve sonra hello çıktı toohello kapsayıcısını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="082c7-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="082c7-143">Kullanım hello [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage) , görev kodu tooupload hello Görev çıkış toohello kapsayıcısında.</span><span class="sxs-lookup"><span data-stu-id="082c7-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="082c7-144">Kapsayıcılar ve bloblar Azure depolama ile çalışma hakkında daha fazla bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="082c7-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="082c7-145">Merhaba dosyası kitaplığı depolanır kuralları olan tüm iş ve görev çıktıları kalıcı hello aynı kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="082c7-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="082c7-146">Çok sayıda görevleri çalışırsanız toopersist hello aynı dosyaları zaman [azaltma sınırları depolama](../storage/common/storage-performance-checklist.md#blobs) zorlanabilir.</span><span class="sxs-lookup"><span data-stu-id="082c7-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="082c7-147">Depolama kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="082c7-147">Create storage container</span></span>

<span data-ttu-id="082c7-148">toopersist Görev çıkış tooAzure depolama, öncelikle çağırarak bir kapsayıcı oluşturmanız [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="082c7-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="082c7-149">Bu uzantı metodu geçen bir [CloudStorageAccount] [ net_cloudstorageaccount] nesnesini parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="082c7-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="082c7-150">Azure portal ve hello alma yöntemleri ilgili hello makalenin sonraki bölümlerinde ele alınan adlandırılmış according toohello dosyası kuralları içeriğinin tarafından keşfedilebilir; böylece standart hello bir kapsayıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="082c7-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="082c7-151">İstemci uygulamanızı genellikle hello kod toocreate bir kapsayıcı yerleştirin &mdash; hello havuzlar, işler ve görevler oluşturan uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="082c7-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="082c7-152">Depolama görev çıkarır</span><span class="sxs-lookup"><span data-stu-id="082c7-152">Store task outputs</span></span>

<span data-ttu-id="082c7-153">Azure storage'da kapsayıcı hazırladığınıza göre görevleri çıktı toohello kapsayıcı hello kullanarak kaydedebilirsiniz [TaskOutputStorage] [ net_taskoutputstorage] sınıfı hello dosyası kuralları Kitaplığı'nda bulundu.</span><span class="sxs-lookup"><span data-stu-id="082c7-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="082c7-154">Görev kodunuzda ilk oluşturun bir [TaskOutputStorage] [ net_taskoutputstorage] nesne sonra hello görev kendi iş tamamlandığında, hello çağırın [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] yöntemi toosave kendi çıktı tooAzure depolama.</span><span class="sxs-lookup"><span data-stu-id="082c7-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="082c7-155">Merhaba `kind` hello parametresinin [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) yöntemi kategorilere ayıran hello dosyaları kalıcı.</span><span class="sxs-lookup"><span data-stu-id="082c7-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="082c7-156">Dört önceden tanımlanmış vardır [TaskOutputKind] [ net_taskoutputkind] türleri: `TaskOutput`, `TaskPreview`, `TaskLog`, ve `TaskIntermediate.` çıktı özel kategoriler de tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="082c7-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="082c7-157">Bu çıktı türü belirli bir görevi çıkışları ne tür bir toplu iş daha sonra Merhaba sorguladığınızda çıkışları toolist kalıcı toospecify izin verir.</span><span class="sxs-lookup"><span data-stu-id="082c7-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="082c7-158">Diğer bir deyişle, bir görev hello çıktıların listelediğinizde hello çıkış türlerinden birini hello listede filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="082c7-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="082c7-159">Örneğin, "Merhaba ver *Önizleme* için görev çıktısını *109*."</span><span class="sxs-lookup"><span data-stu-id="082c7-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="082c7-160">Listeleme ve çıkışları alma hakkında daha fazla görünür [almak çıktı](#retrieve-output) hello makalede daha sonra.</span><span class="sxs-lookup"><span data-stu-id="082c7-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="082c7-161">Merhaba çıktı türü de hello Azure portal belirli bir dosya nerede görüneceğini belirler: *TaskOutput*-kategorilere ayrılmış dosyaları görünür altında **Görev çıkış dosyaları**, ve *TaskLog*dosyaları görünür altında **görev günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="082c7-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="082c7-162">Mağaza iş çıkarır</span><span class="sxs-lookup"><span data-stu-id="082c7-162">Store job outputs</span></span>

<span data-ttu-id="082c7-163">Ayrıca toostoring görev çıktısını alır, tüm bir işle ilişkili hello çıkışları depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="082c7-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="082c7-164">Örneğin, hello birleştirme görevde bir filmi işleme işin, tam olarak işlenen hello film iş çıktısı kalıcı olamadı.</span><span class="sxs-lookup"><span data-stu-id="082c7-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="082c7-165">İş tamamlandığında, istemci uygulamanız listelemek ve hello iş hello çıktıların almak ve tooquery tek tek görevler hello mu değil.</span><span class="sxs-lookup"><span data-stu-id="082c7-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="082c7-166">İş çıktısı tarafından arama hello depolamak [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] yöntemi ve hello belirtin [JobOutputKind] [ net_joboutputkind] ve dosya adı:</span><span class="sxs-lookup"><span data-stu-id="082c7-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="082c7-167">Merhaba olduğu gibi **TaskOutputKind** türü görev çıktıları için kullandığınız hello [JobOutputKind] [ net_joboutputkind] türü toocategorize bir iş dosyaları kalıcı.</span><span class="sxs-lookup"><span data-stu-id="082c7-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="082c7-168">Bu parametre (listesi) belirli bir çıkış türü için toolater sorgu sağlar.</span><span class="sxs-lookup"><span data-stu-id="082c7-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="082c7-169">Merhaba **JobOutputKind** türü çıkış ve önizleme kategorileri içerir ve özel kategoriler oluşturulmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="082c7-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="082c7-170">Depolama görev günlükleri</span><span class="sxs-lookup"><span data-stu-id="082c7-170">Store task logs</span></span>

<span data-ttu-id="082c7-171">Ayrıca toopersisting dosya toodurable depolama bir görev veya iş tamamlandığında, bir görev hello yürütülmesi sırasında güncelleştirilir toopersist dosyalarına ihtiyaç duymayabilirsiniz &mdash; günlük dosyalarını veya `stdout.txt` ve `stderr.txt`, örneğin.</span><span class="sxs-lookup"><span data-stu-id="082c7-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="082c7-172">Bu amaçla hello Azure toplu işlem dosyası kuralları kitaplığı hello sağlar [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="082c7-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="082c7-173">İle [SaveTrackedAsync][net_savetrackedasync], güncelleştirmeler tooa dosyasına (belirttiğiniz bir aralıkta) hello düğümde izlemek ve bu güncelleştirmeleri tooAzure depolama kalır.</span><span class="sxs-lookup"><span data-stu-id="082c7-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="082c7-174">Aşağıdaki kod parçacığını hello kullanırız [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` hello görev hello yürütülmesi sırasında 15 dakikada Azure storage'da:</span><span class="sxs-lookup"><span data-stu-id="082c7-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="082c7-175">Merhaba açıklamalı bölüm `Code tooprocess data and produce output file(s)` göreviniz normalde gerçekleştireceği hello kodu için bir yer tutucudur.</span><span class="sxs-lookup"><span data-stu-id="082c7-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="082c7-176">Örneğin, veriler Azure depolama biriminden yükler ve dönüşüm ya da hesaplama üzerinde gerçekleştiren kodu olabilir.</span><span class="sxs-lookup"><span data-stu-id="082c7-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="082c7-177">Merhaba önemli bu parçacığı parçası gösteren böyle kodda nasıl kayabilir bir `using` blok tooperiodically güncelleştirme dosyası ile [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="082c7-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="082c7-178">Merhaba düğümü aracı hello havuzdaki her düğüme çalışır ve hello düğümü hello Batch hizmeti arasında hello komut ve denetim arabirimi sağlayan bir programdır.</span><span class="sxs-lookup"><span data-stu-id="082c7-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="082c7-179">Merhaba `Task.Delay` çağrıdır hello sonunda bu gerekli `using` düğümü aracı hello blok tooensure toohello stdout.txt dosya hello düğümde standart zaman tooflush Merhaba içeriğine sahip.</span><span class="sxs-lookup"><span data-stu-id="082c7-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="082c7-180">Bu gecikme olmadan bu olası toomiss hello son birkaç saniye çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="082c7-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="082c7-181">Bu gecikme tüm dosyaları için gerekli olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="082c7-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="082c7-182">Dosya ile izleme etkinleştirdiğinizde **SaveTrackedAsync**, yalnızca *ekler* toohello izlenen dosya kalıcı tooAzure depolama şunlardır.</span><span class="sxs-lookup"><span data-stu-id="082c7-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="082c7-183">Yalnızca günlük dosyaları döndürme izlemek için bu yöntemi kullanın veya toowith yazılır diğer dosyalar işlem toohello hello dosya sonuna.</span><span class="sxs-lookup"><span data-stu-id="082c7-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="082c7-184">Çıktı verilerini alma</span><span class="sxs-lookup"><span data-stu-id="082c7-184">Retrieve output data</span></span>

<span data-ttu-id="082c7-185">Hello Azure toplu işlem dosyası kuralları kitaplığı kullanarak, kalıcı çıktı aldığınızda, görev ve iş merkezli bir şekilde bunu.</span><span class="sxs-lookup"><span data-stu-id="082c7-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="082c7-186">Hello için görev veya iş tooknow gerek kalmadan, Azure Storage veya bile dosya adıyla çıkış yolu isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="082c7-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="082c7-187">Bunun yerine, görev tarafından çıktı dosyaları istek veya iş kimliği</span><span class="sxs-lookup"><span data-stu-id="082c7-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="082c7-188">Hello aşağıdaki kod parçacığını işe ait görevleri tekrarlanan, hello görev için hello çıktı dosyaları hakkında bazı bilgiler yazdırır ve sonra depolama biriminden dosyalarını indirir.</span><span class="sxs-lookup"><span data-stu-id="082c7-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="082c7-189">Hello Azure portal görünümü çıktı dosyaları</span><span class="sxs-lookup"><span data-stu-id="082c7-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="082c7-190">Hello Azure portal görüntüler görev çıktı dosyalarını ve kalıcı tooa olan günlükleri bağlı hello kullanarak Azure Storage hesabını [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="082c7-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="082c7-191">Bu kuralları hello tercih ettiğiniz bir dil kendiniz uygulayabilirsiniz veya .NET uygulamalarınızın hello dosyası kuralları kitaplığını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="082c7-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="082c7-192">tooenable hello görüntü çıkış dosyalarınızın hello Portalı'nda hello aşağıdaki gereksinimleri karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="082c7-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="082c7-193">[Bir Azure depolama hesabı bağlantı](#requirement-linked-storage-account) tooyour toplu işlem hesabı.</span><span class="sxs-lookup"><span data-stu-id="082c7-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="082c7-194">Önceden tanımlanmış toohello depolama kapsayıcıları ve dosyaları için adlandırma kuralları çıkışları kalıcı olduğunda uyar.</span><span class="sxs-lookup"><span data-stu-id="082c7-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="082c7-195">Bu kuralları hello tanımını hello dosyası kuralları Kitaplığı'nda bulabilirsiniz [Benioku][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="082c7-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="082c7-196">Merhaba kullanırsanız [Azure toplu işlem dosyası kuralları] [ nuget_package] kitaplığı toopersist, output, dosyalarınızı toohello dosyası kuralları standart göre kalıcı.</span><span class="sxs-lookup"><span data-stu-id="082c7-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="082c7-197">tooview görev çıktısını dosyaları ve hello Azure portalında, toohello görev çıktısı ilgilendiğiniz, ardından da gidin **kayıtlı çıktı dosyaları** veya **Günlükleri kaydedilen**.</span><span class="sxs-lookup"><span data-stu-id="082c7-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="082c7-198">Bu görüntü hello gösterir **kayıtlı çıktı dosyaları** "007" kimlikli hello görev için:</span><span class="sxs-lookup"><span data-stu-id="082c7-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="082c7-199">![Görev dikey penceresinde hello Azure portal çıkarır][2]</span><span class="sxs-lookup"><span data-stu-id="082c7-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="082c7-200">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="082c7-200">Code sample</span></span>

<span data-ttu-id="082c7-201">Merhaba [PersistOutputs] [ github_persistoutputs] örnek proje hello biridir [Azure Batch kod örnekleri] [ github_samples] github'da.</span><span class="sxs-lookup"><span data-stu-id="082c7-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="082c7-202">Bu Visual Studio çözümü nasıl toodurable depolama toouse hello Azure toplu işlem dosyası kuralları kitaplığı toopersist görev çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="082c7-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="082c7-203">toorun hello örnek, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="082c7-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="082c7-204">Açık hello projesinde **Visual Studio 2015 veya daha yeni**.</span><span class="sxs-lookup"><span data-stu-id="082c7-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="082c7-205">Batch ve Storage eklemek **hesabının kimlik bilgilerini** çok**AccountSettings.settings** hello öğesini kullanıma alın projesinde.</span><span class="sxs-lookup"><span data-stu-id="082c7-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="082c7-206">**Yapı** (ancak çalışmaz) hello çözümü.</span><span class="sxs-lookup"><span data-stu-id="082c7-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="082c7-207">İstenirse herhangi bir NuGet paketinin geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="082c7-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="082c7-208">Kullanım hello Azure portal tooupload bir [uygulama paketi](batch-application-packages.md) için **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="082c7-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="082c7-209">Merhaba dahil `PersistOutputsTask.exe` ve bağımlı derlemeleri hello .zip paketindeki kümesi hello uygulama kimliği çok "PersistOutputsTask" ve hello uygulama Paket sürümü "1.0" çok.</span><span class="sxs-lookup"><span data-stu-id="082c7-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="082c7-210">**Başlat** (Çalıştır) hello **PersistOutputs** projesi.</span><span class="sxs-lookup"><span data-stu-id="082c7-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="082c7-211">İstendiğinde toochoose hello Kalıcılık teknolojisi toouse çalışan hello örnek girdiğinizde **1** hello dosyası kuralları kitaplığı toopersist görev çıktısını kullanarak toorun hello örnek.</span><span class="sxs-lookup"><span data-stu-id="082c7-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="082c7-212">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="082c7-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="082c7-213">Merhaba toplu iş dosyası kuralları kitaplığı için .NET Al</span><span class="sxs-lookup"><span data-stu-id="082c7-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="082c7-214">.NET için Hello toplu iş dosyası kuralları kitaplığı edinilebilir [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="082c7-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="082c7-215">Merhaba kitaplığı genişletir hello [CloudJob] [ net_cloudjob] ve [CloudTask] [ net_cloudtask] yeni yöntemleri sınıflarıyla.</span><span class="sxs-lookup"><span data-stu-id="082c7-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="082c7-216">Ayrıca bkz. hello [başvuru belgelerini](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) hello dosyası kuralları kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="082c7-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="082c7-217">Merhaba [kaynak kodu] [ github_file_conventions] Merhaba dosyası kuralları kitaplığı Github'da hello Microsoft Azure SDK'sı .NET havuz için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="082c7-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="082c7-218">Diğer yaklaşımlar kalıcı çıkış verileri keşfedin</span><span class="sxs-lookup"><span data-stu-id="082c7-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="082c7-219">Bkz: [kalan iş ve görev çıktısını tooAzure depolama](batch-task-output.md) kalıcı görevi ve iş verileri genel bakış.</span><span class="sxs-lookup"><span data-stu-id="082c7-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="082c7-220">Bkz: [hello Batch hizmeti API'si ile görev veri tooAzure depolama kalıcı](batch-task-output-files.md) toolearn nasıl toouse hello Batch hizmeti API'si toopersist çıktı verilerini.</span><span class="sxs-lookup"><span data-stu-id="082c7-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Kayıtlı çıktı dosyaları ve Portalı'nda kayıtlı günlükleri seçiciler"
[2]: ./media/batch-task-output/task-output-02.png "Görev dikey penceresinde hello Azure portal çıkarır"
