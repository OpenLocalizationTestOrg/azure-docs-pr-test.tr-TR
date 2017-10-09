---
title: "aaaUse görev bağımlılıkları toorun görevler bağlı diğer görevler - Azure Batch hello tamamlanmasından | Microsoft Docs"
description: "MapReduce stili ve benzer büyük veri işleme ile ilgili diğer görevler hello tamamlanmasından bağımlı görevler oluşturma Azure Batch iş yükleri."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a>Görev bağımlılıkları diğer görevlere bağlı toorun görevler oluşturma

Yalnızca bir üst görev tamamlandıktan sonra görev bağımlılıkları toorun bir görevi veya görev kümesini tanımlayabilirsiniz. Görev bağımlılıkları yararlı olduğu bazı senaryolar şunlardır:

* MapReduce stili iş yükleri hello bulutta.
* İşleri, veri işleme görevlerini yönlendirilmiş Çevrimsiz grafik (DAG) ifade edilebilir.
* Her görevin nerede Hello sonraki görev başlamadan önce tamamlamanız gerekir ön işleme ve sonrası işleme işlemleri.
* Aşağı Akış görevleri Yukarı Akış görevleri hello çıktısını bağımlı diğer işler.

Toplu görev bağımlılıkları ile bir veya daha fazla üst görevleri hello tamamlandıktan sonra işlem düğümlerinde yürütülmesi için zamanlanmış görevler oluşturabilirsiniz. Örneğin, ayrı, paralel görevler içeren bir 3B film her karesini işleyen bir iş oluşturabilirsiniz. Merhaba son görev--hello "Birleştirme görev"--hello tam film yalnızca çerçeveler çizilir hello tüm çerçeveler birleştirmeler başarıyla çizilir.

Yalnızca hello üst görevi başarıyla tamamlandıktan sonra varsayılan olarak, bağımlı görevler çalıştırılmak üzere zamanlandı. Bir bağımlılık eylem toooverride hello varsayılan davranışı belirtin ve hello üst görevi başarısız olduğunda görev çalıştırın. Merhaba bkz [bağımlılık Eylemler](#dependency-actions) ayrıntıları bölümü.  

Diğer görevleri birebir veya bire çok ilişkide bağımlı görevler oluşturabilirsiniz. Burada hello tamamlama görevleri görev kimlikleri belirtilen bir aralıkta Grubu'nun bir görevin bağlı bir aralık bağımlılık de oluşturabilirsiniz. Bu üç temel senaryodan toocreate çok-çok ilişkileri birleştirebilirsiniz.

## <a name="task-dependencies-with-batch-net"></a>Görev bağımlılıkları Batch .NET ile
Bu makalede, nasıl kullanarak tooconfigure görev bağımlılıkları hello aşağıdakiler ele [Batch .NET] [ net_msdn] kitaplığı. İlk nasıl çok gösteriyoruz[görev bağımlılığı etkinleştirmek](#enable-task-dependencies) , işlerini ve nasıl çok göstermek[görev bağımlılıkları ile yapılandırma](#create-dependent-tasks). Merhaba üst başarısız olursa bir bağımlılık eylem toorun bağımlı nasıl toospecify görevler de açıklanmaktadır. Son olarak, hello aşağıdakiler ele [bağımlılık senaryolarına](#dependency-scenarios) toplu destekleyen.

## <a name="enable-task-dependencies"></a>Görev bağımlılıkları etkinleştir
Batch uygulamanızda toouse görev bağımlılıkları, öncelikle hello iş toouse görev bağımlılıkları yapılandırmanız gerekir. Batch .NET içinde etkinleştirmeden, [CloudJob] [ net_cloudjob] ayarlayarak kendi [UsesTaskDependencies] [ net_usestaskdependencies] özelliği çok`true`:

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

Önceki kod parçacığını hello "batchClient" Merhaba örneği olan [BatchClient] [ net_batchclient] sınıfı.

## <a name="create-dependent-tasks"></a>Bağımlı görevler oluşturma
bir veya daha fazla üst görevleri hello tamamlanmasından bağlıdır bir görev toocreate, diğer görevler, görev "bağlıdır" Merhaba hello belirtebilirsiniz. Batch .NET içinde hello yapılandırma [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] hello örneği özelliğiyle [Github_samples] [ net_taskdependencies] sınıfı:

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

Bu kod parçacığını görev kimliği "Çiçekler" bağımlı bir görev oluşturur. Merhaba "Çiçekler" görev görevlere "Yağmur" ve "Sun" bağlıdır. Görev "Çiçekler" bir işlem düğümünde zamanlanmış toorun yalnızca "Yağmur" ve "Sun" tamamladınız görevleri sonra olacaktır.

> [!NOTE]
> Bir görev hello olduğunda toobe başarıyla tamamlandı olarak kabul edilir **tamamlandı** durumu ve kendi **çıkış kodu** olan `0`. Batch .NET içinde yani bir [CloudTask][net_cloudtask].[ Durumu] [ net_taskstate] özellik değerinin `Completed` ve CloudTask'ın hello [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] özellik değeri `0`.
> 
> 

## <a name="dependency-scenarios"></a>Bağımlılık senaryoları
Azure Batch kullanabileceğiniz üç temel görev bağımlılık senaryo vardır: birebir, bir çok ve görev kimliği aralığı bağımlılık. Bu birleşik tooprovide dördüncü bir senaryo, çok-olabilir.

| Senaryo&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Örnek |  |
|:---:| --- | --- |
|  [Bire bir](#one-to-one) |*Görevb* bağlıdır *Göreva* <p/> *Görevb* kadar yürütülmek zamanlanmaz *Göreva* başarıyla tamamlandı |![Diyagram: bire bir görev bağımlılığı][1] |
|  [Bir çok](#one-to-many) |*görevC* hem *görevA* hem de *görevB*’ye bağlıdır <p/> *Görevc* her ikisi de kadar yürütülmek zamanlanmaz *Göreva* ve *Görevb* başarıyla tamamladınız. |![Diyagram: bir çok görev bağımlılığı][2] |
|  [Görev Kimliği aralığı](#task-id-range) |*Görevd* bir dizi göreve bağlıdır <p/> *Görevd* kimlikleri hello görevlerle kadar yürütülmek zamanlanmaz *1* aracılığıyla *10* başarıyla tamamladınız. |![Diyagram: Görev kimliği aralığı bağımlılığı][3] |

> [!TIP]
> Oluşturabileceğiniz **çok-** burada görevlere A ve b C D, E ve F her görevleri bağlı gibi ilişkileri Bu, örneğin, paralel birkaç ölçeklendirin önişlem senaryolarında olduğu birden çok Yukarı Akış görevi hello çıktısını aşağı akış görevlerinizi bağımlı yararlıdır.
> 
> Yalnızca hello üst görevleri başarıyla tamamlandıktan sonra bu bölümde hello örneklerde, bağımlı bir görev çalıştırır. Bağımlı bir görev için varsayılan davranış hello davranıştır. Bir bağımlılık eylem toooverride hello varsayılan davranışı belirterek üst görev başarısız olduktan sonra bağımlı görev çalıştırabilirsiniz. Merhaba bkz [bağımlılık Eylemler](#dependency-actions) ayrıntıları bölümü.

### <a name="one-to-one"></a>Bire bir
Bire bir ilişkide bir görev hello başarılı bir üst görevin tamamlanma bağlıdır. toocreate Merhaba bağımlılık, tek bir görev kimliği toohello sağlamak [Github_samples][net_taskdependencies].[ OnId] [ net_onid] hello doldurmak statik yöntemi [DependsOn] [ net_dependson] özelliği [CloudTask] [ net_cloudtask].

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a>Bir çok
Bir-çok ilişkisi görev birden çok üst görevleri hello tamamlanmasından bağlıdır. toocreate Merhaba bağımlılık, görev kimlikleri toohello koleksiyonunu sağlamak [Github_samples][net_taskdependencies].[ OnIds] [ net_onids] hello doldurmak statik yöntemi [DependsOn] [ net_dependson] özelliği [CloudTask] [ net_cloudtask].

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a>Görev Kimliği aralığı
Üst görevleri bir dizi bir bağımlılık olarak hello hello tamamlama görevleri, kimlikleri bir aralıkta bulunan bir görev bağlıdır.
toocreate hello bağımlılık hello ilk sağlayın ve son kimlikleri hello aralığı toohello görev [Github_samples][net_taskdependencies].[ OnIdRange] [ net_onidrange] hello doldurmak statik yöntemi [DependsOn] [ net_dependson] özelliği [CloudTask] [net_cloudtask].

> [!IMPORTANT]
> Bağımlılıklarınız için görev kimliği aralıklarını kullandığınızda, görev kimlikleri hello aralıktaki hello *gerekir* tamsayı değerleri dize gösterimlerini olabilir.
> 
> Her görev hello aralıktaki hello bağımlılık başarıyla tamamlanmasını ya da çok ayarlamak eşlenen tooa bağımlılık eylem bir hata ile Tamamlanıyor karşılaması gerekir**Satisfy**. Merhaba bkz [bağımlılık Eylemler](#dependency-actions) ayrıntıları bölümü.
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a>Bağımlılık Eylemler

Yalnızca bir üst görev başarıyla tamamlandıktan sonra varsayılan olarak, bağımlı görev veya dizi görevi çalıştırır. Merhaba üst görev başarısız olsa bile, bazı senaryolarda, toorun bağımlı görevler isteyebilirsiniz. Bir bağımlılık eylemi belirterek hello varsayılan davranışı geçersiz kılabilirsiniz. Bir bağımlılık eylemi bağımlı görev hello başarı veya başarısızlık hello üst görevinin durumuna göre uygun toorun olup olmadığını belirtir. 

Örneğin, bağımlı görevi hello Yukarı Akış görevi hello tamamlanmasından verilerden bekliyor varsayalım. Merhaba Yukarı Akış görevi başarısız olursa, hello bağımlı görev hala eski verileri kullanarak mümkün toorun olabilir. Bu durumda, bir bağımlılık eylemin hello bağımlı görev hello üst görev hello başarısızlığını rağmen uygun toorun belirtebilirsiniz.

Bir bağımlılık eylemin hello üst görev için bir çıkış koşulu temel alır. Herhangi bir çıkış koşullarını izleyen hello için bir bağımlılık eylemi belirtebilirsiniz; .NET için bkz: Merhaba [ExitConditions] [ net_exitconditions] sınıfı Ayrıntılar için:

- Ön işleme bir hata oluştuğunda.
- Bir dosyayı karşıya yüklemeyi hata oluşur. Merhaba görev aracılığıyla belirtilen çıkış kodu ile çıkar varsa **exitCodes** veya **exitCodeRanges**ve bir dosya karşıya yükleme hatası, hello eylemin hello çıkış kodu önceliğe tarafından belirtilen karşılaşır.
- Merhaba görev çıktığında hello tarafından tanımlanan bir çıkış kodu ile **ExitCodes** özelliği.
- Merhaba görev çıktığında hello tarafından belirtilen bir aralıkta denk bir çıkış kodu ile **ExitCodeRanges** özelliği.
- Başlangıç görevi tarafından tanımlanmamış bir çıkış kodu ile bulunup bulunmadığını varsayılan durumda, Hello **ExitCodes** veya **ExitCodeRanges**, veya bir ön-işleme hatası ve hello hello görev bulunup bulunmadığını **PreProcessingError**  özelliği ayarlı değil ya da hello gerekmiyorsa görev başarısız bir dosyayla hata ve hello karşıya **FileUploadError** özelliği ayarlı değil. 

toospecify .NET, kümesi hello bağımlılık eylemde [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] hello çıkış koşulu özelliği. Merhaba **DependencyAction** özelliği iki değerden birini alır:

- Ayar hello **DependencyAction** özelliği çok**Satisfy** belirtilen bir hata ile Merhaba üst görev bulunup bulunmadığını bağımlı görevler uygun toorun olduğunu gösterir.
- Ayar hello **DependencyAction** özelliği çok**blok** bağımlı görevler uygun toorun olmadığını gösterir.

Merhaba hello için varsayılan ayar **DependencyAction** özelliği **Satisfy** çıkış kodu 0 için ve **blok** diğer tüm çıkış koşulları için.

Merhaba aşağıdaki kod parçacığını ayarlar hello **DependencyAction** özelliği için bir üst görev. Ön işleme bir hata ile Merhaba üst görev çıkar veya hello ile belirtilen hata kodları hello bağımlı görev engellendi. Başka bir sıfır olmayan hata ile Merhaba üst görev bulunup bulunmadığını hello bağımlı uygun toorun bir görevdir.

```csharp
// Task A is hello parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a>Kod örneği
Merhaba [Github_samples] [ github_taskdependencies] örnek proje hello biridir [Azure Batch kod örnekleri] [ github_samples] github'da. Bu Visual Studio çözümü gösterir:

- Nasıl tooenable görev iş bağımlılığı
- Nasıl toocreate görevler diğer görevlere bağlı
- Tooexecute olanlar nasıl görevler üzerinde işlem düğümü havuzu oluşturacak.

## <a name="next-steps"></a>Sonraki adımlar
### <a name="application-deployment"></a>Uygulama dağıtımı
Merhaba [uygulama paketleri](batch-application-packages.md) batch özelliği bir tooboth dağıtmak için kolay bir yolla ve görevlerinizi yürütmek hello uygulamaları işlem düğümlerini sürüm sağlar.

### <a name="installing-applications-and-staging-data"></a>Uygulama yükleme ve verileri hazırlama
Bkz: [uygulamaların yüklenmesi ve toplu veri hazırlama işlem düğümlerini] [ forum_post] toorun görevleri düğümleriniz hazırlığı yöntemlerine genel bakış için hello Azure Batch Forumunda. Hello Azure Batch ekip üyelerinin, biri tarafından bu post hello farklı şekillerde toocopy uygulamaları iyi öncü yazılır, görev giriş verilerinin ve diğer dosyaları tooyour işlem düğümleri.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diyagram: bire bir bağımlılık"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diyagram: bir çok bağımlılık"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diyagram: görev kimliği aralığı bağımlılığı"
