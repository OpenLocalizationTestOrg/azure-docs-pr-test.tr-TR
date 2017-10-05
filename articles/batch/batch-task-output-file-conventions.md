---
title: "-Azure Batch .NET için Azure Storage iş ve Görev çıkış dosyası kuralları kitaplığıyla kalıcı | Microsoft Docs"
description: ".NET için Azure toplu işlem dosyası kuralları kitaplığı toplu işlem görevi ve iş çıktısı Azure depolama için kalıcı ve kalıcı çıktı Azure portalında görüntülemek için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: a9de327c20463469bc91d9720aa17333a36f919e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="persist-job-and-task-data-to-azure-storage-with-the-batch-file-conventions-library-for-net-to-persist"></a><span data-ttu-id="1097b-103">İş ve görev verileri Azure depolama kalıcı hale getirmek .NET için toplu iş dosyası kuralları kitaplığıyla Sürdür</span><span class="sxs-lookup"><span data-stu-id="1097b-103">Persist job and task data to Azure Storage with the Batch File Conventions library for .NET to persist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="1097b-104">Görev verilerini kalıcı hale getirmek için bir yolu [.NET için Azure toplu işlem dosyası kuralları Kitaplığı][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="1097b-104">One way to persist task data is to use the [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="1097b-105">Görev çıktı verileri Azure depolama işlemi dosyası kuralları kitaplığı basitleştirir ve onu alınıyor.</span><span class="sxs-lookup"><span data-stu-id="1097b-105">The File Conventions library simplifies the process of storing task output data to Azure Storage and retrieving it.</span></span> <span data-ttu-id="1097b-106">Görev ve istemci kodu dosyası kuralları kitaplıkta kullanabilirsiniz &mdash; kalıcı dosyaları için görev kodu ve listelemek ve onları almak için istemci kodu.</span><span class="sxs-lookup"><span data-stu-id="1097b-106">You can use the File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code to list and retrieve them.</span></span> <span data-ttu-id="1097b-107">Görev kodunuzu içinde gibi Yukarı Akış görevlerin çıktısını almak için de kitaplığı kullanabilirsiniz bir [görev bağımlılıkları](batch-task-dependencies.md) senaryo.</span><span class="sxs-lookup"><span data-stu-id="1097b-107">Your task code can also use the library to retrieve the output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="1097b-108">Dosya kuralları kitaplığıyla çıktı dosyalarını almak için belirli iş ya da görev için dosyaları amacı ve kimliği listeleyerek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-108">To retrieve output files with the File Conventions library, you can locate the files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="1097b-109">Adlar veya konumlar dosyaların bilmeniz gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="1097b-109">You don't need to know the names or locations of the files.</span></span> <span data-ttu-id="1097b-110">Örneğin, belirli bir görev için tüm ara dosyaları listelemek için dosyası kuralları kitaplığını kullanın veya belirli bir iş için bir önizleme dosya alın.</span><span class="sxs-lookup"><span data-stu-id="1097b-110">For example, you can use the File Conventions library to list all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="1097b-111">Batch hizmeti API'si 2017-05-01 sürümünden başlayarak, görevler ve sanal makine yapılandırmasıyla oluşturulan havuzu çalışan iş yöneticisi görevleri için kalıcı çıktı verilerini Azure Storage'a destekler.</span><span class="sxs-lookup"><span data-stu-id="1097b-111">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools created with the virtual machine configuration.</span></span> <span data-ttu-id="1097b-112">Batch hizmeti API'si çıktısını bir görev oluşturur ve alternatif dosyası kuralları kitaplığına görevi gören kodundaki kalıcı hale getirmek için basit bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="1097b-112">The Batch service API provides a simple way to persist output from within the code that creates a task and serves as an alternative to the File Conventions library.</span></span> <span data-ttu-id="1097b-113">Çıktı, görevin çalıştığı uygulama güncelleştirmeye gerek kalmadan kalıcı hale getirmek için Batch istemci uygulamalarınızın değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-113">You can modify your Batch client applications to persist output without needing to update the application that your task is running.</span></span> <span data-ttu-id="1097b-114">Daha fazla bilgi için bkz: [kalan görev verileri toplu ile Azure depolama hizmeti API](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="1097b-114">For more information, see [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-the-file-conventions-library-to-persist-task-output"></a><span data-ttu-id="1097b-115">Ne zaman dosyası kuralları Kitaplığı görev çıktısını kalıcı hale getirmek için kullanabilirim?</span><span class="sxs-lookup"><span data-stu-id="1097b-115">When do I use the File Conventions library to persist task output?</span></span>

<span data-ttu-id="1097b-116">Azure Batch görev çıktısını kalıcı hale getirmek için birden fazla yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="1097b-116">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="1097b-117">Dosya kuralları bu senaryolar için uygundur:</span><span class="sxs-lookup"><span data-stu-id="1097b-117">The File Conventions is best suited to these scenarios:</span></span>

- <span data-ttu-id="1097b-118">Görevinizi dosyası kuralları kitaplığı kullanarak dosyaları kalıcı hale getirmek için çalıştıran uygulama kodunu kolayca değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-118">You can easily modify the code for the application that your task is running to persist files using the File Conventions library.</span></span>
- <span data-ttu-id="1097b-119">Görevin çalışmaya devam ederken, Azure Storage veri akışı istersiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-119">You want to stream data to Azure Storage while the task is still running.</span></span>
- <span data-ttu-id="1097b-120">Bulut hizmet yapılandırması veya sanal makine yapılandırması ile oluşturulan havuzlarından veri kalıcı hale getirmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-120">You want to persist data from pools created with either the cloud service configuration or the virtual machine configuration.</span></span>
- <span data-ttu-id="1097b-121">İstemci uygulamanız veya işteki diğer görevler bulun ve Görev çıkış dosyalarını kimlikle veya amacı indirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="1097b-121">Your client application or other tasks in the job needs to locate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="1097b-122">Görev çıktısını Azure portalında görüntülemek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="1097b-122">You want to view task output in the Azure portal.</span></span>

<span data-ttu-id="1097b-123">Senaryonuz Yukarıda listelenenler farklıysa, farklı bir yaklaşım dikkate almanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1097b-123">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="1097b-124">Kalıcı görev çıktısı için diğer seçenekleri hakkında daha fazla bilgi için bkz: [iş ve görev çıktı Azure depolama için kalıcı](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="1097b-124">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-the-batch-file-conventions-standard"></a><span data-ttu-id="1097b-125">Standart toplu işlem dosyası kuralları nedir?</span><span class="sxs-lookup"><span data-stu-id="1097b-125">What is the Batch File Conventions standard?</span></span>

<span data-ttu-id="1097b-126">[Toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) bir adlandırma şeması hedef kapsayıcılarını ve çıktı dosyalarınızı yazılır blob yollar sağlar.</span><span class="sxs-lookup"><span data-stu-id="1097b-126">The [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for the destination containers and blob paths to which your output files are written.</span></span> <span data-ttu-id="1097b-127">Dosyaları kalıcı dosyası kuralları standardını kullanan Azure depolama için Azure portalında görüntülenmek üzere otomatik olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1097b-127">Files persisted to Azure Storage that adhere to the File Conventions standard are automatically available for viewing in the Azure portal.</span></span> <span data-ttu-id="1097b-128">Portal adlandırma kuralı farkındadır ve böylece ona uyması dosyaları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-128">The portal is aware of the naming convention and so can display files that adhere to it.</span></span>

<span data-ttu-id="1097b-129">.NET için dosyası kuralları kitaplığı depolama kapsayıcıları ve Görev çıkış dosyalarını standart dosya kurallarına göre otomatik olarak adlandırır.</span><span class="sxs-lookup"><span data-stu-id="1097b-129">The File Conventions library for .NET automatically names your storage containers and task output files according to the File Conventions standard.</span></span> <span data-ttu-id="1097b-130">Dosya kuralları kitaplık ayrıca iş kimliği, görev kimliği veya amaca göre Azure storage'da çıktı dosyaları sorgulamak için yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="1097b-130">The File Conventions library also provides methods to query output files in Azure Storage according to job ID, task ID, or purpose.</span></span>   

<span data-ttu-id="1097b-131">.NET dışında bir dil ile geliştiriyorsanız, uygulamanızda kendiniz dosyası kuralları standart uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-131">If you are developing with a language other than .NET, you can implement the File Conventions standard yourself in your application.</span></span> <span data-ttu-id="1097b-132">Daha fazla bilgi için bkz: [toplu iş dosyası kuralları hakkında standart](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="1097b-132">For more information, see [About the Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-to-your-batch-account"></a><span data-ttu-id="1097b-133">Batch hesabınıza bir Azure depolama hesabı bağlantı</span><span class="sxs-lookup"><span data-stu-id="1097b-133">Link an Azure Storage account to your Batch account</span></span>

<span data-ttu-id="1097b-134">Çıktı verileri Azure dosyası kuralları kitaplığını kullanarak kalıcı hale getirmek için bir Azure depolama hesabı toplu işlem hesabınıza bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1097b-134">To persist output data to Azure Storage using the File Conventions library, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="1097b-135">Henüz yapmadıysanız, bir depolama hesabı toplu işlem hesabınızı kullanarak bağlantı [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="1097b-135">If you haven't done so already, link a Storage account to your Batch account by using the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="1097b-136">Azure portalında Batch hesabınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="1097b-136">Navigate to your Batch account in the Azure portal.</span></span> 
2. <span data-ttu-id="1097b-137">Altında **ayarları**seçin **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="1097b-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="1097b-138">Batch hesabınızla ilişkili bir depolama hesabı zaten yoksa tıklatın **depolama hesabı (hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="1097b-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="1097b-139">Aboneliğiniz için listeden bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="1097b-139">Select a Storage account from the list for your subscription.</span></span> <span data-ttu-id="1097b-140">En iyi performans için görevlerinizi çalıştırdığı aynı bölgede toplu işlem hesabı olan bir Azure depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1097b-140">For best performance, use an Azure Storage account that is in the same region as the Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="1097b-141">Çıktı verilerini Sürdür</span><span class="sxs-lookup"><span data-stu-id="1097b-141">Persist output data</span></span>

<span data-ttu-id="1097b-142">İş ve görev çıktı verileri dosyası kuralları kitaplığıyla kalıcı hale getirmek için Azure Storage'da kapsayıcı oluşturma ve kapsayıcıya çıkış kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1097b-142">To persist job and task output data with the File Conventions library, create a container in Azure Storage, then save the output to the container.</span></span> <span data-ttu-id="1097b-143">Kullanım [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage) görev çıktısı kapsayıcıya karşıya yüklemek için görev kodunuzda.</span><span class="sxs-lookup"><span data-stu-id="1097b-143">Use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code to upload the task output to the container.</span></span> 

<span data-ttu-id="1097b-144">Kapsayıcılar ve bloblar Azure depolama ile çalışma hakkında daha fazla bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="1097b-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="1097b-145">Kitaplığı, aynı kapsayıcıda depolanır dosyası kuralları olan tüm iş ve görev çıktıları kalıcı.</span><span class="sxs-lookup"><span data-stu-id="1097b-145">All job and task outputs persisted with the File Conventions library are stored in the same container.</span></span> <span data-ttu-id="1097b-146">Çok sayıda görevler dosyaları aynı anda kalıcı çalışırsanız [azaltma sınırları depolama](../storage/common/storage-performance-checklist.md#blobs) zorlanabilir.</span><span class="sxs-lookup"><span data-stu-id="1097b-146">If a large number of tasks try to persist files at the same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="1097b-147">Depolama kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1097b-147">Create storage container</span></span>

<span data-ttu-id="1097b-148">Görev çıktısını Azure depolama için kalıcı hale getirmek için önce bir kapsayıcı çağırarak oluşturmak [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="1097b-148">To persist task output to Azure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="1097b-149">Bu uzantı metodu geçen bir [CloudStorageAccount] [ net_cloudstorageaccount] nesnesini parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="1097b-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="1097b-150">İçeriği Azure portal tarafından keşfedilebilir; böylece dosya kuralları standart göre adlı bir kapsayıcı ve makalenin sonraki bölümlerinde ele alma yöntemleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1097b-150">It creates a container named according to the File Conventions standard,so that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span></span>

<span data-ttu-id="1097b-151">Genellikle istemci uygulamanız bir kapsayıcı oluşturmak için kodu yerleştirdiğiniz &mdash; havuzlar, işler ve görevler oluşturan uygulamayı.</span><span class="sxs-lookup"><span data-stu-id="1097b-151">You typically place the code to create a container in your client application &mdash; the application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference to the linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create the blob storage container for the outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="1097b-152">Depolama görev çıkarır</span><span class="sxs-lookup"><span data-stu-id="1097b-152">Store task outputs</span></span>

<span data-ttu-id="1097b-153">Azure storage'da kapsayıcı hazırladığınıza göre görevleri çıkış kapsayıcıya kullanarak kaydedebilirsiniz [TaskOutputStorage] [ net_taskoutputstorage] dosyası kuralları Kitaplığı'nda sınıfı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="1097b-153">Now that you've prepared a container in Azure Storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the File Conventions library.</span></span>

<span data-ttu-id="1097b-154">Görev kodunuzda ilk oluşturun bir [TaskOutputStorage] [ net_taskoutputstorage] nesne sonra görev kendi iş tamamlandığında, çağrı [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] çıktısını Azure depolamasına kaydetmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="1097b-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code to process data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="1097b-155">`kind` Parametresinin [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) yöntemi kalıcı dosyaları kategorilere ayırır.</span><span class="sxs-lookup"><span data-stu-id="1097b-155">The `kind` parameter of the [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes the persisted files.</span></span> <span data-ttu-id="1097b-156">Dört önceden tanımlanmış vardır [TaskOutputKind] [ net_taskoutputkind] türleri: `TaskOutput`, `TaskPreview`, `TaskLog`, ve `TaskIntermediate.` çıktı özel kategoriler de tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="1097b-157">Bu çıktı türleri toplu belirli bir görevi kalıcı çıkışlar için daha sonra sorguladığınızda listelemek için çıktı türünü belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1097b-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span></span> <span data-ttu-id="1097b-158">Diğer bir deyişle, bir görev çıktıları listelediğinizde çıkış türlerinden birini listede filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span></span> <span data-ttu-id="1097b-159">Örneğin, "ver *Önizleme* için görev çıktısını *109*."</span><span class="sxs-lookup"><span data-stu-id="1097b-159">For example, "Give me the *preview* output for task *109*."</span></span> <span data-ttu-id="1097b-160">Listeleme ve çıkışları alma hakkında daha fazla görünür [almak çıktı](#retrieve-output) sonraki makalede.</span><span class="sxs-lookup"><span data-stu-id="1097b-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span></span>

> [!TIP]
> <span data-ttu-id="1097b-161">Çıktı türü de Azure portalında belirli bir dosya göründüğü belirler: *TaskOutput*-kategorilere ayrılmış dosyaları görünür altında **Görev çıkış dosyaları**, ve *TaskLog* dosyaları görünür altında **görev günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="1097b-161">The output kind also determines where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="1097b-162">Mağaza iş çıkarır</span><span class="sxs-lookup"><span data-stu-id="1097b-162">Store job outputs</span></span>

<span data-ttu-id="1097b-163">Görev çıktıları depolamak ek olarak, tüm bir işle ilişkili çıkışları depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span></span> <span data-ttu-id="1097b-164">Örneğin, bir filmi işleme iş birleştirme görevinde, tamamen işlenmiş film iş çıktısı kalıcı olamadı.</span><span class="sxs-lookup"><span data-stu-id="1097b-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span></span> <span data-ttu-id="1097b-165">İş tamamlandığında, istemci uygulaması listesinde ve işi için çıkış almak ve tek tek görevler sorgu gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1097b-165">When your job is completed, your client application can list and retrieve the outputs for the job, and does not need to query the individual tasks.</span></span>

<span data-ttu-id="1097b-166">İş çıktısı çağırarak depolamak [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] yöntemini belirtin [JobOutputKind] [ net_joboutputkind] ve dosya adı:</span><span class="sxs-lookup"><span data-stu-id="1097b-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="1097b-167">İle **TaskOutputKind** türü görev çıktıları için kullandığınız [JobOutputKind] [ net_joboutputkind] bir işi kategorilere ayırma türü dosyaları kalıcı.</span><span class="sxs-lookup"><span data-stu-id="1097b-167">As with the **TaskOutputKind** type for task outputs, you use the [JobOutputKind][net_joboutputkind] type to categorize a job's persisted files.</span></span> <span data-ttu-id="1097b-168">Bu parametre için sonraki sorgu (liste) belirli bir çıkış türü sağlar.</span><span class="sxs-lookup"><span data-stu-id="1097b-168">This parameter allows you to later query for (list) a specific type of output.</span></span> <span data-ttu-id="1097b-169">**JobOutputKind** türü çıkış ve önizleme kategorileri içerir ve özel kategoriler oluşturulmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="1097b-169">The **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="1097b-170">Depolama görev günlükleri</span><span class="sxs-lookup"><span data-stu-id="1097b-170">Store task logs</span></span>

<span data-ttu-id="1097b-171">Bir görev veya iş tamamlandığında dayanıklı depolama bir dosyaya kalıcı ek olarak, bir görevin yürütülmesi sırasında güncelleştirilen dosyalar kalıcı gerekebilir &mdash; günlük dosyalarını veya `stdout.txt` ve `stderr.txt`, örneğin.</span><span class="sxs-lookup"><span data-stu-id="1097b-171">In addition to persisting a file to durable storage when a task or job completes, you may need to persist files that are updated during the execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="1097b-172">Bu amaç için Azure toplu işlem dosyası kuralları kitaplığı sağlayan [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1097b-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="1097b-173">İle [SaveTrackedAsync][net_savetrackedasync], bir dosyaya (belirttiğiniz bir aralıkta) düğümünde güncelleştirmeleri izlemek ve bu güncelleştirmeleri Azure Storage kalır.</span><span class="sxs-lookup"><span data-stu-id="1097b-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span></span>

<span data-ttu-id="1097b-174">Aşağıdaki kod parçacığında kullanırız [SaveTrackedAsync] [ net_savetrackedasync] güncelleştirmek için `stdout.txt` görevin yürütülmesi sırasında 15 dakikada Azure storage'da:</span><span class="sxs-lookup"><span data-stu-id="1097b-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// The primary task logic is wrapped in a using statement that sends updates to
// the stdout.txt blob in Storage every 15 seconds while the task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code to process data and produce output file(s) */

    // We are tracking the disk file to save our standard output, but the
    // node agent may take up to 3 seconds to flush the stdout stream to
    // disk. So give the file a moment to catch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="1097b-175">Açıklamalı bölüm `Code to process data and produce output file(s)` göreviniz normalde gerçekleştireceği kodu için bir yer tutucudur.</span><span class="sxs-lookup"><span data-stu-id="1097b-175">The commented section `Code to process data and produce output file(s)` is a placeholder for the code that your task would normally perform.</span></span> <span data-ttu-id="1097b-176">Örneğin, veriler Azure depolama biriminden yükler ve dönüşüm ya da hesaplama üzerinde gerçekleştiren kodu olabilir.</span><span class="sxs-lookup"><span data-stu-id="1097b-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="1097b-177">Bu tür kodda nasıl kayabilir bu parçacığı önemli bir parçası gösteren bir `using` sahip bir dosya düzenli olarak güncelleştirmek için blok [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="1097b-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="1097b-178">Düğüm Aracısı havuzdaki her düğüm üzerinde çalışır ve düğümü ile Batch hizmeti arasındaki komut ve denetim arabirimi sağlayan bir programdır.</span><span class="sxs-lookup"><span data-stu-id="1097b-178">The node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="1097b-179">`Task.Delay` Çağrıdır sonunda bu gerekli `using` blok düğümü aracı düğümü üzerindeki stdout.txt dosyaya standart dışı içeriğini temizlemek için zaman sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1097b-179">The `Task.Delay` call is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node.</span></span> <span data-ttu-id="1097b-180">Bu gecikme olmadan çıkış son birkaç saniye kaçırılması mümkündür.</span><span class="sxs-lookup"><span data-stu-id="1097b-180">Without this delay, it is possible to miss the last few seconds of output.</span></span> <span data-ttu-id="1097b-181">Bu gecikme tüm dosyaları için gerekli olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="1097b-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="1097b-182">Dosya ile izleme etkinleştirdiğinizde **SaveTrackedAsync**, yalnızca *ekler* izlenen dosyası Azure depolama alanına kalıcı.</span><span class="sxs-lookup"><span data-stu-id="1097b-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* to the tracked file are persisted to Azure Storage.</span></span> <span data-ttu-id="1097b-183">Yalnızca döndürme olmayan günlük dosyalarını veya dosyanın sonuna ekleme işlemleri ile yazılan diğer dosyalarını izlemek için bu yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="1097b-183">Use this method only for tracking non-rotating log files or other files that are written to with append operations to the end of the file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="1097b-184">Çıktı verilerini alma</span><span class="sxs-lookup"><span data-stu-id="1097b-184">Retrieve output data</span></span>

<span data-ttu-id="1097b-185">Azure toplu işlem dosyası kuralları kitaplığı kullanarak, kalıcı çıktı aldığınızda, görev ve iş merkezli bir şekilde bunu.</span><span class="sxs-lookup"><span data-stu-id="1097b-185">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="1097b-186">Belirtilen çıkış isteyebilir görev ya da Azure Storage veya bile dosya adıyla kendi yolunda bilmenize gerek olmadan iş.</span><span class="sxs-lookup"><span data-stu-id="1097b-186">You can request the output for given task or job without needing to know its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="1097b-187">Bunun yerine, görev tarafından çıktı dosyaları istek veya iş kimliği</span><span class="sxs-lookup"><span data-stu-id="1097b-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="1097b-188">Aşağıdaki kod parçacığını bir işin görevlerini üzerinden tekrarlanan, görev için çıktı dosyaları hakkında bazı bilgiler yazdırır ve sonra dosyalarından depolama biriminden yükler.</span><span class="sxs-lookup"><span data-stu-id="1097b-188">The following code snippet iterates through a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span></span>

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

## <a name="view-output-files-in-the-azure-portal"></a><span data-ttu-id="1097b-189">Azure portalında çıktı dosyalarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="1097b-189">View output files in the Azure portal</span></span>

<span data-ttu-id="1097b-190">Görev çıktı dosyalarını Azure portalı görüntüler ve bağlı bir Azure depolama alanına kalıcı günlükleri kullanarak hesap [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="1097b-190">The Azure portal displays task output files and logs that are persisted to a linked Azure Storage account using the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="1097b-191">Bu kuralları kendiniz de uygulayabileceğiniz bir dil seçiminizi veya .NET uygulamalarınızın dosyası kuralları kitaplıkta kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097b-191">You can implement these conventions yourself in the a language of your choice, or you can use the File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="1097b-192">Çıktı dosyalarınızı Portalı'nda görünen etkinleştirmek için aşağıdaki gereksinimleri karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="1097b-192">To enable the display of your output files in the portal, you must satisfy the following requirements:</span></span>

1. <span data-ttu-id="1097b-193">[Bir Azure depolama hesabı bağlantı](#requirement-linked-storage-account) Batch hesabınıza.</span><span class="sxs-lookup"><span data-stu-id="1097b-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span></span>
2. <span data-ttu-id="1097b-194">Depolama kapsayıcıları ve dosyalar için önceden tanımlanmış adlandırma kuralları için çıkışları kalıcı olduğunda uyar.</span><span class="sxs-lookup"><span data-stu-id="1097b-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="1097b-195">Bu kuralları tanımı dosyası kuralları Kitaplığı'nda bulabilirsiniz [Benioku][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="1097b-195">You can find the definition of these conventions in the File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="1097b-196">Kullanırsanız [Azure toplu işlem dosyası kuralları] [ nuget_package] , çıktı kalıcı hale getirmek için kitaplık dosyası kuralları standart göre dosyalarınıza kalıcı.</span><span class="sxs-lookup"><span data-stu-id="1097b-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, your files are persisted according to the File Conventions standard.</span></span>

<span data-ttu-id="1097b-197">Azure portalında görev çıktı dosyalarını ve günlükleri görüntülemek için ilgilendiğiniz, çıktısı'ye tıklayın ya da görev gidin **kayıtlı çıktı dosyaları** veya **Günlükleri kaydedilen**.</span><span class="sxs-lookup"><span data-stu-id="1097b-197">To view task output files and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="1097b-198">Bu görüntü gösterir **kayıtlı çıktı dosyaları** "007" kimlikli görev için:</span><span class="sxs-lookup"><span data-stu-id="1097b-198">This image shows the **Saved output files** for the task with ID "007":</span></span>

<span data-ttu-id="1097b-199">![Azure portalında görev çıktıları dikey penceresi][2]</span><span class="sxs-lookup"><span data-stu-id="1097b-199">![Task outputs blade in the Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="1097b-200">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="1097b-200">Code sample</span></span>

<span data-ttu-id="1097b-201">[PersistOutputs] [ github_persistoutputs] örnek proje biridir [Azure Batch kod örnekleri] [ github_samples] github'da.</span><span class="sxs-lookup"><span data-stu-id="1097b-201">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="1097b-202">Bu Visual Studio çözümü Azure toplu işlem dosyası kuralları Kitaplığı görev çıktısını dayanıklı depolama için kalıcı hale getirmek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1097b-202">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span></span> <span data-ttu-id="1097b-203">Örneği çalıştırmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="1097b-203">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="1097b-204">Projeyi **Visual Studio 2015 veya daha yeni**.</span><span class="sxs-lookup"><span data-stu-id="1097b-204">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="1097b-205">Batch ve Storage eklemek **hesabının kimlik bilgilerini** için **AccountSettings.settings** öğesini kullanıma alın projesinde.</span><span class="sxs-lookup"><span data-stu-id="1097b-205">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="1097b-206">**Yapı** (ancak çalışmaz) çözümü.</span><span class="sxs-lookup"><span data-stu-id="1097b-206">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="1097b-207">İstenirse herhangi bir NuGet paketinin geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1097b-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="1097b-208">Karşıya yüklemek için Azure portal'ı kullanmanızı bir [uygulama paketi](batch-application-packages.md) için **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="1097b-208">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="1097b-209">Dahil `PersistOutputsTask.exe` ve uygulama kimliği "PersistOutputsTask" ve "1.0" uygulama paketi sürümüne bağımlı derlemeleri .zip paketindeki ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1097b-209">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="1097b-210">**Başlat** (Çalıştır) **PersistOutputs** projesi.</span><span class="sxs-lookup"><span data-stu-id="1097b-210">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="1097b-211">Örnek çalıştırmak için kullanmak için girin Kalıcılık teknolojisi seçmek için istendiğinde **1** görev çıktısını kalıcı hale getirmek için dosya kuralları kitaplığı kullanılarak örneği çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="1097b-211">When prompted to choose the persistence technology to use for running the sample, enter **1** to run the sample using the File Conventions library to persist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1097b-212">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1097b-212">Next steps</span></span>

### <a name="get-the-batch-file-conventions-library-for-net"></a><span data-ttu-id="1097b-213">Toplu iş dosyası kuralları kitaplığı için .NET Al</span><span class="sxs-lookup"><span data-stu-id="1097b-213">Get the Batch File Conventions library for .NET</span></span>

<span data-ttu-id="1097b-214">.NET için toplu iş dosyası kuralları kitaplığı kullanılabilir [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="1097b-214">The Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="1097b-215">Kitaplık genişletir [CloudJob] [ net_cloudjob] ve [CloudTask] [ net_cloudtask] yeni yöntemleri sınıflarıyla.</span><span class="sxs-lookup"><span data-stu-id="1097b-215">The library extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="1097b-216">Ayrıca bkz. [başvuru belgelerini](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) dosyası kuralları kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="1097b-216">Also see the [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for the File Conventions library.</span></span>

<span data-ttu-id="1097b-217">[Kaynak kodu] [ github_file_conventions] için dosya kuralları kitaplığı .NET deposu için Microsoft Azure SDK'sı Github'da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1097b-217">The [source code][github_file_conventions] for the File Conventions library is available on GitHub in the Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="1097b-218">Diğer yaklaşımlar kalıcı çıkış verileri keşfedin</span><span class="sxs-lookup"><span data-stu-id="1097b-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="1097b-219">Bkz: [iş ve görev çıktı Azure depolama için kalıcı](batch-task-output.md) kalıcı görevi ve iş verileri genel bakış.</span><span class="sxs-lookup"><span data-stu-id="1097b-219">See [Persist job and task output to Azure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="1097b-220">Bkz: [kalan görev verileri toplu ile Azure depolama hizmeti API](batch-task-output-files.md) Batch hizmeti API'si çıktı verilerini kalıcı hale getirmek için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1097b-220">See [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md) to learn how to use the Batch service API to persist output data.</span></span>

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
[2]: ./media/batch-task-output/task-output-02.png "Azure portalında görev çıktıları dikey penceresi"
