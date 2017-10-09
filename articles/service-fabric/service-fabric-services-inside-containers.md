---
title: "aaaHow toocontainerize, Azure Service Fabric mikro (Önizleme)"
description: "Azure Service Fabric yeni işlevsellik toocontainerize Service Fabric mikro ekledi. Bu özellik şu anda önizleme sürümündedir."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="c96be-104">Nasıl toocontainerize Service Fabric güvenilir Services ve Reliable Actors (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="c96be-104">How toocontainerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="c96be-105">Service Fabric containerizing Service Fabric mikro (Reliable Services ve güvenilir dayalı aktör Hizmetleri) destekler.</span><span class="sxs-lookup"><span data-stu-id="c96be-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="c96be-106">Daha fazla bilgi için bkz: [service fabric kapsayıcıları](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c96be-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="c96be-107">Bu özellik Önizleme sürümünde olduğu ve bu makalede, bir kapsayıcı içinde çalışan hizmetinizi çeşitli adımları tooget hello sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c96be-107">This feature is in preview and this article provides hello various steps tooget your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="c96be-108">Bu özellik Önizleme aşamasındadır ve üretimde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c96be-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="c96be-109">Şu anda bu özellik yalnızca Windows için çalışır.</span><span class="sxs-lookup"><span data-stu-id="c96be-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-toocontainerize-your-service-fabric-application"></a><span data-ttu-id="c96be-110">Service Fabric uygulamanızı toocontainerize adımları</span><span class="sxs-lookup"><span data-stu-id="c96be-110">Steps toocontainerize your Service Fabric Application</span></span>

1. <span data-ttu-id="c96be-111">Service Fabric uygulamanızı Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="c96be-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="c96be-112">Sınıf ekleme [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour projesi.</span><span class="sxs-lookup"><span data-stu-id="c96be-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span></span> <span data-ttu-id="c96be-113">Merhaba bu sınıftaki bir yardımcı toocorrectly yük hello Service Fabric çalışma zamanı ikili dosyaları, uygulamanızın içinde bir kapsayıcı içinde çalışırken kodudur.</span><span class="sxs-lookup"><span data-stu-id="c96be-113">hello code in this class is a helper toocorrectly load hello Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="c96be-114">Her kod paketi için toocontainerize, başlatma hello yükleyicisi hello program Giriş noktasına ister.</span><span class="sxs-lookup"><span data-stu-id="c96be-114">For each code package you would like toocontainerize, initialize hello loader at hello program entry point.</span></span> <span data-ttu-id="c96be-115">Aşağıdaki kod parçacığını tooyour program giriş noktası dosyasına hello gösterilen hello statik oluşturucu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c96be-115">Add hello static constructor shown in hello following code snippet tooyour program entry point file.</span></span>

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="c96be-116">Derleme ve [paket](service-fabric-package-apps.md#Package-App) projenizi.</span><span class="sxs-lookup"><span data-stu-id="c96be-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="c96be-117">toobuild ve bir paket oluşturun, Çözüm Gezgini'nde hello uygulama projesine sağ tıklayın ve hello seçin **paket** komutu.</span><span class="sxs-lookup"><span data-stu-id="c96be-117">toobuild and create a package, right-click hello application project in Solution Explorer and choose hello **Package** command.</span></span>

5. <span data-ttu-id="c96be-118">Her kod paketi için ihtiyacınız toocontainerize, PowerShell Betiği çalıştırma hello [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="c96be-118">For every code package you need toocontainerize, run hello PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="c96be-119">Merhaba kullanım aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c96be-119">hello usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="c96be-120">Hello betik $dockerPackageOutputDirectoryPath adresindeki Docker yapıları içeren bir klasör oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c96be-120">hello script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="c96be-121">Oluşturulan hello Dockerfile tooexpose Kurulum betikleri gereksinimlerinize göre vb. çalıştıran herhangi bir bağlantı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c96be-121">Modify hello generated Dockerfile tooexpose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="c96be-122">Sonraki çok ihtiyacınız[yapı](service-fabric-get-started-containers.md#Build-Containers) ve [itme](service-fabric-get-started-containers.md#Push-Containers) , Docker kapsayıcısı paket tooyour deposu.</span><span class="sxs-lookup"><span data-stu-id="c96be-122">Next you need too[build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package tooyour repository.</span></span>

7. <span data-ttu-id="c96be-123">Merhaba ApplicationManifest.xml ve ServiceManifest.xml tooadd kapsayıcı görüntü, havuz bilgileri, kayıt defteri kimlik doğrulaması ve bağlantı noktası ana bilgisayar eşleme değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c96be-123">Modify hello ApplicationManifest.xml and ServiceManifest.xml tooadd your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="c96be-124">Merhaba bildirimleri değiştirmek için bkz: [Azure Service Fabric kapsayıcı uygulama oluşturma](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="c96be-124">For modifying hello manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="c96be-125">Merhaba kod paketi tanımında hello hizmet bildirimi gereksinimlerini toobe karşılık gelen kapsayıcı görüntü ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="c96be-125">hello code package definition in hello service manifest needs toobe replaced with corresponding container image.</span></span> <span data-ttu-id="c96be-126">Emin toochange hello EntryPoint tooa ContainerHost türü olun.</span><span class="sxs-lookup"><span data-stu-id="c96be-126">Make sure toochange hello EntryPoint tooa ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="c96be-127">Çoğaltıcı ve hizmet uç noktası başlangıç bağlantı noktası ana bilgisayar eşlemesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c96be-127">Add hello port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="c96be-128">Her iki, bu bağlantı noktalarına çalışma zamanında Service Fabric tarafından atanmış olduğundan, bağlantı noktası eşlemesi için atanmış toozero toouse hello hello ContainerPort ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="c96be-128">Since both these ports are assigned at runtime by Service Fabric, hello ContainerPort is set toozero toouse hello assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="c96be-129">tootest bu uygulama toodeploy gerekir, 5.7 veya daha yüksek sürümünü çalıştıran tooa küme.</span><span class="sxs-lookup"><span data-stu-id="c96be-129">tootest this application, you need toodeploy it tooa cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="c96be-130">Ayrıca, tooedit gerekir ve bu önizleme özelliği hello küme ayarları tooenable güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c96be-130">In addition, you need tooedit and update hello cluster settings tooenable this preview feature.</span></span> <span data-ttu-id="c96be-131">Bu başlangıç adımları [makale](service-fabric-cluster-fabric-settings.md) sonraki gösterilen tooadd hello ayarı.</span><span class="sxs-lookup"><span data-stu-id="c96be-131">Follow hello steps in this [article](service-fabric-cluster-fabric-settings.md) tooadd hello setting shown next.</span></span>
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. <span data-ttu-id="c96be-132">Sonraki [dağıtmak](service-fabric-deploy-remove-applications.md) hello uygulama paketi toothis küme düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="c96be-132">Next [deploy](service-fabric-deploy-remove-applications.md) hello edited application package toothis cluster.</span></span>

<span data-ttu-id="c96be-133">Şimdi, küme çalışmayı kapsayıcılı Service Fabric uygulaması olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c96be-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c96be-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c96be-134">Next steps</span></span>
* <span data-ttu-id="c96be-135">[Service Fabric’te kapsayıcı](service-fabric-get-started-containers.md) çalıştırma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="c96be-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="c96be-136">Service Fabric Hello hakkında bilgi edinin [uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="c96be-136">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
