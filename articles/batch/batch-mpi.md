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
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a>Çok örnekli görevler toorun ileti geçirme arabirimi (MPI) uygulamalarını toplu işlemde kullanın

Çok örnekli görevler toorun bir Azure Batch görev birden çok işlem düğümünde eşzamanlı olarak sağlar. Bu görevler, ileti geçirme arabirimi (MPI) uygulamalarını toplu gibi senaryoları yüksek performans sağlar. Bu makalede, nasıl tooexecute çok örnekli görevleri kullanma hello öğrenin [Batch .NET] [ api_net] kitaplığı.

> [!NOTE]
> Batch .NET, MS-MPI, bu makaledeki örneklerde Hello odaklanmanıza ve Windows işlem düğümleri olsa da, burada tartışılan hello çok örnekli görev kavramları geçerli tooother platformlar ve teknolojiler (Python ve Linux düğümleri, örneğin üzerinde Intel MPI) ' dir.
>
>

## <a name="multi-instance-task-overview"></a>Çok örnekli görev genel bakış
Toplu işlemde her normalde bir görevdir tek işlem düğümü üzerinde--yürütülen birden çok görevleri tooa işi göndermek ve hello Batch hizmetinin her görev bir düğümde yürütülmek zamanlar. Bir görevin yapılandırarak ancak **çok örnekli ayarları**, toplu söyleyin tooinstead bir birincil görev ve ardından birden çok düğümde yürütülen çeşitli görevleri oluşturun.

![Çok örnekli görev genel bakış][1]

Çok örnekli ayarları tooa iş görevle gönderdiğinizde, toplu çeşitli adımları benzersiz toomulti örnekli görevleri gerçekleştirir:

1. Merhaba Batch hizmeti bir oluşturur **birincil** ve birkaç **görevleri** hello çok örnekli ayarlarınızı temel alan. Görevler (tüm alt birincil) toplam sayısı Hello eşleşen hello sayısı **örnekleri** (işlem düğümleri) hello çok örnekli ayarlarında belirtin.
2. Toplu atayan hello birini işlem düğümleri hello **ana**, ve zamanlamaları hello hello yöneticisinde birincil görev tooexecute. Merhaba görevleri tooexecute hello işlem düğümleri ayrılmış toohello çok örnekli görev, bir alt düğüm başına hello kalanı üzerinde zamanlar.
3. Merhaba birincil ve tüm alt görevler yükleme **ortak kaynak dosyaları** hello çok örnekli ayarlarında belirtin.
4. Merhaba ortak kaynak dosyaları indirdikten sonra hello birincil ve alt görevler hello yürütme **koordinasyon komutu** hello çok örnekli ayarlarında belirtin. Başlangıç görevi Yürütülüyor için genellikle kullanılan tooprepare düğümleri Hello koordinasyon komuttur. Bu arka plan Hizmetleri başlatma içerebilir (gibi [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) ve hello düğümlerin hazır tooprocess düğümler arası iletiler olduğunu doğrulama.
5. Merhaba birincil görevi yürütür hello **uygulama komutu** hello ana düğüm üzerinde *sonra* hello koordinasyon komutu tamamlanmış başarıyla hello birincil ve tüm alt görevler tarafından. Merhaba uygulama komutu hello çok örnekli görev kendisini hello komut satırı ve yalnızca hello birincil görev tarafından yürütülen. İçinde bir [MS MPI][msmpi_msdn]-tabanlı çözümün, burada kullanarak MPI özellikli uygulamanızı yürütme budur `mpiexec.exe`.

> [!NOTE]
> Merhaba "çok örnekli görev" hello gibi bir benzersiz görev türü değil işlevsel olarak ayrı olsa da, [StartTask] [ net_starttask] veya [JobPreparationTask] [ net_jobprep]. Merhaba çok örnekli görev yalnızca standart bir Batch görevinde olduğu ([CloudTask] [ net_task] Batch .NET içinde), çok örnekli ayarları yapılandırılır. Bu makalede, biz toothis hello olarak başvuran **çok örnekli görev**.
>
>

## <a name="requirements-for-multi-instance-tasks"></a>Çok örnekli görevler için gereksinimleri
Çok örnekli görevleri gerektiren bir havuzla **etkin düğümler arası iletişim**ile **eşzamanlı görev yürütme devre dışı**. toodisable eşzamanlı Görev Yürütme, kümesi hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) özelliği too1.

Bu kod parçacığını nasıl hello Batch .NET kitaplığını kullanarak toocreate bir havuz için çok örnekli görevler gösterir.

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
> Çok örnekli görev bir havuzdaki düğümler arası iletişim ile devre dışı toorun çalışırsanız veya ile bir *maxTasksPerNode* 1'den büyük değer, hiçbir zaman hello görev zamanlandığı--süresiz olarak hello "etkin" durumda kalır. 
>
> Çok örnekli görevler yalnızca 14 Aralık 2015 tarihinden sonra oluşturulan havuzlarında düğümlerinde yürütebilir.
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a>StartTask tooinstall MPI kullanın
çok örnekli görev MPI uygulamalarla toorun, ilk tooinstall hello hello havuzundaki işlem düğümlerinde MPI uygulaması (MS-MPI veya örneğin Intel MPI) gerekir. İyi zaman toouse budur bir [StartTask][net_starttask], her bir düğümün bir havuzuna katılır veya yeniden yürütür. Bu kod parçacığını hello MS MPI kurulum paketi olarak belirten bir StartTask oluşturur bir [kaynak dosyası][net_resourcefile]. Merhaba başlangıç görevinin komut satırı Hello kaynak dosyası indirilen toohello düğümdür sonra yürütülür. Bu durumda, hello komut satırı katılımsız yükleme MS MPI işlemi gerçekleştirir.

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

### <a name="remote-direct-memory-access-rdma"></a>Doğrudan uzak bellek erişimi (RDMA)
Seçeneğini belirlediğinizde bir [RDMA özellikli boyutu](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) A9 hello için bilgi işlem gibi toplu havuzunuzdaki düğümler, MPI uygulamanızı Azure'nın yüksek performans, düşük gecikme süreli doğrudan uzak bellek erişimi (RDMA) ağ avantajından yararlanabilirsiniz.

"RDMA özellikli" makaleleri aşağıdaki hello belirtilen hello boyutlarını arayın:

* **CloudServiceConfiguration** havuzları

  * [Cloud Services boyutları](../cloud-services/cloud-services-sizes-specs.md) (yalnızca Windows)
* **VirtualMachineConfiguration** havuzları

  * [Azure sanal makineler için Boyutlar](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)
  * [Azure sanal makineler için Boyutlar](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)

> [!NOTE]
> RDMA üzerinde tootake avantajlarından [Linux işlem düğümlerini](batch-linux-nodes.md), kullanmalısınız **Intel MPI** hello düğümlerde. CloudServiceConfiguration ve VirtualMachineConfiguration havuzları hakkında daha fazla bilgi için bkz: hello havuzu bölümünü hello [Batch özelliklerine genel bakış](batch-api-basics.md).
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a>Çok örnekli görev Batch .NET ile oluşturma
Biz hello havuzu gereksinimleri ve MPI paket yükleme kapsamında, hello çok örnekli görev oluşturalım. Bu parçacığında, bir standart oluşturuyoruz [CloudTask][net_task], ardından yapılandırma kendi [MultiInstanceSettings] [ net_multiinstance_prop] özelliği. Daha önce belirtildiği gibi hello çok örnekli görev farklı görev türü, ancak çok örnekli ayarlarla yapılandırılan standart bir Batch görevinde değil.

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

## <a name="primary-task-and-subtasks"></a>Birincil görevi ve alt görevler
Bir görev için çok örnekli ayarları hello oluşturduğunuzda, hello tooexecute hello görev işlem düğümü sayısını belirtin. Merhaba görev tooa işi gönderdiğinizde, hello Batch hizmeti bir oluşturur **birincil** görev ve yeterli **görevleri** hello belirttiğiniz düğüm sayısını birlikte eşleşmesi.

Bu görevleri 0 hello aralığında bir tamsayı kimliği çok atanan*numberOfInstances* - 1. Merhaba görev kimliği 0 ile Merhaba birincil görevdir ve diğer tüm kimliklerini görevleridir. Örneğin, bir görev için çok örnekli ayarları aşağıdaki hello oluşturursanız, hello birincil görev 0 bir kimliğe sahip ve hello görevleri kimlikleri 1 ile 9 arasında olması gerekir.

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a>Ana düğüm
Çok örnekli görev gönderdiğinizde, hello Batch hizmeti hello birini işlem düğümleri olarak hello "Yönetici" düğümü atar ve zamanlamaları hello ana düğüm üzerinde birincil görev tooexecute hello. Merhaba, zamanlanmış tooexecute toohello çok örnekli görev ayrılan hello düğümleri hello kalanı üzerinde görevleridir.

## <a name="coordination-command"></a>Düzenleme komutu
Merhaba **koordinasyon komutu** hello birincil ve alt görevler tarafından yürütülür.

hello koordinasyon komutunun Hello çağırma engelleme--hello koordinasyon komutu için tüm görevleri başarıyla verdi kadar toplu hello uygulama komutu yürütülmez. Merhaba düzenleme komutu bu nedenle tüm gerekli arka plan hizmetleri başlatmak, kullanıma hazır olduğunu doğrulayın ve ardından çıkın. Örneğin, bu düzenleme komut MS-MPI sürüm 7 kullanarak bir çözüm için hello düğümde hello SMPD hizmetini başlatır ve ardından çıkar:

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

Not hello `start` bu koordinasyon komutu. Bu gereklidir çünkü hello `smpd.exe` uygulama hemen yürütme sonrasında döndürmez. Merhaba hello kullanmadan [Başlat] [ cmd_start] komutu, bu düzenleme komut değil döndürür ve bu nedenle hello uygulama komutu çalışmasını engeller.

## <a name="application-command"></a>Uygulama komutu
Merhaba koordinasyon komutu yürütülürken Hello birincil görev ve tüm görevleri tamamladıktan sonra hello çok örnekli görevin komut satırı hello birincil görev tarafından yürütülen *yalnızca*. Bu Merhaba diyoruz **uygulama komutu** toodistinguish hello koordinasyon komutu ondan.

MS-MPI uygulamaları için kullanım hello uygulama komutu tooexecute MPI etkin uygulamanızla `mpiexec.exe`. Örneğin, MS-MPI sürüm 7 kullanarak bir çözüm için bir uygulama komutu şöyledir:

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> Çünkü MS-MPI's `mpiexec.exe` kullanır hello `CCP_NODES` değişken varsayılan olarak (bkz [ortam değişkenleri](#environment-variables)) hello örnek uygulama komut satırı yukarıdaki dışlar.
>
>

## <a name="environment-variables"></a>Ortam değişkenleri
Toplu iş oluşturur birkaç [ortam değişkenleri] [ msdn_env_var] işlem hello belirli toomulti örneği görevlerini düğümleri ayrılan tooa çok örnekli görev. Düzenleme ve uygulama komut satırları, komut dosyaları ve bunların yürütme programları hello gibi bu ortam değişkenleri başvuruda bulunabilir.

Merhaba aşağıdaki ortam değişkenleri tarafından hello Batch hizmetini kullanmak için çok örnekli görevler tarafından oluşturulur:

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

Bunlar üzerinde tam Ayrıntılar ve hello için görünürlük ve içeriği de dahil olmak üzere diğer toplu işlem düğüm ortam değişkenleri bkz [işlem düğümü ortam değişkenleri][msdn_env_var].

> [!TIP]
> Hello toplu Linux MPI kod örneği, bu ortam değişkenleri çeşitli nasıl kullanılabileceğini örneği içerir. Merhaba [koordinasyon cmd] [ coord_cmd_example] komut dosyası Azure depolama biriminden ortak uygulama ve giriş dosyalarını indirir, hello ana düğüm ağ dosya sistemi (NFS) paylaşımında etkinleştirir ve yapılandırır Bash hello diğer düğümler toohello çok örnekli görev NFS istemcileri olarak ayrılmış.
>
>

## <a name="resource-files"></a>Kaynak dosyaları
Çok örnekli görevler için kaynak dosyaları tooconsider iki kümesi vardır: **ortak kaynak dosyaları** , *tüm* görevleri indirin (hem birincil hem de ve alt görevler) ve hello **kaynakdosyaları** hello çok örnekli görev için kendisini, belirtilen *yalnızca birincil hello* görev yüklemeleri.

Bir veya daha fazla belirtebilirsiniz **ortak kaynak dosyaları** hello çok örnekli ayarlarında bir görev. Bu ortak kaynak dosyaları karşıdan yüklenir [Azure Storage](../storage/common/storage-introduction.md) her düğümün içine **görev paylaşılan dizine** hello birincil ve tüm alt görevler. Hello kullanarak uygulama ve düzenleme komut satırlarından hello görev paylaşılan dizine erişebilir `AZ_BATCH_TASK_SHARED_DIR` ortam değişkeni. Merhaba `AZ_BATCH_TASK_SHARED_DIR` yolu her düğüm ayrılmış toohello çok örnekli görev aynıdır, böylece bir tek koordinasyon komutu hello birincil ve tüm alt görevler arasında paylaşabilirsiniz. Toplu "Merhaba dizininde bir uzaktan erişim fikir paylaşmaz", ancak bağlama kullanın ya da ortam değişkenleri hello ucunu önceki bölümünde belirtildiği gibi noktası paylaşın.

Merhaba çok örnekli görev kendisi için indirilen toohello görevin çalışma dizini, belirttiğiniz kaynak dosyaları `AZ_BATCH_TASK_WORKING_DIR`, varsayılan olarak. Buna karşılık, belirtildiği gibi toocommon kaynak dosyaları, yalnızca hello birincil görev hello çok örnekli görev için kendisini belirtilen kaynak dosyaları indirir.

> [!IMPORTANT]
> Her zaman hello ortam değişkenlerini kullanma `AZ_BATCH_TASK_SHARED_DIR` ve `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese komut satırları dizinlerde. Tooconstruct hello yollarını el ile çalışmayın.
>
>

## <a name="task-lifetime"></a>Görev yaşam süresi
Merhaba birincil görev denetimleri hello hello tüm çok örnekli görev ömrü ömrü Hello. Merhaba birincil çıktığında tüm hello görevleri sonlandırılır. Merhaba birincil Hello çıkış kodu hello görevinin hello çıkış kodu ve bu nedenle kullanılan toodetermine hello başarısını veya başarısızlığını hello görev yeniden deneme amaçlı.

Hello alt görevlerin başarısız sıfır dönüş koduyla çıkılıyor gibi hello tüm çok örnekli görev başarısız olur. Hello çok örnekli görev sonra sona erdi ve, denenen tooits yeniden deneme sınırı.

Çok örnekli Görev sildiğinizde, birincil hello ve tüm alt görevleri de hello Batch hizmeti tarafından silinir. Tüm dizinleri eklemeli ve dosyalarına yalnızca standart bir görev için hello işlem düğümleri silinir.

[TaskConstraints] [ net_taskconstraints] hello gibi bir çok örnekli görev için [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], ve [RetentionTime] [ net_taskconstraint_retention] bunlar için standart bir görev ve toohello uygulamak gibi özelliklerini dikkate alınır birincil ve tüm alt görevler. Ancak, hello değiştirirseniz [RetentionTime] [ net_taskconstraint_retention] hello çok örnekli görev toohello işi, bu değişikliği ekledikten sonra özelliktir uygulanan yalnızca toohello birincil görev. Tüm hello görevleri toouse hello özgün devam [RetentionTime][net_taskconstraint_retention].

Merhaba son görevi çok örnekli görev parçası ise bir işlem düğümün son kullanılan görevler listesi alt hello kimliğini yansıtır.

## <a name="obtain-information-about-subtasks"></a>Alt görevler hakkında bilgi edinin
Merhaba Batch .NET kitaplığını, çağrı hello kullanarak görevleri tooobtain bilgi [CloudTask.ListSubtasks] [ net_task_listsubtasks] yöntemi. Bu yöntem, tüm görevler bilgileri döndürür ve hello hakkında bilgi işlem hello görevleri yürütülen düğümü. Bu bilgilerden, her alt ait kök dizini, hello havuzu kimliği, geçerli durumu, çıkış kodu ve daha fazla belirleyebilirsiniz. Bu bilgiler hello ile birlikte kullanabileceğiniz [PoolOperations.GetNodeFile] [ poolops_getnodefile] yöntemi tooobtain hello alt 's dosyaları. Bu yöntem hello birincil görev (kimliği 0) için bilgi döndürmüyor unutmayın.

> [!NOTE]
> Aksi belirtilmediği sürece, birden çok örneği üzerinde çalışacağı Batch .NET yöntemleri hello [CloudTask] [ net_task] kendisini uygulamak *yalnızca* toohello birincil görev. Örneğin, hello çağırdığınızda [CloudTask.ListNodeFiles] [ net_task_listnodefiles] çok örnekli görev yöntemi, yalnızca hello birincil görev dosyaları döndürülür.
>
>

Merhaba aşağıdaki kod parçacığını nasıl tooobtain bilgi alt görev yanı sıra dosya içerikleri üzerinde yürütülen hello düğümlerden isteği gösterir.

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

## <a name="code-sample"></a>Kod örneği
Merhaba [MultiInstanceTasks] [ github_mpi] kodu örneği github'daki gösteren nasıl toouse çok örnekli görev toorun bir [MS MPI] [ msmpi_msdn] Toplu işlem düğümlerinde uygulama. Merhaba adımları [hazırlık](#preparation) ve [yürütme](#execution) toorun hello örnek.

### <a name="preparation"></a>Hazırlama
1. Merhaba ilk iki adımları [nasıl toocompile ve basit bir MS-MPI program Çalıştır][msmpi_howto]. Bu, aşağıdaki hello hello prerequesites adım karşılar.
2. Derleme bir *sürüm* hello sürümü [MPIHelloWorld] [ helloworld_proj] örnek MPI programı. Bu işlem düğümlerinde hello çok örnekli görev tarafından çalıştırılacak hello programıdır.
3. İçeren bir zip dosyası oluşturma `MPIHelloWorld.exe` (hangi, 2. adım yerleşik) ve `MSMpiSetup.exe` (hangi indirdiğiniz 1. adım). Bir uygulama paketi hello sonraki adım olarak bu zip dosyasını yükleyeceksiniz.
4. Kullanım hello [Azure portal] [ portal] toocreate toplu [uygulama](batch-application-packages.md) "MPIHelloWorld" olarak adlandırılan ve hello önceki adımda oluşturduğunuz sürümü olarak "1.0" Merhaba zip dosyası belirtin Merhaba uygulama paketi. Bkz: [karşıya yükleyin ve uygulamalarını yönetin](batch-application-packages.md#upload-and-manage-applications) daha fazla bilgi için.

> [!TIP]
> Derleme bir *sürüm* sürümü `MPIHelloWorld.exe` böylece ek bağımlılıkları tooinclude yoksa (örneğin, `msvcp140d.dll` veya `vcruntime140d.dll`) uygulama paketi.
>
>

### <a name="execution"></a>Yürütme
1. Merhaba karşıdan [azure-batch-samples] [ github_samples_zip] github'dan.
2. Açık hello MultiInstanceTasks **çözüm** Visual Studio 2015'te ya da daha yeni. Merhaba `MultiInstanceTasks.sln` çözüm dosyasını bulunur:

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. Batch ve Storage hesabı kimlik bilgilerinizi girin `AccountSettings.settings` hello içinde **öğesini kullanıma alın** projesi.
4. **Derleme ve çalıştırma** Merhaba MultiInstanceTasks çözüm tooexecute hello MPI örnek uygulaması üzerinde işlem düğümlerini Batch havuzunda.
5. *İsteğe bağlı*: kullanım hello [Azure portal] [ portal] veya hello [Batch Gezgini] [ batch_explorer] tooexamine hello örnek havuz, iş, ve görevi ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask"), önce hello kaynakları silin.

> [!TIP]
> İndirebilirsiniz [Visual Studio Community] [ visual_studio] ücretsiz Visual Studio yoksa.
>
>

Çıktı `MultiInstanceTasks.exe` benzer toohello aşağıda verilmiştir:

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

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba Microsoft HPC & Azure Batch ekip blogu anlatılmaktadır [MPI desteklemek için Azure batch Linux][blog_mpi_linux]ve kullanma hakkında bilgi içerir [OpenFOAM] [ openfoam] toplu ile. Merhaba Python kod örnekleri bulabilirsiniz [OpenFOAM örneği github'daki][github_mpi].
* Nasıl çok öğrenin[Linux işlem düğümleri havuzları oluşturma](batch-linux-nodes.md) Azure Batch MPI çözümlerinizi kullanmak için.

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
