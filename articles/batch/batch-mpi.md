---
title: "aaaUse çok örnekli görevler toorun MPI uygulamaları - Azure Batch | Microsoft Docs"
description: "Azure Batch hello çok örnekli görev kullanarak tooexecute ileti geçirme arabirimi (MPI) uygulamalarını nasıl yazın öğrenin."
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
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="faa3d-103">Çok örnekli görevler toorun ileti geçirme arabirimi (MPI) uygulamalarını toplu işlemde kullanın</span><span class="sxs-lookup"><span data-stu-id="faa3d-103">Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="faa3d-104">Çok örnekli görevler toorun bir Azure Batch görev birden çok işlem düğümünde eşzamanlı olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="faa3d-104">Multi-instance tasks allow you toorun an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="faa3d-105">Bu görevler, ileti geçirme arabirimi (MPI) uygulamalarını toplu gibi senaryoları yüksek performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="faa3d-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="faa3d-106">Bu makalede, nasıl tooexecute çok örnekli görevleri kullanma hello öğrenin [Batch .NET] [ api_net] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="faa3d-106">In this article, you learn how tooexecute multi-instance tasks using hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="faa3d-107">Batch .NET, MS-MPI, bu makaledeki örneklerde Hello odaklanmanıza ve Windows işlem düğümleri olsa da, burada tartışılan hello çok örnekli görev kavramları geçerli tooother platformlar ve teknolojiler (Python ve Linux düğümleri, örneğin üzerinde Intel MPI) ' dir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-107">While hello examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, hello multi-instance task concepts discussed here are applicable tooother platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="faa3d-108">Çok örnekli görev genel bakış</span><span class="sxs-lookup"><span data-stu-id="faa3d-108">Multi-instance task overview</span></span>
<span data-ttu-id="faa3d-109">Toplu işlemde her normalde bir görevdir tek işlem düğümü üzerinde--yürütülen birden çok görevleri tooa işi göndermek ve hello Batch hizmetinin her görev bir düğümde yürütülmek zamanlar.</span><span class="sxs-lookup"><span data-stu-id="faa3d-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks tooa job, and hello Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="faa3d-110">Bir görevin yapılandırarak ancak **çok örnekli ayarları**, toplu söyleyin tooinstead bir birincil görev ve ardından birden çok düğümde yürütülen çeşitli görevleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="faa3d-110">However, by configuring a task's **multi-instance settings**, you tell Batch tooinstead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="faa3d-111">![Çok örnekli görev genel bakış][1]</span><span class="sxs-lookup"><span data-stu-id="faa3d-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="faa3d-112">Çok örnekli ayarları tooa iş görevle gönderdiğinizde, toplu çeşitli adımları benzersiz toomulti örnekli görevleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="faa3d-112">When you submit a task with multi-instance settings tooa job, Batch performs several steps unique toomulti-instance tasks:</span></span>

1. <span data-ttu-id="faa3d-113">Merhaba Batch hizmeti bir oluşturur **birincil** ve birkaç **görevleri** hello çok örnekli ayarlarınızı temel alan.</span><span class="sxs-lookup"><span data-stu-id="faa3d-113">hello Batch service creates one **primary** and several **subtasks** based on hello multi-instance settings.</span></span> <span data-ttu-id="faa3d-114">Görevler (tüm alt birincil) toplam sayısı Hello eşleşen hello sayısı **örnekleri** (işlem düğümleri) hello çok örnekli ayarlarında belirtin.</span><span class="sxs-lookup"><span data-stu-id="faa3d-114">hello total number of tasks (primary plus all subtasks) matches hello number of **instances** (compute nodes) you specify in hello multi-instance settings.</span></span>
2. <span data-ttu-id="faa3d-115">Toplu atayan hello birini işlem düğümleri hello **ana**, ve zamanlamaları hello hello yöneticisinde birincil görev tooexecute.</span><span class="sxs-lookup"><span data-stu-id="faa3d-115">Batch designates one of hello compute nodes as hello **master**, and schedules hello primary task tooexecute on hello master.</span></span> <span data-ttu-id="faa3d-116">Merhaba görevleri tooexecute hello işlem düğümleri ayrılmış toohello çok örnekli görev, bir alt düğüm başına hello kalanı üzerinde zamanlar.</span><span class="sxs-lookup"><span data-stu-id="faa3d-116">It schedules hello subtasks tooexecute on hello remainder of hello compute nodes allocated toohello multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="faa3d-117">Merhaba birincil ve tüm alt görevler yükleme **ortak kaynak dosyaları** hello çok örnekli ayarlarında belirtin.</span><span class="sxs-lookup"><span data-stu-id="faa3d-117">hello primary and all subtasks download any **common resource files** you specify in hello multi-instance settings.</span></span>
4. <span data-ttu-id="faa3d-118">Merhaba ortak kaynak dosyaları indirdikten sonra hello birincil ve alt görevler hello yürütme **koordinasyon komutu** hello çok örnekli ayarlarında belirtin.</span><span class="sxs-lookup"><span data-stu-id="faa3d-118">After hello common resource files have been downloaded, hello primary and subtasks execute hello **coordination command** you specify in hello multi-instance settings.</span></span> <span data-ttu-id="faa3d-119">Başlangıç görevi Yürütülüyor için genellikle kullanılan tooprepare düğümleri Hello koordinasyon komuttur.</span><span class="sxs-lookup"><span data-stu-id="faa3d-119">hello coordination command is typically used tooprepare nodes for executing hello task.</span></span> <span data-ttu-id="faa3d-120">Bu arka plan Hizmetleri başlatma içerebilir (gibi [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) ve hello düğümlerin hazır tooprocess düğümler arası iletiler olduğunu doğrulama.</span><span class="sxs-lookup"><span data-stu-id="faa3d-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that hello nodes are ready tooprocess inter-node messages.</span></span>
5. <span data-ttu-id="faa3d-121">Merhaba birincil görevi yürütür hello **uygulama komutu** hello ana düğüm üzerinde *sonra* hello koordinasyon komutu tamamlanmış başarıyla hello birincil ve tüm alt görevler tarafından.</span><span class="sxs-lookup"><span data-stu-id="faa3d-121">hello primary task executes hello **application command** on hello master node *after* hello coordination command has been completed successfully by hello primary and all subtasks.</span></span> <span data-ttu-id="faa3d-122">Merhaba uygulama komutu hello çok örnekli görev kendisini hello komut satırı ve yalnızca hello birincil görev tarafından yürütülen.</span><span class="sxs-lookup"><span data-stu-id="faa3d-122">hello application command is hello command line of hello multi-instance task itself, and is executed only by hello primary task.</span></span> <span data-ttu-id="faa3d-123">İçinde bir [MS MPI][msmpi_msdn]-tabanlı çözümün, burada kullanarak MPI özellikli uygulamanızı yürütme budur `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="faa3d-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="faa3d-124">Merhaba "çok örnekli görev" hello gibi bir benzersiz görev türü değil işlevsel olarak ayrı olsa da, [StartTask] [ net_starttask] veya [JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="faa3d-124">Though it is functionally distinct, hello "multi-instance task" is not a unique task type like hello [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="faa3d-125">Merhaba çok örnekli görev yalnızca standart bir Batch görevinde olduğu ([CloudTask] [ net_task] Batch .NET içinde), çok örnekli ayarları yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="faa3d-125">hello multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="faa3d-126">Bu makalede, biz toothis hello olarak başvuran **çok örnekli görev**.</span><span class="sxs-lookup"><span data-stu-id="faa3d-126">In this article, we refer toothis as hello **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="faa3d-127">Çok örnekli görevler için gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="faa3d-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="faa3d-128">Çok örnekli görevleri gerektiren bir havuzla **etkin düğümler arası iletişim**ile **eşzamanlı görev yürütme devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="faa3d-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="faa3d-129">toodisable eşzamanlı Görev Yürütme, kümesi hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) özelliği too1.</span><span class="sxs-lookup"><span data-stu-id="faa3d-129">toodisable concurrent task execution, set hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property too1.</span></span>

<span data-ttu-id="faa3d-130">Bu kod parçacığını nasıl hello Batch .NET kitaplığını kullanarak toocreate bir havuz için çok örnekli görevler gösterir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-130">This code snippet shows how toocreate a pool for multi-instance tasks using hello Batch .NET library.</span></span>

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
> <span data-ttu-id="faa3d-131">Çok örnekli görev bir havuzdaki düğümler arası iletişim ile devre dışı toorun çalışırsanız veya ile bir *maxTasksPerNode* 1'den büyük değer, hiçbir zaman hello görev zamanlandığı--süresiz olarak hello "etkin" durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="faa3d-131">If you try toorun a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, hello task is never scheduled--it remains indefinitely in hello "active" state.</span></span> 
>
> <span data-ttu-id="faa3d-132">Çok örnekli görevler yalnızca 14 Aralık 2015 tarihinden sonra oluşturulan havuzlarında düğümlerinde yürütebilir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a><span data-ttu-id="faa3d-133">StartTask tooinstall MPI kullanın</span><span class="sxs-lookup"><span data-stu-id="faa3d-133">Use a StartTask tooinstall MPI</span></span>
<span data-ttu-id="faa3d-134">çok örnekli görev MPI uygulamalarla toorun, ilk tooinstall hello hello havuzundaki işlem düğümlerinde MPI uygulaması (MS-MPI veya örneğin Intel MPI) gerekir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-134">toorun MPI applications with a multi-instance task, you first need tooinstall an MPI implementation (MS-MPI or Intel MPI, for example) on hello compute nodes in hello pool.</span></span> <span data-ttu-id="faa3d-135">İyi zaman toouse budur bir [StartTask][net_starttask], her bir düğümün bir havuzuna katılır veya yeniden yürütür.</span><span class="sxs-lookup"><span data-stu-id="faa3d-135">This is a good time toouse a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="faa3d-136">Bu kod parçacığını hello MS MPI kurulum paketi olarak belirten bir StartTask oluşturur bir [kaynak dosyası][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="faa3d-136">This code snippet creates a StartTask that specifies hello MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="faa3d-137">Merhaba başlangıç görevinin komut satırı Hello kaynak dosyası indirilen toohello düğümdür sonra yürütülür.</span><span class="sxs-lookup"><span data-stu-id="faa3d-137">hello start task's command line is executed after hello resource file is downloaded toohello node.</span></span> <span data-ttu-id="faa3d-138">Bu durumda, hello komut satırı katılımsız yükleme MS MPI işlemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-138">In this case, hello command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="faa3d-139">Doğrudan uzak bellek erişimi (RDMA)</span><span class="sxs-lookup"><span data-stu-id="faa3d-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="faa3d-140">Seçeneğini belirlediğinizde bir [RDMA özellikli boyutu](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) A9 hello için bilgi işlem gibi toplu havuzunuzdaki düğümler, MPI uygulamanızı Azure'nın yüksek performans, düşük gecikme süreli doğrudan uzak bellek erişimi (RDMA) ağ avantajından yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="faa3d-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for hello compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="faa3d-141">"RDMA özellikli" makaleleri aşağıdaki hello belirtilen hello boyutlarını arayın:</span><span class="sxs-lookup"><span data-stu-id="faa3d-141">Look for hello sizes specified as "RDMA capable" in hello following articles:</span></span>

* <span data-ttu-id="faa3d-142">**CloudServiceConfiguration** havuzları</span><span class="sxs-lookup"><span data-stu-id="faa3d-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="faa3d-143">[Cloud Services boyutları](../cloud-services/cloud-services-sizes-specs.md) (yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="faa3d-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="faa3d-144">**VirtualMachineConfiguration** havuzları</span><span class="sxs-lookup"><span data-stu-id="faa3d-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="faa3d-145">[Azure sanal makineler için Boyutlar](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="faa3d-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="faa3d-146">[Azure sanal makineler için Boyutlar](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="faa3d-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="faa3d-147">RDMA üzerinde tootake avantajlarından [Linux işlem düğümlerini](batch-linux-nodes.md), kullanmalısınız **Intel MPI** hello düğümlerde.</span><span class="sxs-lookup"><span data-stu-id="faa3d-147">tootake advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on hello nodes.</span></span> <span data-ttu-id="faa3d-148">CloudServiceConfiguration ve VirtualMachineConfiguration havuzları hakkında daha fazla bilgi için bkz: hello havuzu bölümünü hello [Batch özelliklerine genel bakış](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="faa3d-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see hello Pool section of hello [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="faa3d-149">Çok örnekli görev Batch .NET ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="faa3d-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="faa3d-150">Biz hello havuzu gereksinimleri ve MPI paket yükleme kapsamında, hello çok örnekli görev oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="faa3d-150">Now that we've covered hello pool requirements and MPI package installation, let's create hello multi-instance task.</span></span> <span data-ttu-id="faa3d-151">Bu parçacığında, bir standart oluşturuyoruz [CloudTask][net_task], ardından yapılandırma kendi [MultiInstanceSettings] [ net_multiinstance_prop] özelliği.</span><span class="sxs-lookup"><span data-stu-id="faa3d-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="faa3d-152">Daha önce belirtildiği gibi hello çok örnekli görev farklı görev türü, ancak çok örnekli ayarlarla yapılandırılan standart bir Batch görevinde değil.</span><span class="sxs-lookup"><span data-stu-id="faa3d-152">As mentioned earlier, hello multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="faa3d-153">Birincil görevi ve alt görevler</span><span class="sxs-lookup"><span data-stu-id="faa3d-153">Primary task and subtasks</span></span>
<span data-ttu-id="faa3d-154">Bir görev için çok örnekli ayarları hello oluşturduğunuzda, hello tooexecute hello görev işlem düğümü sayısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="faa3d-154">When you create hello multi-instance settings for a task, you specify hello number of compute nodes that are tooexecute hello task.</span></span> <span data-ttu-id="faa3d-155">Merhaba görev tooa işi gönderdiğinizde, hello Batch hizmeti bir oluşturur **birincil** görev ve yeterli **görevleri** hello belirttiğiniz düğüm sayısını birlikte eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="faa3d-155">When you submit hello task tooa job, hello Batch service creates one **primary** task and enough **subtasks** that together match hello number of nodes you specified.</span></span>

<span data-ttu-id="faa3d-156">Bu görevleri 0 hello aralığında bir tamsayı kimliği çok atanan*numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="faa3d-156">These tasks are assigned an integer id in hello range of 0 too*numberOfInstances* - 1.</span></span> <span data-ttu-id="faa3d-157">Merhaba görev kimliği 0 ile Merhaba birincil görevdir ve diğer tüm kimliklerini görevleridir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-157">hello task with id 0 is hello primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="faa3d-158">Örneğin, bir görev için çok örnekli ayarları aşağıdaki hello oluşturursanız, hello birincil görev 0 bir kimliğe sahip ve hello görevleri kimlikleri 1 ile 9 arasında olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-158">For example, if you create hello following multi-instance settings for a task, hello primary task would have an id of 0, and hello subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="faa3d-159">Ana düğüm</span><span class="sxs-lookup"><span data-stu-id="faa3d-159">Master node</span></span>
<span data-ttu-id="faa3d-160">Çok örnekli görev gönderdiğinizde, hello Batch hizmeti hello birini işlem düğümleri olarak hello "Yönetici" düğümü atar ve zamanlamaları hello ana düğüm üzerinde birincil görev tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="faa3d-160">When you submit a multi-instance task, hello Batch service designates one of hello compute nodes as hello "master" node, and schedules hello primary task tooexecute on hello master node.</span></span> <span data-ttu-id="faa3d-161">Merhaba, zamanlanmış tooexecute toohello çok örnekli görev ayrılan hello düğümleri hello kalanı üzerinde görevleridir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-161">hello subtasks are scheduled tooexecute on hello remainder of hello nodes allocated toohello multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="faa3d-162">Düzenleme komutu</span><span class="sxs-lookup"><span data-stu-id="faa3d-162">Coordination command</span></span>
<span data-ttu-id="faa3d-163">Merhaba **koordinasyon komutu** hello birincil ve alt görevler tarafından yürütülür.</span><span class="sxs-lookup"><span data-stu-id="faa3d-163">hello **coordination command** is executed by both hello primary and subtasks.</span></span>

<span data-ttu-id="faa3d-164">hello koordinasyon komutunun Hello çağırma engelleme--hello koordinasyon komutu için tüm görevleri başarıyla verdi kadar toplu hello uygulama komutu yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="faa3d-164">hello invocation of hello coordination command is blocking--Batch does not execute hello application command until hello coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="faa3d-165">Merhaba düzenleme komutu bu nedenle tüm gerekli arka plan hizmetleri başlatmak, kullanıma hazır olduğunu doğrulayın ve ardından çıkın.</span><span class="sxs-lookup"><span data-stu-id="faa3d-165">hello coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="faa3d-166">Örneğin, bu düzenleme komut MS-MPI sürüm 7 kullanarak bir çözüm için hello düğümde hello SMPD hizmetini başlatır ve ardından çıkar:</span><span class="sxs-lookup"><span data-stu-id="faa3d-166">For example, this coordination command for a solution using MS-MPI version 7 starts hello SMPD service on hello node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="faa3d-167">Not hello `start` bu koordinasyon komutu.</span><span class="sxs-lookup"><span data-stu-id="faa3d-167">Note hello use of `start` in this coordination command.</span></span> <span data-ttu-id="faa3d-168">Bu gereklidir çünkü hello `smpd.exe` uygulama hemen yürütme sonrasında döndürmez.</span><span class="sxs-lookup"><span data-stu-id="faa3d-168">This is required because hello `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="faa3d-169">Merhaba hello kullanmadan [Başlat] [ cmd_start] komutu, bu düzenleme komut değil döndürür ve bu nedenle hello uygulama komutu çalışmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="faa3d-169">Without hello use of hello [start][cmd_start] command, this coordination command would not return, and would therefore block hello application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="faa3d-170">Uygulama komutu</span><span class="sxs-lookup"><span data-stu-id="faa3d-170">Application command</span></span>
<span data-ttu-id="faa3d-171">Merhaba koordinasyon komutu yürütülürken Hello birincil görev ve tüm görevleri tamamladıktan sonra hello çok örnekli görevin komut satırı hello birincil görev tarafından yürütülen *yalnızca*.</span><span class="sxs-lookup"><span data-stu-id="faa3d-171">Once hello primary task and all subtasks have finished executing hello coordination command, hello multi-instance task's command line is executed by hello primary task *only*.</span></span> <span data-ttu-id="faa3d-172">Bu Merhaba diyoruz **uygulama komutu** toodistinguish hello koordinasyon komutu ondan.</span><span class="sxs-lookup"><span data-stu-id="faa3d-172">We call this hello **application command** toodistinguish it from hello coordination command.</span></span>

<span data-ttu-id="faa3d-173">MS-MPI uygulamaları için kullanım hello uygulama komutu tooexecute MPI etkin uygulamanızla `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="faa3d-173">For MS-MPI applications, use hello application command tooexecute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="faa3d-174">Örneğin, MS-MPI sürüm 7 kullanarak bir çözüm için bir uygulama komutu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="faa3d-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="faa3d-175">Çünkü MS-MPI's `mpiexec.exe` kullanır hello `CCP_NODES` değişken varsayılan olarak (bkz [ortam değişkenleri](#environment-variables)) hello örnek uygulama komut satırı yukarıdaki dışlar.</span><span class="sxs-lookup"><span data-stu-id="faa3d-175">Because MS-MPI's `mpiexec.exe` uses hello `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) hello example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="faa3d-176">Ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="faa3d-176">Environment variables</span></span>
<span data-ttu-id="faa3d-177">Toplu iş oluşturur birkaç [ortam değişkenleri] [ msdn_env_var] işlem hello belirli toomulti örneği görevlerini düğümleri ayrılan tooa çok örnekli görev.</span><span class="sxs-lookup"><span data-stu-id="faa3d-177">Batch creates several [environment variables][msdn_env_var] specific toomulti-instance tasks on hello compute nodes allocated tooa multi-instance task.</span></span> <span data-ttu-id="faa3d-178">Düzenleme ve uygulama komut satırları, komut dosyaları ve bunların yürütme programları hello gibi bu ortam değişkenleri başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-178">Your coordination and application command lines can reference these environment variables, as can hello scripts and programs they execute.</span></span>

<span data-ttu-id="faa3d-179">Merhaba aşağıdaki ortam değişkenleri tarafından hello Batch hizmetini kullanmak için çok örnekli görevler tarafından oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="faa3d-179">hello following environment variables are created by hello Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="faa3d-180">Bunlar üzerinde tam Ayrıntılar ve hello için görünürlük ve içeriği de dahil olmak üzere diğer toplu işlem düğüm ortam değişkenleri bkz [işlem düğümü ortam değişkenleri][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="faa3d-180">For full details on these and hello other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="faa3d-181">Hello toplu Linux MPI kod örneği, bu ortam değişkenleri çeşitli nasıl kullanılabileceğini örneği içerir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-181">hello Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="faa3d-182">Merhaba [koordinasyon cmd] [ coord_cmd_example] komut dosyası Azure depolama biriminden ortak uygulama ve giriş dosyalarını indirir, hello ana düğüm ağ dosya sistemi (NFS) paylaşımında etkinleştirir ve yapılandırır Bash hello diğer düğümler toohello çok örnekli görev NFS istemcileri olarak ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="faa3d-182">hello [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on hello master node, and configures hello other nodes allocated toohello multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="faa3d-183">Kaynak dosyaları</span><span class="sxs-lookup"><span data-stu-id="faa3d-183">Resource files</span></span>
<span data-ttu-id="faa3d-184">Çok örnekli görevler için kaynak dosyaları tooconsider iki kümesi vardır: **ortak kaynak dosyaları** , *tüm* görevleri indirin (hem birincil hem de ve alt görevler) ve hello **kaynakdosyaları** hello çok örnekli görev için kendisini, belirtilen *yalnızca birincil hello* görev yüklemeleri.</span><span class="sxs-lookup"><span data-stu-id="faa3d-184">There are two sets of resource files tooconsider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and hello **resource files** specified for hello multi-instance task itself, which *only hello primary* task downloads.</span></span>

<span data-ttu-id="faa3d-185">Bir veya daha fazla belirtebilirsiniz **ortak kaynak dosyaları** hello çok örnekli ayarlarında bir görev.</span><span class="sxs-lookup"><span data-stu-id="faa3d-185">You can specify one or more **common resource files** in hello multi-instance settings for a task.</span></span> <span data-ttu-id="faa3d-186">Bu ortak kaynak dosyaları karşıdan yüklenir [Azure Storage](../storage/common/storage-introduction.md) her düğümün içine **görev paylaşılan dizine** hello birincil ve tüm alt görevler.</span><span class="sxs-lookup"><span data-stu-id="faa3d-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by hello primary and all subtasks.</span></span> <span data-ttu-id="faa3d-187">Hello kullanarak uygulama ve düzenleme komut satırlarından hello görev paylaşılan dizine erişebilir `AZ_BATCH_TASK_SHARED_DIR` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="faa3d-187">You can access hello task shared directory from application and coordination command lines by using hello `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="faa3d-188">Merhaba `AZ_BATCH_TASK_SHARED_DIR` yolu her düğüm ayrılmış toohello çok örnekli görev aynıdır, böylece bir tek koordinasyon komutu hello birincil ve tüm alt görevler arasında paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="faa3d-188">hello `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated toohello multi-instance task, thus you can share a single coordination command between hello primary and all subtasks.</span></span> <span data-ttu-id="faa3d-189">Toplu "Merhaba dizininde bir uzaktan erişim fikir paylaşmaz", ancak bağlama kullanın ya da ortam değişkenleri hello ucunu önceki bölümünde belirtildiği gibi noktası paylaşın.</span><span class="sxs-lookup"><span data-stu-id="faa3d-189">Batch does not "share" hello directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in hello tip on environment variables.</span></span>

<span data-ttu-id="faa3d-190">Merhaba çok örnekli görev kendisi için indirilen toohello görevin çalışma dizini, belirttiğiniz kaynak dosyaları `AZ_BATCH_TASK_WORKING_DIR`, varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="faa3d-190">Resource files that you specify for hello multi-instance task itself are downloaded toohello task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="faa3d-191">Buna karşılık, belirtildiği gibi toocommon kaynak dosyaları, yalnızca hello birincil görev hello çok örnekli görev için kendisini belirtilen kaynak dosyaları indirir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-191">As mentioned, in contrast toocommon resource files, only hello primary task downloads resource files specified for hello  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="faa3d-192">Her zaman hello ortam değişkenlerini kullanma `AZ_BATCH_TASK_SHARED_DIR` ve `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese komut satırları dizinlerde.</span><span class="sxs-lookup"><span data-stu-id="faa3d-192">Always use hello environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese directories in your command lines.</span></span> <span data-ttu-id="faa3d-193">Tooconstruct hello yollarını el ile çalışmayın.</span><span class="sxs-lookup"><span data-stu-id="faa3d-193">Do not attempt tooconstruct hello paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="faa3d-194">Görev yaşam süresi</span><span class="sxs-lookup"><span data-stu-id="faa3d-194">Task lifetime</span></span>
<span data-ttu-id="faa3d-195">Merhaba birincil görev denetimleri hello hello tüm çok örnekli görev ömrü ömrü Hello.</span><span class="sxs-lookup"><span data-stu-id="faa3d-195">hello lifetime of hello primary task controls hello lifetime of hello entire multi-instance task.</span></span> <span data-ttu-id="faa3d-196">Merhaba birincil çıktığında tüm hello görevleri sonlandırılır.</span><span class="sxs-lookup"><span data-stu-id="faa3d-196">When hello primary exits, all of hello subtasks are terminated.</span></span> <span data-ttu-id="faa3d-197">Merhaba birincil Hello çıkış kodu hello görevinin hello çıkış kodu ve bu nedenle kullanılan toodetermine hello başarısını veya başarısızlığını hello görev yeniden deneme amaçlı.</span><span class="sxs-lookup"><span data-stu-id="faa3d-197">hello exit code of hello primary is hello exit code of hello task, and is therefore used toodetermine hello success or failure of hello task for retry purposes.</span></span>

<span data-ttu-id="faa3d-198">Hello alt görevlerin başarısız sıfır dönüş koduyla çıkılıyor gibi hello tüm çok örnekli görev başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="faa3d-198">If any of hello subtasks fail, exiting with a non-zero return code, for example, hello entire multi-instance task fails.</span></span> <span data-ttu-id="faa3d-199">Hello çok örnekli görev sonra sona erdi ve, denenen tooits yeniden deneme sınırı.</span><span class="sxs-lookup"><span data-stu-id="faa3d-199">hello multi-instance task is then terminated and retried, up tooits retry limit.</span></span>

<span data-ttu-id="faa3d-200">Çok örnekli Görev sildiğinizde, birincil hello ve tüm alt görevleri de hello Batch hizmeti tarafından silinir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-200">When you delete a multi-instance task, hello primary and all subtasks are also deleted by hello Batch service.</span></span> <span data-ttu-id="faa3d-201">Tüm dizinleri eklemeli ve dosyalarına yalnızca standart bir görev için hello işlem düğümleri silinir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-201">All subtask directories and their files are deleted from hello compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="faa3d-202">[TaskConstraints] [ net_taskconstraints] hello gibi bir çok örnekli görev için [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], ve [RetentionTime] [ net_taskconstraint_retention] bunlar için standart bir görev ve toohello uygulamak gibi özelliklerini dikkate alınır birincil ve tüm alt görevler.</span><span class="sxs-lookup"><span data-stu-id="faa3d-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply toohello primary and all subtasks.</span></span> <span data-ttu-id="faa3d-203">Ancak, hello değiştirirseniz [RetentionTime] [ net_taskconstraint_retention] hello çok örnekli görev toohello işi, bu değişikliği ekledikten sonra özelliktir uygulanan yalnızca toohello birincil görev.</span><span class="sxs-lookup"><span data-stu-id="faa3d-203">However, if you change hello [RetentionTime][net_taskconstraint_retention] property after adding hello multi-instance task toohello job, this change is applied only toohello primary task.</span></span> <span data-ttu-id="faa3d-204">Tüm hello görevleri toouse hello özgün devam [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="faa3d-204">All of hello subtasks continue toouse hello original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="faa3d-205">Merhaba son görevi çok örnekli görev parçası ise bir işlem düğümün son kullanılan görevler listesi alt hello kimliğini yansıtır.</span><span class="sxs-lookup"><span data-stu-id="faa3d-205">A compute node's recent task list reflects hello id of a subtask if hello recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="faa3d-206">Alt görevler hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="faa3d-206">Obtain information about subtasks</span></span>
<span data-ttu-id="faa3d-207">Merhaba Batch .NET kitaplığını, çağrı hello kullanarak görevleri tooobtain bilgi [CloudTask.ListSubtasks] [ net_task_listsubtasks] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="faa3d-207">tooobtain information on subtasks by using hello Batch .NET library, call hello [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="faa3d-208">Bu yöntem, tüm görevler bilgileri döndürür ve hello hakkında bilgi işlem hello görevleri yürütülen düğümü.</span><span class="sxs-lookup"><span data-stu-id="faa3d-208">This method returns information on all subtasks, and information about hello compute node that executed hello tasks.</span></span> <span data-ttu-id="faa3d-209">Bu bilgilerden, her alt ait kök dizini, hello havuzu kimliği, geçerli durumu, çıkış kodu ve daha fazla belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="faa3d-209">From this information, you can determine each subtask's root directory, hello pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="faa3d-210">Bu bilgiler hello ile birlikte kullanabileceğiniz [PoolOperations.GetNodeFile] [ poolops_getnodefile] yöntemi tooobtain hello alt 's dosyaları.</span><span class="sxs-lookup"><span data-stu-id="faa3d-210">You can use this information in combination with hello [PoolOperations.GetNodeFile][poolops_getnodefile] method tooobtain hello subtask's files.</span></span> <span data-ttu-id="faa3d-211">Bu yöntem hello birincil görev (kimliği 0) için bilgi döndürmüyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="faa3d-211">Note that this method does not return information for hello primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="faa3d-212">Aksi belirtilmediği sürece, birden çok örneği üzerinde çalışacağı Batch .NET yöntemleri hello [CloudTask] [ net_task] kendisini uygulamak *yalnızca* toohello birincil görev.</span><span class="sxs-lookup"><span data-stu-id="faa3d-212">Unless otherwise stated, Batch .NET methods that operate on hello multi-instance [CloudTask][net_task] itself apply *only* toohello primary task.</span></span> <span data-ttu-id="faa3d-213">Örneğin, hello çağırdığınızda [CloudTask.ListNodeFiles] [ net_task_listnodefiles] çok örnekli görev yöntemi, yalnızca hello birincil görev dosyaları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="faa3d-213">For example, when you call hello [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only hello primary task's files are returned.</span></span>
>
>

<span data-ttu-id="faa3d-214">Merhaba aşağıdaki kod parçacığını nasıl tooobtain bilgi alt görev yanı sıra dosya içerikleri üzerinde yürütülen hello düğümlerden isteği gösterir.</span><span class="sxs-lookup"><span data-stu-id="faa3d-214">hello following code snippet shows how tooobtain subtask information, as well as request file contents from hello nodes on which they executed.</span></span>

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
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

## <a name="code-sample"></a><span data-ttu-id="faa3d-215">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="faa3d-215">Code sample</span></span>
<span data-ttu-id="faa3d-216">Merhaba [MultiInstanceTasks] [ github_mpi] kodu örneği github'daki gösteren nasıl toouse çok örnekli görev toorun bir [MS MPI] [ msmpi_msdn] Toplu işlem düğümlerinde uygulama.</span><span class="sxs-lookup"><span data-stu-id="faa3d-216">hello [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how toouse a multi-instance task toorun an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="faa3d-217">Merhaba adımları [hazırlık](#preparation) ve [yürütme](#execution) toorun hello örnek.</span><span class="sxs-lookup"><span data-stu-id="faa3d-217">Follow hello steps in [Preparation](#preparation) and [Execution](#execution) toorun hello sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="faa3d-218">Hazırlama</span><span class="sxs-lookup"><span data-stu-id="faa3d-218">Preparation</span></span>
1. <span data-ttu-id="faa3d-219">Merhaba ilk iki adımları [nasıl toocompile ve basit bir MS-MPI program Çalıştır][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="faa3d-219">Follow hello first two steps in [How toocompile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="faa3d-220">Bu, aşağıdaki hello hello prerequesites adım karşılar.</span><span class="sxs-lookup"><span data-stu-id="faa3d-220">This satisfies hello prerequesites for hello following step.</span></span>
2. <span data-ttu-id="faa3d-221">Derleme bir *sürüm* hello sürümü [MPIHelloWorld] [ helloworld_proj] örnek MPI programı.</span><span class="sxs-lookup"><span data-stu-id="faa3d-221">Build a *Release* version of hello [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="faa3d-222">Bu işlem düğümlerinde hello çok örnekli görev tarafından çalıştırılacak hello programıdır.</span><span class="sxs-lookup"><span data-stu-id="faa3d-222">This is hello program that will be run on compute nodes by hello multi-instance task.</span></span>
3. <span data-ttu-id="faa3d-223">İçeren bir zip dosyası oluşturma `MPIHelloWorld.exe` (hangi, 2. adım yerleşik) ve `MSMpiSetup.exe` (hangi indirdiğiniz 1. adım).</span><span class="sxs-lookup"><span data-stu-id="faa3d-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="faa3d-224">Bir uygulama paketi hello sonraki adım olarak bu zip dosyasını yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="faa3d-224">You'll upload this zip file as an application package in hello next step.</span></span>
4. <span data-ttu-id="faa3d-225">Kullanım hello [Azure portal] [ portal] toocreate toplu [uygulama](batch-application-packages.md) "MPIHelloWorld" olarak adlandırılan ve hello önceki adımda oluşturduğunuz sürümü olarak "1.0" Merhaba zip dosyası belirtin Merhaba uygulama paketi.</span><span class="sxs-lookup"><span data-stu-id="faa3d-225">Use hello [Azure portal][portal] toocreate a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify hello zip file you created in hello previous step as version "1.0" of hello application package.</span></span> <span data-ttu-id="faa3d-226">Bkz: [karşıya yükleyin ve uygulamalarını yönetin](batch-application-packages.md#upload-and-manage-applications) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="faa3d-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="faa3d-227">Derleme bir *sürüm* sürümü `MPIHelloWorld.exe` böylece ek bağımlılıkları tooinclude yoksa (örneğin, `msvcp140d.dll` veya `vcruntime140d.dll`) uygulama paketi.</span><span class="sxs-lookup"><span data-stu-id="faa3d-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have tooinclude any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="faa3d-228">Yürütme</span><span class="sxs-lookup"><span data-stu-id="faa3d-228">Execution</span></span>
1. <span data-ttu-id="faa3d-229">Merhaba karşıdan [azure-batch-samples] [ github_samples_zip] github'dan.</span><span class="sxs-lookup"><span data-stu-id="faa3d-229">Download hello [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="faa3d-230">Açık hello MultiInstanceTasks **çözüm** Visual Studio 2015'te ya da daha yeni.</span><span class="sxs-lookup"><span data-stu-id="faa3d-230">Open hello MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="faa3d-231">Merhaba `MultiInstanceTasks.sln` çözüm dosyasını bulunur:</span><span class="sxs-lookup"><span data-stu-id="faa3d-231">hello `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="faa3d-232">Batch ve Storage hesabı kimlik bilgilerinizi girin `AccountSettings.settings` hello içinde **öğesini kullanıma alın** projesi.</span><span class="sxs-lookup"><span data-stu-id="faa3d-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="faa3d-233">**Derleme ve çalıştırma** Merhaba MultiInstanceTasks çözüm tooexecute hello MPI örnek uygulaması üzerinde işlem düğümlerini Batch havuzunda.</span><span class="sxs-lookup"><span data-stu-id="faa3d-233">**Build and run** hello MultiInstanceTasks solution tooexecute hello MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="faa3d-234">*İsteğe bağlı*: kullanım hello [Azure portal] [ portal] veya hello [Batch Gezgini] [ batch_explorer] tooexamine hello örnek havuz, iş, ve görevi ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask"), önce hello kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="faa3d-234">*Optional*: Use hello [Azure portal][portal] or hello [Batch Explorer][batch_explorer] tooexamine hello sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete hello resources.</span></span>

> [!TIP]
> <span data-ttu-id="faa3d-235">İndirebilirsiniz [Visual Studio Community] [ visual_studio] ücretsiz Visual Studio yoksa.</span><span class="sxs-lookup"><span data-stu-id="faa3d-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="faa3d-236">Çıktı `MultiInstanceTasks.exe` benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="faa3d-236">Output from `MultiInstanceTasks.exe` is similar toohello following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

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

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="faa3d-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="faa3d-237">Next steps</span></span>
* <span data-ttu-id="faa3d-238">Merhaba Microsoft HPC & Azure Batch ekip blogu anlatılmaktadır [MPI desteklemek için Azure batch Linux][blog_mpi_linux]ve kullanma hakkında bilgi içerir [OpenFOAM] [ openfoam] toplu ile.</span><span class="sxs-lookup"><span data-stu-id="faa3d-238">hello Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="faa3d-239">Merhaba Python kod örnekleri bulabilirsiniz [OpenFOAM örneği github'daki][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="faa3d-239">You can find Python code samples for hello [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="faa3d-240">Nasıl çok öğrenin[Linux işlem düğümleri havuzları oluşturma](batch-linux-nodes.md) Azure Batch MPI çözümlerinizi kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="faa3d-240">Learn how too[create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

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
