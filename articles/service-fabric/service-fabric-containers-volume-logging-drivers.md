---
title: "Service Fabric Docker oluşturan Önizleme aaaAzure | Microsoft Docs"
description: "Azure Service Fabric Docker Compose biçimi toomake kabul eder, Service Fabric kullanarak daha kolay tooorchestrate exsiting kapsayıcıları. Bu destek, şu anda önizlemede değil."
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
ms.openlocfilehash: 824044fd698f0ed94c4212722bc82187905315dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a>Birim eklenti ve günlük sürücüleri, kapsayıcı için belirtme

Service Fabric destekleyen belirtme [Docker birim eklentileri](https://docs.docker.com/engine/extend/plugins_volume/) ve [Docker günlük sürücüleri](https://docs.docker.com/engine/admin/logging/overview/) kapsayıcı hizmetiniz için. Merhaba eklentileri hello uygulama bildiriminde hello bildirimi aşağıdaki gösterildiği gibi belirtilir:


```xml
?xml version="1.0" encoding="UTF-8"?>
<ApplicationManifest ApplicationTypeName="WinNodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Description>Calculator Application</Description>
    <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
      <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
    </Parameters>
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeServicePackage" ServiceManifestVersion="1.0"/>
     <Policies>
       <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv"> 
        <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
        <RepositoryCredentials PasswordEncrypted="false" Password="****" AccountName="test"/>
        <LogConfig Driver="etwlogs" >
          <DriverOption Name="test" Value="vale"/>
        </LogConfig>
        <Volume Source="c:\workspace" Destination="c:\testmountlocation1" IsReadOnly="false"></Volume>
        <Volume Source="d:\myfolder" Destination="c:\testmountlocation2" IsReadOnly="true"> </Volume>
        <Volume Source="myexternalvolume" Destination="c:\testmountlocation3" Driver="sf" IsReadOnly="true"></Volume>
       </ContainerHostPolicies>
   </Policies>
    </ServiceManifestImport>
    <ServiceTemplates>
        <StatelessService ServiceTypeName="StatelessNodeService" InstanceCount="5">
            <SingletonPartition></SingletonPartition>
        </StatelessService>
    </ServiceTemplates>
</ApplicationManifest>
```

Örnek önceki hello hello `Source` hello için etiket `Volume` toohello kaynak klasöre başvuruyor. Merhaba kaynak klasörü hello Merhaba kapsayıcılara ya da kalıcı bir uzak depo barındıran VM bir klasörde olabilir. Merhaba `Destination` etiketi olan hello hello konumu `Source` eşlenen toowithin hello çalıştığı kapsayıcı. 

Bir birim eklentisi belirtirken, Service Fabric belirtilen hello parametreleri kullanarak hello birimi otomatik olarak oluşturur. Merhaba `Source` etiketi adıdır hello hello birim ve hello `Driver` etiketi hello birimin sürücü eklentisi belirtir. Seçenekler hello kullanılarak belirtilebilir `DriverOption` etiketi hello aşağıdaki kod parçacığında gösterildiği gibi:

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

Docker günlük sürücü belirtilmişse gerekli toodeploy aracıları (veya kapsayıcıları) toohandle hello hello kümede günlüklerini alır.  Merhaba `DriverOption` etiketi kullanılan toospecify günlük sürücü seçenekleri de olabilir.

Aşağıdaki makaleleri toodeploy kapsayıcıları tooa Service Fabric kümesi toohello bakın:


[Service Fabric bir kapsayıcıda dağıtma](service-fabric-deploy-container.md)

