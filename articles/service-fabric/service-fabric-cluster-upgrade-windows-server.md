---
title: "tek başına Azure Service Fabric kümesi Windows Server'da aaaUpgrade | Microsoft Docs"
description: "Hello Azure Service Fabric kod ve/veya hello küme güncelleştirme modu ayarı dahil olmak üzere bir tek başına Service Fabric kümesi çalıştıran yapılandırma yükseltin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="a2b50-103">Windows Server kümesi, tek başına Azure Service Fabric yükseltme</span><span class="sxs-lookup"><span data-stu-id="a2b50-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2b50-104">Azure küme</span><span class="sxs-lookup"><span data-stu-id="a2b50-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="a2b50-105">Tek başına küme</span><span class="sxs-lookup"><span data-stu-id="a2b50-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="a2b50-106">Tüm modern, hello özelliği tooupgrade anahtar toohello uzun vadeli başarı ürününüzün sistemidir.</span><span class="sxs-lookup"><span data-stu-id="a2b50-106">For any modern system, hello ability tooupgrade is a key toohello long-term success of your product.</span></span> <span data-ttu-id="a2b50-107">Azure Service Fabric kümesi sahip olduğunuz bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="a2b50-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="a2b50-108">Bu makalede, bu hello küme Service Fabric kod ve yapılandırmaları desteklenen sürümleri her zaman çalışır nasıl emin olabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="a2b50-108">This article describes how you can make sure that hello cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="a2b50-109">Kümenizde çalışan denetim hello Service Fabric sürüm</span><span class="sxs-lookup"><span data-stu-id="a2b50-109">Control hello Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="a2b50-110">Küme toodownload güncelleştirmeleri tooset hizmet Microsoft kümesi hello yeni bir sürümü yayımlandığında dokusu **fabricClusterAutoupgradeEnabled** yapılandırma tootrue küme.</span><span class="sxs-lookup"><span data-stu-id="a2b50-110">tooset your cluster toodownload updates of Service Fabric when Microsoft releases a new version, set hello **fabricClusterAutoupgradeEnabled** cluster configuration tootrue.</span></span> <span data-ttu-id="a2b50-111">tooselect, küme toobe üzerinde kümesi hello istediğiniz desteklenen bir sürümünü Service Fabric **fabricClusterAutoupgradeEnabled** yapılandırma toofalse küme.</span><span class="sxs-lookup"><span data-stu-id="a2b50-111">tooselect a supported version of Service Fabric that you want your cluster toobe on, set hello **fabricClusterAutoupgradeEnabled** cluster configuration toofalse.</span></span>

> [!NOTE]
> <span data-ttu-id="a2b50-112">Kümenizi desteklenen bir Service Fabric sürümü her zaman çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2b50-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="a2b50-113">Service Fabric yeni bir sürümünü hello sürüm Microsoft sunar, hello önceki sürümü en az 60 gün hello duyuru başlangıç tarihinden sonra destek sona ermesi için işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="a2b50-113">When Microsoft announces hello release of a new version of Service Fabric, hello previous version is marked for end of support after a minimum of 60 days from hello date of hello announcement.</span></span> <span data-ttu-id="a2b50-114">Yeni sürümler duyurdu [hello Service Fabric ekip blogunda](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="a2b50-114">New releases are announced [on hello Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="a2b50-115">Merhaba yeni kullanılabilir toochoose bu noktada sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="a2b50-115">hello new release is available toochoose at that point.</span></span>
>
>

<span data-ttu-id="a2b50-116">Her Service Fabric düğümü ayrı fiziksel veya sanal makine üzerinde nerede ayrılmış bir üretim stili düğüm yapılandırması yalnızca kullanıyorsanız, küme toohello yeni sürüm yükseltme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2b50-116">You can upgrade your cluster toohello new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="a2b50-117">Birden fazla Service Fabric düğümü tek bir fiziksel veya sanal makine üzerinde olduğu bir geliştirme kümeniz varsa hello yeni sürümü hello kümeye yeniden oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2b50-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create hello cluster with hello new version.</span></span>

<span data-ttu-id="a2b50-118">İki ayrı iş akışları, küme toohello en son sürümünü veya desteklenen bir Service Fabric sürüme yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2b50-118">Two distinct workflows can upgrade your cluster toohello latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="a2b50-119">Bir iş akışı bağlantı toodownload hello en son sürüme otomatik olarak sahip kümeler için kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="a2b50-119">One workflow is for clusters that have connectivity toodownload hello latest version automatically.</span></span> <span data-ttu-id="a2b50-120">Merhaba diğer bağlantı toodownload hello son Service Fabric sürümü olmayan kümeler için iş akışıdır.</span><span class="sxs-lookup"><span data-stu-id="a2b50-120">hello other workflow is for clusters that do not have connectivity toodownload hello latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="a2b50-121">Bağlantı toodownload hello en son kod ve yapılandırma kümeleri yükseltme</span><span class="sxs-lookup"><span data-stu-id="a2b50-121">Upgrade clusters that have connectivity toodownload hello latest code and configuration</span></span>
<span data-ttu-id="a2b50-122">Küme düğümlerinizi çok Internet bağlantınız varsa bu adımları tooupgrade küme desteklenen tooa sürümünüzü kullanın[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a2b50-122">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="a2b50-123">Çok bağlantınız kümeleri için[http://download.microsoft.com](http://download.microsoft.com), Microsoft düzenli olarak yeni Service Fabric sürümler için hello kullanılabilirliğini denetler.</span><span class="sxs-lookup"><span data-stu-id="a2b50-123">For clusters that have connectivity too[http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for hello availability of new Service Fabric versions.</span></span>

<span data-ttu-id="a2b50-124">Yeni bir Service Fabric sürümü kullanılabilir olduğunda, hello paket toohello küme yerel olarak yüklenir ve yükseltme için sağlanmış.</span><span class="sxs-lookup"><span data-stu-id="a2b50-124">When a new Service Fabric version is available, hello package is downloaded locally toohello cluster and provisioned for upgrade.</span></span> <span data-ttu-id="a2b50-125">Ayrıca, tooinform hello müşteri bu yeni sürümün hello sistem aşağıdaki benzer toohello olan bir açık küme sistem durumu uyarısı gösterir:</span><span class="sxs-lookup"><span data-stu-id="a2b50-125">Additionally, tooinform hello customer of this new version, hello system shows an explicit cluster health warning that's similar toohello following:</span></span>

<span data-ttu-id="a2b50-126">"hello geçerli küme sürümü [version #] desteği [Date] sonlandırır."</span><span class="sxs-lookup"><span data-stu-id="a2b50-126">“hello current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="a2b50-127">Merhaba küme hello en son sürümünü çalıştırdıktan sonra hello uyarı kaybolduktan.</span><span class="sxs-lookup"><span data-stu-id="a2b50-127">After hello cluster is running hello latest version, hello warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="a2b50-128">Küme yükseltme iş akışı</span><span class="sxs-lookup"><span data-stu-id="a2b50-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="a2b50-129">Merhaba küme sistem durumu uyarısı gördükten sonra aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="a2b50-129">After you see hello cluster health warning, do hello following:</span></span>

1. <span data-ttu-id="a2b50-130">Merhaba kümedeki düğümler olarak listelenen yönetici erişimi tooall hello makineleri herhangi makineden toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a2b50-130">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="a2b50-131">Bu komut dosyasını çalıştırmak hello makine toobe hello kümesinin parçası yok.</span><span class="sxs-lookup"><span data-stu-id="a2b50-131">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. <span data-ttu-id="a2b50-132">Merhaba yükseltmeden Service Fabric sürümlerinin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="a2b50-132">Get hello list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="a2b50-133">Bir çıkış benzer toothis almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a2b50-133">You should get an output similar toothis:</span></span>

    ![Doku sürümlerini alma][getfabversions]
3. <span data-ttu-id="a2b50-135">Küme yükseltme tooan kullanılabilir sürüm başlamayı [başlangıç ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd</span><span class="sxs-lookup"><span data-stu-id="a2b50-135">Start a cluster upgrade tooan available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="a2b50-136">toomonitor hello ilerleme hello yükseltme durumunu Service Fabric Explorer veya Windows PowerShell komutunu aşağıdaki çalışma hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2b50-136">toomonitor hello progress of hello upgrade, you can use Service Fabric Explorer or run hello following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="a2b50-137">Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır.</span><span class="sxs-lookup"><span data-stu-id="a2b50-137">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="a2b50-138">toospecify özel sistem durumu ilkeleri hello için **başlangıç ServiceFabricClusterUpgrade** komutu, belgelerine bakın [başlangıç ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2b50-138">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="a2b50-139">Hello geri alma sonuçlandı hello sorunları giderdikten sonra aynı adımları daha önce açıklandığı gibi aşağıdaki hello tarafından hello yükseltmeyi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a2b50-139">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="a2b50-140">Sahip kümeler yükseltme <U>hiç bağlantı</u> toodownload hello en son kod ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a2b50-140">Upgrade clusters that have <U>no connectivity</u> toodownload hello latest code and configuration</span></span>
<span data-ttu-id="a2b50-141">Küme düğümlerinizi Internet bağlantısı çok yoksa bu adımları tooupgrade küme desteklenen tooa sürümünüzü kullanmak[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a2b50-141">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes do not have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="a2b50-142">Bağlı toohello Internet olmayan bir küme çalıştırıyorsanız, yeni bir sürümü hakkında toomonitor hello Service Fabric ekip blogu toolearn sahip olur.</span><span class="sxs-lookup"><span data-stu-id="a2b50-142">If you are running a cluster that is not connected toohello Internet, you will have toomonitor hello Service Fabric team blog toolearn about a new release.</span></span> <span data-ttu-id="a2b50-143">Merhaba sistem küme sistem durumu uyarı tooalert gösterme, yeni bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="a2b50-143">hello system does not show a cluster health warning tooalert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="a2b50-144">Otomatik sağlama vs el ile sağlama</span><span class="sxs-lookup"><span data-stu-id="a2b50-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="a2b50-145">tooenable otomatik karşıdan yükleme ve kayıt hello en son kod sürümü için Service Fabric güncelleştirme hizmeti ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a2b50-145">tooenable automatic downloading and registration for hello latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="a2b50-146">Toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt hello içinde başvurmak [tek başına paket](service-fabric-cluster-standalone-package-contents.md) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="a2b50-146">Refer toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside hello [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="a2b50-147">El ile işlem için aşağıdaki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a2b50-147">For manual process, follow hello instructions below.</span></span>

<span data-ttu-id="a2b50-148">Özellik toofalse yapılandırma yükseltmeye başlamadan önce aşağıdaki, küme yapılandırma tooset hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a2b50-148">Modify your cluster configuration tooset hello following property toofalse before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="a2b50-149">Çok başvuran[başlangıç ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) kullanım ayrıntıları için.</span><span class="sxs-lookup"><span data-stu-id="a2b50-149">Refer too[Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="a2b50-150">Merhaba yapılandırma yükseltmeye başlamadan önce JSON emin tooupdate 'clusterConfigurationVersion' olun.</span><span class="sxs-lookup"><span data-stu-id="a2b50-150">Make sure tooupdate 'clusterConfigurationVersion' in your JSON before you start hello configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="a2b50-151">Küme yükseltme iş akışı</span><span class="sxs-lookup"><span data-stu-id="a2b50-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="a2b50-152">Get-ServiceFabricClusterUpgrade hello kümedeki hello düğümlerinden biri çalıştırın ve hello TargetCodeVersion dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a2b50-152">Run Get-ServiceFabricClusterUpgrade from one of hello nodes in hello cluster and note hello TargetCodeVersion.</span></span>
2. <span data-ttu-id="a2b50-153">Internet bağlantılı makine toolist çalışma hello aşağıdakini tüm hello geçerli sürümüyle uyumlu sürümlerini yükseltin ve hello ilişkili indirme bağlantıları paketinden karşılık gelen hello indirin.</span><span class="sxs-lookup"><span data-stu-id="a2b50-153">Run hello following from an internet connected machine toolist all upgrade compatible versions with hello current version and download hello corresponding package from hello associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="a2b50-154">Merhaba kümedeki düğümler olarak listelenen yönetici erişimi tooall hello makineleri herhangi makineden toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a2b50-154">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="a2b50-155">Bu komut dosyasını çalıştırmak hello makine toobe hello kümesinin parçası yok</span><span class="sxs-lookup"><span data-stu-id="a2b50-155">hello machine that this script is run on does not have toobe part of hello cluster</span></span>

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="a2b50-156">Merhaba indirilen paketi hello küme görüntü deposuna kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="a2b50-156">Copy hello downloaded package into hello cluster image store.</span></span>

5. <span data-ttu-id="a2b50-157">Kopyalanan hello paketi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a2b50-157">Register hello copied package.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="a2b50-158">Küme yükseltme tooan kullanılabilir sürüm başlatın.</span><span class="sxs-lookup"><span data-stu-id="a2b50-158">Start a cluster upgrade tooan available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="a2b50-159">Service Fabric Explorer üzerinde hello yükseltme hello ilerlemesini izleyebilirsiniz veya hello aşağıdaki PowerShell komutunu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2b50-159">You can monitor hello progress of hello upgrade on Service Fabric Explorer, or you can run hello following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="a2b50-160">Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır.</span><span class="sxs-lookup"><span data-stu-id="a2b50-160">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="a2b50-161">toospecify özel sistem durumu ilkeleri hello için **başlangıç ServiceFabricClusterUpgrade** komutu, hello belgelerine bakın [başlangıç ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2b50-161">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see hello documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="a2b50-162">Hello geri alma sonuçlandı hello sorunları giderdikten sonra aynı adımları daha önce açıklandığı gibi aşağıdaki hello tarafından hello yükseltmeyi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a2b50-162">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>


## <a name="upgrade-hello-cluster-configuration"></a><span data-ttu-id="a2b50-163">Yükseltme hello küme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="a2b50-163">Upgrade hello cluster configuration</span></span>
<span data-ttu-id="a2b50-164">Merhaba yapılandırma Yükseltmeyi başlatmadan önce hello tek başına paketinde hello powershell betiğini çalıştırarak, yeni küme yapılandırma json test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2b50-164">Before you initiate hello configuration upgrade, you can test your new cluster configuration json by running hello powershell script in hello standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
<span data-ttu-id="a2b50-165">or</span><span class="sxs-lookup"><span data-stu-id="a2b50-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

<span data-ttu-id="a2b50-166">Bazı yapılandırmalar olamaz, uç noktaları gibi küme adı, düğüm IP yükseltilmiş vb.. Merhaba yeni küme yapılandırma json hello eskisinin karşı test ve herhangi bir sorun varsa hello Powershell penceresinde hataları atar.</span><span class="sxs-lookup"><span data-stu-id="a2b50-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test hello new cluster configuration json against hello old one and throw errors in hello Powershell window if there is any issue.</span></span>

<span data-ttu-id="a2b50-167">tooupgrade hello küme yapılandırması yükseltmesi çalıştırmak **başlangıç ServiceFabricClusterConfigurationUpgrade**.</span><span class="sxs-lookup"><span data-stu-id="a2b50-167">tooupgrade hello cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="a2b50-168">Merhaba yapılandırma yükseltme yükseltme etki alanı tarafından işlenen yükseltme etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="a2b50-168">hello configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="a2b50-169">Küme sertifikası config yükseltme</span><span class="sxs-lookup"><span data-stu-id="a2b50-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="a2b50-170">Küme sertifikası küme düğümleri arasında kimlik doğrulaması için kullanılan, hata küme düğümleri arasında hello iletişimi engeller çünkü hello sertifika geçir şekilde ek dikkatli gerçekleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="a2b50-170">Cluster certificate is used for authentication between cluster nodes, so hello certificate roll over should be performed with extra caution because failure will block hello communication among cluster nodes.</span></span>  
<span data-ttu-id="a2b50-171">Teknik olarak, üç seçenekleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="a2b50-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="a2b50-172">Tek sertifika yükseltme: hello yükseltme yolu ' (birincil) -> sertifika B (birincil) sertifika, sertifika C (birincil) -> ->...'.</span><span class="sxs-lookup"><span data-stu-id="a2b50-172">Single certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="a2b50-173">Double sertifika yükseltme: hello yükseltme yolu ' (birincil) -> sertifika sertifika (birincil) ve B (ikincil) sertifika B (birincil) -> -> (birincil) sertifika B ve C (ikincil) sertifika C (birincil) -> ->...'.</span><span class="sxs-lookup"><span data-stu-id="a2b50-173">Double certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="a2b50-174">Sertifika türü yükseltme: sertifika parmak izi tabanlı yapılandırma <> – CommonName tabanlı sertifika yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="a2b50-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="a2b50-175">Örneğin, sertifika parmak izi (birincil) ve parmak izi B (ikincil) sertifika CommonName c -></span><span class="sxs-lookup"><span data-stu-id="a2b50-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a2b50-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a2b50-176">Next steps</span></span>
* <span data-ttu-id="a2b50-177">Bilgi nasıl toocustomize bazı [Service Fabric kümesi ayarlarını](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="a2b50-177">Learn how toocustomize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="a2b50-178">Nasıl çok öğrenin[kümenizi ölçeğini](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="a2b50-178">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="a2b50-179">Hakkında bilgi edinin [uygulama yükseltmelerini](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="a2b50-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
