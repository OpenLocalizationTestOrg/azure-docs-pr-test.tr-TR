---
title: "bir tek başına Azure Service Fabric kümesi aaaCreate | Microsoft Docs"
description: "Bir Azure Service Fabric kümesi oluşturmayı herhangi bir makinede (fiziksel veya sanal) şirket içi olup olmadığını veya tüm bulut Windows Server'ı çalıştıran."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="d76ae-103">Windows Server çalıştıran tek başına kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d76ae-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="d76ae-104">Azure Service Fabric toocreate Service Fabric kümeleri tüm sanal makineler veya Windows Server çalıştıran bilgisayarlarda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d76ae-104">You can use Azure Service Fabric toocreate Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="d76ae-105">Yani, dağıtmak ve Service Fabric uygulamaları birbirine bağlı bir Windows Server bilgisayarlar kümesi içeren herhangi bir ortamda çalıştırılabilir, şirket içinde veya herhangi bir bulut sağlayıcısına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="d76ae-106">Service Fabric kümeleri kurulum paketi toocreate hello tek başına Windows Server paket adlı Service Fabric sağlar.</span><span class="sxs-lookup"><span data-stu-id="d76ae-106">Service Fabric provides a setup package toocreate Service Fabric clusters called hello standalone Windows Server package.</span></span>

<span data-ttu-id="d76ae-107">Bu makalede, tek başına Service Fabric kümesi oluşturma hello adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d76ae-107">This article walks you through hello steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d76ae-108">Bu tek başına Windows Server paketi ticari olarak kullanılabilir ve üretim dağıtımları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="d76ae-109">Bu paket, "Önizleme"aşamasında olan yeni Service Fabric özellikler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="d76ae-110">Çok aşağı kaydırarak"[Önizleme bu paketinde bulunan özellikler](#previewfeatures_anchor)."</span><span class="sxs-lookup"><span data-stu-id="d76ae-110">Scroll down too"[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="d76ae-111">hello Önizleme özellikleri bölümüne hello listesi.</span><span class="sxs-lookup"><span data-stu-id="d76ae-111">section for hello list of hello preview features.</span></span> <span data-ttu-id="d76ae-112">Yapabilecekleriniz [hello EULA bir kopyasını indirin](http://go.microsoft.com/fwlink/?LinkID=733084) şimdi.</span><span class="sxs-lookup"><span data-stu-id="d76ae-112">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="d76ae-113">Merhaba Windows Server için Service Fabric paketi için destek alma</span><span class="sxs-lookup"><span data-stu-id="d76ae-113">Get support for hello Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="d76ae-114">Merhaba topluluğa hello Service Fabric tek başına paketi hakkında Windows Server için hello sor [Azure Service Fabric Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="d76ae-114">Ask hello community about hello Service Fabric standalone package for Windows Server in hello [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="d76ae-115">İçin bilet [Service Fabric profesyonel desteği](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="d76ae-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="d76ae-116">Microsoft Profesyonel desteği hakkında daha fazla bilgi [burada](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="d76ae-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="d76ae-117">Ayrıca destek bu paket için bir parçası olarak alabilirsiniz [Microsoft Premier Destek](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="d76ae-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="d76ae-118">Daha fazla ayrıntı için lütfen bkz. [Azure Service Fabric destek seçenekleri](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="d76ae-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="d76ae-119">Merhaba çalıştırma desteği amacıyla toocollect günlükleri [Service Fabric tek başına günlük Toplayıcı](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="d76ae-119">toocollect logs for support purposes, run hello [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="d76ae-120">Merhaba Windows Server için Service Fabric paketi yükle</span><span class="sxs-lookup"><span data-stu-id="d76ae-120">Download hello Service Fabric for Windows Server package</span></span>
<span data-ttu-id="d76ae-121">toocreate hello küme, kullanım hello Windows Server için Service Fabric paketi (Windows Server 2012 R2 ve daha yeni) burada bulundu:</span><span class="sxs-lookup"><span data-stu-id="d76ae-121">toocreate hello cluster, use hello Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="d76ae-122">
[Bağlantı - Service Fabric tek başına paketi - Windows Server'ı karşıdan yükle](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="d76ae-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="d76ae-123">Merhaba paket içeriğine ayrıntılarını bulun [burada](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="d76ae-123">Find details on contents of hello package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="d76ae-124">Merhaba Service Fabric çalışma zamanı paketi küme oluşturma sırasında otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-124">hello Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="d76ae-125">Bir makineden dağıtma değil toohello bağlıysa Internet, lütfen bant dışı hello çalışma zamanı paketini buradan indirin:</span><span class="sxs-lookup"><span data-stu-id="d76ae-125">If deploying from a machine not connected toohello internet, please download hello runtime package out of band from here:</span></span> <br><span data-ttu-id="d76ae-126">
[Bağlantı - Service Fabric çalışma zamanı - Windows Server'ı karşıdan yükle](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="d76ae-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="d76ae-127">Tek başına küme yapılandırma örnekleri adresindeki bulun:</span><span class="sxs-lookup"><span data-stu-id="d76ae-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="d76ae-128">
[Tek başına küme yapılandırma örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="d76ae-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a><span data-ttu-id="d76ae-129">Merhaba kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d76ae-129">Create hello cluster</span></span>
<span data-ttu-id="d76ae-130">Service Fabric, dağıtılan tooa bir makine geliştirme küme hello kullanarak olabilir *ClusterConfig.Unsecure.DevCluster.json* dahil dosya [örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="d76ae-130">Service Fabric can be deployed tooa one-machine development cluster by using hello *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="d76ae-131">Merhaba tek başına paket tooyour makine, kopyalama hello örnek yapılandırma dosyasını toohello yerel makine, ardından çalışma hello paketini açma *CreateServiceFabricCluster.ps1* hello tek başına bir yönetici PowerShell oturumundan aracılığıyla Paket klasörü:</span><span class="sxs-lookup"><span data-stu-id="d76ae-131">Unpack hello standalone package tooyour machine, copy hello sample config file toohello local machine, then run hello *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from hello standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="d76ae-132">Adım 1A: Güvenli olmayan yerel geliştirme kümesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="d76ae-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="d76ae-133">Bkz: Merhaba ortam Kurulumu kısmına [planlama ve küme dağıtımınızı hazırlama](service-fabric-cluster-standalone-deployment-preparation.md) ayrıntıları sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="d76ae-133">See hello Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="d76ae-134">Çalışan geliştirme senaryolarını tamamladığınızda, hello Service Fabric kümesi hello makineden bölümünde toosteps bakarak kaldırabilirsiniz "[bir kümesini kaldırmak](#removecluster_anchor)".</span><span class="sxs-lookup"><span data-stu-id="d76ae-134">If you're finished running development scenarios, you can remove hello Service Fabric cluster from hello machine by referring toosteps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="d76ae-135">Adım 1B: çoklu makine bir küme oluşturun</span><span class="sxs-lookup"><span data-stu-id="d76ae-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="d76ae-136">Merhaba planlama aracılığıyla ilerlemiş sonra aşağıdaki bağlantıdaki, hello adresindeki hazırlık adımları ayrıntılı olursunuz toocreate küme yapılandırma dosyanızı kullanarak, üretim kümeniz hazır.</span><span class="sxs-lookup"><span data-stu-id="d76ae-136">After you have gone through hello planning and preparation steps detailed at hello below link, you are ready toocreate your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="d76ae-137">
[Planlama ve küme dağıtımınızı hazırlama](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="d76ae-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="d76ae-138">Merhaba çalıştırarak yazdığınız hello yapılandırma dosyasını doğrulamak *TestConfiguration.ps1* hello tek başına paket klasörüne betikten:</span><span class="sxs-lookup"><span data-stu-id="d76ae-138">Validate hello configuration file you have written by running hello *TestConfiguration.ps1* script from hello standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="d76ae-139">Bir çıktı görmeniz gerekir aşağıdaki gibi.</span><span class="sxs-lookup"><span data-stu-id="d76ae-139">You should see output like below.</span></span> <span data-ttu-id="d76ae-140">Merhaba altındaki alanda "Başarılı" "True" olarak döndürülürse, sağlamlık denetimleri geçtikten ve hello küme toobe dağıtılabilir hello giriş yapılandırmasına bağlı olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="d76ae-140">If hello bottom field "Passed" is returned as "True", sanity checks have passed and hello cluster looks toobe deployable based on hello input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. <span data-ttu-id="d76ae-141">Merhaba küme oluşturma: hello çalıştırmak *CreateServiceFabricCluster.ps1* betik toodeploy hello Service Fabric kümesi hello yapılandırmasındaki her makine arasında.</span><span class="sxs-lookup"><span data-stu-id="d76ae-141">Create hello cluster:  Run hello *CreateServiceFabricCluster.ps1* script toodeploy hello Service Fabric cluster across each machine in hello configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="d76ae-142">Dağıtım izlemeleri toohello VM/makine hello CreateServiceFabricCluster.ps1 PowerShell Betiği çalıştırdığınız yazılır.</span><span class="sxs-lookup"><span data-stu-id="d76ae-142">Deployment traces are written toohello VM/machine on which you ran hello CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="d76ae-143">Bunlar hangi hello komut dosyasını çalıştırmak hello dizininde dayalı hello alt DeploymentTraces, bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-143">These can be found in hello subfolder DeploymentTraces, based in hello directory from which hello script was run.</span></span> <span data-ttu-id="d76ae-144">Service Fabric olduysa toosee tooa makine doğru şekilde dağıtıldığını, yüklü hello dosyaları (göre varsayılan c:\ProgramData\SF) hello küme yapılandırma dosyasındaki FabricSettings bölümünde ayrıntılı olarak hello FabricDataRoot dizininde bulabilir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-144">toosee if Service Fabric was deployed correctly tooa machine, find hello installed files in hello FabricDataRoot directory, as detailed in hello cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="d76ae-145">De FabricHost.exe ve Fabric.exe işlemleri Görev Yöneticisi'nde çalışan görülebilir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="d76ae-146">Adım 1C: Çevrimdışı (internet kesilmiş) küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="d76ae-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="d76ae-147">Merhaba Service Fabric çalışma zamanı paketi küme oluşturma sırasında otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-147">hello Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="d76ae-148">Ne zaman bir küme toomachines dağıtma değil izin ver bağlı toohello Internet toodownload hello Service Fabric çalışma zamanı ayrı olarak paketini ve küme oluşturma sırasında hello yolu tooit sağlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-148">When deploying a cluster toomachines not connected toohello internet, you will need toodownload hello Service Fabric runtime package separately, and provide hello path tooit at cluster creation.</span></span>
<span data-ttu-id="d76ae-149">Merhaba çalışma zamanı paketi ayrı olarak yüklenebilen, başka bir makineden toohello bağlı Internet adresindeki [karşıdan yükleme bağlantısı - Service Fabric çalışma zamanı - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="d76ae-149">hello runtime package can be downloaded separately, from another machine connected toohello internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="d76ae-150">Merhaba çevrimdışı kümeden dağıtma ve çalıştırarak hello küme oluşturma hello çalışma zamanı paketi toowhere kopyalama `CreateServiceFabricCluster.ps1` hello ile `-FabricRuntimePackagePath` dahil, aşağıda gösterildiği gibi parametre:</span><span class="sxs-lookup"><span data-stu-id="d76ae-150">Copy hello runtime package toowhere you are deploying hello offline cluster from, and create hello cluster by running `CreateServiceFabricCluster.ps1` with hello `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="d76ae-151">Burada `.\ClusterConfig.json` ve `.\MicrosoftAzureServiceFabric.cab` hello yolları toohello küme yapılandırmasını ve hello çalışma zamanı .cab dosyası sırasıyla şunlardır.</span><span class="sxs-lookup"><span data-stu-id="d76ae-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are hello paths toohello cluster configuration and hello runtime .cab file respectively.</span></span>


### <a name="step-2-connect-toohello-cluster"></a><span data-ttu-id="d76ae-152">2. adım: toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="d76ae-152">Step 2: Connect toohello cluster</span></span>
<span data-ttu-id="d76ae-153">tooconnect tooa güvenli küme, bkz: [Service fabric bağlanmak toosecure küme](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d76ae-153">tooconnect tooa secure cluster, see [Service fabric connect toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="d76ae-154">tooconnect tooan güvenli olmayan küme, hello aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d76ae-154">tooconnect tooan unsecure cluster, run hello following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="d76ae-155">Örnek:</span><span class="sxs-lookup"><span data-stu-id="d76ae-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="d76ae-156">3. adım: Service Fabric Explorer Getir</span><span class="sxs-lookup"><span data-stu-id="d76ae-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="d76ae-157">Service Fabric Explorer ya da doğrudan hello makineler http://localhost:19080/Explorer/index.html veya uzaktan http://< biri ile toohello küme bağlanabilir artık*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.</span><span class="sxs-lookup"><span data-stu-id="d76ae-157">Now you can connect toohello cluster with Service Fabric Explorer either directly from one of hello machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="d76ae-158">Ekleme ve düğümlerini Kaldır</span><span class="sxs-lookup"><span data-stu-id="d76ae-158">Add and remove nodes</span></span>
<span data-ttu-id="d76ae-159">Ekleme veya düğümleri tooyour tek başına Service Fabric kümesi, iş gereksinimleriniz değiştikçe kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d76ae-159">You can add or remove nodes tooyour standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="d76ae-160">Bkz: [ekleme veya kaldırma düğümleri tooa Service Fabric tek başına küme](service-fabric-cluster-windows-server-add-remove-nodes.md) ayrıntılı adımlar için.</span><span class="sxs-lookup"><span data-stu-id="d76ae-160">See [Add or Remove nodes tooa Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="d76ae-161">Bir küme Kaldır</span><span class="sxs-lookup"><span data-stu-id="d76ae-161">Remove a cluster</span></span>
<span data-ttu-id="d76ae-162">Merhaba çalıştırmak tooremove bir küme *RemoveServiceFabricCluster.ps1* PowerShell Betiği hello paket klasörüne ve hello yol toohello JSON yapılandırma dosyası geçirin.</span><span class="sxs-lookup"><span data-stu-id="d76ae-162">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="d76ae-163">İsteğe bağlı olarak hello silme hello günlük için bir konum belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d76ae-163">You can optionally specify a location for hello log of hello deletion.</span></span>

<span data-ttu-id="d76ae-164">Bu komut dosyası düğümleriyle hello küme yapılandırma dosyasında listelenen yönetici erişimi tooall hello makinelerin bulunduğu herhangi bir makinede çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-164">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="d76ae-165">Bu komut dosyasını çalıştırmak hello makine toobe hello kümesinin parçası yok.</span><span class="sxs-lookup"><span data-stu-id="d76ae-165">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a><span data-ttu-id="d76ae-166">Toplanan telemetri verileri nasıl ve ne tooopt onu dışında</span><span class="sxs-lookup"><span data-stu-id="d76ae-166">Telemetry data collected and how tooopt out of it</span></span>
<span data-ttu-id="d76ae-167">Varsayılan olarak, hello ürün telemetri hello Service Fabric kullanım tooimprove hello üründe toplar.</span><span class="sxs-lookup"><span data-stu-id="d76ae-167">As a default, hello product collects telemetry on hello Service Fabric usage tooimprove hello product.</span></span> <span data-ttu-id="d76ae-168">Merhaba hello kurulumunun bir parçası için bağlantı çok denetler olarak çalıştırılan en iyi yöntem Çözümleyicisi[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="d76ae-168">hello Best Practice Analyzer that runs as a part of hello setup checks for connectivity too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="d76ae-169">Erişilebilir durumda değilse, telemetri dışında tercih sürece hello kurulum başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d76ae-169">If it is not reachable, hello setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="d76ae-170">Merhaba telemetri ardışık düzen çalıştığında veri çok aşağıdaki tooupload hello[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) günde bir kez.</span><span class="sxs-lookup"><span data-stu-id="d76ae-170">hello telemetry pipeline tries tooupload hello following data too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="d76ae-171">En yüksek çaba karşıya yükleme ve hello küme işlevselliğini üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="d76ae-171">It is a best-effort upload and has no impact on hello cluster functionality.</span></span> <span data-ttu-id="d76ae-172">Merhaba telemetri çalıştığı Yük Devretme Yöneticisi birincil hello hello düğümden yalnızca gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-172">hello telemetry is only sent from hello node that runs hello failover manager primary.</span></span> <span data-ttu-id="d76ae-173">Başka bir düğüm telemetri gönderir.</span><span class="sxs-lookup"><span data-stu-id="d76ae-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="d76ae-174">Merhaba telemetri hello şunlardan oluşur:</span><span class="sxs-lookup"><span data-stu-id="d76ae-174">hello telemetry consists of hello following:</span></span>

* <span data-ttu-id="d76ae-175">Hizmetlerin sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-175">Number of services</span></span>
* <span data-ttu-id="d76ae-176">ServiceTypes sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="d76ae-177">Uygulama sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-177">Number of Applications</span></span>
* <span data-ttu-id="d76ae-178">ApplicationUpgrades sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="d76ae-179">Sistemdeki yük devretme birimi sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="d76ae-180">Inbuildfailoverunits sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="d76ae-181">UnhealthyFailoverUnits sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="d76ae-182">Çoğaltmaların sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-182">Number of Replicas</span></span>
* <span data-ttu-id="d76ae-183">InBuildReplicas sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="d76ae-184">StandByReplicas sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="d76ae-185">OfflineReplicas sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="d76ae-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="d76ae-186">CommonQueueLength</span></span>
* <span data-ttu-id="d76ae-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="d76ae-187">QueryQueueLength</span></span>
* <span data-ttu-id="d76ae-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="d76ae-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="d76ae-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="d76ae-189">CommitQueueLength</span></span>
* <span data-ttu-id="d76ae-190">Düğüm sayısı</span><span class="sxs-lookup"><span data-stu-id="d76ae-190">Number of Nodes</span></span>
* <span data-ttu-id="d76ae-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="d76ae-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="d76ae-192">ClusterId: Her küme için rastgele oluşturulmuş bir GUID budur</span><span class="sxs-lookup"><span data-stu-id="d76ae-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="d76ae-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="d76ae-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="d76ae-194">Merhaba sanal makine ya da hangi hello telemetri karşıya Makine IP adresi</span><span class="sxs-lookup"><span data-stu-id="d76ae-194">IP address of hello virtual machine or machine from which hello telemetry is uploaded</span></span>

<span data-ttu-id="d76ae-195">toodisable telemetri çok hello ekleyin*özellikleri* yapılandırmada, küme: *enableTelemetry: yanlış*.</span><span class="sxs-lookup"><span data-stu-id="d76ae-195">toodisable telemetry, add hello following too*properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="d76ae-196">Bu pakete dahil önizleme özellikleri</span><span class="sxs-lookup"><span data-stu-id="d76ae-196">Preview features included in this package</span></span>
<span data-ttu-id="d76ae-197">yok.</span><span class="sxs-lookup"><span data-stu-id="d76ae-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="d76ae-198">Merhaba ile yeni başlangıç [hello tek başına küme Windows Server için GA sürümü (sürüm 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), küme toofuture sürümler, el ile veya otomatik olarak yükseltme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d76ae-198">Starting with hello new [GA version of hello standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster toofuture releases, manually or automatically.</span></span> <span data-ttu-id="d76ae-199">Çok başvuran[bir tek başına Service Fabric kümesi sürümüne yükseltmenizi](service-fabric-cluster-upgrade-windows-server.md) Ayrıntılar için belge.</span><span class="sxs-lookup"><span data-stu-id="d76ae-199">Refer too[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d76ae-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d76ae-200">Next steps</span></span>
* [<span data-ttu-id="d76ae-201">Dağıtma ve PowerShell kullanarak uygulamaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="d76ae-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="d76ae-202">Tek başına Windows kümesi için yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="d76ae-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="d76ae-203">Ekleme veya düğümleri tooa tek başına Service Fabric kümesi kaldırma</span><span class="sxs-lookup"><span data-stu-id="d76ae-203">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="d76ae-204">Bir tek başına Service Fabric kümesi sürümüne yükseltme</span><span class="sxs-lookup"><span data-stu-id="d76ae-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="d76ae-205">Azure VM'ler Windows çalıştıran bir tek başına Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="d76ae-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="d76ae-206">Windows güvenliği kullanarak Windows'u bir tek başına kümede güvenli</span><span class="sxs-lookup"><span data-stu-id="d76ae-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="d76ae-207">Tek başına küme X509 kullanarak Windows güvenli sertifikaları</span><span class="sxs-lookup"><span data-stu-id="d76ae-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
