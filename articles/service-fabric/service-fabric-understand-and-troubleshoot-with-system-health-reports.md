---
title: "Sistem durumu raporlarını ile aaaTroubleshoot | Microsoft Docs"
description: "Sorun giderme küme veya uygulama sorunları için Azure Service Fabric bileşenleri ve bunların kullanım tarafından gönderilen hello sistem durumu raporları açıklar."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a>Sistem durumu raporları tootroubleshoot kullanın
Azure Service Fabric bileşenleri raporda hello kutusu dışında hello kümedeki tüm varlıklar. Merhaba [sistem durumu deposu](service-fabric-health-introduction.md#health-store) oluşturur ve hello sistem raporlarına dayalı varlıklar siler. Bu da onları varlık etkileşimleri yakalayan bir hiyerarşide düzenler.

> [!NOTE]
> Sistem durumu ile ilgili toounderstand kavramları hakkında daha fazla okuma [Service Fabric sistem durumu modeli](service-fabric-health-introduction.md).
> 
> 

Sistem durumu raporlarını küme ve uygulama işlevselliğini ve sistem durumu üzerinden bayrağı sorunların görünürlük sağlar. Uygulamalar ve hizmetler için sistem durumu raporlarını varlıkları uygulanır ve Service Fabric perspektif hello doğru davranmakta olduğunu doğrulayın. Merhaba raporları tüm sistem durumu hello iş mantığı hello hizmetinin veya askıdaki işlemleri algılamak izleme sağlamaz. Kullanıcı Hizmetleri hello sistem durumu bilgileri belirli tootheir mantığı verilerle zenginleştirmek.

> [!NOTE]
> Watchdogs durum raporları görünür yalnızca *sonra* hello sistem bileşenleri bir varlık oluşturun. Bir varlık silindiğinde, hello sistem durumu deposu ile ilişkili tüm sistem durumu raporları otomatik olarak siler. Merhaba varlık yeni bir örneğini oluştururken hello aynı durum geçerlidir (örneğin, yeni bir durum bilgisi olan kalıcı hizmet çoğaltma örneği oluşturulur). Merhaba eski örneği ile ilişkili tüm raporlar silinir ve hello deposundan temizlendi.
> 
> 

Merhaba sistem bileşeni raporları hello ile başlayan hello kaynağa göre tanımlanır "**sistem.**" önek. Geçersiz parametreler raporlarla reddedildi olarak watchdogs için kaynakları, aynı önek hello kullanamazsınız.
Şimdi ne tetikler toounderstand bazı sistem bakma raporları ve toocorrect hello nasıl olası sorunları bunlar temsil eder.

> [!NOTE]
> Service Fabric hello küme ve uygulama olanlar içine görünürlüğünü artırmak koşullar ilgi tooadd raporlarda devam eder. Varolan raporları de Gelişmiş ile daha fazla ayrıntı toohelp sorun giderme hello sorunu daha hızlı.
> 
> 

## <a name="cluster-system-health-reports"></a>Sistem durumu raporlarını küme
Merhaba küme durumu varlık hello health store içinde otomatik olarak oluşturulur. Her şeyi düzgün çalışmıyorsa, sistemi raporu yok.

### <a name="neighborhood-loss"></a>Komşuları kaybı
**System.Federation** Komşuları kaybı algıladığında bir hata bildirir. tek tek düğümlerden Hello rapordur ve hello düğüm kimliği hello özellik adı dahil edilir. İki olay (Merhaba boşluk rapor her iki tarafında) genellikle bir Komşuları hello tüm Service Fabric halka kaybederseniz bekleyebilirsiniz. Daha fazla Semt kaybolursa, daha fazla olay vardır.

Merhaba rapor hello genel kira zaman aşımı toolive hello zaman olarak belirtir. Merhaba koşul etkin kaldığı sürece hello rapor hello TTL süresince her yarısı gönderilir. Merhaba olay süresi dolduğunda, otomatik olarak kaldırılır. Merhaba raporlama düğümü çalışmıyor olsa bile hello rapor hello health Store'dan doğru temizlenir, süresi dolan davranış sağlar kaldırılır.

* **SourceId**: System.Federation
* **Özellik**: ile başlayan **Komşuları** ve düğüm bilgiler yer almaktadır
* **Sonraki adımlar**: neden hello Komşuları (örneğin, küme düğümleri arasındaki onay hello iletişimi) kaybolur araştırın.

## <a name="node-system-health-reports"></a>Düğüm sistem durumu raporları
**System.FM**, hello Yük Devretme Yöneticisi hizmetini temsil eder, küme düğümleri hakkında bilgi yönetir hello yetkilisi. Her düğüm System.FM durumunu gösteren bir raporu olması gerekir. Merhaba düğümü varlıklar hello düğüm durumu kaldırıldığında kaldırılır (bkz [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Düğüm yukarı/aşağı
Merhaba düğümü (Bu da çalışır durumda) hello halkası katıldığında System.FM Tamam bildirir. Merhaba halkası Hello düğümü departs zaman bir hata bildiriyor (aşağı, yükseltme ya da yalnızca bozulmuş başarısız oldu çünkü). Merhaba sistem durumu mağaza tarafından oluşturulmuş hello sistem durumu hiyerarşi bağıntı System.FM düğüm raporları ile birlikte dağıtılan varlıklarda eylemi alır. Merhaba düğüm tüm dağıtılan varlıkların sanal üst dikkate alır. Yukarı System.FM tarafından hello ile aynı hello varlıkla ilişkili hello örneği olarak örnek olarak hello düğümü bildirilirse bu düğümde dağıtılan hello varlıklar sorguları sunulur. System.FM o hello düğümü kapalı veya (yeni bir örneği) yeniden bildirdiğinde hello sistem durumu depolama yalnızca düğüm aşağı hello veya hello düğümünün hello önceki örneğinde bulunabilir dağıtılan hello varlıklar otomatik olarak temizler.

* **SourceId**: System.FM
* **Özellik**: durumu
* **Sonraki adımlar**: hello düğümü için bir yükseltme çalışmıyorsa, onu yükseltildikten sonra geri gelmesi. Bu durumda, hello sistem durumu geri tooOK geçmelisiniz. Merhaba düğümü geri gelmez veya bu başarısız olursa hello sorunu daha fazla araştırma gerekir.

Merhaba aşağıdaki örnek hello System.FM olay Tamam düğümü için bir sistem durumu ile görüntülenir:

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a>Sertifika süre sonu
**System.FabricNode** hello düğüm tarafından kullanılan sertifika sona erme olduğunda bir uyarı bildirir. Düğüm başına üç sertifika vardır: **Certificate_cluster**, **Certificate_server**, ve **Certificate_default_client**. Merhaba geçerlilik süresi en az iki hafta sonra hello rapor sistem durumu Tamam olur. Merhaba sona erme iki hafta içinde hello rapor türü bir uyarı olur. Bu olayların TTL sonsuzdur ve bir düğüm hello küme ayrıldığında bunlar kaldırılır.

* **SourceId**: System.FabricNode
* **Özellik**: ile başlayan **sertifika** ve hello sertifika türü hakkında daha fazla bilgi içerir
* **Sonraki adımlar**: sona erme olmaları durumunda hello sertifikaları güncelleştirin.

### <a name="load-capacity-violation"></a>Yük kapasite ihlali
düğüm kapasitesi ihlaline neden algıladığında bir uyarı hello Service Fabric yük dengeleyici bildirir.

* **SourceId**: System.PLB
* **Özellik**: ile başlayan **kapasitesi**
* **Sonraki adımlar**: onay sağlanan Ölçümler ve görünüm hello geçerli kapasite hello düğümde.

## <a name="application-system-health-reports"></a>Uygulama sistem durumu raporları
**System.CM**, hello Küme Yöneticisi hizmetini temsil eder, bir uygulamayla ilgili bilgileri yönetir hello yetkilisi.

### <a name="state"></a>Durum
Merhaba uygulaması oluşturulduğunda veya güncelleştirilmiş System.CM olarak Tamam bildirir. Merhaba uygulaması silindiğinde deposundan kaldırılabilir böylece hello sistem durumu deposu bildirir.

* **SourceId**: System.CM
* **Özellik**: durumu
* **Sonraki adımlar**: Merhaba uygulaması oluşturduysanız veya güncelleştirilmiş hello Küme Yöneticisi sistem durumu raporu içermelidir. Aksi takdirde, sorgu vererek Merhaba uygulaması hello durumunu denetleyin (örneğin, PowerShell cmdlet'ini hello **Get-ServiceFabricApplication - ApplicationName *applicationName***).

Merhaba aşağıdaki örnek hello durum olayı üzerinde hello gösterir **fabric: / WordCount** uygulama:

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a>Hizmet sistem durumu raporları
**System.FM**, hello Yük Devretme Yöneticisi hizmetini temsil eder, hizmetler hakkında bilgi yönetir hello yetkilisi.

### <a name="state"></a>Durum
Merhaba hizmet oluşturduğunuzda System.FM olarak Tamam bildirir. Merhaba hizmet silindiğinde hello health Store'dan hello varlık siler.

* **SourceId**: System.FM
* **Özellik**: durumu

Merhaba aşağıdaki örnek hello durum olayı hello hizmette gösterir **fabric: / WordCount/WordCountWebService**:

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a>Hizmet bağıntı hatası
**System.PLB** başka bir hizmetle ilişkili hizmet toobe güncelleştirme bir benzeşim zinciri oluşturur algıladığında bir hata bildirir. başarılı güncelleştirme gerçekleştiğinde hello rapor temizlenir.

* **SourceId**: System.PLB
* **Özellik**: ServiceDescription
* **Sonraki adımlar**: onay hello bağıntılı hizmeti açıklamaları.

## <a name="partition-system-health-reports"></a>Bölüm sistem durumu raporları
**System.FM**, hello Yük Devretme Yöneticisi hizmetini temsil eder, hizmet bölümleri hakkında bilgi yönetir hello yetkilisi.

### <a name="state"></a>Durum
Merhaba bölümü oluşturulup oluşturulmadığını ve iyi durumda olduğunda System.FM olarak Tamam bildirir. Merhaba Bölüm silindiğinde hello health Store'dan hello varlık siler.

Merhaba bölüm hello minimum yineleme sayısı ise, bir hata bildirir. Merhaba bölümü hello minimum yineleme sayısı değil, ancak hello hedef çoğaltma sayısı olan, bir uyarı bildirir. Merhaba bölüm çekirdek kaybında System.FM bir hata bildirir.

Diğer önemli olayları Hello yeniden yapılandırma beklenenden ve hello yapı beklenenden daha uzun sürerse uzun sürerse bir uyarı içerir. Beklenen hello kez hello derleme ve yeniden yapılandırma için hizmet senaryolarını temel alarak yapılandırılabilir. Örneğin, bir hizmet durumunun SQL veritabanı gibi bir terabayt varsa hello yapı durumu küçük miktarda bir hizmet için daha uzun sürer.

* **SourceId**: System.FM
* **Özellik**: durumu
* **Sonraki adımlar**: hello sistem durumu iyi değil, bazı çoğaltmaları oluşturulan, açılan ya da yükseltilen tooprimary veya ikincil doğru şekilde yapıldığını değil mümkündür. Çoğu durumda, bir hizmet hata hello açık veya rolü Değiştir uygulamasında hello temel nedeni oluşturur.

Aşağıdaki örnek hello sağlıklı bir bölüm gösterir:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Merhaba aşağıdaki örnek hedef yineleme sayısı: bir bölüm hello durumunu gösterir. Merhaba sonraki adımdır nasıl yapılandırıldığını gösterir tooget hello bölüm açıklaması: **MinReplicaSetSize** üç ve **TargetReplicaSetSize** yedi değil. Ardından hello kümedeki düğüm sayısını hello alırken: beş. Merhaba hedef çoğaltmaların sayısı hello kullanılabilir düğüm sayısından daha yüksek olduğu için bu nedenle bu durumda, iki çoğaltma yerleştirilemez.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a>Çoğaltma kısıtlama ihlali
**System.PLB** çoğaltma kısıtlama ihlali algılar ve tüm çoğaltmalarını yerleştirilemiyor varsa bir uyarı bildirir. Hello rapor ayrıntılarının hangi kısıtlamaları ve hello çoğaltma yerleştirme özellikleri engelliyor.

* **SourceId**: System.PLB
* **Özellik**: ile başlayan **ReplicaConstraintViolation**

## <a name="replica-system-health-reports"></a>Çoğaltma sistem durumu raporları
**System.RA**, hello yeniden yapılandırma aracı bileşeni temsil eden durumda hello çoğaltma durumu için hello yetkilidir.

### <a name="state"></a>Durum
**System.RA** hello çoğaltma oluşturduğunuzda Tamam bildirir.

* **SourceId**: System.RA
* **Özellik**: durumu

Aşağıdaki örnek hello sağlıklı bir çoğaltma gösterir:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a>Çoğaltma açma durumu
Merhaba API çağrısı çağrıldığında bu sistem durumu raporu hello açıklamasını hello başlangıç zamanı (Eşgüdümlü Evrensel Saat) içerir.

**System.RA** hello çoğaltma açık yapılandırılmış hello süresinden daha uzun sürerse bir uyarı raporları (varsayılan: 30 dakika). Hizmet kullanılabilirliği Hello API etkiler, hello rapor çok daha hızlı (bir yapılandırılabilir aralığıyla, varsayılan değer 30 saniyedir) verilir. ölçülen hello zaman hello çoğaltıcı açın ve açık hello hizmeti için harcanan hello süre içerir. Merhaba açarsanız hello özelliği değişiklikleri tooOK tamamlar.

* **SourceId**: System.RA
* **Özellik**: **ReplicaOpenStatus**
* **Sonraki adımlar**: hello sistem durumu iyi değil, neden hello çoğaltma açık beklenenden uzun sürüyor araştırın.

### <a name="slow-service-api-call"></a>Yavaş hizmeti API çağrısı
**System.RAP** ve **System.Replicator** çağrısı toohello kullanıcı hizmet kodu yapılandırılmış hello süreden uzun sürerse bir uyarı rapor. Merhaba çağrısı tamamlandığında hello uyarı temizlenir.

* **SourceId**: System.RAP veya System.Replicator
* **Özellik**: hello yavaş API hello adı. Merhaba açıklama hello zaman hello API'si hakkında daha fazla ayrıntı bekleyen açıldı sağlar.
* **Sonraki adımlar**: hello çağrısı neden beklenenden uzun sürüyor araştırın.

Aşağıdaki örneğine hello bir bölüm çekirdek kaybına ve hello araştırma bitti adımları toofigure neden çıkışı gösterir. Durumunu almak için hello çoğaltmaları biri bir uyarı sistem durumu sahip. Bunu hello hizmet işlemi System.RAP tarafından bildirilen bir olayı beklenenden daha uzun sürer gösterir. Bu bilgileri alındıktan sonra hello sonraki adıma hello hizmet koduna toolook olduğu ve var. araştırın. Bu durumda, hello **RunAsync** hello durum bilgisi olan hizmet uygulaması işlenmeyen bir özel durum oluşturur. Merhaba çoğaltmaları geri dönüştürülmesi tüm yinelemeleri hello uyarı durumunda göremeyebilirsiniz. Alma hello sistem durumu yeniden deneyin ve farklılıklarını hello çoğaltma kimliği arayın Bazı durumlarda, hello deneme ipuçları verebilirsiniz.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

Hatalı bir uygulama hello hello hata ayıklayıcı altında başlattığınızda hello Tanılama Olayları windows hello durum RunAsync göster:

![Visual Studio 2015 Tanılama Olayları: RunAsync hatası fabric: / HelloWorldStatefulApplication.][1]

Visual Studio 2015 Tanılama Olayları: RunAsync hatası **fabric: / HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>Çoğaltma kuyruğu dolu
**System.Replicator** hello çoğaltma sırası dolu olduğunda bir uyarı bildirir. Bir veya daha fazla ikincil çoğaltmaları yavaş tooacknowledge işlemler olduğundan hello üzerinde birincil, çoğaltma sırası genellikle tam haline gelir. Merhaba hizmeti yavaş tooapply hello işlemleri olduğunda ikincil hello üzerinde bu genellikle gerçekleşir. Merhaba sırası dolu olduğunda hello uyarı temizlenir.

* **SourceId**: System.Replicator
* **Özellik**: **PrimaryReplicationQueueStatus** veya **SecondaryReplicationQueueStatus**hello çoğaltma rolü bağlı olarak

### <a name="slow-naming-operations"></a>Yavaş adlandırma işlemleri
**System.NamingService** adlandırma işlemi kabul edilebilir daha uzun sürerse, birincil Çoğaltmada durumu raporları. Adlandırma işlemleri örnekleri [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) veya [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync). Daha fazla yöntem FabricClient altında örneğin altında bulunabilir [hizmet yönetimi yöntemleri](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) veya [özellik yönetimi yöntemleri](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> Merhaba adlandırma hizmeti hello Küme hizmeti adları tooa konumunda çözümler ve kullanıcıların toomanage hizmet adları ve özellikleri sağlar. Bu hizmet bölümlenmiş bir Service Fabric kalıcı olur. Merhaba bölümden biri hello tüm Service Fabric adları ve Hizmetleri hakkında meta veriler içeren Authority Owner temsil eder. Merhaba Service Fabric adları hello hizmet Genişletilebilir olacak şekilde Name Owner bölümleri adlı eşlenen toodifferent bölümlerdir. Daha fazla bilgi edinin [hizmet adlandırma](service-fabric-architecture.md).
> 
> 

Bir adlandırma işlemi beklenenden daha uzun sürerse, hello işlemi hello uyarı raporda ile işaretlenir *hizmet bölüm adlandırma hello birincil çoğaltmasını hizmet hello işlemi*. Merhaba işlem başarıyla tamamlanırsa hello uyarı temizlenir. Merhaba işlemi bir hata ile tamamlarsa, hello sistem durumu raporu hello hatayla ilgili ayrıntılar içerir.

* **SourceId**: System.NamingService
* **Özellik**: önek ile başlayan **Duration_** ve hello yavaş işlemi ve hangi hello üzerinde işlem uygulanır hello Service Fabric adını tanımlar. Örneğin, hizmet adı doku oluşturma: / MyApp/MyService gereken çok uzun, hello özelliği Duration_AOCreateService.fabric:/MyApp/MyService. AO noktaları toohello rolü hello adlandırma bölüm bu adı ve işlem için.
* **Sonraki adımlar**: onay neden hello adlandırma işlemi başarısız olur. Her bir işlemin farklı kök neden olabilir. Örneğin, silme hizmet takılmış bir düğümde hello uygulama ana bilgisayarı hello servis kodu tooa kullanıcı hata nedeniyle bir düğümde kilitlenen tutar olduğundan.

Aşağıdaki örneğine hello oluşturma hizmeti işlemi gösterilmektedir. Merhaba işlemi yapılandırılan hello süreden daha uzun sürdü. AO yeniden deneme sayısı ve iş tooNO gönderir. HİÇBİR tamamlanmış hello son işlem zaman aşımı ile. Bu durumda, hello aynı çoğaltma hello AO ve rol için birincil özelliğidir.

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>DeployedApplication sistem durumu raporları
**System.Hosting** hello yetkilisi dağıtılan varlıklar üzerinde.

### <a name="activation"></a>Etkinleştirme
Bir uygulama hello düğümde başarıyla etkinleştirildi System.Hosting olarak Tamam bildirir. Aksi takdirde bir hata bildirir.

* **SourceId**: System.Hosting
* **Özellik**: hello ürün sürümüne dahil olmak üzere etkinleştirme
* **Sonraki adımlar**: neden hello etkinleştirme başarısız hello uygulamanın sağlıksız olduğunu gerekiyorsa araştırın.

Merhaba aşağıdaki örnek başarılı etkinleştirme gösterir:

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>İndir
**System.Hosting** hello uygulama paketin indirmesi başarısız olursa bir hata bildirir.

* **SourceId**: System.Hosting
* **Özellik**:  **indirin:*RolloutVersion***
* **Sonraki adımlar**: hello indirme hello düğümde neden başarısız araştırın.

## <a name="deployedservicepackage-system-health-reports"></a>DeployedServicePackage sistem durumu raporları
**System.Hosting** hello yetkilisi dağıtılan varlıklar üzerinde.

### <a name="service-package-activation"></a>Hizmet paketi etkinleştirme
System.Hosting Tamam hello hizmet paketi etkinleştirme hello düğümde başarılı olup olmadığını bildirir. Aksi takdirde bir hata bildirir.

* **SourceId**: System.Hosting
* **Özellik**: etkinleştirme
* **Sonraki adımlar**: neden hello etkinleştirme başarısız araştırın.

### <a name="code-package-activation"></a>Kod paketi etkinleştirme
**System.Hosting** hello etkinleştirme başarılı olduğunda Tamam her kod paketi için raporlar. Merhaba etkinleştirme başarısız olursa, yapılandırılan bir uyarı bildirir. Varsa **CodePackage** tooactivate başarısız olduğunda veya yapılandırılmış hello büyük bir hata ile sona erer **CodePackageHealthErrorThreshold**, barındırma bir hata bildirir. Bir hizmet paketi birden çok kod paketler içeriyorsa, bir etkinleştirme raporu her biri için oluşturulur.

* **SourceId**: System.Hosting
* **Özellik**: kullanır hello önek **CodePackageActivation** ve hello kod paketi ve hello giriş noktası olarak hello adını içeren  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint*** (örneğin, **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Hizmet türü kayıt
**System.Hosting** hello hizmet türü başarıyla kaydedilmişse Tamam bildirir. Merhaba kayıt zamanında yapıldığında değildi hata raporları (kullanılarak yapılandırılan **ServiceTypeRegistrationTimeout**). Merhaba çalışma zamanı kapattıysanız, hello hizmet türü hello düğümden kaydı ve barındırma bir uyarı bildirir.

* **SourceId**: System.Hosting
* **Özellik**: kullanır hello önek **ServiceTypeRegistration** ve hello hizmet türü adı içerir (örneğin, **ServiceTypeRegistration:FileStoreServiceType**)

Aşağıdaki örnek hello sağlıklı dağıtılmış hizmet paketi gösterir:

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>İndir
**System.Hosting** hello hizmet paketin indirmesi başarısız olursa bir hata bildirir.

* **SourceId**: System.Hosting
* **Özellik**:  **indirin:*RolloutVersion***
* **Sonraki adımlar**: hello indirme hello düğümde neden başarısız araştırın.

### <a name="upgrade-validation"></a>Yükseltme doğrulaması
**System.Hosting** hello yükseltme sırasında doğrulama başarısız veya hello varsa hello düğümde yükseltme başarısız olursa bir hata bildirir.

* **SourceId**: System.Hosting
* **Özellik**: kullanır hello önek **FabricUpgradeValidation** ve hello yükseltme sürümünü içerir
* **Açıklama**: işaret toohello hata ile karşılaşıldı

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric sistem durumu raporlarını görüntüle](service-fabric-view-entities-aggregated-health.md)

[Nasıl tooreport ve onay sistem durumu hizmeti](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[İzleme ve Hizmetleri yerel olarak tanılama](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md)

