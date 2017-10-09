---
title: "Azure mikro aaaSimulate başarısızlık | Microsoft Docs"
description: "Bu makalede, Microsoft Azure Service Fabric bulunan hello Test Edilebilirlik eylemler hakkında alınmaktadır."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a>Test Edilebilirlik Eylemler
Sipariş toosimulate güvenilir olmayan bir altyapı'da, Azure Service Fabric, yolları toosimulate ile Merhaba Geliştirici çeşitli gerçek hataları ve durumu geçişleri sağlar. Bu Test Edilebilirlik eylemler olarak sunulur. Merhaba Eylemler hello belirli bir arıza ekleme, durum geçişi veya doğrulama neden alt düzey API'leri. Bu eylemler ile birleştirerek kapsamlı test senaryoları için hizmetlerinizi yazabilirsiniz.

Service Fabric, bazı ortak test senaryoları bu eylemleri oluşan sağlar. Tootest ortak durumu geçişleri ve hata durumları dikkatle seçilen bu yerleşik senaryolar kullanan öneririz. Ancak, hello yerleşik senaryolarla henüz kapsamında yer almayan veya uygulamanız için özel olarak hazırlanmış özel olan senaryolar için tooadd kapsamı istediğinizde Eylemler kullanılan toocreate özel test senaryoları olabilir.

C# uygulamalarının hello eylemlerin hello System.Fabric.dll derlemesi bulunamadı. Merhaba sistem Fabric PowerShell modülü hello Microsoft.ServiceFabric.Powershell.dll derlemesi bulunamadı. Çalışma zamanı yüklemesinin bir parçası olarak hello ServiceFabric PowerShell Modülü yüklü tooallow kullanım kolaylığı için ' dir.

## <a name="graceful-vs-ungraceful-fault-actions"></a>Normal durunda hataya Eylemler karşılaştırması
Test Edilebilirlik Eylemler iki ana demet sınıflandırılır:

* Durunda hatası: Bu hataları hataları makine yeniden başlatmaları gibi benzetimini gerçekleştirmek ve işlem kilitleniyor. Hatalar bu gibi durumlarda hello yürütme bağlamı işleminin aniden durdurur. Bu, hello uygulama yeniden başlatılmadan önce hello durumunun temizleme çalıştırabileceğiniz anlamına gelir.
* Normal hatası: Bu hataları çoğaltma taşır gibi normal eylemlerin ve Yük Dengeleme tarafından tetiklenen düşme benzetimini yapma. Böyle durumlarda, hello hizmeti hello bildirimi Kapat alır ve hello durumunu çıkmadan önce temizleyebilirsiniz.

Daha iyi kalite doğrulama hello hizmetini çalıştırmak ve iş yükünü inducing çeşitli normal ve durunda hataları oluştu. Durunda hataları burada hello hizmeti aniden bazı iş akışı hello ortadaki çıkılıyor senaryoları uygulamaktadır. Merhaba hizmet çoğaltma Service Fabric tarafından geri yüklendikten sonra bu testleri hello kurtarma yolu. Bu, veri tutarlılığı ve hello hizmeti durumu hataları sonra doğru olup olmadığını yönetilmesini test yardımcı olur. Merhaba diğer hatalar (Merhaba normal hata sayısı) sınama kümesi hello hizmet Service Fabric tarafından taşınan tooreplicas doğru şekilde yanıt verir. Bu işleme iptal hello RunAsync yönteminde sınar. Merhaba hizmetinin toocheck hello iptal belirteci ayarlayın, durumunu doğru şekilde kaydedin ve hello RunAsync yöntemi çıkın olmak için gerekir.

## <a name="testability-actions-list"></a>Test Edilebilirlik eylemler listesi
| Eylem | Açıklama | Yönetilen API | PowerShell cmdlet'i | Normal/durunda hataları |
| --- | --- | --- | --- | --- |
| CleanTestState |Merhaba küme hello test sürücüsünün hatalı bir kapanma durumunda tüm hello test durumlarını kaldırır. |CleanTestStateAsync |Remove-ServiceFabricTestState |Uygulanamaz |
| InvokeDataLoss |Veri kaybı hizmet bölüme uygulanmasını. |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |Normal |
| InvokeQuorumLoss |Belirtilen durum bilgisi olan hizmet bölüm çekirdek kayıp yerleştirir. |InvokeQuorumLossAsync |Çağırma ServiceFabricQuorumLoss |Normal |
| Birincil taşıma |Taşıma hello birincil çoğaltma bir durum bilgisi olan hizmet toohello belirtilen küme düğümü belirtilen. |MovePrimaryAsync |Taşıma ServiceFabricPrimaryReplica |Normal |
| İkincil taşıma |Merhaba geçerli ikincil çoğaltma bir durum bilgisi olan hizmet tooa farklı küme düğümü taşır. |MoveSecondaryAsync |Taşıma ServiceFabricSecondaryReplica |Normal |
| RemoveReplica |Bir çoğaltma hatası bir kümeden bir çoğaltma kaldırarak benzetimini yapar. Bu hello çoğaltma kapatılacak ve toorole geçirecektir 'None', durumunun tamamı hello kümeden kaldırma. |RemoveReplicaAsync |Remove-ServiceFabricReplica |Normal |
| RestartDeployedCodePackage |Kod paketi işlemi başarısız bir kümedeki bir düğümün dağıtılmış kod paketi yeniden başlatarak benzetimini yapar. Bu işlemde barındırılan tüm hello kullanıcı hizmet çoğaltmalar yeniden hello kod paket işlemi durdurur. |RestartDeployedCodePackageAsync |Yeniden başlatma ServiceFabricDeployedCodePackage |Durunda |
| RestartNode |Bir Service Fabric kümesi düğüm hatasından bir düğümü yeniden başlatarak benzetimini yapar. |RestartNodeAsync |Yeniden başlatma ServiceFabricNode |Durunda |
| RestartPartition |Bir veri merkezi Kararma veya küme Kararma senaryosu bir bölüm, bazı veya tüm çoğaltmaları yeniden başlatarak benzetimini yapar. |RestartPartitionAsync |Restart-ServiceFabricPartition |Normal |
| RestartReplica |Bir çoğaltma hatası kalıcı çoğaltma bir kümede yeniden hello çoğaltma kapatma ve yeniden açmayı benzetimini yapar. |RestartReplicaAsync |Yeniden başlatma ServiceFabricReplica |Normal |
| BaşlangıçDüğümü |Bir düğüm zaten durdurulmuş bir kümede başlatır. |StartNodeAsync |Start-ServiceFabricNode |Uygulanamaz |
| StopNode |Bir düğüm hatasından bir küme düğümünde durdurarak benzetimini yapar. BaşlangıçDüğümü çağrılıncaya kadar hello düğümü kapalı kalır. |StopNodeAsync |Stop-ServiceFabricNode |Durunda |
| ValidateApplication |Merhaba kullanılabilirlik ve bazı hata hello sisteme inducing sonra genellikle bir uygulamadaki tüm Service Fabric Hizmetleri durumunu doğrular. |ValidateApplicationAsync |Test-ServiceFabricApplication |Uygulanamaz |
| ValidateService |Merhaba kullanılabilirlik ve Service Fabric hizmeti bazı hata hello sisteme genellikle inducing sonra doğrular. |ValidateServiceAsync |Test-ServiceFabricService |Uygulanamaz |

## <a name="running-a-testability-action-using-powershell"></a>PowerShell kullanarak bir Test Edilebilirlik eylem çalıştırma
Bu öğretici şunların nasıl yapıldığını gösterir toorun PowerShell kullanarak bir Test Edilebilirlik eylem. Şunları öğreneceksiniz nasıl toorun yerel (bir çalıştırma) küme veya bir Azure kümesine karşı Test Edilebilirlik eylem. Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell modülü--otomatik olarak yüklenir hello Microsoft Service Fabric MSI yükleyin. Merhaba modülü, PowerShell istemi açtığınızda otomatik olarak yüklenir.

Eğitmen kesimleri:

* [Bir eylem karşı bir kutusunu küme çalıştırın](#run-an-action-against-a-one-box-cluster)
* [Bir eylem Azure bir küme karşı çalıştırma](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>Bir eylem karşı bir kutusunu küme çalıştırın
toorun yerel bir küme karşı Test Edilebilirlik eylem, toohello küme ve Yönetici modu açık hello PowerShell komut isteminde önce bağlanın. Bize hello Ara **yeniden ServiceFabricNode** eylem.

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

Burada, eylemin hello **yeniden ServiceFabricNode** "Düğüm1" adlı bir düğümde çalıştırın. Hello tamamlanma modu, hello düğümü yeniden başlatma eylemi gerçekten başarılı olup olmadığını doğrulamalıdır değil olduğunu belirtir. Hello yeniden başlatma eylemi gerçekten başarılı olup olmadığını belirten hello tamamlama modu "Doğrula" olarak tooverify neden olur. Merhaba düğüm adıyla doğrudan belirtmek yerine, çoğaltma, bir bölüm anahtarı ve hello tür ile aşağıdaki gibi belirtebilirsiniz:

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**Yeniden başlatma ServiceFabricNode** kullanılan toorestart bir kümede bir Service Fabric olmalıdır. Bu, tüm bu düğümde barındırılan hello sistemi hizmeti ve kullanıcı hizmet çoğaltmalar yeniden hello Fabric.exe işlemi durdurulacak. Bu API tootest kullanarak, hizmetinizi hello yük devretme kurtarma yolları boyunca hatalar ortaya çıkarmaya yardımcı olur. Merhaba kümedeki düğüm hatalarını benzetimini yardımcı olur.

Merhaba aşağıdaki ekran gösterilir hello **yeniden ServiceFabricNode** eylem Test Edilebilirlik komutu.

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

Merhaba hello ilk çıkış **Get-ServiceFabricNode** (Merhaba Service Fabric PowerShell modülden bir cmdlet) bu hello yerel küme sahip beş düğüm gösterir: Node.1 tooNode.5. Merhaba Test Edilebilirlik eylem (cmdlet'ini) sonra **yeniden ServiceFabricNode** hello düğümde yürütülen Node.4 adlı, biz bu hello düğümün çalışır durumda kalma süresi sıfırlama bakın.

### <a name="run-an-action-against-an-azure-cluster"></a>Bir eylem Azure bir küme karşı çalıştırma
Bir Test Edilebilirlik eylemi (PowerShell kullanarak) çalıştıran bir Azure küme karşı benzer toorunning hello yerel bir küme karşı eylemdir. bağlantı toohello yerel küme, yerine hello eylem çalıştırmadan önce fark, yalnızca hello tooconnect toohello Azure ihtiyacınız ilk küme.

## <a name="running-a-testability-action-using-c35"></a>C & #35 kullanarak bir Test Edilebilirlik eylemi çalıştıran;
C# kullanarak bir Test Edilebilirlik eylemi toorun, öncelikle tooconnect toohello küme FabricClient kullanarak gerekir. Ardından hello gerekli parametreleri toorun hello eylem edinin. Farklı parametreler kullanılabilir toorun hello aynı eylemi.
Merhaba kümede hello RestartServiceFabricNode eylemin hello düğümü bilgileri (düğüm adı ve düğüm örnek kimliği) kullanarak olan tek yönlü toorun bakarak.

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

Parametre açıklaması:

* **CompleteMode** bu hello modu doğrulama hello yeniden başlatma eylemi gerçekten başarılı olup olmadığını belirtir. Hello yeniden başlatma eylemi gerçekten başarılı olup olmadığını belirten hello tamamlama modu "Doğrula" olarak tooverify neden olur.  
* **OperationTimeout** kümeleri hello hello işlemi toofinish süresini TimeoutException özel durum önce.
* **CancellationToken** iptal bekleyen çağrı toobe sağlar.

Merhaba düğüm adıyla doğrudan belirtmek yerine, bir bölüm anahtarı ve hello tür çoğaltma aracılığıyla belirtebilirsiniz.

Daha fazla bilgi için bkz: [PartitionSelector ve ReplicaSelector](#partition_replica_selector).

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a>PartitionSelector ve ReplicaSelector
### <a name="partitionselector"></a>PartitionSelector
PartitionSelector Test Edilebilirlik kullanıma sunulan bir yardımcı olan ve olduğu kullanılan tooselect belirli bir bölüm üzerinde hangi tooperform hello Test Edilebilirlik eylemlerden herhangi birini. Merhaba bölüm kimliği önceden biliniyorsa kullanılan tooselect belirli bir bölüm olabilir. Veya, hello bölüm anahtarı sağlayabilir ve hello işlemi hello bölüm kimliği dahili olarak çözer. Rastgele bir bölüm seçme hello seçeneğiniz de vardır.

toouse bu yardımcı hello PartitionSelector nesnesi oluşturun ve hello Select * yöntemlerden birini kullanarak hello bölümü seçin. Daha sonra hello PartitionSelector nesne toohello gerektirdiği API geçirin. Hiçbir seçeneği seçili değilse tooa rastgele bölümü varsayılan olarak ayarlanır.

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a>ReplicaSelector
ReplicaSelector Test Edilebilirlik kullanıma sunulan bir yardımcı olan ve kullanılan toohelp seçin hangi tooperform kopyada hello Test Edilebilirlik eylemlerden herhangi birini. Merhaba çoğaltma kimliği önceden biliniyorsa kullanılan tooselect belirli bir çoğaltma olabilir. Ayrıca, bir birincil çoğaltmayı veya rastgele ikincil seçme hello seçeneğiniz vardır. ReplicaSelector PartitionSelector türetilen, yani tooselect gerekiyor her ikisi de tooperform hello Test Edilebilirlik işlemi istediğiniz çoğaltma ve hello bölüm hello.

toouse bu yardımcı ReplicaSelector nesnesi oluşturun ve tooselect hello çoğaltma ve hello bölümü istediğiniz hello biçimde ayarlayın. Ardından hello gerektirdiği API geçirebilirsiniz. Hiçbir seçeneği seçili değilse tooa rastgele çoğaltma ve rastgele bölümü varsayılan olarak.

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a>Sonraki adımlar
* [Test Edilebilirlik senaryoları](service-fabric-testability-scenarios.md)
* Nasıl tootest hizmetinizi
  * [Hataları sırasında hizmet iş yüklerinin benzetimi](service-fabric-testability-workload-tests.md)
  * [Hizmetten hizmete iletişim hatası](service-fabric-testability-scenarios-service-communication.md)

