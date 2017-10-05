---
title: "Tek başına Azure Service Fabric kümesi oluştur | Microsoft Docs"
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
ms.openlocfilehash: 6aa2905a97ec6b8c125f2ab9572a8e40bf525b27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="8dd85-103">Windows Server çalıştıran tek başına kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dd85-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="8dd85-104">Azure Service Fabric, tüm sanal makineler veya Windows Server çalıştıran bilgisayarlarda Service Fabric kümeleri oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8dd85-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="8dd85-105">Yani, dağıtmak ve Service Fabric uygulamaları birbirine bağlı bir Windows Server bilgisayarlar kümesi içeren herhangi bir ortamda çalıştırılabilir, şirket içinde veya herhangi bir bulut sağlayıcısına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="8dd85-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="8dd85-106">Service Fabric tek başına Windows Server paket adlı Service Fabric kümeleri oluşturmak için Kurulum paketini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8dd85-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span></span>

<span data-ttu-id="8dd85-107">Bu makalede, tek başına Service Fabric kümesi oluşturma adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8dd85-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8dd85-108">Bu tek başına Windows Server paketi ticari olarak kullanılabilir ve üretim dağıtımları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8dd85-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="8dd85-109">Bu paket, "Önizleme"aşamasında olan yeni Service Fabric özellikler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8dd85-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="8dd85-110">Ekranı aşağı kaydırarak "[Önizleme bu paketinde bulunan özellikler](#previewfeatures_anchor)."</span><span class="sxs-lookup"><span data-stu-id="8dd85-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="8dd85-111">Önizleme özellikleri bölümüne listesi.</span><span class="sxs-lookup"><span data-stu-id="8dd85-111">section for the list of the preview features.</span></span> <span data-ttu-id="8dd85-112">Yapabilecekleriniz [EULA'yı bir kopyasını indirin](http://go.microsoft.com/fwlink/?LinkID=733084) şimdi.</span><span class="sxs-lookup"><span data-stu-id="8dd85-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="8dd85-113">Windows Server için Service Fabric paketi için destek alma</span><span class="sxs-lookup"><span data-stu-id="8dd85-113">Get support for the Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="8dd85-114">Windows Server için Service Fabric tek başına paketi hakkında topluluğa sor [Azure Service Fabric Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="8dd85-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="8dd85-115">İçin bilet [Service Fabric profesyonel desteği](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="8dd85-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="8dd85-116">Microsoft Profesyonel desteği hakkında daha fazla bilgi [burada](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="8dd85-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="8dd85-117">Ayrıca destek bu paket için bir parçası olarak alabilirsiniz [Microsoft Premier Destek](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="8dd85-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="8dd85-118">Daha fazla ayrıntı için lütfen bkz. [Azure Service Fabric destek seçenekleri](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="8dd85-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="8dd85-119">Destek amacıyla günlükleri toplamak için çalıştırın [Service Fabric tek başına günlük Toplayıcı](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="8dd85-119">To collect logs for support purposes, run the [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="8dd85-120">Windows Server için Service Fabric paketi yükle</span><span class="sxs-lookup"><span data-stu-id="8dd85-120">Download the Service Fabric for Windows Server package</span></span>
<span data-ttu-id="8dd85-121">Küme oluşturmak için Windows Server için Service Fabric paketi kullanın (Windows Server 2012 R2 ve daha yeni) burada bulundu:</span><span class="sxs-lookup"><span data-stu-id="8dd85-121">To create the cluster, use the Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="8dd85-122">
[Bağlantı - Service Fabric tek başına paketi - Windows Server'ı karşıdan yükle](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="8dd85-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="8dd85-123">Paket içeriğine ayrıntılarını bulun [burada](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="8dd85-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="8dd85-124">Service Fabric çalışma zamanı paketi küme oluşturma sırasında otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8dd85-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="8dd85-125">Lütfen internet'e bağlı bir makineden dağıtma, bant dışı çalışma zamanı paketini buradan indirin:</span><span class="sxs-lookup"><span data-stu-id="8dd85-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span></span> <br><span data-ttu-id="8dd85-126">
[Bağlantı - Service Fabric çalışma zamanı - Windows Server'ı karşıdan yükle](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="8dd85-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="8dd85-127">Tek başına küme yapılandırma örnekleri adresindeki bulun:</span><span class="sxs-lookup"><span data-stu-id="8dd85-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="8dd85-128">
[Tek başına küme yapılandırma örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="8dd85-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-the-cluster"></a><span data-ttu-id="8dd85-129">Kümeyi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dd85-129">Create the cluster</span></span>
<span data-ttu-id="8dd85-130">Service Fabric dağıtılabilir bir makine geliştirme kümeye kullanarak *ClusterConfig.Unsecure.DevCluster.json* dahil dosya [örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="8dd85-130">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="8dd85-131">Makinenize tek başına paketini açın, yerel makineye örnek yapılandırma dosyasını kopyalayın ve ardından Çalıştır *CreateServiceFabricCluster.ps1* tek başına paket klasörüne bir yönetici PowerShell oturumu aracılığıyla betikten :</span><span class="sxs-lookup"><span data-stu-id="8dd85-131">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="8dd85-132">Adım 1A: Güvenli olmayan yerel geliştirme kümesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="8dd85-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="8dd85-133">Ortam Kurulumu kısmına bakın [planlama ve küme dağıtımınızı hazırlama](service-fabric-cluster-standalone-deployment-preparation.md) ayrıntıları sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="8dd85-133">See the Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="8dd85-134">Çalışan geliştirme senaryolarını tamamlandı verirseniz, Service Fabric kümesi makineden bölümünde açıklanan adımları izleyerek başvurarak kaldırabilirsiniz "[bir kümesini kaldırmak](#removecluster_anchor)".</span><span class="sxs-lookup"><span data-stu-id="8dd85-134">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="8dd85-135">Adım 1B: çoklu makine bir küme oluşturun</span><span class="sxs-lookup"><span data-stu-id="8dd85-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="8dd85-136">Planlama aracılığıyla ilerlemiş ve hazırlık adımları ayrıntılı adresindeki sonra aşağıdaki bağlantıda, küme yapılandırma dosyanızı kullanarak, üretim kümesi oluşturmak için hazır.</span><span class="sxs-lookup"><span data-stu-id="8dd85-136">After you have gone through the planning and preparation steps detailed at the below link, you are ready to create your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="8dd85-137">
[Planlama ve küme dağıtımınızı hazırlama](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="8dd85-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="8dd85-138">Yapılandırma dosyasını çalıştırarak yazdığınız doğrulamak *TestConfiguration.ps1* tek başına paket klasörüne betikten:</span><span class="sxs-lookup"><span data-stu-id="8dd85-138">Validate the configuration file you have written by running the *TestConfiguration.ps1* script from the standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="8dd85-139">Bir çıktı görmeniz gerekir aşağıdaki gibi.</span><span class="sxs-lookup"><span data-stu-id="8dd85-139">You should see output like below.</span></span> <span data-ttu-id="8dd85-140">Alt alanın "Geçirilen" döndürülür "True" olarak, sağlamlık denetimleri geçtikten ve küme görünüyorsa dağıtılabilir için giriş yapılandırmasına bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="8dd85-140">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
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

2. <span data-ttu-id="8dd85-141">Küme oluşturma: çalıştırmak *CreateServiceFabricCluster.ps1* Service Fabric kümesi yapılandırmasındaki her makine üzerinden dağıtmak için komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="8dd85-141">Create the cluster:  Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="8dd85-142">VM/CreateServiceFabricCluster.ps1 PowerShell Betiği çalıştırıldığı makineye dağıtım izlemeleri yazılır.</span><span class="sxs-lookup"><span data-stu-id="8dd85-142">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="8dd85-143">Bunlar, komut dosyası çalıştırıldığı dizinde göre alt DeploymentTraces, bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="8dd85-143">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span></span> <span data-ttu-id="8dd85-144">Service Fabric bir makineye doğru şekilde dağıtıldı olmadığını görmek için FabricDataRoot dizininde (göre varsayılan c:\ProgramData\SF) küme yapılandırma dosyasındaki FabricSettings bölümünde ayrıntılı olarak yüklenen dosyalar bulun.</span><span class="sxs-lookup"><span data-stu-id="8dd85-144">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="8dd85-145">De FabricHost.exe ve Fabric.exe işlemleri Görev Yöneticisi'nde çalışan görülebilir.</span><span class="sxs-lookup"><span data-stu-id="8dd85-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="8dd85-146">Adım 1C: Çevrimdışı (internet kesilmiş) küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dd85-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="8dd85-147">Service Fabric çalışma zamanı paketi küme oluşturma sırasında otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8dd85-147">The Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="8dd85-148">İnternet'e bağlı olmayan makinelere bir küme dağıtımı sırasında Service Fabric çalışma zamanı paketi ayrı olarak indirebilir ve küme oluşturma sırasında bunu yolunu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dd85-148">When deploying a cluster to machines not connected to the internet, you will need to download the Service Fabric runtime package separately, and provide the path to it at cluster creation.</span></span>
<span data-ttu-id="8dd85-149">Çalışma zamanı paketi, internet'e bağlı başka bir makineden ayrı ayrı, indirilebilir [karşıdan yükleme bağlantısı - Service Fabric çalışma zamanı - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="8dd85-149">The runtime package can be downloaded separately, from another machine connected to the internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="8dd85-150">Burada, çevrimdışı kümeden dağıtıyorsanız ve çalıştırarak küme oluşturma çalışma zamanı paketi kopyalamak `CreateServiceFabricCluster.ps1` ile `-FabricRuntimePackagePath` dahil, aşağıda gösterildiği gibi parametre:</span><span class="sxs-lookup"><span data-stu-id="8dd85-150">Copy the runtime package to where you are deploying the offline cluster from, and create the cluster by running `CreateServiceFabricCluster.ps1` with the `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="8dd85-151">Burada `.\ClusterConfig.json` ve `.\MicrosoftAzureServiceFabric.cab` küme yapılandırmasını ve çalışma zamanı .cab dosyası için sırasıyla yollardır.</span><span class="sxs-lookup"><span data-stu-id="8dd85-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are the paths to the cluster configuration and the runtime .cab file respectively.</span></span>


### <a name="step-2-connect-to-the-cluster"></a><span data-ttu-id="8dd85-152">2. adım: kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="8dd85-152">Step 2: Connect to the cluster</span></span>
<span data-ttu-id="8dd85-153">Güvenli bir kümeye bağlanmak için bkz: [Service fabric güvenli kümeye bağlanma](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="8dd85-153">To connect to a secure cluster, see [Service fabric connect to secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="8dd85-154">Güvenli olmayan bir kümeye bağlanmak için aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8dd85-154">To connect to an unsecure cluster, run the following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="8dd85-155">Örnek:</span><span class="sxs-lookup"><span data-stu-id="8dd85-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="8dd85-156">3. adım: Service Fabric Explorer Getir</span><span class="sxs-lookup"><span data-stu-id="8dd85-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="8dd85-157">Service Fabric Explorer ya da doğrudan http://localhost:19080/Explorer/index.html veya uzaktan http://< makinelerden biri ile kümeye bağlanabilir artık*IPAddressofaMachine*>: 19080/Explorer / index.HTML.</span><span class="sxs-lookup"><span data-stu-id="8dd85-157">Now you can connect to the cluster with Service Fabric Explorer either directly from one of the machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="8dd85-158">Ekleme ve düğümlerini Kaldır</span><span class="sxs-lookup"><span data-stu-id="8dd85-158">Add and remove nodes</span></span>
<span data-ttu-id="8dd85-159">Ekleyebilir veya iş gereksinimleriniz değiştikçe, tek başına Service Fabric kümesi düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8dd85-159">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="8dd85-160">Bkz: [ekleme veya kaldırma Service Fabric tek başına küme düğümlerine](service-fabric-cluster-windows-server-add-remove-nodes.md) ayrıntılı adımlar için.</span><span class="sxs-lookup"><span data-stu-id="8dd85-160">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="8dd85-161">Bir küme Kaldır</span><span class="sxs-lookup"><span data-stu-id="8dd85-161">Remove a cluster</span></span>
<span data-ttu-id="8dd85-162">Bir kümeyi kaldırmak için paket klasöründen *RemoveServiceFabricCluster.ps1* PowerShell betiğini çalıştırın ve yolu JSON yapılandırma dosyasına geçirin.</span><span class="sxs-lookup"><span data-stu-id="8dd85-162">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="8dd85-163">İsteğe bağlı olarak silme işleminin günlüğü için bir konum belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8dd85-163">You can optionally specify a location for the log of the deletion.</span></span>

<span data-ttu-id="8dd85-164">Bu komut dosyası, küme yapılandırma dosyasındaki düğümler olarak listelenen tüm makineler yönetici erişimi olan herhangi bir makinede çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8dd85-164">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="8dd85-165">Bu komut dosyasını çalıştırmak makine kümesinin parçası olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8dd85-165">The machine that this script is run on does not have to be part of the cluster.</span></span>

```
# Removes Service Fabric from each machine in the configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from the current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-to-opt-out-of-it"></a><span data-ttu-id="8dd85-166">Toplanan telemetri verileri ve onu dışında kabul etme</span><span class="sxs-lookup"><span data-stu-id="8dd85-166">Telemetry data collected and how to opt out of it</span></span>
<span data-ttu-id="8dd85-167">Varsayılan olarak, ürün telemetri ürünü geliştirmek için Service Fabric kullanımı hakkında bilgi toplar.</span><span class="sxs-lookup"><span data-stu-id="8dd85-167">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span></span> <span data-ttu-id="8dd85-168">Bağlantı kurulumunun bir parçası çalıştıran en iyi yöntem Çözümleyicisi kontrol [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="8dd85-168">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="8dd85-169">Erişilebilir durumda değilse, telemetri dışında tercih sürece kurulum başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="8dd85-169">If it is not reachable, the setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="8dd85-170">Aşağıdaki veriler karşıya yüklemek telemetri ardışık düzen çalışır [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) günde bir kez.</span><span class="sxs-lookup"><span data-stu-id="8dd85-170">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="8dd85-171">En yüksek çaba karşıya yükleme ve küme işlevselliğini üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="8dd85-171">It is a best-effort upload and has no impact on the cluster functionality.</span></span> <span data-ttu-id="8dd85-172">Telemetriyi yalnızca yük devretme çalışan düğümü gönderilen birincil Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="8dd85-172">The telemetry is only sent from the node that runs the failover manager primary.</span></span> <span data-ttu-id="8dd85-173">Başka bir düğüm telemetri gönderir.</span><span class="sxs-lookup"><span data-stu-id="8dd85-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="8dd85-174">Telemetri aşağıdakilerden oluşur:</span><span class="sxs-lookup"><span data-stu-id="8dd85-174">The telemetry consists of the following:</span></span>

* <span data-ttu-id="8dd85-175">Hizmetlerin sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-175">Number of services</span></span>
* <span data-ttu-id="8dd85-176">ServiceTypes sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="8dd85-177">Uygulama sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-177">Number of Applications</span></span>
* <span data-ttu-id="8dd85-178">ApplicationUpgrades sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="8dd85-179">Sistemdeki yük devretme birimi sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="8dd85-180">Inbuildfailoverunits sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="8dd85-181">UnhealthyFailoverUnits sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="8dd85-182">Çoğaltmaların sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-182">Number of Replicas</span></span>
* <span data-ttu-id="8dd85-183">InBuildReplicas sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="8dd85-184">StandByReplicas sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="8dd85-185">OfflineReplicas sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="8dd85-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="8dd85-186">CommonQueueLength</span></span>
* <span data-ttu-id="8dd85-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="8dd85-187">QueryQueueLength</span></span>
* <span data-ttu-id="8dd85-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="8dd85-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="8dd85-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="8dd85-189">CommitQueueLength</span></span>
* <span data-ttu-id="8dd85-190">Düğüm sayısı</span><span class="sxs-lookup"><span data-stu-id="8dd85-190">Number of Nodes</span></span>
* <span data-ttu-id="8dd85-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="8dd85-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="8dd85-192">ClusterId: Her küme için rastgele oluşturulmuş bir GUID budur</span><span class="sxs-lookup"><span data-stu-id="8dd85-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="8dd85-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="8dd85-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="8dd85-194">Sanal makine ya da telemetri karşıya Makine IP adresi</span><span class="sxs-lookup"><span data-stu-id="8dd85-194">IP address of the virtual machine or machine from which the telemetry is uploaded</span></span>

<span data-ttu-id="8dd85-195">Telemetri devre dışı bırakmak için aşağıdakileri ekleyin *özellikleri* yapılandırmada, küme: *enableTelemetry: yanlış*.</span><span class="sxs-lookup"><span data-stu-id="8dd85-195">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="8dd85-196">Bu pakete dahil önizleme özellikleri</span><span class="sxs-lookup"><span data-stu-id="8dd85-196">Preview features included in this package</span></span>
<span data-ttu-id="8dd85-197">yok.</span><span class="sxs-lookup"><span data-stu-id="8dd85-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="8dd85-198">Yeni başlangıç [Windows Server için tek başına küme GA sürümü (sürüm 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), kümenizi el ile veya otomatik olarak gelecek sürümlerde için yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8dd85-198">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span></span> <span data-ttu-id="8dd85-199">Başvurmak [bir tek başına Service Fabric kümesi sürümüne yükseltmenizi](service-fabric-cluster-upgrade-windows-server.md) Ayrıntılar için belge.</span><span class="sxs-lookup"><span data-stu-id="8dd85-199">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8dd85-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8dd85-200">Next steps</span></span>
* [<span data-ttu-id="8dd85-201">Dağıtma ve PowerShell kullanarak uygulamaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="8dd85-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="8dd85-202">Tek başına Windows kümesi için yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="8dd85-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="8dd85-203">Bir tek başına Service Fabric kümesi düğümlerine Ekle Kaldır</span><span class="sxs-lookup"><span data-stu-id="8dd85-203">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="8dd85-204">Bir tek başına Service Fabric kümesi sürümüne yükseltme</span><span class="sxs-lookup"><span data-stu-id="8dd85-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="8dd85-205">Azure VM'ler Windows çalıştıran bir tek başına Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="8dd85-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="8dd85-206">Windows güvenliği kullanarak Windows'u bir tek başına kümede güvenli</span><span class="sxs-lookup"><span data-stu-id="8dd85-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="8dd85-207">Tek başına küme X509 kullanarak Windows güvenli sertifikaları</span><span class="sxs-lookup"><span data-stu-id="8dd85-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
