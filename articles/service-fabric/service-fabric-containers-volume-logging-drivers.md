---
title: "Azure Service Fabric Docker Compose Önizleme | Microsoft Docs"
description: "Azure Service Fabric Service Fabric kullanarak exsiting kapsayıcıları düzenlemek kolay hale getirmek için Docker Compose'u biçimi kabul eder. Bu destek, şu anda önizlemede değil."
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
ms.openlocfilehash: b12ef95add6347621f7d4865fac46568f91a1e12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a>Birim eklenti ve günlük sürücüleri, kapsayıcı için belirtme

Service Fabric destekleyen belirtme [Docker birim eklentileri](https://docs.docker.com/engine/extend/plugins_volume/) ve [Docker günlük sürücüleri](https://docs.docker.com/engine/admin/logging/overview/) kapsayıcı hizmetiniz için. Eklenti uygulama bildiriminde aşağıdaki bildiriminde gösterildiği gibi belirtilir:


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

Önceki örnekte `Source` etiketinde `Volume` kaynak klasörü gösterir. Kaynak klasörü kapsayıcıları ya da kalıcı bir uzak depo barındıran VM bir klasörde olabilir. `Destination` Etiketi konumudur, `Source` çalışan kapsayıcıda eşlenir. 

Bir birim eklentisi belirtirken, Service Fabric belirtilen parametreleri kullanarak birimi otomatik olarak oluşturur. `Source` Etiketi birim adıdır ve `Driver` etiketi birimin sürücü eklentisi belirtir. Seçenekleri kullanılarak belirtilebilir `DriverOption` etiketi aşağıdaki kod parçacığında gösterildiği gibi:

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

Docker günlük sürücü belirtilirse, kümede günlükleri işlemek için aracıları (veya kapsayıcıları) dağıtmak gereklidir.  `DriverOption` Etiketi de günlüğü sürücü seçeneklerini belirtmek için kullanılabilir.

Service Fabric kümesine kapsayıcıları dağıtmak için aşağıdaki makalelere bakın:


[Service Fabric bir kapsayıcıda dağıtma](service-fabric-deploy-container.md)

