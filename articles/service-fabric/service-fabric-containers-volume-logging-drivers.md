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
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="239a0-104">Birim eklenti ve günlük sürücüleri, kapsayıcı için belirtme</span><span class="sxs-lookup"><span data-stu-id="239a0-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="239a0-105">Service Fabric destekleyen belirtme [Docker birim eklentileri](https://docs.docker.com/engine/extend/plugins_volume/) ve [Docker günlük sürücüleri](https://docs.docker.com/engine/admin/logging/overview/) kapsayıcı hizmetiniz için.</span><span class="sxs-lookup"><span data-stu-id="239a0-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="239a0-106">Merhaba eklentileri hello uygulama bildiriminde hello bildirimi aşağıdaki gösterildiği gibi belirtilir:</span><span class="sxs-lookup"><span data-stu-id="239a0-106">hello plugins are specified in hello application manifest as shown in hello following manifest:</span></span>


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

<span data-ttu-id="239a0-107">Örnek önceki hello hello `Source` hello için etiket `Volume` toohello kaynak klasöre başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="239a0-107">In hello preceding example, hello `Source` tag for hello `Volume` refers toohello source folder.</span></span> <span data-ttu-id="239a0-108">Merhaba kaynak klasörü hello Merhaba kapsayıcılara ya da kalıcı bir uzak depo barındıran VM bir klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="239a0-108">hello source folder could be a folder in hello VM that hosts hello containers or a persistent remote store.</span></span> <span data-ttu-id="239a0-109">Merhaba `Destination` etiketi olan hello hello konumu `Source` eşlenen toowithin hello çalıştığı kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="239a0-109">hello `Destination` tag is hello location that hello `Source` is mapped toowithin hello running container.</span></span> 

<span data-ttu-id="239a0-110">Bir birim eklentisi belirtirken, Service Fabric belirtilen hello parametreleri kullanarak hello birimi otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="239a0-110">When specifying a volume plugin, Service Fabric automatically creates hello volume using hello parameters specified.</span></span> <span data-ttu-id="239a0-111">Merhaba `Source` etiketi adıdır hello hello birim ve hello `Driver` etiketi hello birimin sürücü eklentisi belirtir.</span><span class="sxs-lookup"><span data-stu-id="239a0-111">hello `Source` tag is hello name of hello volume, and hello `Driver` tag specifies hello volume driver plugin.</span></span> <span data-ttu-id="239a0-112">Seçenekler hello kullanılarak belirtilebilir `DriverOption` etiketi hello aşağıdaki kod parçacığında gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="239a0-112">Options can be specified using hello `DriverOption` tag as shown in hello following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="239a0-113">Docker günlük sürücü belirtilmişse gerekli toodeploy aracıları (veya kapsayıcıları) toohandle hello hello kümede günlüklerini alır.</span><span class="sxs-lookup"><span data-stu-id="239a0-113">If a Docker log driver is specified, it is necessary toodeploy agents (or containers) toohandle hello logs in hello cluster.</span></span>  <span data-ttu-id="239a0-114">Merhaba `DriverOption` etiketi kullanılan toospecify günlük sürücü seçenekleri de olabilir.</span><span class="sxs-lookup"><span data-stu-id="239a0-114">hello `DriverOption` tag can be used toospecify log driver options as well.</span></span>

<span data-ttu-id="239a0-115">Aşağıdaki makaleleri toodeploy kapsayıcıları tooa Service Fabric kümesi toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="239a0-115">Refer toohello following articles toodeploy containers tooa Service Fabric cluster:</span></span>


[<span data-ttu-id="239a0-116">Service Fabric bir kapsayıcıda dağıtma</span><span class="sxs-lookup"><span data-stu-id="239a0-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

