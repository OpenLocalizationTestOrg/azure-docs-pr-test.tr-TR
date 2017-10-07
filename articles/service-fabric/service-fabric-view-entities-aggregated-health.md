---
title: "aaaHow tooview Azure Service Fabric varlıkları toplanan sistem durumu | Microsoft Docs"
description: "Nasıl tooquery, görüntülemek ve sistem durumu sorgularının ve genel sorgular aracılığıyla Azure Service Fabric varlıkları toplanan Sistem Değerlendirme açıklar."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a>Service Fabric sistem durumu raporlarını görüntüle
Azure Service Fabric tanıtır bir [sistem durumu modeli](service-fabric-health-introduction.md) hangi sistem bileşenleri ve watchdogs yerel koşulları rapor için sistem durumu varlıkları ile bunların izlemekte olduğunuz. Merhaba [sistem durumu deposu](service-fabric-health-introduction.md#health-store) varlıklar sağlıklı olup tüm sistem durumu verileri toodetermine toplar.

Merhaba küme hello sistem bileşenleri tarafından gönderilen sistem durumu raporları ile birlikte otomatik olarak doldurulur. Ayrıntılı bilgi için [kullanım sistem durumu raporları tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).

Service Fabric birden çok yol tooget toplanan hello durumunu hello varlıklar sağlar:

* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) veya diğer görsel Araçlar
* Sistem durumu sorgularının (aracılığıyla, PowerShell, API veya REST)
* Genel sistem durumu (aracılığıyla, PowerShell, API veya REST) hello özelliklerinden biri olarak varlıklar, bu dönüş listesini sorgular

Şimdi bu seçenekleri toodemonstrate beş düğümler ve hello yerel bir küme kullanın [fabric: / WordCount uygulamasını](http://aka.ms/servicefabric-wordcountapp). Merhaba **fabric: / WordCount** iki varsayılan hizmet, bir durum bilgisi olan hizmet türü içeren uygulama `WordCountServiceType`ve durum bilgisiz hizmet türü `WordCountWebServiceType`. Merhaba değiştirilen `ApplicationManifest.xml` toorequire yedi hedef çoğaltmaları hello durum bilgisi olan hizmet ve bir bölüm. Merhaba kümede yalnızca beş düğüm olduğundan hello sistem bileşenleri hello hizmet bölüme bir uyarı hello hedef sayısı olduğundan bildirin.

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a>Service Fabric Explorer'da sistem durumu
Service Fabric Explorer hello küme görsel görünümünü sağlar. Merhaba resimde, görebilirsiniz:

* Merhaba uygulama **fabric: / WordCount** tarafından raporlanan bir hata olayı olduğundan (hata) kırmızıdır **MyWatchdog** hello özelliği için **kullanılabilirlik**.
* Kendi hizmetlerden biri **fabric: / WordCount/WordCountService** sarı (uyarı). Merhaba hizmet yedi yinelemelerle yapılandırılır ve iki repicas yerleştirilemez şekilde hello kümesinin beş düğümü vardır. Burada gösterilmese hello hizmeti sistem rapordan nedeniyle sarı bölümdür `System.FM` olduğunu belirten `Partition is below target replica or instance count`. Merhaba sarı bölüm Tetikleyicileri sarı hizmet hello.
* Merhaba küme hello kırmızı nedeniyle kırmızı uygulamasıdır.

Merhaba değerlendirme varsayılan ilkelerden hello küme bildirimi ve uygulama bildirimi kullanır. Bunlar, katı ilkeleri ve herhangi bir hata tolerans değil.

Service Fabric Explorer ile Merhaba küme görünümü:

![Service Fabric Explorer ile Merhaba küme görüntüleyin.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> Daha fazla bilgi edinin [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

## <a name="health-queries"></a>Sistem durumu sorgularının sayısı
Service Fabric her desteklenen hello için sistem durumu sorgularının sunan [varlık türleri](service-fabric-health-introduction.md#health-entities-and-hierarchy). Merhaba yöntemleri kullanarak API aracılığıyla erişilebilir [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlet'leri ve REST. Bu sorguları hello varlık tüm sistem bilgilerini döndürür: hello toplanan sistem durumu, varlık sistem durumu olayları, alt sistem durumlarını (varsa), (Merhaba varlık sağlıklı olmadığında) sağlıksız değerlendirmeleri ve alt sistem durumu istatistikleri (zaman uygulanabilir).

> [!NOTE]
> Merhaba health store içinde tam olarak doldurulan bir sistem durumu varlık döndürülür. Merhaba varlık (silinmez) etkin ve sistem raporu olması gerekir. Merhaba hiyerarşi zinciri kendi üst varlıklarını ayrıca sistem raporları sahip olmalıdır. Bu koşulların herhangi biri değil sağlanırsa, hello durumu return sorgular bir [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) ile [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` gösterir neden hello varlık alınmadı.
>
>

Merhaba sistem durumu sorgularının hello varlık türüne bağlıdır hello varlık tanımlayıcısı geçmesi gerekir. Merhaba sorguları isteğe bağlı sistem durumu ilkesi parametreleri kabul eder. Sistem durumu ilkeleri belirtilirse, hello [sistem durumu ilkeleri](service-fabric-health-introduction.md#health-policies) hello küme veya uygulama bildirimden değerlendirmesi için kullanılır. Sistem durumu ilkeleri için bir tanım Hello bildirimleri içermiyorsa, hello varsayılan sistem durumu ilkeleri değerlendirme için kullanılır. Merhaba varsayılan sistem durumu ilkeleri hataları tolerans değil. Merhaba sorgular yalnızca kısmi alt döndürmek için filtreler de kabul veya belirtilen filtreler saygı olayları--hello olanları hello. Başka bir filtre hello alt istatistikleri hariç izin verir.

> [!NOTE]
> Merhaba ileti yanıt boyutu azaltılmış şekilde hello çıkış filtreleri hello sunucu tarafında uygulanır. Toolimit hello veri döndürülen yerine filtreleri hello istemci tarafında uygulama hello çıkış filtreleri kullanmanızı öneririz.
>
>

Bir varlığın durumu içerir:

* Merhaba hello varlık sistem durumu birleştirilir. Varlık sistem durumu raporları, alt sistem durumlarını (varsa) ve sistem durumu ilkeleri göre hello sistem durumu depoya göre hesaplanır. Daha fazla bilgi edinin [varlık sistem durumu değerlendirmesi](service-fabric-health-introduction.md#health-evaluation).  
* Sistem durumu olayları hello varlıkta hello.
* alt bulunabilir hello varlıklar için tüm alt sistem durumlarının Hello koleksiyonu. Merhaba sistem durumlarını ve toplanan sistem durumu hello varlık tanımlayıcıları içerir. tooget tüm sistem için bir alt hello sorgu durumu hello alt varlık türü için çağırın ve hello alt tanımlayıcıda geçirin.
* Hello varlık sağlam değilse bu noktası toohello rapor hello sağlıksız değerlendirmeleri hello varlığın hello durum tetikledi. Merhaba değerlendirmeleri özyinelemeli, geçerli sistem durumu tetiklenen hello alt sistem durumu değerlendirmesini içeren ' dir. Örneğin, bir izleme bir çoğaltma karşı bir hata bildirdi. Merhaba uygulama sistem tooan sağlıksız hizmet nedeniyle sağlıksız bir değerlendirme gösterir; Merhaba hizmettir tooa bölümünde hata nedeniyle sağlıksız; Merhaba bölümdür tooa çoğaltma hatası nedeniyle sağlıksız; Merhaba çoğaltma toohello izleme hata sistem durumu raporu sağlam değil.
* alt hello varlıklar tüm alt türleri için Hello sistem durumu istatistikleri. Örneğin, küme durumu uygulamalar, hizmetler, bölümler, çoğaltmaları toplam sayısını hello gösterir ve varlıkları hello kümedeki dağıtılabilir. Hizmet çoğaltmaları hello altında belirtilen ve hello toplam bölüm sayısı hizmetin sistem durumunu gösterir.

## <a name="get-cluster-health"></a>Küme durumu Al
Döndürür hello küme varlık durumunu hello ve uygulamaların ve düğümler (Merhaba Küme alt) hello sistem durumlarını içerir. Giriş:

* [İsteğe bağlı] hello küme sistem durumu ilkesi tooevaluate hello düğümler ve hello küme olayları kullanılır.
* [İsteğe bağlı] hello uygulama sistem durumu ilkesi Eşlem ' hello sistem durumu ilkeleri ile toooverride hello uygulama bildirim ilkeleri kullanılır.
* [İsteğe bağlı] Olaylar, düğümleri ve hangi girişlerin belirtin uygulamaları filtreler ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir. Tüm olayları, düğümleri ve uygulamaları hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu markalarıdır.
* [İsteğe bağlı] Tooexclude sağlık istatistikleri filtreleyin.
* [İsteğe bağlı] Filtre tooinclude fabric: / sistem durumu istatistiklerine hello sağlık istatistikleri. Yalnızca hello sağlık istatistikleri değil çıkarıldığında geçerlidir. Varsayılan olarak, hello sistem durumu İstatistikler yalnızca kullanıcı uygulamaları ve hello sistem uygulaması için istatistikleri içerir.

### <a name="api"></a>API
tooget küme sistem durumu, oluşturma bir `FabricClient` ve çağrı hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) yöntemi kendi **HealthManager**.

Merhaba aşağıdaki çağrıyı hello küme durumu alır:

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

Merhaba aşağıdaki kodu hello küme durumu bir özel küme sistem durumu ilkesi kullanarak alır ve düğümler ve uygulamalar için filtreler. Merhaba sağlık istatistikleri hello doku içerdiğini belirtir: / Sistem istatistikleri. Oluşturduğu [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), hello giriş bilgilerini içerir.

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Merhaba cmdlet tooget hello küme durumu [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth). İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.

Merhaba hello küme beş düğümü, hello sistem uygulaması ve doku durumda: / WordCount açıklandığı şekilde yapılandırılmış.

cmdlet aşağıdaki Merhaba, varsayılan sistem durumu ilkeleri kullanarak küme durumu alır. Merhaba toplanmış uyarı sistem durumu, çünkü hello fabric: / WordCount uygulamasını uyarı. Merhaba sağlıksız değerlendirmeleri Ayrıntıları toplanan hello durumu tetikleyen hello koşullara nasıl sağladığını unutmayın.

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

Merhaba aşağıdaki PowerShell cmdlet'ini hello küme hello durumunu özel uygulama İlkesi kullanarak alır. Sonuçları tooget yalnızca uygulamalar ve hata veya uyarı düğümler filtreler. Tüm sağlıklı olarak sonuç olarak, düğüm, döndürülür. Yalnızca doku hello: / WordCount uygulamasını hello uygulamaları filtre dikkate alır. Merhaba özel ilke hello doku için hata olarak tooconsider uyarıları belirttiğinden: / WordCount uygulama hello hata olduğu gibi değerlendirilir ve bu nedenle hello kümedir.

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a>REST
Küme durumu ile alabilirsiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) veya [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.

## <a name="get-node-health"></a>Düğüm durumu Al
Döndürür, bir düğüm varlık durumunu hello ve hello düğümde bildirilen hello sistem durumu olayları içerir. Giriş:

* Merhaba düğümü tanımlar [gerekli] hello düğüm adı.
* [İsteğe bağlı] hello küme sistem durumu ilkesi ayarlarını tooevaluate sistem durumu kullanılır.
* [İsteğe bağlı] Hangi girişlerin belirten olaylar için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir. Tüm olaylar hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu verilmiştir.

### <a name="api"></a>API
tooget düğüm durumu hello API aracılığıyla oluşturma bir `FabricClient` ve çağrı hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) kendi HealthManager yöntemi.

Merhaba aşağıdaki kodu hello düğüm durumu hello belirtilen düğüm adı alır:

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

Merhaba olayları filtresi ve özel İlkesi aracılığıyla düğüm adı ve geçişleri belirtilen için hello aşağıdaki kodu hello düğüm durumu alır [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Merhaba cmdlet tooget hello düğüm durumu [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth). İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.
cmdlet aşağıdaki Merhaba, varsayılan sistem durumu ilkeleri kullanarak hello düğüm durumu alır:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Merhaba aşağıdaki cmdlet'i hello tüm düğümlerinin sistem durumunu hello kümede alır:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a>REST
Düğüm durumu ile alabileceğiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) veya bir [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.

## <a name="get-application-health"></a>Uygulama durumunu Al
Bir uygulama varlığı hello durumunu döndürür. Dağıtılan hello uygulama ve hizmet öğelerini hello sistem durumlarını içerir. Giriş:

* Merhaba uygulaması tanımlayan [gerekli] hello uygulama adı (URI).
* [İsteğe bağlı] hello uygulama durumu ilkesi toooverride hello uygulama bildirim ilkeleri kullanılır.
* [İsteğe bağlı] Olaylar, hizmetler ve hangi girişlerin belirtin dağıtılan uygulamalar için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir. Tüm olaylar, hizmetler ve dağıtılan uygulamalar hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu var.
* [İsteğe bağlı] Tooexclude hello sağlık istatistikleri filtreleyin. Belirtilmezse, hello sistem durumu istatistikleri hello Tamam, uyarı ve hata sayısı için tüm uygulama alt öğeleri içerir: Hizmetler, bölümler, çoğaltmalar, dağıtılan uygulamalar ve hizmet paketleri dağıtılabilir.

### <a name="api"></a>API
tooget uygulama sistem oluşturma bir `FabricClient` ve çağrı hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) kendi HealthManager yöntemi.

Merhaba aşağıdaki kodu hello uygulama sağlığını hello belirtilen uygulama adı (URI) alır:

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

Merhaba aşağıdaki kodu hello uygulama sağlığını hello belirtilen uygulama adı (URI) için filtrelerle alır ve özel ilkelerinde belirtilen aracılığıyla [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Merhaba cmdlet tooget hello uygulama durumu [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps). İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.

Merhaba aşağıdaki cmdlet'i döndürür hello hello durumunu **fabric: / WordCount** uygulama:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

PowerShell cmdlet özel ilkeler geçişte aşağıdaki hello. Ayrıca, alt ve olayları filtreler.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a>REST
Uygulama health ile alabilirsiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) veya [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.

## <a name="get-service-health"></a>Hizmet durumunu Al
Bir hizmet varlığı hello durumunu döndürür. Merhaba bölüm sistem durumlarını içerir. Giriş:

* Merhaba hizmet tanımlayan [gerekli] hello hizmet adı (URI).
* [İsteğe bağlı] hello uygulama durumu ilkesi toooverride hello uygulama bildirim İlkesi kullanılır.
* [İsteğe bağlı] Olayları ve hangi girişlerin belirtmek bölümleri için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir. Tüm olayları ve bölümleri hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu markalarıdır.
* [İsteğe bağlı] Tooexclude sağlık istatistikleri filtreleyin. Belirtilmezse, sistem durumu istatistikleri göster hello Tamam Merhaba, tüm bölümler ve çoğaltmalar Merhaba hizmetinin uyarı ve hata sayısı.

### <a name="api"></a>API
tooget hizmet durumu hello API aracılığıyla oluşturma bir `FabricClient` ve çağrı hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) kendi HealthManager yöntemi.

Merhaba aşağıda belirtilen hizmet adı (URI) hizmetiyle hello durumunu alır:

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

Merhaba aşağıdaki kodu alır hello hizmet durumu hello belirtilen hizmet adı (URI), filtreleri ve özel ilke aracılığıyla belirtme [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Merhaba cmdlet tooget hello hizmet durumu [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth). İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.

cmdlet aşağıdaki Merhaba, varsayılan sistem durumu ilkeleri kullanarak hello hizmet durumu alır:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a>REST
Hizmet durumu ile alabileceğiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) veya bir [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.

## <a name="get-partition-health"></a>Bölüm durumu Al
Bir bölüm varlık hello durumunu döndürür. Merhaba çoğaltma sistem durumlarını içerir. Giriş:

* [Gerekli] hello bölüm hello bölüm tanımlayan kimlik (GUID).
* [İsteğe bağlı] hello uygulama durumu ilkesi toooverride hello uygulama bildirim İlkesi kullanılır.
* [İsteğe bağlı] Olayları ve hangi girişlerin belirtin çoğaltmaları için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir. Tüm olayları ve çoğaltmaları hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu markalarıdır.
* [İsteğe bağlı] Tooexclude sağlık istatistikleri filtreleyin. Belirtilmezse, kaç tane çoğaltmaları Tamam, uyarı ve hata durumlarıdır hello sistem durumu istatistiklerini gösterir.

### <a name="api"></a>API
tooget bölüm durumu hello API aracılığıyla oluşturma bir `FabricClient` ve çağrı hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) kendi HealthManager yöntemi. toospecify isteğe bağlı parametreleri, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a>PowerShell
Merhaba cmdlet tooget hello bölüm durumu [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth). İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.

Hello aşağıdaki cmdlet'i alır hello tüm bölümleri için hello sistem durumu **fabric: / WordCount/WordCountService** hizmeti ve filtreleri çoğaltma sistem durumlarını çıkışı:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
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
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Bölüm health ile alabileceğiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) veya bir [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.

## <a name="get-replica-health"></a>Çoğaltma durumu Al
Bir durum bilgisi olan hizmet çoğaltmayı veya bir durum bilgisiz hizmet örneği Hello durumunu döndürür. Giriş:

* Merhaba çoğaltma tanımlayan [gerekli] hello bölüm kimlik (GUID) ve çoğaltma kimliği.
* [İsteğe bağlı] hello uygulama sistem durumu ilkesi parametreleri toooverride hello uygulama bildirim ilkeleri kullanılır.
* [İsteğe bağlı] Hangi girişlerin belirten olaylar için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir. Tüm olaylar hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu verilmiştir.

### <a name="api"></a>API
tooget hello çoğaltma durumu hello API aracılığıyla oluşturma bir `FabricClient` ve çağrı hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) kendi HealthManager yöntemi. Gelişmiş parametrelerini, kullanım toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a>PowerShell
Merhaba cmdlet tooget hello çoğaltma durumu [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth). İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.

Merhaba aşağıdaki cmdlet'i hello birincil çoğaltma hello hizmetinin tüm bölümler için başlangıç durumunu alır:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Çoğaltma sistem durumu ile alabileceğiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) veya bir [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.

## <a name="get-deployed-application-health"></a>Dağıtılmış uygulama durumunu Al
Düğümün varlık üzerinde dağıtılmış bir uygulaması hello durumunu döndürür. Dağıtılan hello hizmet paketi sistem durumlarını içerir. Giriş:

* Merhaba tanımlamak [gerekli] hello uygulama adı (URI) ve düğüm adı (dize) uygulama dağıtıldı.
* [İsteğe bağlı] hello uygulama durumu ilkesi toooverride hello uygulama bildirim ilkeleri kullanılır.
* [İsteğe bağlı] Olayları ve hangi girişlerin belirtin dağıtılmış hizmet paketleri için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir. Tüm olayları ve dağıtılmış hizmet paketleri hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu markalarıdır.
* [İsteğe bağlı] Tooexclude sağlık istatistikleri filtreleyin. Belirtilmezse, hello sağlık istatistikleri Tamam, uyarı ve hata sistem durumlarının dağıtılmış hizmet paketleri hello sayısını gösterir.

### <a name="api"></a>API
tooget hello durumunu hello API aracılığıyla bir düğümde dağıtılan bir uygulama oluşturmak bir `FabricClient` ve çağrı hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) kendi HealthManager yöntemi. toospecify isteğe bağlı parametreleri, [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a>PowerShell
Merhaba cmdlet tooget dağıtılan hello uygulama sağlığını olan [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps). İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i. uygulamanın dağıtıldığı çıkışı toofind çalıştırmak [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) ve hello bakma dağıtılan uygulama alt.

Merhaba aşağıdaki cmdlet'i alır hello hello durumunu **fabric: / WordCount** dağıtılan uygulama **_Node_2**.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
Dağıtılmış uygulama sistem durumu ile alabilirsiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) veya [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.

## <a name="get-deployed-service-package-health"></a>Dağıtılan hizmet paketi durumu Al
Dağıtılan hizmet paketi varlık durumunu döndürür hello. Giriş:

* [Gerekli] hello uygulama adı (URI), düğüm adı (dize) ve hizmet bildirim adı (dize) hello tanımlayan hizmet paketi dağıtıldı.
* [İsteğe bağlı] hello uygulama durumu ilkesi toooverride hello uygulama bildirim İlkesi kullanılır.
* [İsteğe bağlı] Hangi girişlerin belirten olaylar için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir. Tüm olaylar hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu verilmiştir.

### <a name="api"></a>API
Merhaba API aracılığıyla dağıtılan hizmet paketi tooget hello durumunu oluşturmak bir `FabricClient` ve çağrı hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) kendi HealthManager yöntemi. toospecify isteğe bağlı parametreleri, [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a>PowerShell
Merhaba cmdlet tooget dağıtılan hello hizmet paketi durumu olan [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth). İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i. uygulamanın dağıtıldığı, toosee çalıştırmak [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) ve dağıtılan hello uygulamaları arayın. olan hizmet paketleri bir uygulamada arama sırasında hello toosee dağıtılan hizmet paketi alt hello içinde [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) çıktı.

Merhaba aşağıdaki cmdlet'i alır hello hello durumunu **WordCountServicePkg** hello hizmet paketi **fabric: / WordCount** dağıtılan uygulama **_Node_2**. Merhaba varlık **System.Hosting** başarılı hizmet paketi ve giriş noktası etkinleştirme ve başarılı hizmet türü kaydı için raporları.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
Dağıtılan hizmet paketi durumu ile alabileceğiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) veya bir [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.

## <a name="health-chunk-queries"></a>Sistem durumu öbek sorguları
Merhaba sistem durumu öbek sorgular giriş filtreleri başına (yinelemeli olarak), çok düzeyli Küme alt döndürebilir. Büyük bir esnekliğe hello alt seçerken izin Gelişmiş Filtreler destekleyen toobe döndürdü. Merhaba filtreler alt hello benzersiz tanımlayıcı veya diğer grup kimlikleri ve/veya sistem durumlarını tarafından belirtebilirsiniz. Varsayılan olarak, hiç alt öğe, her zaman birinci düzeydeki alt öğeleri dahil karşılıklı toohealth komutları dahil edilir.

Merhaba [sistem durumu sorgularının](service-fabric-view-entities-aggregated-health.md#health-queries) hello dönüş yalnızca ilk düzeyi alt belirtilen gerekli filtreleri her varlık. tooget hello alt hello alt ilgi her bir varlık için ek sistem durumu API'leri çağırmanız gerekir. Benzer şekilde, belirli varlıkları tooget hello durumunu, istenen her varlık için bir sistem durumu API çağırmalıdır. Merhaba filtreleme Gelişmiş öbek sorgu toorequest sağlar hello ileti boyutu ve iletileri hello sayısını en aza bir sorgu ilgi birden çok öğe.

Merhaba hello öbek sorgu, sistem durumu daha fazla küme varlıklar (gerekli kök dizininde başlayan olası tüm küme varlıklar) için tek çağrıda alabilirsiniz olduğunu değeridir. Karmaşık sistem durumu sorgusu gibi ifade edebilirsiniz:

* Dönüş yalnızca uygulamalar hata ve bu uygulamalar için uyarı veya hata tüm hizmetleri içerir. Döndürülen hizmetler için tüm bölümleri içerir.
* Yalnızca hello durumunu adlarıyla belirtilen dört uygulamaları döndür.
* Yalnızca hello durumunu uygulamaları istenen uygulama türü döndürür.
* Tüm dağıtılan varlık, bir düğümde döndür. Tüm uygulamalar, hello belirtilen düğümdeki tüm dağıtılan uygulamaları ve bu düğümdeki tüm dağıtılan hello hizmet paketleri döndürür.
* Tüm çoğaltmaları hata döndürür. Tüm uygulamalar, hizmetler, bölümler ve yalnızca çoğaltmalar hata döndürür.
* Tüm uygulamaları döndür. Belirtilen bir hizmeti için tüm bölümleri içerir.

Şu anda hello sistem durumu öbek sorgu yalnızca hello küme varlık için açıktır. İçeren bir küme durumu öbek döndürür:

* Merhaba küme durumu birleştirilir.
* Hello sağlık durumu öbek listesi giriş filtreleri saygı düğümleri.
* Hello sağlık durumu öbek giriş filtreleri saygı uygulamaların listesi. Her uygulama sistem durumu öbek giriş filtreleri ve hello filtreleri saygı tüm dağıtılmış uygulamaları öbek listesiyle saygı tüm hizmetleri ile öbek listesini içerir. Merhaba alt hizmetler ve dağıtılan uygulamalar için aynı. Bu şekilde hello kümedeki tüm varlıklar olası istediyseniz, hiyerarşik bir biçimde döndürülebilir.

### <a name="cluster-health-chunk-query"></a>Küme durumu öbek sorgu
Döndürür hello küme varlık durumunu hello ve hello hiyerarşik sağlık durumu öbekleri gerekli alt içerir. Giriş:

* [İsteğe bağlı] hello küme sistem durumu ilkesi tooevaluate hello düğümler ve hello küme olayları kullanılır.
* [İsteğe bağlı] hello uygulama sistem durumu ilkesi Eşlem ' hello sistem durumu ilkeleri ile toooverride hello uygulama bildirim ilkeleri kullanılır.
* [İsteğe bağlı] Düğümler ve hangi girişlerin belirtin uygulamalar için filtreleri ilgilendiğiniz ve hello sonucunda döndürülmelidir. Merhaba filtreleri belirli tooan varlık/Grup varlıkların veya o düzeyde uygulanabilir tooall varlıklardır. filtrelerin listesi Hello bir genel filtre ve/veya hello sorgu tarafından döndürülen belirli tanımlayıcıları toofine çizgisi varlıklar için filtreleri içerebilir. Merhaba alt öğe boş ise, varsayılan olarak döndürülmez.
  Merhaba filtreler hakkında daha fazla bilgiyi [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) ve [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter). Merhaba uygulama filtreleri can yinelemeli çocuklar için Gelişmiş filtreler belirtin.

Merhaba öbek sonuç hello filtreleri saygı hello alt öğeleri içerir.

Şu anda hello öbek sorgu sağlıksız değerlendirmeleri veya varlık olaylarını döndürmüyor. Bu ek bilgileri hello var olan küme sistem durumu sorgusu kullanılarak edinilebilir.

### <a name="api"></a>API
tooget küme durumu öbek, oluşturma bir `FabricClient` ve çağrı hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) yöntemi kendi **HealthManager**. İçinde geçirebilirsiniz [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe sistem durumu ilkeleri ve Gelişmiş filtreleri.

Merhaba aşağıdaki kodu küme durumu Öbek ile Gelişmiş filtreleri alır.

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Merhaba cmdlet tooget hello küme durumu [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk). İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.

Hata dışında her zaman döndürülmesi gereken belirli bir düğüm, yalnızca olmaları durumunda hello aşağıdaki kodu düğümleri alır.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

cmdlet aşağıdaki hello küme Öbek ile uygulama filtrelerini alır.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

Merhaba aşağıdaki cmdlet'i tüm dağıtılan varlıklar bir düğümde döndürür.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a>REST
Küme durumu Öbek ile alabileceğiniz bir [GET isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) veya [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) sistem durumu ilkeleri ve Gelişmiş filtreleri hello gövdesinde açıklanan içerir.

## <a name="general-queries"></a>Genel sorgular
Genel sorguları belirtilen bir türün Service Fabric varlıkların listesini döndürür. Merhaba API sunulur (Merhaba yöntemleri aracılığıyla **FabricClient.QueryManager**), PowerShell cmdlet'leri ve REST. Bu sorgular, alt sorgular birden çok bileşenlerini toplama. Bunlardan biri olan hello [sistem durumu deposu](service-fabric-health-introduction.md#health-store), toplanan her sorgu sonucu için sistem durumu, hello doldurur.  

> [!NOTE]
> Genel sorgular hello toplanan sistem durumu hello varlığın dönün ve zengin sistem durumu verileri içermez. Bir varlık sağlam değilse, sistem durumu sorguları tooget ile olayları, alt sistem durumlarını ve sağlıksız değerlendirmeleri gibi tüm sistem durumu bilgilerini, izleyebilirsiniz.
>
>

Genel sorgular bir varlık için bir bilinmeyen sistem durumu döndürürse, bu hello sistem durumu depoyu hello varlık hakkında tam veri yok mümkündür. Ayrıca bir alt sorgu toohello sistem durumu deposu başarılı değildi mümkündür (örneğin, bir iletişim hatası oluştu veya hello sistem durumu deposu kısıtlanan). Merhaba varlık için bir sistem durumu sorgusu ile izle. Merhaba alt sorgu ağ sorunları gibi geçici bir hatayla karşılaştı, bu izleme sorgu başarılı olabilir. Bu aynı zamanda, daha fazla ayrıntı neden hello varlık sunulmaz hakkında hello health Store'dan verebilir.

Merhaba içeren sorgular **HealthState** varlıklar için:

* Düğüm listesi: (disk belleği) hello kümede hello liste düğümlerine döndürür.
  * API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)
  * PowerShell: Get-ServiceFabricNode
* Uygulama listesi: döndürür hello (disk belleği) hello kümedeki uygulamaların listesi.
  * API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)
  * PowerShell: Get-ServiceFabricApplication
* Hizmet listesi: (disk belleği) bir uygulamanın hizmet hello listesini döndürür.
  * API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)
  * PowerShell: Get-ServiceFabricService
* Bölüm listesi: (disk belleği) bir hizmet bölümlerinde hello listesi döndürür.
  * API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)
  * PowerShell: Get-ServiceFabricPartition
* Çoğaltma Listesi: (disk belleği) bir bölüm kopyalarını hello listesini döndürür.
  * API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)
  * PowerShell: Get-ServiceFabricReplica
* Uygulama listesi dağıtılan: bir düğümde dağıtılan uygulamalar hello listesini döndürür.
  * API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication
* Hizmet paketi listesi dağıtılan: dağıtılan bir uygulama, hizmet paketleri hello listesini döndürür.
  * API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication

> [!NOTE]
> Bazı hello sorguları, disk belleğine alınan sonuçları döndürür. Merhaba bu sorguların return türetilmiş bir listedir [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1). Merhaba sonuçları bir ileti uymuyorsa yalnızca bir sayfa döndürülür ve bir ContinuationToken, numaralandırma durduğu izler. Aynı sorgu ve hello devamlılık belirteci hello önceki sorgu tooget sonraki sonuçlarından geçirin toocall hello devam edin.
>
>

### <a name="examples"></a>Örnekler
Merhaba aşağıdaki kodu hello sağlıksız uygulamaları hello kümede alır:

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

Merhaba aşağıdaki cmdlet'i alır hello doku hello uygulama ayrıntılarını: / WordCount uygulamasını. Sistem durumu uyarı konumunda olduğuna dikkat edin.

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

Merhaba aşağıdaki cmdlet'i hello hata sistem durumu hizmetleriyle alır:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a>Küme ve uygulama yükseltme
Merhaba küme ve uygulama izlenen bir yükseltme sırasında Service Fabric sistem durumu tooensure her şeyi sağlıklı kalmasını denetler. Bir varlık olarak yapılandırılmış sistem durumu ilkeleri kullanılarak hesaplanan sağlıksız ise hello yükseltme yükseltme özgü ilkeler toodetermine hello bir sonraki eylem geçerlidir. Merhaba yükseltme (örneğin, hata koşullarını düzelttikten veya ilkelerini değiştirme) duraklatılmış tooallow kullanıcı etkileşimi olabilir veya bu otomatik olarak toohello önceki iyi sürümüne geri.

Sırasında bir *küme* yükseltme, hello Küme Yükseltme durumu alma. Merhaba yükseltme Durumu sağlıksız değerlendirmeleri, hangi noktası toowhat hello kümede sağlıksız olduğunu içerir. Toohealth sorunları Hello yükseltme geri alınması durumunda, hello yükseltme durumu hello son sağlıksız nedenleri hatırlıyor. Bu bilgileri yöneticilerin hello yükseltme geri alındı veya durduruldu sonra nelerin yanlış gittiğini araştırmanıza yardımcı olabilir.

Benzer şekilde, sırasında bir *uygulama* yükseltme, tüm sağlıksız değerlendirmeleri hello uygulama yükseltme durumunu da bulunur.

Merhaba aşağıdaki hello uygulama yükseltme durumu değiştirilmiş bir yapı için gösterir: / WordCount uygulamasını. Bir izleme çoğaltmalarını birinde bir hata bildirdi. Merhaba durumu denetimleri değil geri dikkate alır çünkü hello yükseltme alınıyor.

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

Merhaba hakkında daha fazla bilgiyi [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).

## <a name="use-health-evaluations-tootroubleshoot"></a>Sistem durumu değerlendirmesini tootroubleshoot kullanın
Merhaba küme ya da bir uygulama ile ilgili bir sorun olduğunda hello küme veya uygulama sistem durumu toopinpoint sorunun ne olduğunu arayın. Merhaba sağlıksız değerlendirmeleri hangi tetiklenen hello geçerli iyi olmayan sistem durumu hakkında ayrıntılar verilmektedir. Gerekiyorsa, sağlam olmayan alt varlıkları tooidentify hello kök nedeni ayrıntıya girebilirsiniz.

Örneğin, bir hata raporu çoğaltmalarını birinde olduğundan bir uygulama sağlıksız düşünün. Merhaba aşağıdaki Powershell cmdlet'ini hello sağlıksız değerlendirmeleri gösterir:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

Daha fazla bilgi hello çoğaltma tooget arayabilirsiniz:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> Merhaba sağlıksız değerlendirmeleri göster hello ilk neden hello varlık toocurrent sistem durumu değerlendirilir. Bu durum tetiklemek birden çok olay olabilir, ancak bunlar değil olması yansıtılır hello değerlendirmeleri. tooget hello sistem durumu varlıkları toofigure hello kümedeki tüm hello sağlıksız raporların aşağı ayrıntıya hakkında daha fazla bilgi.
>
>

## <a name="next-steps"></a>Sonraki adımlar
[Sistem durumu raporları tootroubleshoot kullanın](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Özel Service Fabric sistem durumu rapor ekleme](service-fabric-report-health.md)

[Nasıl tooreport ve onay sistem durumu hizmeti](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[İzleme ve Hizmetleri yerel olarak tanılama](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md)
