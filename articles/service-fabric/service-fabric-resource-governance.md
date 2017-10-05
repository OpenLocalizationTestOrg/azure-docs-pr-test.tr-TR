---
title: "Azure Service Fabric kaynak İdaresi kapsayıcıları ve hizmetler için | Microsoft Docs"
description: "Azure Service Fabric iç veya dış kapsayıcıları çalışan hizmetler için kaynak sınırları belirtmenize olanak tanır."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88d44953ad83f9e7401fd087a39842e4a3790124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="resource-governance"></a>Kaynak İdaresi 

Birden fazla hizmet aynı düğümü veya küme üzerinde çalışırken, bir hizmetin diğer hizmetlere starving daha fazla kaynak tüketebilir mümkündür. Bu sorunu gürültülü komşu sorun olarak adlandırılır. Service Fabric ayırmaları ve her kaynakları garanti ve ayrıca kaynak kullanımını sınırlamak için hizmet sınırları belirtmek Geliştirici sağlar. 

## <a name="resource-governance-metrics"></a>Kaynak İdaresi ölçümleri 

Kaynak İdaresi Service Fabric desteklenir [hizmet paketi](service-fabric-application-model.md). Hizmet Paketi için atanmış olan kaynakları daha fazla kod paketler arasında bölünebilir. Belirtilen kaynak sınırları ayrıca kaynakları ayırma anlamına gelir. Service Fabric destekler CPU ve bellek iki yerleşik kullanarak hizmet paketi belirtme [ölçümleri](service-fabric-cluster-resource-manager-metrics.md):

* CPU (ölçüm adı `ServiceFabric:/_CpuCores`): bir çekirdek ana makinede kullanılabilir mantıksal bir çekirdek olduğundan ve tüm çekirdek tüm düğümler arasında ağırlıklı aynı.
* Bellek (ölçüm adı `ServiceFabric:/_MemoryInMB`): bellek megabayt cinsinden ifade edilir ve makinede kullanılabilir fiziksel bellek eşler.

Yeni hizmet paketleri kullanılabilir kaynakları aştı açılmasını çalışma zamanı reddeder - yalnızca geçici ayırma garantileri sağlanır. Ancak, başka bir yürütülebilir dosya veya kapsayıcı düğümde yerleştirdiyseniz, özgün ayırma garantileri ihlal.

Bu iki ölçümler için [küme Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) toplam küme kapasite, kümedeki her düğümde yük izler ve küme kaynaklarında kaldı. Bu iki ölçümleri herhangi bir diğer kullanıcı veya özel bir ölçü eşdeğerdir ve varolan tüm özellikler bunlarla kullanılabilir:
* Küme olabilir [dengeli](service-fabric-cluster-resource-manager-balancing.md) göre bu iki ölçümleri (varsayılan davranıştır).
* Küme olabilir [birleştirilmiş](service-fabric-cluster-resource-manager-defragmentation-metrics.md) bu iki ölçümleri göre.
* Zaman [bir küme açıklayan](service-fabric-cluster-resource-manager-cluster-description.md), arabelleğe alınan kapasite iki bu ölçümleri ayarlanabilir.

[Dinamik yük raporlama](service-fabric-cluster-resource-manager-metrics.md) bu ölçümleri desteklenmiyor ve bu ölçümleri oluşturma zamanında tanımlanır için yükler.

## <a name="cluster-set-up-for-enabling-resource-governance"></a>Küme kümesi kaynak İdaresi etkinleştirmek için

Kapasite el ile kümedeki her düğüm türü şu şekilde tanımlanması:

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
Kaynak İdaresi yalnızca kullanıcı Hizmetleri ve sistem hizmetleri üzerinde izin verilir. Kapasite, bazı çekirdek ve bellek belirtirken sol sistem hizmetleri için ayrılmamış gerekir. En iyi performans için aşağıdaki ayar da küme bildiriminde açık olmalıdır: 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>Kaynak İdaresi belirtme 

Kaynak İdaresi sınırları uygulama bildirimi (ServiceManifestImport bölümüne) aşağıdaki örnekte gösterildiği gibi belirtilir:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has the number of CPU cores defined, but doesn't have the MemoryInMB defined.
  In this case, Service Fabric will sum the limits on code packages and uses the sum as 
  the overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
Bu örnekte, hizmet paketi ServicePackageA nereye yerleştirileceğini düğümlerinde bir temel alır. Bu hizmet paketi iki kod paket (CodeA1 ve CodeA2) içerir ve her ikisini de belirtin `CpuShares` parametresi. CpuShares 512:256 oranını çekirdek iki kod paket arasında böler. Bu nedenle, bu örnekte, bir çekirdek iki üç CodeA1 alır ve CodeA2 üçte bir çekirdek (ve aynı yazılım garantisi ayırma) alır. Ne zaman CpuShares kod paketler için belirtilmeyen durumunda, Service Fabric çekirdek bunları arasında eşit olarak böler.

Her iki kod paketi için 1024 MB bellek (ve aynı yazılım garantisi ayırma) sınırlı olacak şekilde bellek sınırları kesin. Kod paketleri (kapsayıcılar veya işlemler) bu sınırı aşan miktarda bellek ayıramazlar ve bunu denediklerinde yetersiz bellek özel durumu ortaya çıkar. Kaynak sınırı zorlamasının çalışması için, hizmet paketi içindeki tüm kod paketlerinin bellek sınırlarının belirtilmiş olması gerekir.


## <a name="next-steps"></a>Sonraki adımlar
* Küme Kaynak Yöneticisi hakkında daha fazla bilgi için bu okuma [makale](service-fabric-cluster-resource-manager-introduction.md).
* Uygulama modeli hakkında daha fazla bilgi için hizmet paketleri, kod paketleri ve nasıl çoğaltmaları için eşleştirebilirsiniz bu okuma [makale](service-fabric-application-model.md).
