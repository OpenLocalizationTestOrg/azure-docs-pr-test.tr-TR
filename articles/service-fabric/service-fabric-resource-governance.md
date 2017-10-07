---
title: "Service Fabric kaynak İdaresi kapsayıcıları ve hizmetler için aaaAzure | Microsoft Docs"
description: "Azure Service Fabric toospecify kaynak sınırları içinde veya dışında kapsayıcıları çalışan hizmetleri sağlar."
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
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a>Kaynak İdaresi 

Birden çok hizmet üzerinde çalışan Merhaba, aynı düğüm veya kümenin bir hizmetin diğer hizmetlere starving daha fazla kaynak tüketebilir mümkündür. Bu sorunu başvurulan tooas hello gürültülü komşu sorunudur. Service Fabric hello Geliştirici toospecify ayırmaları ve hizmet tooguarantee kaynakları başına sınırları sağlar ve ayrıca kaynak kullanımını sınırlama. 

## <a name="resource-governance-metrics"></a>Kaynak İdaresi ölçümleri 

Kaynak İdaresi Service Fabric desteklenir [hizmet paketi](service-fabric-application-model.md). tooService paket atanan hello kaynakları daha fazla kod paketler arasında bölünebilir. Belirtilen hello kaynak sınırları ayrıca hello ayırma hello kaynakların anlamına gelir. Service Fabric destekler CPU ve bellek iki yerleşik kullanarak hizmet paketi belirtme [ölçümleri](service-fabric-cluster-resource-manager-metrics.md):

* CPU (ölçüm adı `ServiceFabric:/_CpuCores`): bir çekirdek hello ana makinede kullanılabilir mantıksal bir çekirdek olduğundan ve tüm çekirdek tüm düğümler arasında ağırlıklı aynı hello.
* Bellek (ölçüm adı `ServiceFabric:/_MemoryInMB`): bellek megabayt cinsinden ifade edilir ve hello makinede kullanılabilir toophysical bellek eşler.

Yeni hizmet paketleri kullanılabilir kaynakları aştı açılmasını Hello çalışma zamanı reddeder - yalnızca geçici ayırma garantileri sağlanır. Ancak, başka bir yürütülebilir dosya veya kapsayıcı hello düğümde yerleştirdiyseniz, hello özgün ayırma garantileri ihlal.

Bu iki ölçümleri hello [küme Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) toplam küme kapasite, hello yük hello kümedeki her düğümde izler ve hello küme kaynaklarında kaldı. Bu iki ölçümleri eşdeğer tooany diğer kullanıcı veya özel bir ölçü ve varolan tüm özellikler bunlarla kullanılabilir:
* Küme olabilir [dengeli](service-fabric-cluster-resource-manager-balancing.md) toothese iki ölçümleri (varsayılan davranış) göre.
* Küme olabilir [birleştirilmiş](service-fabric-cluster-resource-manager-defragmentation-metrics.md) toothese iki ölçümleri göre.
* Zaman [bir küme açıklayan](service-fabric-cluster-resource-manager-cluster-description.md), arabelleğe alınan kapasite iki bu ölçümleri ayarlanabilir.

[Dinamik yük raporlama](service-fabric-cluster-resource-manager-metrics.md) bu ölçümleri desteklenmiyor ve bu ölçümleri oluşturma zamanında tanımlanır için yükler.

## <a name="cluster-set-up-for-enabling-resource-governance"></a>Küme kümesi kaynak İdaresi etkinleştirmek için

Kapasite el ile Merhaba kümedeki her düğüm türü şu şekilde tanımlanması:

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
Kaynak İdaresi yalnızca kullanıcı Hizmetleri ve sistem hizmetleri üzerinde izin verilir. Kapasite, bazı çekirdek ve bellek belirtirken sol sistem hizmetleri için ayrılmamış gerekir. En iyi performans için aşağıdaki ayar hello ayrıca hello küme bildiriminde açık olmalıdır: 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>Kaynak İdaresi belirtme 

Kaynak İdaresi sınırları hello uygulama bildirimi (ServiceManifestImport bölümüne) hello aşağıdaki örnekte gösterildiği gibi belirtilir:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
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
  
Bu örnekte, hizmet paketi ServicePackageA nereye yerleştirileceğini hello düğümlerinde bir temel alır. Bu hizmet paketi iki kod paket (CodeA1 ve CodeA2) içerir ve her ikisi de hello belirtin `CpuShares` parametresi. CpuShares 512:256 Hello oranını hello çekirdek hello iki kod paketler arasında böler. Bu nedenle, bu örnekte, bir çekirdek iki üç CodeA1 alır ve çekirdek üçte CodeA2 alır (ve yazılım garantisi rezervasyonu hello aynı). CpuShares kod paketler için belirtilmediğinde Service Fabric hello çekirdek bunları arasında eşit olarak böler durumda.

Her iki kod paketi sınırlı too1024; bu nedenle bellek sınırları absolute MB bellek (ve aynı hello yumuşak garantisi rezervasyonu). Kod paketler (kapsayıcıları veya işlemler) Bu sınır ve toodo çalışırken daha fazla bellek böylece bir bellek yetersiz özel durum sonuçları mümkün tooallocate yok. Kaynak sınırı zorlaması toowork için bir hizmet paketi içindeki tüm kod paketleri belirtilen bellek sınırlarını olması gerekir.


## <a name="next-steps"></a>Sonraki adımlar
* toolearn daha hakkında Küme Kaynak Yöneticisi, bu okuma [makale](service-fabric-cluster-resource-manager-introduction.md).
* uygulama modeli, hizmet paketleri, kod paketleri ve çoğaltmaları toothem nasıl eşleme hakkında daha fazla toolearn okuma bu [makale](service-fabric-application-model.md).
