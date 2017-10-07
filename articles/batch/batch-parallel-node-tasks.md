---
title: "Paralel toouse aaaRun görevlerinde işlem kaynaklarını verimli bir şekilde - Azure Batch | Microsoft Docs"
description: "Azure Batch havuzundaki her düğümde daha az işlem düğümlerini ve çalışan eş zamanlı görevleri kullanarak verimliliği ve maliyetleri artırın"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a>Toplu işlem düğümleri toomaximize kullanımını eşzamanlı olarak çalışan görevler 

Birden fazla görev aynı anda Azure Batch havuzundaki her işlem düğümünde çalıştırarak hello havuzdaki düğümlerin daha az sayıda kaynak kullanımı en üst düzeye çıkarabilirsiniz. Bazı iş yükleri için bu kısa iş süreleri ve daha düşük maliyetli neden olabilir.

Bir düğümün kaynakları tooa tek görev tümünün ayrılması bazı senaryolarda yararlı olsa da, bazı durumlarda bu kaynakları birden çok görevleri tooshare izin vererek yararlanabilirsiniz:

* **Veri aktarımı en aza** görevleri mümkün tooshare veri olduğunda. Bu senaryoda, önemli ölçüde veri aktarımı ücretlerine paylaşılan veri tooa daha az sayıda düğüm kopyalayarak azaltabilir ve her bir düğümde Paralel Görevler yürütme. Bu özellikle, Hello veri toobe kopyalanan tooeach düğümü coğrafi bölgeler arasında aktarılması geçerlidir.
* **Bellek kullanımını en üst düzeye çıkarma** görevleri bellek, ancak yalnızca dönemlerde kısa süre ve yürütme sırasında değişken zamanlarda büyük bir miktarını ne zaman gerektirir. Daha az, ancak büyük kullanan, daha fazla bellek tooefficiently düğümleriyle böyle artışlarını işlem. Bu düğümler her düğümde paralel olarak çalışan birden çok görev gerekir, ancak farklı zamanlarda her görev hello düğümleri çoktur bellek yararlanmak.
* **Düğüm sayı sınırları Azaltıcı** düğümler arası iletişimin olduğunda bir havuzu içinde gerekli. Şu anda, sınırlı too50 işlem düğümleri havuzları düğümler arası iletişim için yapılandırılan içindedir. Bu tür bir havuzdaki her düğüme mümkün tooexecute görevi paralel ise, görevlerin daha fazla sayıda eşzamanlı olarak çalıştırılabilir.
* **Bir şirket içi işlem kümesi çoğaltma**, bilgi işlem ortamı tooAzure ilk taşıdığınızda gibi. Geçerli şirket içi çözümünüzü işlem düğümü başına birden çok görev yürütülürse hello en fazla sayıyı artırabilirsiniz düğümü görevlerin toomore yakından yapılandırmayı yansıtmak.

## <a name="example-scenario"></a>Örnek senaryo
Bir örnek tooillustrate olarak Merhaba paralel görev yürütme avantajları, görev uygulamanızı CPU ve bellek gereksinimleri karşıladığından emin düşünelim şekilde [standart\_D1](../cloud-services/cloud-services-sizes-specs.md) düğümleri yeterli. Ancak, sipariş toofinish hello işinde gerekli hello zaman içinde bu düğümler 1.000 gereklidir.

Standart kullanmak yerine\_1 CPU çekirdeği olan D1 düğümleri kullanabilir [standart\_D14](../cloud-services/cloud-services-sizes-specs.md) 16 çekirdeğe sahip ve paralel görev yürütme etkinleştiren düğümleri. Bu nedenle, *16 kez daha az düğümü* 63 gerekli olacak yalnızca--1.000 düğümleri yerine kullanılabilir. Büyük uygulama dosyaları veya başvuru verileri her düğüm için gerekirse, hello veri kopyalanan tooonly 16 düğüme olduğundan ek olarak, iş süresi ve verimlilik yeniden geliştirildi.

## <a name="enable-parallel-task-execution"></a>Paralel görev yürütme etkinleştir
Paralel görev yürütme için işlem düğümlerine hello havuzu düzeyinde yapılandırın. Merhaba Batch .NET kitaplığı ile Merhaba ayarlamak [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] bir havuz oluşturduğunuzda özelliği. Merhaba Batch REST API'si kullanıyorsanız, hello ayarlamak [maxTasksPerNode] [ rest_addpool] havuzu oluşturma sırasında hello istek gövdesindeki öğesi.

Azure Batch tooset toofour kez (4 x) hello düğüm çekirdek sayısı düğümü başına en fazla görevleri sağlar. Örneğin, hello kullanırsanız havuz boyutu "Büyük" (dört çekirdek), düğümler ile sonra yapılandırılır `maxTasksPerNode` too16 ayarlanabilir. Merhaba her hello düğümü boyutları için çekirdek sayısı hakkında daha fazla bilgi için bkz: [Cloud Services boyutları](../cloud-services/cloud-services-sizes-specs.md). Hizmet sınırları hakkında daha fazla bilgi için bkz: [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md).

> [!TIP]
> Hesap hello içine emin tootake olması `maxTasksPerNode` değeri, yapısı oluştururken bir [otomatik ölçeklendirme formülü] [ enable_autoscaling] havuzunuz için. Örneğin, veren bir formül `$RunningTasks` önemli ölçüde görevleri düğümü başına bir artış tarafından etkilenebilir. Bkz: [ölçek işlem düğümlerini Azure Batch havuzunda otomatik olarak](batch-automatic-scaling.md) daha fazla bilgi için.
>
>

## <a name="distribution-of-tasks"></a>Dağıtım görevleri
Bir havuzdaki işlem düğümleri Hello görevler eşzamanlı olarak yürütebilir hello havuzdaki hello düğümleri dağıtılmış hello görevleri toobe istediğiniz önemli toospecify olur.

Hello kullanarak [CloudPool.TaskSchedulingPolicy] [ task_schedule] özelliği, görevler ("yayılmak") hello havuzdaki tüm düğümlere eşit olarak atanmalıdır belirtebilirsiniz. Veya ("sevk") hello havuzdaki tooanother düğüme atanan görevleri önce mümkün olduğunca çok görevleri tooeach düğümü atanmalıdır belirtebilirsiniz.

Bu özellik nasıl değerlidir örnek olarak, hello havuzu göz önünde bulundurun [standart\_D14](../cloud-services/cloud-services-sizes-specs.md) ile yapılandırılmış düğümlerin (Merhaba Yukarıdaki örnekteki) bir [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] 16 değeri. Merhaba, [CloudPool.TaskSchedulingPolicy] [ task_schedule] ile yapılandırılmış bir [ComputeNodeFillType] [ fill_type] , *paketi*, her düğümün tüm 16 çekirdeğe kullanımını en üst düzeye ve izin bir [otomatik ölçeklendirmeyi havuzu](batch-automatic-scaling.md) tooprune kullanılmayan düğümleri hello havuzundan (düğümler atanmış herhangi bir görevi olmadan). Bu kaynak kullanımını en aza indirir ve para kaydeder.

## <a name="batch-net-example"></a>Batch .NET örnek
Bu [Batch .NET] [ api_net] API kod parçacığını en fazla düğüm başına dört görevler dört büyük düğümleri içeren bir havuzu isteği toocreate gösterir. Bir görev görevleri önceki tooassigning görevleri tooanother düğümle hello havuzdaki her düğüm doldurur ilke zamanlama belirtir. Merhaba Batch .NET API'si kullanarak havuzları ekleme ile ilgili daha fazla bilgi için bkz: [BatchClient.PoolOperations.CreatePool][poolcreate_net].

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a>Batch REST örneği
Bu [Batch REST] [ api_rest] API parçacığı en fazla düğüm başına dört görevleri iki büyük düğümleri içeren bir havuzu isteği toocreate gösterir. Merhaba REST API kullanarak havuzları ekleme ile ilgili daha fazla bilgi için bkz: [bir havuz tooan hesabı eklemek][rest_addpool].

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> Merhaba ayarlayabilirsiniz `maxTasksPerNode` öğesi ve [MaxTasksPerComputeNode] [ maxtasks_net] havuzu oluşturma zamanında yalnızca özelliği. Bir havuzu zaten oluşturulduktan sonra bunlar değiştirilemez.
>
>

## <a name="code-sample"></a>Kod örneği
Merhaba [ParallelNodeTasks] [ parallel_tasks_sample] GitHub projede hello hello kullanımını göstermektedir [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] özelliği.

Merhaba bu C# konsol uygulaması kullanan [Batch .NET] [ api_net] kitaplığı toocreate havuzu bir veya daha fazla ile işlem düğümlerini. Bu düğümler toosimulate değişken yük yapılandırılabilir bir dizi görevi yürütür. Merhaba uygulamasından çıkışın, her görevin hangi düğümlerin yürütülen belirtir. Merhaba uygulaması ayrıca hello iş parametrelerini ve süresi bir özetini sağlar. Merhaba Özet hello örnek uygulamasının iki farklı çalıştırmalarını hello çıktısını kısmı aşağıda yer almaktadır.

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

Hello ilk yürütme hello örnek uygulamasının hello havuzunu ve her düğüm, bir görevin hello varsayılan ayar olarak tek bir düğüm ile hello iş süresi boyunca 30 dakikadır gösterir.

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

Merhaba iş süresi önemli bir düşüş ikinci hello örnek gösterir çalıştırın. Paralel görev yürütme toocomplete hello işi için neredeyse hello zaman bir Çeyrek içinde sağlayan düğüm başına dört görevlerle Hello havuzu yapılandırılmış olmasıdır.

> [!NOTE]
> Merhaba iş süreleri hello özetleri yukarıdaki içinde havuzu oluşturma zamanı içermez. Her hello işlerin yukarıdaki işlem düğümleri bundan hello oluşturulan gönderilen toopreviously havuzları edildi *boşta* gönderme zaman durum.
>
>

## <a name="next-steps"></a>Sonraki adımlar
### <a name="batch-explorer-heat-map"></a>Batch Explorer ısı Haritası
Merhaba [Azure Batch Gezgini][batch_explorer], hello Azure Batch birini [örnek uygulamaları][github_samples], içeren bir *ısıHaritası* görev yürütme görselleştirme sağlayan özelliktir. Ne zaman, yürütme hello [ParallelTasks] [ parallel_tasks_sample] kullanabileceğiniz örnek uygulama hello ısı Haritası özelliği tooeasily her düğümde Paralel Görevler hello yürütülmesi görselleştirin.

![Batch Explorer ısı Haritası][1]

*Şu anda yürütülmekte olan dört görevleri her düğüm ile dört düğüm havuzu gösteren batch Explorer ısı Haritası*

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
