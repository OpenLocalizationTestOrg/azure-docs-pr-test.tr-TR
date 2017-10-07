---
title: "Sayım tarafından bir işin ilerleme durumunu - Azure Batch görevleri aaaMonitor | Microsoft Docs"
description: "Merhaba işinin ilerlemesini hello görev sayar alma işlemi toocount görevler için bir işi çağırarak izleyin. Etkin, çalışan ve tamamlanan görevler ve başarılı veya başarısız olduğunu görevler tarafından sayımı elde edebilirsiniz."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: 03957d8a3d678bf44587f3bc7f988a76885c2af0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a>Görevler tarafından durumu toomonitor bir işin ilerleme durumunu (Önizleme) sayısı

Görevleri çalışan azure Batch işinin bir verimli şekilde toomonitor hello ilerlemesini sağlar. Merhaba çağırabilirsiniz [alma görev sayar] [ rest_get_task_counts] işlemi toofind bir etkin, çalışıyor veya tamamlanmış durumda kaç görevlerdir ve kaç tane sahip başarılı veya başarısız oldu. Her durumda görevleri Hello sayısı sayım tarafından daha kolay hello işin ilerleme tooa kullanıcı görüntüleyebilir, ya da beklenmeyen gecikmeler veya hello iş etkileyebilecek hataları algılar.

> [!IMPORTANT]
> Merhaba görev sayar alma işlemi şu anda önizlemede değil ve henüz Azure kamu, Azure Çin ve Azure Almanya kullanılabilir değil. 
>
>

## <a name="how-tasks-are-counted"></a>Görevlerin nasıl sayılır

Merhaba görev sayar alma işlemi aşağıdaki gibi görevleri durumuna göre sayar:

- Bir görev olarak sayılır **etkin** zaman, sıraya alınan ve mümkün toorun olmakla birlikte, şu anda tooa işlem düğümü atanmadı. Bir görev olarak da sayılır **etkin** henüz tamamlanmadı üst göreve bağımlı olması durumunda. Görev bağımlılıkları ile ilgili daha fazla bilgi için bkz: [görev bağımlılıkları diğer görevlere bağlı toorun görevler oluşturma](batch-task-dependencies.md). 
- Bir görev olarak sayılır **çalıştıran** zaman tooa işlem düğümü atanmış, ancak henüz tamamlanmadı. Bir görev olarak sayılır **çalıştıran** durumuna olduğunda ya da `preparing` veya `running`, hello tarafından belirtildiği şekilde [bir görev hakkında bilgi alma] [ rest_get_task] işlemi.
- Bir görev olarak sayılır **tamamlandı** olduğu zaman artık uygun toorun. Bir görev olarak sayılan **tamamlandı** sahip genellikle başarıyla tamamlandı ya da veya başarısız sona erdi ve ayrıca, yeniden deneme sınırını aştı. 

Merhaba görev sayar alma işlemi de kaç görevlerin başarılı veya başarısız olduğunu bildirir. Toplu göreve başarılı olup hello kontrol ederek belirler **sonuç** hello [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] özelliği Özellik:

    - Bir görev olarak sayılır **başarılı** görev yürütme hello sonuç ise `success`.
    - Bir görev olarak sayılır **başarısız** görev yürütme hello sonuç ise `failure`.

Görev durumları hakkında daha fazla bilgi için bkz: [bir görev hakkında bilgi alma][rest_get_task].

Merhaba aşağıdaki .NET kod örneği nasıl tooretrieve görev durumuna göre sayar gösterir: 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
Console.WriteLine("ValidationStatus: {0}", taskCounts.ValidationStatus);
```

> [!NOTE]
> REST için benzer bir desen ve tooget görev için bir işi sayar diğer desteklenen dilleri kullanabilirsiniz. 
> 
> 

## <a name="consistency-checking-for-task-counts"></a>Tutarlılık denetimini görev sayılarını

Merhaba Batch hizmeti, birden çok zaman uyumsuz bir Dağıtılmış Sistem parçalarını veri toplamayı tarafından görev sayıları toplar. sayıları görev tooensure doğru hello sistem birden çok bileşenden karşı tutarlılık denetimleri gerçekleştirerek durumu sayısına yönelik toplu ek doğrulama sağlar. Vardır sürece daha azını 200.000 görevleri hello işinde toplu bu tutarlılık denetimleri gerçekleştirir. Merhaba tutarlılık hataları bulur hello olası olayda, toplu hello işleminin sonucu hello hello tutarlılık denetimi sonuçlarına dayalı hello alma görevlerini sayar düzeltir. Merhaba tutarlılık denetimi hello görev sayar alma işlemi üzerinde kullanan müşteriler kendi çözüm için ihtiyaç duydukları hello doğru bilgileri almak bir ek ölçü tooensure olur.

Merhaba **validationStatus** hello yanıt özelliği, toplu hello tutarlılık denetimi gerçekleştirip gerçekleştirmediğini belirtir. Toplu mümkün toocheck durumu sayıları hello gerçek durumları hello sistemde tutulan karşı ayarlanmadı, ardından hello **validationStatus** özelliği olarak ayarlanmış çok`unvalidated`. Performans nedenleriyle toplu gerçekleştirmez hello iş içeriyorsa hello tutarlılık denetimi birden çok 200.000 görevler, bunu hello **validationStatus** özelliği ayarlanmış olabilir çok`unvalidated` bu durumda. Çok sınırlı veri kaybı son derece düşüktür ancak hello görev sayısı bu durumda, mutlaka yanlış değildir. 

Bir görev durumu değiştiğinde hello toplama ardışık hello değişiklik birkaç saniye içinde işler. Hello görev sayar alma işlemi, bu süre içinde güncelleştirilmiş hello görev sayıları yansıtır. Görev durumundaki bir değişikliği Hello toplama ardışık isabetsizliği varsa, ancak sonra değişiklik olmadığını hello sonraki doğrulama geçişini kadar kayıtlı. Bu süre boyunca görev sayıları toohello eksik olay biraz yanlış olabilir, ancak hello sonraki doğrulama geçişte düzeltilir.

## <a name="best-practices-for-counting-a-jobs-tasks"></a>Bir iş görevlerinin saymak için en iyi uygulamalar

Merhaba görev sayar alma işlemi çağırmadan hello en verimli şekilde tooreturn durumuna göre bir iş görevlerinin temel sayısını olur. Batch hizmeti sürümü 2017 06 01.5.1 kullanıyorsanız, yazma veya, kod toouse alma görev sayar güncelleştirme öneririz.

Merhaba görev sayar alma işlemi 2017 06 01.5.1'den önceki toplu işlem hizmeti sürümlerinde kullanılabilir değildir. Merhaba hizmeti daha eski bir sürümü kullanıyorsanız, ardından bir liste sorgu toocount görevleri bir işi kullanın. Daha fazla bilgi için bkz: [oluşturma sorguları toolist Batch kaynaklarını verimli bir şekilde](batch-efficient-list-queries.md).

## <a name="next-steps"></a>Sonraki adımlar

* Merhaba bkz [Batch özelliklerine genel bakış](batch-api-basics.md) toolearn Batch hizmeti kavramları ve özellikler hakkında daha fazla bilgi. Merhaba makale havuzlar, işlem düğümleri, işler ve görevler gibi birincil Batch kaynaklarını hello açıklanır ve hello hizmetin özelliklerine genel bakış sağlar.
* Hello kullanarak Batch özellikli bir uygulama geliştirme hello temellerini öğrenin [Batch .NET istemci kitaplığını](batch-dotnet-get-started.md) veya [Python](batch-python-tutorial.md). Bu Tanıtım makaleler hello Batch hizmeti tooexecute kullanan çalışan bir uygulama birden çok işlem düğümlerinde iş yükü Kılavuzu.


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job
