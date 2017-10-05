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
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="72609-104">Birim eklenti ve günlük sürücüleri, kapsayıcı için belirtme</span><span class="sxs-lookup"><span data-stu-id="72609-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="72609-105">Service Fabric destekleyen belirtme [Docker birim eklentileri](https://docs.docker.com/engine/extend/plugins_volume/) ve [Docker günlük sürücüleri](https://docs.docker.com/engine/admin/logging/overview/) kapsayıcı hizmetiniz için.</span><span class="sxs-lookup"><span data-stu-id="72609-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="72609-106">Eklenti uygulama bildiriminde aşağıdaki bildiriminde gösterildiği gibi belirtilir:</span><span class="sxs-lookup"><span data-stu-id="72609-106">The plugins are specified in the application manifest as shown in the following manifest:</span></span>


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

<span data-ttu-id="72609-107">Önceki örnekte `Source` etiketinde `Volume` kaynak klasörü gösterir.</span><span class="sxs-lookup"><span data-stu-id="72609-107">In the preceding example, the `Source` tag for the `Volume` refers to the source folder.</span></span> <span data-ttu-id="72609-108">Kaynak klasörü kapsayıcıları ya da kalıcı bir uzak depo barındıran VM bir klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="72609-108">The source folder could be a folder in the VM that hosts the containers or a persistent remote store.</span></span> <span data-ttu-id="72609-109">`Destination` Etiketi konumudur, `Source` çalışan kapsayıcıda eşlenir.</span><span class="sxs-lookup"><span data-stu-id="72609-109">The `Destination` tag is the location that the `Source` is mapped to within the running container.</span></span> 

<span data-ttu-id="72609-110">Bir birim eklentisi belirtirken, Service Fabric belirtilen parametreleri kullanarak birimi otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="72609-110">When specifying a volume plugin, Service Fabric automatically creates the volume using the parameters specified.</span></span> <span data-ttu-id="72609-111">`Source` Etiketi birim adıdır ve `Driver` etiketi birimin sürücü eklentisi belirtir.</span><span class="sxs-lookup"><span data-stu-id="72609-111">The `Source` tag is the name of the volume, and the `Driver` tag specifies the volume driver plugin.</span></span> <span data-ttu-id="72609-112">Seçenekleri kullanılarak belirtilebilir `DriverOption` etiketi aşağıdaki kod parçacığında gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="72609-112">Options can be specified using the `DriverOption` tag as shown in the following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="72609-113">Docker günlük sürücü belirtilirse, kümede günlükleri işlemek için aracıları (veya kapsayıcıları) dağıtmak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="72609-113">If a Docker log driver is specified, it is necessary to deploy agents (or containers) to handle the logs in the cluster.</span></span>  <span data-ttu-id="72609-114">`DriverOption` Etiketi de günlüğü sürücü seçeneklerini belirtmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="72609-114">The `DriverOption` tag can be used to specify log driver options as well.</span></span>

<span data-ttu-id="72609-115">Service Fabric kümesine kapsayıcıları dağıtmak için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="72609-115">Refer to the following articles to deploy containers to a Service Fabric cluster:</span></span>


[<span data-ttu-id="72609-116">Service Fabric bir kapsayıcıda dağıtma</span><span class="sxs-lookup"><span data-stu-id="72609-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

