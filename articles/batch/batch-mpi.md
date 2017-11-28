---
title: "Azure Batch MPI uygulamaları - çalıştırmak için çok örnekli görevleri kullanma | Microsoft Docs"
description: "Çok örnekli görev türü kullanarak Azure Batch'de ileti geçirme arabirimi (MPI) uygulamaları çalıştırma hakkında bilgi edinin."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77d12d6d48b22dfb3e7f09f273dffc11401bb15f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-multi-instance-tasks-to-run-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="f8984-103">Batch'de ileti geçirme arabirimi (MPI) uygulamalarını çalıştırmak için çok örnekli görevleri kullanma</span><span class="sxs-lookup"><span data-stu-id="f8984-103">Use multi-instance tasks to run Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="f8984-104">Çok örnekli görevler, bir Azure Batch görev birden çok işlem düğümlerinde aynı anda çalışmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f8984-104">Multi-instance tasks allow you to run an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="f8984-105">Bu görevler, ileti geçirme arabirimi (MPI) uygulamalarını toplu gibi senaryoları yüksek performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8984-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="f8984-106">Bu makalede, kullanarak çok örnekli görevleri çalıştırma hakkında bilgi edinin [Batch .NET] [ api_net] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="f8984-106">In this article, you learn how to execute multi-instance tasks using the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="f8984-107">Batch .NET, MS-MPI, bu makaledeki örneklerde odaklanmanıza ve Windows işlem düğümleri olsa da, burada açıklanan çok örnekli görev kavramlar, diğer platformlar ve teknolojiler (Python ve Linux düğümleri, örneğin üzerinde Intel MPI) için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f8984-107">While the examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, the multi-instance task concepts discussed here are applicable to other platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="f8984-108">Çok örnekli görev genel bakış</span><span class="sxs-lookup"><span data-stu-id="f8984-108">Multi-instance task overview</span></span>
<span data-ttu-id="f8984-109">Toplu işlemde her normalde bir görevdir tek işlem düğümü üzerinde--yürütülen bir iş birden çok görevler gönderebilir ve toplu işlem hizmetinin her görev bir düğümde yürütülmek zamanlar.</span><span class="sxs-lookup"><span data-stu-id="f8984-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks to a job, and the Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="f8984-110">Ancak, bir görevin yapılandırma tarafından **çok örnekli ayarları**, bunun yerine bir birincil görev ve sonra birden çok düğümde yürütülen çeşitli görevleri oluşturmak üzere toplu söyleyin.</span><span class="sxs-lookup"><span data-stu-id="f8984-110">However, by configuring a task's **multi-instance settings**, you tell Batch to instead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="f8984-111">![Çok örnekli görev genel bakış][1]</span><span class="sxs-lookup"><span data-stu-id="f8984-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="f8984-112">Bir iş çok örnekli ayarlarla bir görev gönderdiğinizde, toplu iş çok örnekli görevleri benzersiz çeşitli adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="f8984-112">When you submit a task with multi-instance settings to a job, Batch performs several steps unique to multi-instance tasks:</span></span>

1. <span data-ttu-id="f8984-113">Batch hizmeti bir oluşturur **birincil** ve birkaç **görevleri** çok örnekli ayarlara göre.</span><span class="sxs-lookup"><span data-stu-id="f8984-113">The Batch service creates one **primary** and several **subtasks** based on the multi-instance settings.</span></span> <span data-ttu-id="f8984-114">Görevler (tüm alt birincil) toplam sayısı sayısıyla eşleştiğini **örnekleri** (işlem düğümleri) çok örnekli ayarlarında belirtin.</span><span class="sxs-lookup"><span data-stu-id="f8984-114">The total number of tasks (primary plus all subtasks) matches the number of **instances** (compute nodes) you specify in the multi-instance settings.</span></span>
2. <span data-ttu-id="f8984-115">Toplu işlem düğümleri olarak birini atar **ana**ve ana yürütmek için birincil görev zamanlar.</span><span class="sxs-lookup"><span data-stu-id="f8984-115">Batch designates one of the compute nodes as the **master**, and schedules the primary task to execute on the master.</span></span> <span data-ttu-id="f8984-116">Çok örnekli görev, bir alt düğüm başına ayrılan işlem düğümleri geri kalanı yürütmek için alt görevler zamanlar.</span><span class="sxs-lookup"><span data-stu-id="f8984-116">It schedules the subtasks to execute on the remainder of the compute nodes allocated to the multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="f8984-117">Birincil ve tüm alt görevler herhangi indirme **ortak kaynak dosyaları** çok örnekli ayarlarında belirtin.</span><span class="sxs-lookup"><span data-stu-id="f8984-117">The primary and all subtasks download any **common resource files** you specify in the multi-instance settings.</span></span>
4. <span data-ttu-id="f8984-118">Sonra ortak kaynak dosyaları yüklenmiş, birincil ve alt görevleri yürütme **koordinasyon komutu** çok örnekli ayarlarında belirtin.</span><span class="sxs-lookup"><span data-stu-id="f8984-118">After the common resource files have been downloaded, the primary and subtasks execute the **coordination command** you specify in the multi-instance settings.</span></span> <span data-ttu-id="f8984-119">Düzenleme komutu genellikle görev yürütmek için düğümleri hazırlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f8984-119">The coordination command is typically used to prepare nodes for executing the task.</span></span> <span data-ttu-id="f8984-120">Bu arka plan Hizmetleri başlatma içerebilir (gibi [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) ve düğümlerin düğümler arası iletileri işlemek hazır olduğunu doğrulama.</span><span class="sxs-lookup"><span data-stu-id="f8984-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that the nodes are ready to process inter-node messages.</span></span>
5. <span data-ttu-id="f8984-121">Birincil görevi yürütür **uygulama komutu** ana düğüm üzerinde *sonra* koordinasyon komutu başarıyla birincil ve tüm alt görevler tarafından tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="f8984-121">The primary task executes the **application command** on the master node *after* the coordination command has been completed successfully by the primary and all subtasks.</span></span> <span data-ttu-id="f8984-122">Uygulama komutu çok örnekli görev komut satırı ve yalnızca birincil görev tarafından yürütülen.</span><span class="sxs-lookup"><span data-stu-id="f8984-122">The application command is the command line of the multi-instance task itself, and is executed only by the primary task.</span></span> <span data-ttu-id="f8984-123">İçinde bir [MS MPI][msmpi_msdn]-tabanlı çözümün, burada kullanarak MPI özellikli uygulamanızı yürütme budur `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="f8984-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="f8984-124">İşlevsel olarak ayrı olsa da, "çok örnekli görev" gibi benzersiz görev türü değil [StartTask] [ net_starttask] veya [JobPreparationTask][net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="f8984-124">Though it is functionally distinct, the "multi-instance task" is not a unique task type like the [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="f8984-125">Çok örnekli görev yalnızca standart bir Batch görevinde olduğu ([CloudTask] [ net_task] Batch .NET içinde), çok örnekli ayarları yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="f8984-125">The multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="f8984-126">Bu makalede, biz bu başvurmak **çok örnekli görev**.</span><span class="sxs-lookup"><span data-stu-id="f8984-126">In this article, we refer to this as the **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="f8984-127">Çok örnekli görevler için gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="f8984-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="f8984-128">Çok örnekli görevleri gerektiren bir havuzla **etkin düğümler arası iletişim**ile **eşzamanlı görev yürütme devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="f8984-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="f8984-129">Eşzamanlı görev yürütme devre dışı bırakmak için ayarlanmış [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) özelliği 1.</span><span class="sxs-lookup"><span data-stu-id="f8984-129">To disable concurrent task execution, set the [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property to 1.</span></span>

<span data-ttu-id="f8984-130">Bu kod parçacığını bir havuz Batch .NET kitaplığını kullanarak çok örnekli görevleri için oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f8984-130">This code snippet shows how to create a pool for multi-instance tasks using the Batch .NET library.</span></span>

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> <span data-ttu-id="f8984-131">Düğümler arası iletişim devre dışı veya ile bir havuzda çok örnekli görev çalıştırmayı denerseniz bir *maxTasksPerNode* 1'den büyük değer, görev hiçbir zaman zamanlanmış--süresiz olarak "etkin" durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="f8984-131">If you try to run a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, the task is never scheduled--it remains indefinitely in the "active" state.</span></span> 
>
> <span data-ttu-id="f8984-132">Çok örnekli görevler yalnızca 14 Aralık 2015 tarihinden sonra oluşturulan havuzlarında düğümlerinde yürütebilir.</span><span class="sxs-lookup"><span data-stu-id="f8984-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-to-install-mpi"></a><span data-ttu-id="f8984-133">MPI yüklemek için StartTask kullanın</span><span class="sxs-lookup"><span data-stu-id="f8984-133">Use a StartTask to install MPI</span></span>
<span data-ttu-id="f8984-134">Çok örnekli görev MPI uygulamaları çalıştırmak için önce havuzundaki işlem düğümlerinde MPI uygulaması (MS-MPI veya örneğin Intel MPI) yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8984-134">To run MPI applications with a multi-instance task, you first need to install an MPI implementation (MS-MPI or Intel MPI, for example) on the compute nodes in the pool.</span></span> <span data-ttu-id="f8984-135">Bu kullanmak için iyi bir zamandır bir [StartTask][net_starttask], her bir düğümün bir havuzuna katılır veya yeniden yürütür.</span><span class="sxs-lookup"><span data-stu-id="f8984-135">This is a good time to use a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="f8984-136">Bu kod parçacığını MS MPI kurulum paketi olarak belirten bir StartTask oluşturur bir [kaynak dosyası][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="f8984-136">This code snippet creates a StartTask that specifies the MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="f8984-137">Başlangıç görevinin komut satırı kaynak dosyası düğüme İndirildikten sonra yürütülür.</span><span class="sxs-lookup"><span data-stu-id="f8984-137">The start task's command line is executed after the resource file is downloaded to the node.</span></span> <span data-ttu-id="f8984-138">Bu durumda, komut satırı katılımsız yükleme MS MPI işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="f8984-138">In this case, the command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for the pool which we use for installing MS-MPI on
// the nodes as they join the pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit the fully configured pool to the Batch service to actually create
// the pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="f8984-139">Doğrudan uzak bellek erişimi (RDMA)</span><span class="sxs-lookup"><span data-stu-id="f8984-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="f8984-140">Seçeneğini belirlediğinizde bir [RDMA özellikli boyutu](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) , Batch havuzundaki işlem düğümleri için A9 gibi MPI uygulamanızı Azure'nın yüksek performans, düşük gecikme süreli doğrudan uzak bellek erişimi (RDMA) ağ avantajından yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8984-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for the compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="f8984-141">Aşağıdaki makalelerde "RDMA özellikli" belirtilen boyutlarını arayın:</span><span class="sxs-lookup"><span data-stu-id="f8984-141">Look for the sizes specified as "RDMA capable" in the following articles:</span></span>

* <span data-ttu-id="f8984-142">**CloudServiceConfiguration** havuzları</span><span class="sxs-lookup"><span data-stu-id="f8984-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="f8984-143">[Cloud Services boyutları](../cloud-services/cloud-services-sizes-specs.md) (yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="f8984-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="f8984-144">**VirtualMachineConfiguration** havuzları</span><span class="sxs-lookup"><span data-stu-id="f8984-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="f8984-145">[Azure sanal makineler için Boyutlar](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="f8984-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="f8984-146">[Azure sanal makineler için Boyutlar](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="f8984-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="f8984-147">RDMA yararlanmak [Linux işlem düğümlerini](batch-linux-nodes.md), kullanmalısınız **Intel MPI** düğümler üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f8984-147">To take advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on the nodes.</span></span> <span data-ttu-id="f8984-148">Havuzu bölümünü CloudServiceConfiguration ve VirtualMachineConfiguration havuzları hakkında daha fazla bilgi için bkz: [Batch özelliklerine genel bakış](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="f8984-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see the Pool section of the [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="f8984-149">Çok örnekli görev Batch .NET ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8984-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="f8984-150">Biz MPI paket yükleme ve havuzu gereksinimlerini ele, çok örnekli görev oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="f8984-150">Now that we've covered the pool requirements and MPI package installation, let's create the multi-instance task.</span></span> <span data-ttu-id="f8984-151">Bu parçacığında, bir standart oluşturuyoruz [CloudTask][net_task], ardından yapılandırma kendi [MultiInstanceSettings] [ net_multiinstance_prop] özelliği.</span><span class="sxs-lookup"><span data-stu-id="f8984-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="f8984-152">Daha önce belirtildiği gibi çok örnekli görev farklı görev türü, ancak çok örnekli ayarlarla yapılandırılan standart bir Batch görevinde değil.</span><span class="sxs-lookup"><span data-stu-id="f8984-152">As mentioned earlier, the multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create the multi-instance task. Its command line is the "application command"
// and will be executed *only* by the primary, and only after the primary and
// subtasks execute the CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure the task's MultiInstanceSettings. The CoordinationCommandLine will be executed by
// the primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit the task to the job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on the nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="f8984-153">Birincil görevi ve alt görevler</span><span class="sxs-lookup"><span data-stu-id="f8984-153">Primary task and subtasks</span></span>
<span data-ttu-id="f8984-154">Bir görev için çok örnekli ayarları oluşturduğunuzda, görev yürütmek üzere olduğunuz işlem düğümü sayısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="f8984-154">When you create the multi-instance settings for a task, you specify the number of compute nodes that are to execute the task.</span></span> <span data-ttu-id="f8984-155">Bir iş görevi gönderdiğinizde, Batch hizmeti bir oluşturur **birincil** görev ve yeterli **görevleri** belirttiğiniz düğüm sayısını birlikte eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="f8984-155">When you submit the task to a job, the Batch service creates one **primary** task and enough **subtasks** that together match the number of nodes you specified.</span></span>

<span data-ttu-id="f8984-156">Bu görevler için 0 aralığında bir tamsayı kimliği atanır *numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="f8984-156">These tasks are assigned an integer id in the range of 0 to *numberOfInstances* - 1.</span></span> <span data-ttu-id="f8984-157">Kimliği 0 olan görev birincil bir görevdir ve diğer tüm kimliklerini görevleridir.</span><span class="sxs-lookup"><span data-stu-id="f8984-157">The task with id 0 is the primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="f8984-158">Örneğin, bir görev için aşağıdaki çok örnekli ayarları oluşturursanız, birincil görev 0 bir kimliğe sahip ve alt görevler kimlikleri 1 ile 9 arasında olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8984-158">For example, if you create the following multi-instance settings for a task, the primary task would have an id of 0, and the subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="f8984-159">Ana düğüm</span><span class="sxs-lookup"><span data-stu-id="f8984-159">Master node</span></span>
<span data-ttu-id="f8984-160">Çok örnekli görev gönderdiğinizde, Batch hizmeti işlem düğümlerinden biri olarak "Yönetici" düğümü atar ve ana düğümde yürütmek için birincil görev zamanlar.</span><span class="sxs-lookup"><span data-stu-id="f8984-160">When you submit a multi-instance task, the Batch service designates one of the compute nodes as the "master" node, and schedules the primary task to execute on the master node.</span></span> <span data-ttu-id="f8984-161">Alt görevler için çok örnekli görev ayrılan düğümler kalanı yürütmek üzere zamanlanır.</span><span class="sxs-lookup"><span data-stu-id="f8984-161">The subtasks are scheduled to execute on the remainder of the nodes allocated to the multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="f8984-162">Düzenleme komutu</span><span class="sxs-lookup"><span data-stu-id="f8984-162">Coordination command</span></span>
<span data-ttu-id="f8984-163">**Koordinasyon komutu** birincil tarafından yürütülen ve alt görevlerin.</span><span class="sxs-lookup"><span data-stu-id="f8984-163">The **coordination command** is executed by both the primary and subtasks.</span></span>

<span data-ttu-id="f8984-164">Düzenleme komutu çağırma engelleme--toplu düzenleme komutu için tüm görevleri başarıyla verdi kadar uygulama komutu yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="f8984-164">The invocation of the coordination command is blocking--Batch does not execute the application command until the coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="f8984-165">Düzenleme komutu bu nedenle tüm gerekli arka plan hizmetleri başlatmak, kullanıma hazır olduğunu doğrulayın ve sonra çıkın.</span><span class="sxs-lookup"><span data-stu-id="f8984-165">The coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="f8984-166">Örneğin, bu düzenleme komut 7 düğümde SMPD hizmeti başlatılır MS MPI sürümünü kullanan bir çözüm için çıkar:</span><span class="sxs-lookup"><span data-stu-id="f8984-166">For example, this coordination command for a solution using MS-MPI version 7 starts the SMPD service on the node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="f8984-167">Kullanımına dikkat edin `start` bu koordinasyon komutu.</span><span class="sxs-lookup"><span data-stu-id="f8984-167">Note the use of `start` in this coordination command.</span></span> <span data-ttu-id="f8984-168">Bu gereklidir çünkü `smpd.exe` uygulama hemen yürütme sonrasında döndürmez.</span><span class="sxs-lookup"><span data-stu-id="f8984-168">This is required because the `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="f8984-169">Kullanmadan [Başlat] [ cmd_start] komutu, bu düzenleme komut değil döndürür ve bu nedenle uygulama komutu çalışmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="f8984-169">Without the use of the [start][cmd_start] command, this coordination command would not return, and would therefore block the application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="f8984-170">Uygulama komutu</span><span class="sxs-lookup"><span data-stu-id="f8984-170">Application command</span></span>
<span data-ttu-id="f8984-171">Düzenleme komutu yürütülürken birincil görev ve tüm görevleri tamamladıktan sonra çok örnekli görevin komut satırı birincil görev tarafından yürütülen *yalnızca*.</span><span class="sxs-lookup"><span data-stu-id="f8984-171">Once the primary task and all subtasks have finished executing the coordination command, the multi-instance task's command line is executed by the primary task *only*.</span></span> <span data-ttu-id="f8984-172">Bu diyoruz **uygulama komutu** koordinasyon komuttan ayırt etmek için.</span><span class="sxs-lookup"><span data-stu-id="f8984-172">We call this the **application command** to distinguish it from the coordination command.</span></span>

<span data-ttu-id="f8984-173">MS-MPI uygulamaları için uygulama MPI etkin uygulamanızla yürütmek için komutunu `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="f8984-173">For MS-MPI applications, use the application command to execute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="f8984-174">Örneğin, MS-MPI sürüm 7 kullanarak bir çözüm için bir uygulama komutu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f8984-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="f8984-175">Çünkü MS-MPI's `mpiexec.exe` kullanan `CCP_NODES` değişken varsayılan olarak (bkz [ortam değişkenleri](#environment-variables)), yukarıdaki örnek uygulama komut satırı dışlar.</span><span class="sxs-lookup"><span data-stu-id="f8984-175">Because MS-MPI's `mpiexec.exe` uses the `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) the example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="f8984-176">Ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="f8984-176">Environment variables</span></span>
<span data-ttu-id="f8984-177">Toplu oluşturur birkaç [ortam değişkenleri] [ msdn_env_var] çok örnekli görevler için çok örnekli görev ayrılan işlem düğümlerinde özgüdür.</span><span class="sxs-lookup"><span data-stu-id="f8984-177">Batch creates several [environment variables][msdn_env_var] specific to multi-instance tasks on the compute nodes allocated to a multi-instance task.</span></span> <span data-ttu-id="f8984-178">Komut dosyaları ve bunların yürütme programları gibi düzenleme ve uygulama komut satırları bu ortam değişkenleri başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="f8984-178">Your coordination and application command lines can reference these environment variables, as can the scripts and programs they execute.</span></span>

<span data-ttu-id="f8984-179">Aşağıdaki ortam değişkenleri çok örnekli görevler tarafından kullanılmak üzere Batch hizmeti tarafından oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="f8984-179">The following environment variables are created by the Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="f8984-180">Düğüm ortam değişkenleri, görünürlük ve içeriği de dahil olmak üzere bunlar üzerinde tam Ayrıntılar ve diğer toplu işlem için bkz: [işlem düğümü ortam değişkenleri][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="f8984-180">For full details on these and the other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="f8984-181">Toplu Linux MPI kod örneği, bu ortam değişkenleri çeşitli nasıl kullanılabileceğini örneği içerir.</span><span class="sxs-lookup"><span data-stu-id="f8984-181">The Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="f8984-182">[Koordinasyon cmd] [ coord_cmd_example] Bash betiğini indirir ortak uygulama ve giriş dosyaları Azure Storage'dan, ana düğüm ağ dosya sistemi (NFS) paylaşımında etkinleştirir ve NFS istemcisi olarak çok örnekli görev ayrılan diğer düğümlere yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f8984-182">The [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on the master node, and configures the other nodes allocated to the multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="f8984-183">Kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="f8984-183">Resource files</span></span>
<span data-ttu-id="f8984-184">Kaynak dosyaları için çok örnekli görevler dikkate alınması gereken iki kümesi vardır: **ortak kaynak dosyaları** , *tüm* görevleri indirin (hem birincil hem de ve alt görevler) ve **kaynak dosyaları** çok örnekli görev için kendisini, belirtilen *yalnızca birincil* görev yüklemeleri.</span><span class="sxs-lookup"><span data-stu-id="f8984-184">There are two sets of resource files to consider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and the **resource files** specified for the multi-instance task itself, which *only the primary* task downloads.</span></span>

<span data-ttu-id="f8984-185">Bir veya daha fazla belirtebilirsiniz **ortak kaynak dosyaları** bir görev için çok örnekli ayarlarında.</span><span class="sxs-lookup"><span data-stu-id="f8984-185">You can specify one or more **common resource files** in the multi-instance settings for a task.</span></span> <span data-ttu-id="f8984-186">Bu ortak kaynak dosyaları karşıdan yüklenir [Azure Storage](../storage/common/storage-introduction.md) her düğümün içine **görev paylaşılan dizine** birincil ve tüm alt görevler.</span><span class="sxs-lookup"><span data-stu-id="f8984-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by the primary and all subtasks.</span></span> <span data-ttu-id="f8984-187">Kullanarak uygulama ve düzenleme komut satırlarından görev paylaşılan dizine erişebilir `AZ_BATCH_TASK_SHARED_DIR` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="f8984-187">You can access the task shared directory from application and coordination command lines by using the `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="f8984-188">`AZ_BATCH_TASK_SHARED_DIR` Yolu için çok örnekli görev ayrılan her düğümde aynı, böylece bir tek koordinasyon komutu birincil ve tüm alt görevler arasında paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8984-188">The `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated to the multi-instance task, thus you can share a single coordination command between the primary and all subtasks.</span></span> <span data-ttu-id="f8984-189">Toplu "bir uzaktan erişim fikir dizininde paylaşmaz", ancak bağlama kullanın ya da ortam değişkenleri ipucu önceki bölümünde belirtildiği gibi noktası paylaşın.</span><span class="sxs-lookup"><span data-stu-id="f8984-189">Batch does not "share" the directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in the tip on environment variables.</span></span>

<span data-ttu-id="f8984-190">Çok örnekli görev için belirttiğiniz kaynak dosyaları, görevin çalışma dizinine yüklenir `AZ_BATCH_TASK_WORKING_DIR`, varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="f8984-190">Resource files that you specify for the multi-instance task itself are downloaded to the task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="f8984-191">, Sık kullanılan kaynak dosyaları aksine belirtildiği gibi yalnızca birincil görev çok örnekli görev kendisi için belirtilen kaynak dosyaları indirir.</span><span class="sxs-lookup"><span data-stu-id="f8984-191">As mentioned, in contrast to common resource files, only the primary task downloads resource files specified for the  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8984-192">Her zaman ortam değişkenlerini kullanma `AZ_BATCH_TASK_SHARED_DIR` ve `AZ_BATCH_TASK_WORKING_DIR` bu dizinleri, komut satırında başvurmak için.</span><span class="sxs-lookup"><span data-stu-id="f8984-192">Always use the environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` to refer to these directories in your command lines.</span></span> <span data-ttu-id="f8984-193">Yollarını el ile oluşturmak çalışmayın.</span><span class="sxs-lookup"><span data-stu-id="f8984-193">Do not attempt to construct the paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="f8984-194">Görev yaşam süresi</span><span class="sxs-lookup"><span data-stu-id="f8984-194">Task lifetime</span></span>
<span data-ttu-id="f8984-195">Birincil görev ömrü tüm çok örnekli görev ömrü denetler.</span><span class="sxs-lookup"><span data-stu-id="f8984-195">The lifetime of the primary task controls the lifetime of the entire multi-instance task.</span></span> <span data-ttu-id="f8984-196">Birincil çıktığında tüm görevleri sonlandırılır.</span><span class="sxs-lookup"><span data-stu-id="f8984-196">When the primary exits, all of the subtasks are terminated.</span></span> <span data-ttu-id="f8984-197">Birincil çıkış kodu, görevin çıkış kodu ve bu nedenle başarı veya başarısızlık görev yeniden deneme amaçlı belirlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f8984-197">The exit code of the primary is the exit code of the task, and is therefore used to determine the success or failure of the task for retry purposes.</span></span>

<span data-ttu-id="f8984-198">Herhangi bir alt görevler başarısız olursa, sıfır olmayan dönüş koduyla çıkma Örneğin, tüm çok örnekli görev başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f8984-198">If any of the subtasks fail, exiting with a non-zero return code, for example, the entire multi-instance task fails.</span></span> <span data-ttu-id="f8984-199">Çok örnekli görev sonra sona erdi ve, yeniden deneme sınırına kadar denenecek.</span><span class="sxs-lookup"><span data-stu-id="f8984-199">The multi-instance task is then terminated and retried, up to its retry limit.</span></span>

<span data-ttu-id="f8984-200">Çok örnekli Görev sildiğinizde, birincil ve tüm alt görevler de Batch hizmeti tarafından silinir.</span><span class="sxs-lookup"><span data-stu-id="f8984-200">When you delete a multi-instance task, the primary and all subtasks are also deleted by the Batch service.</span></span> <span data-ttu-id="f8984-201">Tüm dizinleri eklemeli ve dosyalarına yalnızca standart bir görev için bilgi işlem düğümleri silinir.</span><span class="sxs-lookup"><span data-stu-id="f8984-201">All subtask directories and their files are deleted from the compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="f8984-202">[TaskConstraints] [ net_taskconstraints] için çok örnekli görev gibi [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], ve [RetentionTime] [ net_taskconstraint_retention] bunlar için standart bir görev ve birincil ve tüm alt görevleri uygulamak gibi özelliklerini dikkate alınır.</span><span class="sxs-lookup"><span data-stu-id="f8984-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as the [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply to the primary and all subtasks.</span></span> <span data-ttu-id="f8984-203">Ancak, değiştirirseniz [RetentionTime] [ net_taskconstraint_retention] özelliği bu değişiklik iş için çok örnekli görev ekledikten sonra yalnızca birincil göreve uygulanır.</span><span class="sxs-lookup"><span data-stu-id="f8984-203">However, if you change the [RetentionTime][net_taskconstraint_retention] property after adding the multi-instance task to the job, this change is applied only to the primary task.</span></span> <span data-ttu-id="f8984-204">Tüm alt görevlerin özgün kullanmaya devam [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="f8984-204">All of the subtasks continue to use the original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="f8984-205">Yeni görev çok örnekli görev parçası ise, bir işlem düğümün son kullanılan görevler listesi alt görev kimliği yansıtır.</span><span class="sxs-lookup"><span data-stu-id="f8984-205">A compute node's recent task list reflects the id of a subtask if the recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="f8984-206">Alt görevler hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="f8984-206">Obtain information about subtasks</span></span>
<span data-ttu-id="f8984-207">Batch .NET kitaplığını kullanarak görevleri hakkında bilgi edinmek için arama [CloudTask.ListSubtasks] [ net_task_listsubtasks] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f8984-207">To obtain information on subtasks by using the Batch .NET library, call the [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="f8984-208">Bu yöntem, tüm alt görevler hakkında bilgi ve görevler yürütülen işlem düğümü hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="f8984-208">This method returns information on all subtasks, and information about the compute node that executed the tasks.</span></span> <span data-ttu-id="f8984-209">Bu bilgilerden, her alt ait kök dizini, havuz kimliğini, geçerli durumu, çıkış kodu ve daha fazla belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8984-209">From this information, you can determine each subtask's root directory, the pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="f8984-210">Bu bilgi ile birlikte kullanabileceğiniz [PoolOperations.GetNodeFile] [ poolops_getnodefile] alt görevi'nin dosyaları elde etmek için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f8984-210">You can use this information in combination with the [PoolOperations.GetNodeFile][poolops_getnodefile] method to obtain the subtask's files.</span></span> <span data-ttu-id="f8984-211">Bu yöntem (kimliği 0) birincil görev için bilgi döndürmüyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f8984-211">Note that this method does not return information for the primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="f8984-212">Aksi belirtilmediği sürece, Batch .NET yöntemleri, çalışan çok örneğinde [CloudTask] [ net_task] kendisini uygulamak *yalnızca* birincil görev.</span><span class="sxs-lookup"><span data-stu-id="f8984-212">Unless otherwise stated, Batch .NET methods that operate on the multi-instance [CloudTask][net_task] itself apply *only* to the primary task.</span></span> <span data-ttu-id="f8984-213">Örneğin, size çağırdığınızda [CloudTask.ListNodeFiles] [ net_task_listnodefiles] çok örnekli görev yöntemi, yalnızca birincil görev dosyaları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f8984-213">For example, when you call the [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only the primary task's files are returned.</span></span>
>
>

<span data-ttu-id="f8984-214">Aşağıdaki kod parçacığını gibi alt bilgi elde üzerinde yürütülen düğümlerden dosya içeriklerini isteği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f8984-214">The following code snippet shows how to obtain subtask information, as well as request file contents from the nodes on which they executed.</span></span>

```csharp
// Obtain the job and the multi-instance task from the Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain the list of subtasks for the task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over the subtasks and print their stdout and stderr
// output if the subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a><span data-ttu-id="f8984-215">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="f8984-215">Code sample</span></span>
<span data-ttu-id="f8984-216">[MultiInstanceTasks] [ github_mpi] kodu örneği github'daki çok örnekli görev çalıştırmak için nasıl kullanılacağını gösteren bir [MS MPI] [ msmpi_msdn] uygulama batch işlem düğümlerinde.</span><span class="sxs-lookup"><span data-stu-id="f8984-216">The [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how to use a multi-instance task to run an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="f8984-217">Adımları [hazırlık](#preparation) ve [yürütme](#execution) örneği çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="f8984-217">Follow the steps in [Preparation](#preparation) and [Execution](#execution) to run the sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="f8984-218">Hazırlama</span><span class="sxs-lookup"><span data-stu-id="f8984-218">Preparation</span></span>
1. <span data-ttu-id="f8984-219">İlk iki adımları [derlemek ve basit bir MS-MPI program çalıştırmak nasıl][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="f8984-219">Follow the first two steps in [How to compile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="f8984-220">Aşağıdaki adımı prerequesites karşılar.</span><span class="sxs-lookup"><span data-stu-id="f8984-220">This satisfies the prerequesites for the following step.</span></span>
2. <span data-ttu-id="f8984-221">Derleme bir *sürüm* sürümü [MPIHelloWorld] [ helloworld_proj] örnek MPI programı.</span><span class="sxs-lookup"><span data-stu-id="f8984-221">Build a *Release* version of the [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="f8984-222">Bu işlem düğümlerinde çok örnekli görev tarafından çalıştırılacak programıdır.</span><span class="sxs-lookup"><span data-stu-id="f8984-222">This is the program that will be run on compute nodes by the multi-instance task.</span></span>
3. <span data-ttu-id="f8984-223">İçeren bir zip dosyası oluşturma `MPIHelloWorld.exe` (hangi, 2. adım yerleşik) ve `MSMpiSetup.exe` (hangi indirdiğiniz 1. adım).</span><span class="sxs-lookup"><span data-stu-id="f8984-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="f8984-224">Sonraki adımda bir uygulama paketi olarak bu zip dosyasını yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f8984-224">You'll upload this zip file as an application package in the next step.</span></span>
4. <span data-ttu-id="f8984-225">Kullanım [Azure portal] [ portal] toplu oluşturmak için [uygulama](batch-application-packages.md) "MPIHelloWorld" olarak adlandırılan ve önceki adımda oluşturduğunuz uygulama paketi "1.0" sürümü olarak zip dosyası belirtin.</span><span class="sxs-lookup"><span data-stu-id="f8984-225">Use the [Azure portal][portal] to create a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify the zip file you created in the previous step as version "1.0" of the application package.</span></span> <span data-ttu-id="f8984-226">Bkz: [karşıya yükleyin ve uygulamalarını yönetin](batch-application-packages.md#upload-and-manage-applications) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f8984-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="f8984-227">Derleme bir *sürüm* sürümü `MPIHelloWorld.exe` böylece ek bağımlılıkları içerecek şekilde yoksa (örneğin, `msvcp140d.dll` veya `vcruntime140d.dll`) uygulama paketi.</span><span class="sxs-lookup"><span data-stu-id="f8984-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have to include any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="f8984-228">Yürütme</span><span class="sxs-lookup"><span data-stu-id="f8984-228">Execution</span></span>
1. <span data-ttu-id="f8984-229">Karşıdan [azure-batch-samples] [ github_samples_zip] github'dan.</span><span class="sxs-lookup"><span data-stu-id="f8984-229">Download the [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="f8984-230">MultiInstanceTasks açmak **çözüm** Visual Studio 2015'te ya da daha yeni.</span><span class="sxs-lookup"><span data-stu-id="f8984-230">Open the MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="f8984-231">`MultiInstanceTasks.sln` Çözüm dosyasını bulunur:</span><span class="sxs-lookup"><span data-stu-id="f8984-231">The `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="f8984-232">Batch ve Storage hesabı kimlik bilgilerinizi girin `AccountSettings.settings` içinde **öğesini kullanıma alın** projesi.</span><span class="sxs-lookup"><span data-stu-id="f8984-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in the **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="f8984-233">**Derleme ve çalıştırma** MultiInstanceTasks çözüm MPI yürütmek için örnek bir Batch havuzundaki işlem düğümlerinde uygulama.</span><span class="sxs-lookup"><span data-stu-id="f8984-233">**Build and run** the MultiInstanceTasks solution to execute the MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="f8984-234">*İsteğe bağlı*: kullanım [Azure portal] [ portal] veya [Batch Gezgini] [ batch_explorer] incelemek için örnek havuz, iş ve görev ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask"), önce silmek kaynakları.</span><span class="sxs-lookup"><span data-stu-id="f8984-234">*Optional*: Use the [Azure portal][portal] or the [Batch Explorer][batch_explorer] to examine the sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete the resources.</span></span>

> [!TIP]
> <span data-ttu-id="f8984-235">İndirebilirsiniz [Visual Studio Community] [ visual_studio] ücretsiz Visual Studio yoksa.</span><span class="sxs-lookup"><span data-stu-id="f8984-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="f8984-236">Çıktı `MultiInstanceTasks.exe` aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="f8984-236">Output from `MultiInstanceTasks.exe` is similar to the following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] to job [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks to complete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="f8984-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f8984-237">Next steps</span></span>
* <span data-ttu-id="f8984-238">Microsoft HPC & Azure Batch ekip blogu anlatılmaktadır [MPI desteklemek için Azure batch Linux][blog_mpi_linux]ve kullanma hakkında bilgi içerir [OpenFOAM] [ openfoam] toplu ile.</span><span class="sxs-lookup"><span data-stu-id="f8984-238">The Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="f8984-239">Python kodu örnekleri bulabilirsiniz [OpenFOAM örneği github'daki][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="f8984-239">You can find Python code samples for the [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="f8984-240">Bilgi nasıl [Linux işlem düğümleri havuzları oluşturma](batch-linux-nodes.md) Azure Batch MPI çözümlerinizi kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="f8984-240">Learn how to [create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Çok örnekli genel bakış"
