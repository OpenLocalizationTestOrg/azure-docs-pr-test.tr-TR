---
title: "aaaRun Azure Batch iş yükleri uygun maliyetli düşük öncelikli vm'lerde (Önizleme) | Microsoft Docs"
description: "Azure Batch iş yükünü nasıl tooprovision düşük öncelikli sanal makineleri tooreduce hello maliyet öğrenin."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a>Düşük öncelikli sanal makineleri toplu (Önizleme) ile kullanma

Azure Batch Batch iş yükü düşük versiyonda öncelik sanal makineleri (VM'ler) tooreduce hello maliyeti sunar. Düşük öncelikli sanal makineleri de ekonomiktir işlem gücü, büyük bir miktarını sağlayarak, toplu iş yüklerinin yeni türleri mümkün kılar.

Düşük öncelikli sanal makineleri Azure'da fazlalık kapasite yararlanın. Düşük öncelikli sanal makineleri, havuzlarınızı belirttiğinizde, Azure Batch bu fazlalık kullanılabilir olduğunda otomatik olarak kullanabilirsiniz.

düşük öncelikli sanal makineleri kullanma hello kolaylığını hiçbir fazlalık kapasite Azure içinde kullanılabilir olduğunda bu VM'lerin etkisiz ' dir. Bu nedenle, düşük öncelikli sanal makineleri belirli türde bir iş yükleri için en uygun. Düşük öncelikli sanal makineleri toplu ve burada hello iş tamamlanma zamanı esnek ve hello iş üzerinde birçok VM dağıtılmış zaman uyumsuz işleme iş yükleri için kullanın.

Düşük öncelikli sanal makineleri özel VM'ler önemli ölçüde daha az pahalıdır. Fiyatlandırma ayrıntıları için bkz: [Batch fiyatlandırması](https://azure.microsoft.com/pricing/details/batch/).

Düşük öncelikli sanal makineleri için bir ek tartışma hello blog yayını duyurusuna bakın: [toplu bir hello fiyat kesir bilgi işlem](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).

> [!IMPORTANT]
> Düşük öncelikli sanal makineleri şu anda önizlemede ve yalnızca toplu işlemde çalışan iş yükleri için kullanılabilir. 
>
>

## <a name="use-cases-for-low-priority-vms"></a>Düşük öncelikli VM'ler için kullanım örnekleri

Düşük öncelikli sanal makineleri Hello özelliklerini göz önüne alındığında, hangi iş yüklerini kullanabilir ve bunları kullanamazsınız? Genel olarak, işleri birçok paralel görevlere bozuk veya çıkışı ölçeği ve üzerinde birçok VM dağıtılan birçok iş iyi bir tercihtir toplu işleme iş yüklerinin olduğunu.

-   Azure, uygun işlerinde fazlalık kapasite kullanımını toomaximize çıkışı ölçeklendirebilirsiniz.

-   Bazen VM'ler kullanılabilir durumda olmayabilir veya, işleri için sınırlı kapasite neden olur ve tootask kesinti ve tekrar bölümlerini etkisiz. İşlerini, bu nedenle toorun sürebilir hello zamanında esnek olmalıdır.

-   İşlerini uzun görevlerle kesintiye varsa daha etkilenmiş olabilir. Uzun süre çalışan bunlar yürütme gibi görevleri denetim noktası oluşturma toosave ilerleme uygulamak ise, ardından kesinti etkisini çok daha az olabilir. Kesinti Hello etkisini çok daha az olduğu gibi kısa yürütme süreleri görevlerle toowork en iyi olan düşük öncelikli VM'ler eğilimi gösterir.

-   Uzun süre çalışan birden çok VM kullanan MPI işlerini uygun toouse olmayan bir etkisiz VM düşük öncelikli VM'ler büyük olasılıkla sağlama toohello tüm işi yeniden çalıştırmak toobe sahip olur.

Düşük öncelikli VM'ler durumlarda uygun toouse bazı toplu işlem örnekleri kullanın:

-   **Geliştirme ve test**: özel olarak, büyük ölçekli çözümleri geliştirdiğinizde, önemli tasarrufları alırlar. Sınama tüm türleri yararlanabilirsiniz, ancak büyük ölçekli yük test etme ve gerileme sınaması harika kullanır.

-   **İsteğe bağlı kapasite ekleme**: düşük öncelikli sanal makineleri, normal özel VM'ler - tamamlamak için kullanılabilir kullanılabilir olduğunda, işleri ölçeklendirmek ve bu nedenle daha hızlı tamamlamak için daha düşük maliyetli; VM'ler kullanılabilir hello taban ayrılmış seçtiğinizde kullanılabilir.

-   **Esnek iş yürütme süresi**: hello zaman işlerinde esneklik ise toocomplete, sahip sonra kapasite olası bırakmaları izin; Bununla birlikte, hello ile düşük öncelikli sanal makineleri işleri eklenmesi sık daha hızlı ve daha düşük maliyetli bir çalışır.

Batch havuzları, düşük öncelikli sanal makineleri hello esneklik bağlı olarak birkaç şekilde, iş yürütme süresi yapılandırılan toouse olabilir:

-   Düşük öncelikli sanal makineleri yalnızca bir havuzda kullanılabilir ve toplu herhangi preempted kapasite kullanılabilir olduğunda yalnızca kurtarır. Düşük öncelikli yalnızca VM'ler kullanılır gibi hello ucuz yolu tooexecute işleri budur.

-   Düşük öncelikli sanal makineleri, sabit bir taban çizgisi özel VM'ler ile birlikte kullanılabilir. Merhaba ayrılmış sanal sabit sayıda iş İleri aşamalara her zaman bazı kapasite tookeep olan sağlar.

-   Böylece ucuz düşük öncelikli sanal makineleri yalnızca kullanılabilir olduğunda kullanılır, ancak adanmış bir hello tam fiyatlı VM'ler gerektiğinde tookeep kapasite kullanılabilir tookeep hello işleri en düşük düzeyde yukarı ölçeklendirilemez ayrılmış ve düşük öncelikli sanal makineleri, dinamik karışımı olabilir İleri aşamalara.

## <a name="batch-support-for-low-priority-vms"></a>Düşük öncelikli VM'ler için toplu desteği

Azure Batch kolay tooconsume ve düşük öncelikli Vm'lerden fayda çeşitli özellikleri sağlar:

-   Batch havuzları özel VM'ler ve düşük öncelikli sanal makineleri içerebilir. bir havuzu oluşturulduğunda veya hello açık yeniden boyutlandırma işlemi veya Otomatik ölçek kullanarak mevcut bir havuz için herhangi bir zamanda değiştirildi VM her tür hello sayısı belirtilebilir. İş ve görev gönderimi değişmeden kalır ve hello havuzunda hello VM türleriyle endişelenmeniz gerekmez. Ayrıca, bir havuz tamamen kullanın düşük öncelikli sanal makineleri toorun işleri mümkün, ancak özel VM'ler yukarı döndürme olarak ailenin hello kapasite çalışan işleri korumak için en düşük eşiğin altına düşerse olası toohave unutulmamalıdır.

-   Batch havuzlarının otomatik olarak toohello hedef düşük öncelikli VM'lerin sayısını arama. VM'ler etkisiz, toplu işlem kapasitesi ve dönüş toohello hedef kayıp tooreplace hello deneyecek.

-   Kesintiye görevleri Hello durumda toplu algılar ve otomatik olarak disablecomputenodeschedulingoption görevleri toobe yeniden çalıştırın.

-   Düşük öncelikli sanal makineleri özel VM'ler farklı bir çekirdek kotası var. 
    düşük öncelikli sanal makineleri daha az maliyet olduğundan hello teklif düşük öncelikli VM'ler için özel VM'ler, yüksektir. Bkz: [Batch Hizmeti kotaları ve sınırlarına](batch-quota-limit.md#resource-quotas) daha fazla bilgi için.    

> [!NOTE]
> Düşük öncelikli sanal makineleri şu anda desteklenmemektedir hello havuzu ayırma modu ayarlandığı çok Batch hesapları için[kullanıcı aboneliği](batch-account-create-portal.md#user-subscription-mode).
>
>

## <a name="create-and-update-pools"></a>Oluşturma ve havuzları güncelleştirme

Batch havuzundaki (Ayrıca başvurulan tooas işlem düğümleri) hem adanmış hem de düşük öncelikli sanal makineleri içerebilir. Hem özel hem de düşük öncelikli VM'ler için hello hedef işlem düğümü sayısını ayarlayabilirsiniz. Merhaba düğümlerin hedef sayısını belirtir hello numarası toohave hello havuzunda istediğiniz Vm'leri.

Örneğin, bir Azure bulut hizmeti VM'ler 5 hedefle kullanarak havuzu toocreate VM'ler ve 20 düşük öncelikli sanal makineleri ayrılmış:

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

VM'ler ve 20 düşük öncelikli sanal makineleri toocreate 5 bir hedef Azure sanal makinelerini (Bu durumda Linux VM'ler) kullanarak havuzu bir adanmış:

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

Hem özel hem de düşük öncelikli VM'ler için hello geçerli düğüm sayısını alabilirsiniz:

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

Merhaba düğümü adanmış veya düşük öncelikli bir VM ise havuz düğümleri özelliği tooindicate vardır:

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

Bir veya daha fazla düğüm havuzunda etkisiz, havuzu üzerinde bir liste düğümleri işlemi hala düğümleri döndürür, düşük öncelikli düğüm geçerli sayısını hello değişmeden kalır, ancak bu düğüm varsa durumlarına toothe ayarlamak **geçersiz kılındı**durumu. Toplu toofind değiştirme VM'ler deneyecek ve hello düğümleri Git başarılı olursa, **oluşturma** ve ardından **başlangıç** durumları görev yürütme için kullanılabilir hale gelmeden önce olduğu gibi yeni düğümler.

## <a name="scale-a-pool-containing-low-priority-vms"></a>Düşük öncelikli sanal makineleri içeren bir havuzu ölçeklendirme

Yalnızca özel VM'ler oluşan havuzlarıyla gibi hello boyutlandırma yöntemini çağırarak veya Otomatik ölçek kullanarak olası tooscale bir havuz içeren düşük öncelik VM'ler değil.

Merhaba havuzu yeniden boyutlandırma işlemi değerini güncelleştiren bir ikinci isteğe bağlı parametresi alan **targetLowPriorityNodes**:

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

Merhaba havuzu otomatik ölçeklendirme formülü aşağıdaki gibi düşük öncelikli sanal makineleri destekler:

-   Almak veya ayarlamak hello değişkenin değeri olarak hello hizmet tanımlı **$TargetLowPriorityNodes**.

-   Merhaba hello hizmet tanımlı değişkenin değerini alabilir **$CurrentLowPriorityNodes**.

-   Merhaba hello hizmet tanımlı değişkenin değerini alabilir **$PreemptedNodeCount**. 
    Bu değişken döndürür. hello hello düğümlerin sayısı durumu etkisiz ve yukarı veya aşağı hello kullanılamaz etkisiz düğüm hello sayısını bağlı olarak ayrılmış düğüm sayısını ölçeklendirmenizi sağlar.

## <a name="jobs-and-tasks"></a>İşler ve görevler

İşlerini ve görevleri düşük önceliğe düğümleri için çok az desteği gerektirir; Merhaba yalnızca desteği aşağıdaki gibidir:

-   Merhaba JobManagerTask özelliği bir işin sahip yeni bir özellik **AllowLowPriorityNode**. 
    Bu özelliği true olduğunda hello iş yöneticisi görevi ya da bir adanmış veya düşük öncelikli düğümünde zamanlanabilir. Bu özellik false ise, hello iş yöneticisi görevi yalnızca ayrılmış düğüm zamanlanmış tooa olacaktır.

-   Bir [ortam değişkeni](batch-compute-node-environment-variables.md) düşük öncelikli veya ayrılmış bir düğümde çalışan olup olmadığını belirleyebilmek kullanılabilir tooa görev uygulamasıdır. AZ_BATCH_NODE_IS_DEDICATED Hello ortam değişkenidir.

## <a name="handling-preemption"></a>Önalım işleme

Sanal makineleri bazen etkisiz; Bu gerçekleştiğinde, toplu aşağıdaki hello:

-   Merhaba etkisiz VM'ye sahip çok güncelleştirilmiş durumlarına**geçersiz kılındı**.
-   Görevler çalışıyormuş bu görevleri yeniden kuyruğa ve yeniden çalıştırın. ardından hello düğümü VM'ler etkisiz.
-   Merhaba VM etkili bir şekilde hello kaybolmasına VM üzerinde yerel olarak depolanan tooany veriler baştaki silinir.
-   Merhaba havuzu tooreach hello düşük öncelikli düğüm sayısını kullanılabilir sürekli olarak çalışır. Yedek kapasite bulunduğunda, düğümlerin kimlikleri tutmak ancak, oluşturulmak yeniden başlatılır **oluşturma** ve **başlangıç** görev zamanlama için kullanılabilir önce belirtir.
-   Önalım sayıları hello Azure portal'ın bir ölçü olarak kullanılabilir.

## <a name="metrics"></a>Ölçümler

Yeni ölçümleri hello kullanılabilir [Azure portal](https://portal.azure.com) düşük öncelikli düğümleri için. Bu ölçümler şunlardır:

- Düşük öncelikli düğüm sayısı
- Düşük öncelikli çekirdek sayısı 
- Etkisiz düğüm sayısı

hello Azure portal tooview ölçümlerini:

1. Tooyour hello portalda Batch hesabı gidin ve Batch hesabınızın hello ayarlarını görüntüleyin.
2. Seçin **ölçümleri** hello gelen **izleme** bölümü.
3. Hello istediğiniz hello ölçümleri seçin **kullanılabilir ölçümler** listesi.

![Düşük öncelikli düğümleri için ölçümleri](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a>Sonraki adımlar

* Okuma hello [geliştiriciler için Batch özelliklerine genel bakış](batch-api-basics.md), önemli bilgiler herkesin toouse toplu hazırlanıyor. Merhaba makale Batch uygulamanızı oluştururken kullanabileceğiniz birçok API özellikleri Batch hizmeti kaynak havuzları, düğümleri, işler ve görevler ve hello gibi hakkında daha ayrıntılı bilgi içerir.
* Merhaba hakkında bilgi edinin [Batch API'lerini ve araçları](batch-apis-tools.md) Batch çözümleri oluşturmak için kullanılabilir.
