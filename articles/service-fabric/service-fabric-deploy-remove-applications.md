---
title: "Azure Service Fabric uygulama dağıtımı | Microsoft Docs"
description: "Dağıtma ve Service Fabric PowerShell kullanarak uygulamalarda Kaldır."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: edef23a8cdab7fd0bef54456f0caabb9db273bf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="13071-103">Dağıtma ve PowerShell kullanarak uygulamaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="13071-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="13071-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13071-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="13071-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13071-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="13071-106">FabricClient API’leri</span><span class="sxs-lookup"><span data-stu-id="13071-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="13071-107">Bir kez bir [uygulama türü paketlenmiş][10], Azure Service Fabric kümesi içine dağıtımı için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="13071-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="13071-108">Dağıtım aşağıdaki üç adımdan oluşur:</span><span class="sxs-lookup"><span data-stu-id="13071-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="13071-109">Uygulama paketi görüntü deposuna karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="13071-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="13071-110">Uygulama türünü kaydetme</span><span class="sxs-lookup"><span data-stu-id="13071-110">Register the application type</span></span>
3. <span data-ttu-id="13071-111">Uygulama örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="13071-111">Create the application instance</span></span>

<span data-ttu-id="13071-112">Bir uygulamanın dağıtıldığını ve bir örnek kümede çalışan sonra uygulama örneği ve uygulama türünü silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13071-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="13071-113">Bir uygulamayı kümeden tamamen kaldırmak için aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="13071-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="13071-114">Çalışan Kaldır (veya Sil) uygulama örneği</span><span class="sxs-lookup"><span data-stu-id="13071-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="13071-115">Artık ihtiyacınız varsa uygulama türü kaydını kaldırma</span><span class="sxs-lookup"><span data-stu-id="13071-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="13071-116">Uygulama paketi görüntü deposundan kaldırır</span><span class="sxs-lookup"><span data-stu-id="13071-116">Remove the application package from the image store</span></span>

<span data-ttu-id="13071-117">Kullanırsanız [uygulamalarında hata ayıklama ve dağıtma için Visual Studio](service-fabric-publish-app-remote-cluster.md) yerel geliştirme kümenizde yukarıdaki adımların tümünü otomatik olarak bir PowerShell komut dosyası işlenir.</span><span class="sxs-lookup"><span data-stu-id="13071-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="13071-118">Bu komut dosyası içinde bulunur *betikleri* uygulama projesi klasörü.</span><span class="sxs-lookup"><span data-stu-id="13071-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="13071-119">Bu makalede, Visual Studio dışında aynı işlemleri gerçekleştirebilmeleri için komut dosyası yaptıklarını üzerinde arka plan sağlar.</span><span class="sxs-lookup"><span data-stu-id="13071-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="13071-120">Kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="13071-120">Connect to the cluster</span></span>
<span data-ttu-id="13071-121">Bu makaledeki tüm PowerShell komutları çalıştırmadan önce her zaman başlamayı [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Service Fabric kümeye bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="13071-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) to connect to the Service Fabric cluster.</span></span> <span data-ttu-id="13071-122">Yerel geliştirme kümeye bağlanmak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="13071-122">To connect to the local development cluster, run the following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="13071-123">Bir uzak küme veya Azure Active Directory, X509 kullanılarak güvenlik altına kümeye bağlanma örnekleri için sertifikalar veya Windows Active Directory bkz [güvenli kümeye Bağlan](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="13071-123">For examples of connecting to a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-the-application-package"></a><span data-ttu-id="13071-124">Uygulama paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="13071-124">Upload the application package</span></span>
<span data-ttu-id="13071-125">Uygulama paketini karşıya yükleme, iç Service Fabric bileşenleri tarafından erişilebilen bir konuma koyan.</span><span class="sxs-lookup"><span data-stu-id="13071-125">Uploading the application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="13071-126">Uygulama paketi yerel olarak doğrulamak istiyorsanız, kullanmak [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="13071-126">If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="13071-127">[Kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) komutu, küme görüntü deposu için uygulama paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="13071-127">The [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads the application package to the cluster image store.</span></span>
<span data-ttu-id="13071-128">**Get-ImageStoreConnectionStringFromClusterManifest** Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet, görüntü deposu bağlantı dizesini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="13071-128">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="13071-129">SDK modülü içeri aktarmak için aşağıdakini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="13071-129">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="13071-130">Derleme ve adlı bir uygulama paketi varsayalım *MyApplication* Visual Studio 2015'te.</span><span class="sxs-lookup"><span data-stu-id="13071-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="13071-131">Varsayılan olarak, ApplicationManifest.xml listelenen uygulama türü adı "MyApplicationType" bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="13071-131">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="13071-132">Gerekli uygulama bildirimini, hizmet bildirimlerini ve kod/config/veri paketleri içeren uygulama paketi bulunan *C:\Users\<kullanıcıadı\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="13071-132">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="13071-133">Aşağıdaki komut, uygulama paketinin içeriğini listeler:</span><span class="sxs-lookup"><span data-stu-id="13071-133">The following command lists the contents of the application package:</span></span>

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

<span data-ttu-id="13071-134">Uygulama paketi büyük ve/veya birçok dosyaları yoksa, şunları yapabilirsiniz [onu Sıkıştır](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="13071-134">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="13071-135">Sıkıştırma, boyutu ve dosya sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="13071-135">The compression reduces the size and the number of files.</span></span>
<span data-ttu-id="13071-136">Yan etkisi, kaydetme ve kayıt uygulama türü daha hızlı.</span><span class="sxs-lookup"><span data-stu-id="13071-136">The side effect is that registering and un-registering the application type are faster.</span></span> <span data-ttu-id="13071-137">Özellikle paket sıkıştırmak için zaman eklerseniz karşıya yükleme zamanı şu anda, yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="13071-137">Upload time may be slower currently, especially if you include the time to compress the package.</span></span> 

<span data-ttu-id="13071-138">Bir paket sıkıştırmak için aynı kullanın [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) komutu.</span><span class="sxs-lookup"><span data-stu-id="13071-138">To compress a package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="13071-139">Sıkıştırma yapılabilir ayrı karşıya yükleme işlemini kullanarak `SkipCopy` bayrağı veya karşıya yükleme işlemi ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="13071-139">Compression can be done separate from upload, by using the `SkipCopy` flag, or together with the upload operation.</span></span> <span data-ttu-id="13071-140">Sıkıştırılmış paketi üzerinde sıkıştırma uygulama yok.</span><span class="sxs-lookup"><span data-stu-id="13071-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="13071-141">Sıkıştırılmış paketi sıkıştırmasını kaldırma için aynı kullanın [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) komutunu `UncompressPackage` geçin.</span><span class="sxs-lookup"><span data-stu-id="13071-141">To uncompress a compressed package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with the `UncompressPackage` switch.</span></span>

<span data-ttu-id="13071-142">Aşağıdaki cmdlet'i paketi görüntü deposuna kopyalama olmadan sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="13071-142">The following cmdlet compresses the package without copying it to the image store.</span></span> <span data-ttu-id="13071-143">Paket sıkıştırılmış dosya için artık içerir `Code` ve `Config` paketler.</span><span class="sxs-lookup"><span data-stu-id="13071-143">The package now includes zipped files for the `Code` and `Config` packages.</span></span> <span data-ttu-id="13071-144">(Paylaşım, uygulama türü adı ve sürümü için ayıklama belirli doğrulamaları paketini gibi) çok sayıda dahili işlemleri için gerekli olduğu için uygulama ve hizmet bildirimlerini, daraltılmış değil.</span><span class="sxs-lookup"><span data-stu-id="13071-144">The application and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="13071-145">Bildirimleri sıkıştırma bu işlemleri verimli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="13071-145">Zipping the manifests would make these operations inefficient.</span></span>

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

<span data-ttu-id="13071-146">Büyük uygulama paketlerini için sıkıştırma zaman alır.</span><span class="sxs-lookup"><span data-stu-id="13071-146">For large application packages, the compression takes time.</span></span> <span data-ttu-id="13071-147">En iyi sonuçlar için hızlı bir SSD sürücüsü kullanın.</span><span class="sxs-lookup"><span data-stu-id="13071-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="13071-148">Sıkıştırma zamanları ve sıkıştırılmış paket boyutu Ayrıca paket içeriğini göre farklılık.</span><span class="sxs-lookup"><span data-stu-id="13071-148">The compression times and the size of the compressed package also differ based on the package content.</span></span>
<span data-ttu-id="13071-149">Örneğin, ilk ve sıkıştırma süresiyle sıkıştırılmış paket boyutu göster bazı paketler için sıkıştırma istatistikleri aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="13071-149">For example, here is compression statistics for some packages, which show the initial and the compressed package size, with the compression time.</span></span>

|<span data-ttu-id="13071-150">Başlangıç boyutu (MB)</span><span class="sxs-lookup"><span data-stu-id="13071-150">Initial size (MB)</span></span>|<span data-ttu-id="13071-151">Dosya sayısı</span><span class="sxs-lookup"><span data-stu-id="13071-151">File count</span></span>|<span data-ttu-id="13071-152">Sıkıştırma zamanı</span><span class="sxs-lookup"><span data-stu-id="13071-152">Compression Time</span></span>|<span data-ttu-id="13071-153">Sıkıştırılmış paket boyutu (MB)</span><span class="sxs-lookup"><span data-stu-id="13071-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="13071-154">100</span><span class="sxs-lookup"><span data-stu-id="13071-154">100</span></span>|<span data-ttu-id="13071-155">100</span><span class="sxs-lookup"><span data-stu-id="13071-155">100</span></span>|<span data-ttu-id="13071-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="13071-156">00:00:03.3547592</span></span>|<span data-ttu-id="13071-157">60</span><span class="sxs-lookup"><span data-stu-id="13071-157">60</span></span>|
|<span data-ttu-id="13071-158">512</span><span class="sxs-lookup"><span data-stu-id="13071-158">512</span></span>|<span data-ttu-id="13071-159">100</span><span class="sxs-lookup"><span data-stu-id="13071-159">100</span></span>|<span data-ttu-id="13071-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="13071-160">00:00:16.3850303</span></span>|<span data-ttu-id="13071-161">307</span><span class="sxs-lookup"><span data-stu-id="13071-161">307</span></span>|
|<span data-ttu-id="13071-162">1024</span><span class="sxs-lookup"><span data-stu-id="13071-162">1024</span></span>|<span data-ttu-id="13071-163">500</span><span class="sxs-lookup"><span data-stu-id="13071-163">500</span></span>|<span data-ttu-id="13071-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="13071-164">00:00:32.5907950</span></span>|<span data-ttu-id="13071-165">615</span><span class="sxs-lookup"><span data-stu-id="13071-165">615</span></span>|
|<span data-ttu-id="13071-166">2048</span><span class="sxs-lookup"><span data-stu-id="13071-166">2048</span></span>|<span data-ttu-id="13071-167">1000</span><span class="sxs-lookup"><span data-stu-id="13071-167">1000</span></span>|<span data-ttu-id="13071-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="13071-168">00:01:04.3775554</span></span>|<span data-ttu-id="13071-169">1231</span><span class="sxs-lookup"><span data-stu-id="13071-169">1231</span></span>|
|<span data-ttu-id="13071-170">5012</span><span class="sxs-lookup"><span data-stu-id="13071-170">5012</span></span>|<span data-ttu-id="13071-171">100</span><span class="sxs-lookup"><span data-stu-id="13071-171">100</span></span>|<span data-ttu-id="13071-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="13071-172">00:02:45.2951288</span></span>|<span data-ttu-id="13071-173">3074</span><span class="sxs-lookup"><span data-stu-id="13071-173">3074</span></span>|

<span data-ttu-id="13071-174">Bir paket sıkıştırılmış sonra onu bir veya birden çok Service Fabric kümesi için gerektiği şekilde yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="13071-174">Once a package is compressed, it can be uploaded to one or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="13071-175">Sıkıştırılmış ve sıkıştırılmamış paketler için aynı dağıtım mekanizmadır.</span><span class="sxs-lookup"><span data-stu-id="13071-175">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="13071-176">Paket sıkıştırılmış ise, bu nedenle küme görüntü deposunda depolanır ve uygulamayı çalıştırmadan önce düğümde sıkıştırılmamış.</span><span class="sxs-lookup"><span data-stu-id="13071-176">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>


<span data-ttu-id="13071-177">Aşağıdaki örnek paketi görüntü deposuna "MyApplicationV1" adlı bir klasöre yükler:</span><span class="sxs-lookup"><span data-stu-id="13071-177">The following example uploads the package to the image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="13071-178">**Get-ImageStoreConnectionStringFromClusterManifest** Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet, görüntü deposu bağlantı dizesini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="13071-178">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="13071-179">SDK modülü içeri aktarmak için aşağıdakini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="13071-179">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="13071-180">Belirtmezseniz, *- ApplicationPackagePathInImageStore* parametresi, uygulama paketi Image store "Hata ayıklama" klasörüne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="13071-180">If you do not specify the *-ApplicationPackagePathInImageStore* parameter, the application package is copied into the "Debug" folder in the image store.</span></span>

<span data-ttu-id="13071-181">Bir paketi yükleme süresini birden çok faktörlere bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="13071-181">The time it takes to upload a package differs depending on multiple factors.</span></span> <span data-ttu-id="13071-182">Bu etkenler paketin, paket boyutu ve dosya boyutları dosya sayısı bazılarıdır.</span><span class="sxs-lookup"><span data-stu-id="13071-182">Some of these factors are the number of files in the package, the package size, and the file sizes.</span></span> <span data-ttu-id="13071-183">Kaynak makine ve Service Fabric kümesi arasındaki ağ hızı karşıya yükleme zamanı da etkiler.</span><span class="sxs-lookup"><span data-stu-id="13071-183">The network speed between the source machine and the Service Fabric cluster also impacts the upload time.</span></span> <span data-ttu-id="13071-184">İçin varsayılan zaman aşımı [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 30 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="13071-184">The default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="13071-185">Açıklanan etkenlere bağlı olarak zaman aşımı süresini artırın gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="13071-185">Depending on the described factors, you may have to increase the timeout.</span></span> <span data-ttu-id="13071-186">Paket Kopyala çağrısında sıkıştırma, sıkıştırma zaman da dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13071-186">If you are compressing the package in the copy call, you need to also consider the compression time.</span></span>

<span data-ttu-id="13071-187">Bkz: [görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) resim ve görüntü deposu hakkında ek bilgi için bağlantı dizesi depolar.</span><span class="sxs-lookup"><span data-stu-id="13071-187">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="13071-188">Uygulama paketi Kaydet</span><span class="sxs-lookup"><span data-stu-id="13071-188">Register the application package</span></span>
<span data-ttu-id="13071-189">Uygulama türü ve sürümü, uygulama paketi kaydedildikten sonra kullanılabilir hale uygulama bildiriminde bildirildi.</span><span class="sxs-lookup"><span data-stu-id="13071-189">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="13071-190">Sistem önceki adımda karşıya yüklenen paket okur, paket doğrular, paket içeriğini işler ve işlenen paket bir iç sistem konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="13071-190">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="13071-191">Çalıştırma [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) kümede uygulama türünü kaydetme ve dağıtım için kullanılabilir hale getirmek için cmdlet:</span><span class="sxs-lookup"><span data-stu-id="13071-191">Run the [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet to register the application type in the cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="13071-192">"MyApplicationV1" uygulama paketi bulunduğu Image store klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="13071-192">"MyApplicationV1" is the folder in the image store where the application package is located.</span></span> <span data-ttu-id="13071-193">Uygulama türü adı "MyApplicationType" Sürüm "1.0.0 (her ikisi de uygulama bildiriminde bulunur)" ile şimdi kümedeki kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="13071-193">The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) is now registered in the cluster.</span></span>

<span data-ttu-id="13071-194">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) komut, yalnızca sistem uygulama paketi başarıyla kaydolduktan sonra döndürür.</span><span class="sxs-lookup"><span data-stu-id="13071-194">The [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after the system has successfully registered the application package.</span></span> <span data-ttu-id="13071-195">Ne kadar süreyle kayıt alır boyutu ve uygulama paketi içeriğini bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="13071-195">How long registration takes depends on the size and contents of the application package.</span></span> <span data-ttu-id="13071-196">Gerekirse, **- TimeoutSec** parametre (60 saniye olan varsayılan zaman aşımı) daha uzun bir süre sağlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="13071-196">If needed, the **-TimeoutSec** parameter can be used to supply a longer timeout (the default timeout is 60 seconds).</span></span>

<span data-ttu-id="13071-197">Paket veya zaman aşımına uğruyor kullanırsanız büyük bir uygulamanız varsa, **- zaman uyumsuz** parametresi.</span><span class="sxs-lookup"><span data-stu-id="13071-197">If you have a large application package or if you are experiencing timeouts, use the **-Async** parameter.</span></span> <span data-ttu-id="13071-198">Komutu, küme kayıt komutu kabul eder ve gerektiğinde işleme devam döndürür.</span><span class="sxs-lookup"><span data-stu-id="13071-198">The command returns when the cluster accepts the register command, and the processing continues as needed.</span></span>
<span data-ttu-id="13071-199">[Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) komutu tüm başarıyla kayıtlı uygulama türü sürümleri ve kayıt durumlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="13071-199">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="13071-200">Kayıt tamamlandığında belirlemek için bu komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="13071-200">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-the-application"></a><span data-ttu-id="13071-201">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="13071-201">Create the application</span></span>
<span data-ttu-id="13071-202">Bir uygulama kullanarak başarıyla kaydettirildi herhangi bir uygulama türü sürümü örneği [yeni ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="13071-202">You can instantiate an application from any application type version that has been registered successfully by using the [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="13071-203">Her bir uygulama adı ile başlamalıdır *"fabric:"* düzen ve her bir uygulama örneği için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="13071-203">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="13071-204">Hedef uygulama türü uygulama bildiriminde tanımlanan varsayılan hizmetlerin de oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="13071-204">Any default services defined in the application manifest of the target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="13071-205">Verilen herhangi bir kayıtlı uygulama türü sürümü için birden çok uygulama örneği oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="13071-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="13071-206">Her uygulama örneği yalıtımı, kendi çalışma dizini ve işlem ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="13071-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="13071-207">Hangi adlı görmek için uygulama ve hizmetlere çalıştırmak kümede çalışan [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) ve [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="13071-207">To see which named apps and services are running in the cluster, run the [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a><span data-ttu-id="13071-208">Bir uygulamayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="13071-208">Remove an application</span></span>
<span data-ttu-id="13071-209">Uygulama örneğini artık gerekli olmadığında kalıcı olarak adını kullanarak kaldırabilirsiniz [Kaldır ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="13071-209">When an application instance is no longer needed, you can permanently remove it by name using the [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="13071-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) tüm hizmet durumunu da, kalıcı olarak kaldırma uygulamaya ait tüm hizmetleri otomatik olarak kaldırır.</span><span class="sxs-lookup"><span data-stu-id="13071-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="13071-211">Bu işlem geri alınamaz ve uygulama durumu kurtarılamıyor.</span><span class="sxs-lookup"><span data-stu-id="13071-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="13071-212">Bir uygulama türü kaydını kaldırma</span><span class="sxs-lookup"><span data-stu-id="13071-212">Unregister an application type</span></span>
<span data-ttu-id="13071-213">Belirli bir uygulama türü sürümü artık gerekli olmadığında kullanılarak uygulama türü kaydını [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="13071-213">When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="13071-214">Kullanılmayan uygulama türleri kaydını Image store tarafından kullanılan depolama alanını serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="13071-214">Unregistering unused application types releases storage space used by the image store.</span></span> <span data-ttu-id="13071-215">Uygulama türü olarak hiçbir uygulamaları karşı oluşturulur ve uygulama Beklemede yükseltmeler, Hayır başvurduğunuzdan sürece kaydı olabilir.</span><span class="sxs-lookup"><span data-stu-id="13071-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="13071-216">Çalıştırma [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) kümede kayıtlı uygulama türlerini görmek için:</span><span class="sxs-lookup"><span data-stu-id="13071-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) to see the application types currently registered in the cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="13071-217">Çalıştırma [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) belirli uygulama türü kaydını kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="13071-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) to unregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="13071-218">Bir uygulama paketi görüntü deposundan kaldırır</span><span class="sxs-lookup"><span data-stu-id="13071-218">Remove an application package from the image store</span></span>
<span data-ttu-id="13071-219">Bir uygulama paketi artık gerekli olmadığında, sistem kaynakları serbest görüntü deposundan silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13071-219">When an application package is no longer needed, you can delete it from the image store to free up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="13071-220">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="13071-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="13071-221">Kopya ServiceFabricApplicationPackage bir ImageStoreConnectionString için sorar</span><span class="sxs-lookup"><span data-stu-id="13071-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="13071-222">Service Fabric SDK ortam zaten ayarlanmış doğru Varsayılanları olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="13071-222">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="13071-223">Ancak gerekirse, tüm komutlar için ImageStoreConnectionString Service Fabric kümesi kullanarak değer eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="13071-223">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="13071-224">Küme bildiriminde ImageStoreConnectionString bulabilirsiniz kullanarak alınan [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) ve Get-ImageStoreConnectionStringFromClusterManifest komutlar:</span><span class="sxs-lookup"><span data-stu-id="13071-224">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="13071-225">**Get-ImageStoreConnectionStringFromClusterManifest** Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet, görüntü deposu bağlantı dizesini almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="13071-225">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="13071-226">SDK modülü içeri aktarmak için aşağıdakini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="13071-226">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="13071-227">ImageStoreConnectionString küme bildiriminde bulunur:</span><span class="sxs-lookup"><span data-stu-id="13071-227">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="13071-228">Bkz: [görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) resim ve görüntü deposu hakkında ek bilgi için bağlantı dizesi depolar.</span><span class="sxs-lookup"><span data-stu-id="13071-228">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="13071-229">Büyük uygulama paketini dağıtma</span><span class="sxs-lookup"><span data-stu-id="13071-229">Deploy large application package</span></span>
<span data-ttu-id="13071-230">Sorun: [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) büyük uygulama paketi (GB sırasını) için zaman aşımına uğradı.</span><span class="sxs-lookup"><span data-stu-id="13071-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="13071-231">Deneyin:</span><span class="sxs-lookup"><span data-stu-id="13071-231">Try:</span></span>
- <span data-ttu-id="13071-232">Daha büyük zaman aşımını belirtmek [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) komutu ile `TimeoutSec` parametresi.</span><span class="sxs-lookup"><span data-stu-id="13071-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="13071-233">Varsayılan olarak, zaman aşımı 30 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="13071-233">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="13071-234">Kaynak makine ve küme arasındaki ağ bağlantısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="13071-234">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="13071-235">Bağlantı yavaş ise, bir makine daha iyi bir ağ bağlantısı ile kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="13071-235">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="13071-236">İstemci makine küme başka bir bölgede ise, bir istemci makine bir daha yakından ya da aynı bölgede küme olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="13071-236">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="13071-237">Dış azaltma devreyi olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="13071-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="13071-238">Örneğin, görüntü deposu azure depolama kullanacak şekilde yapılandırıldığında, karşıya yükleme kısıtlanan.</span><span class="sxs-lookup"><span data-stu-id="13071-238">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="13071-239">Sorun: karşıya yükleme paketi başarıyla tamamlandı ancak [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) zaman aşımına uğradı.</span><span class="sxs-lookup"><span data-stu-id="13071-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out.</span></span>
<span data-ttu-id="13071-240">Deneyin:</span><span class="sxs-lookup"><span data-stu-id="13071-240">Try:</span></span>
- <span data-ttu-id="13071-241">[Paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) görüntü deposuna kopyalama önce.</span><span class="sxs-lookup"><span data-stu-id="13071-241">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="13071-242">Sıkıştırma küçültür ve hangi sırayla trafik miktarını azaltır ve bu Service Fabric çalışma dosyaları sayısı gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="13071-242">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="13071-243">Karşıya yükleme işlemi (özellikle sıkıştırma zaman eklerseniz) daha yavaş olabilir, ancak kaydedin ve kaydı uygulama türü daha hızlı.</span><span class="sxs-lookup"><span data-stu-id="13071-243">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="13071-244">Daha büyük zaman aşımını belirtmek [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) ile `TimeoutSec` parametresi.</span><span class="sxs-lookup"><span data-stu-id="13071-244">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="13071-245">Belirtin `Async` için geçiş [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="13071-245">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="13071-246">Komutu, küme komutu kabul eder ve uygulama türü kaydını zaman uyumsuz olarak devam döndürür.</span><span class="sxs-lookup"><span data-stu-id="13071-246">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span> <span data-ttu-id="13071-247">Bu nedenle, bu durumda daha yüksek bir zaman aşımı belirtmek için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="13071-247">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="13071-248">[Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) komutu tüm başarıyla kayıtlı uygulama türü sürümleri ve kayıt durumlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="13071-248">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="13071-249">Kayıt tamamlandığında belirlemek için bu komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="13071-249">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="13071-250">Birçok dosyalarıyla uygulama paketini dağıtma</span><span class="sxs-lookup"><span data-stu-id="13071-250">Deploy application package with many files</span></span>
<span data-ttu-id="13071-251">Sorun: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) zaman aşımına uğraması için uygulama paketi birçok dosyalarla (binlerce sırasını).</span><span class="sxs-lookup"><span data-stu-id="13071-251">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="13071-252">Deneyin:</span><span class="sxs-lookup"><span data-stu-id="13071-252">Try:</span></span>
- <span data-ttu-id="13071-253">[Paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) görüntü deposuna kopyalama önce.</span><span class="sxs-lookup"><span data-stu-id="13071-253">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="13071-254">Sıkıştırma dosyalarının sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="13071-254">The compression reduces the number of files.</span></span>
- <span data-ttu-id="13071-255">Daha büyük zaman aşımını belirtmek [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) ile `TimeoutSec` parametresi.</span><span class="sxs-lookup"><span data-stu-id="13071-255">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="13071-256">Belirtin `Async` için geçiş [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="13071-256">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="13071-257">Komutu, küme komutu kabul eder ve uygulama türü kaydını zaman uyumsuz olarak devam döndürür.</span><span class="sxs-lookup"><span data-stu-id="13071-257">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span>
<span data-ttu-id="13071-258">Bu nedenle, bu durumda daha yüksek bir zaman aşımı belirtmek için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="13071-258">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="13071-259">[Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) komutu tüm başarıyla kayıtlı uygulama türü sürümleri ve kayıt durumlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="13071-259">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="13071-260">Kayıt tamamlandığında belirlemek için bu komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="13071-260">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="13071-261">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="13071-261">Next steps</span></span>
[<span data-ttu-id="13071-262">Service Fabric uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="13071-262">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="13071-263">Service Fabric sistem durumu giriş</span><span class="sxs-lookup"><span data-stu-id="13071-263">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="13071-264">Tanılama ve bir Service Fabric hizmeti sorun giderme</span><span class="sxs-lookup"><span data-stu-id="13071-264">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="13071-265">Service Fabric uygulamada modeli</span><span class="sxs-lookup"><span data-stu-id="13071-265">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
