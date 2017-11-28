---
title: "aaaAzure Service Fabric uygulama dağıtımı | Microsoft Docs"
description: "Nasıl Service Fabric PowerShell kullanarak toodeploy ekleme ve kaldırma uygulamalarda."
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
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="ddcd9-103">Dağıtma ve PowerShell kullanarak uygulamaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="ddcd9-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ddcd9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddcd9-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="ddcd9-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ddcd9-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="ddcd9-106">FabricClient API’leri</span><span class="sxs-lookup"><span data-stu-id="ddcd9-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="ddcd9-107">Bir kez bir [uygulama türü paketlenmiş][10], Azure Service Fabric kümesi içine dağıtımı için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="ddcd9-108">Dağıtım hello aşağıdaki üç adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="ddcd9-109">Merhaba uygulama paketi toohello görüntü deposuna karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="ddcd9-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="ddcd9-110">Merhaba uygulama türünü kaydetme</span><span class="sxs-lookup"><span data-stu-id="ddcd9-110">Register hello application type</span></span>
3. <span data-ttu-id="ddcd9-111">Merhaba uygulama örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddcd9-111">Create hello application instance</span></span>

<span data-ttu-id="ddcd9-112">Bir uygulamanın dağıtıldığını ve bir örnek hello kümede çalışan sonra hello uygulama örneği ve uygulama türünü silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="ddcd9-113">bir uygulama hello kümeden toocompletely Kaldır hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="ddcd9-114">Uygulama örneğini çalıştıran hello Kaldır (veya Sil)</span><span class="sxs-lookup"><span data-stu-id="ddcd9-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="ddcd9-115">Artık ihtiyacınız varsa hello uygulama türü kaydını kaldırma</span><span class="sxs-lookup"><span data-stu-id="ddcd9-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="ddcd9-116">Merhaba görüntü deposundan Hello uygulama paketini kaldırma</span><span class="sxs-lookup"><span data-stu-id="ddcd9-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="ddcd9-117">Kullanırsanız [uygulamalarında hata ayıklama ve dağıtma için Visual Studio](service-fabric-publish-app-remote-cluster.md) yerel geliştirme kümenizde yukarıdaki adımların tümünü hello bir PowerShell komut dosyası otomatik olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="ddcd9-118">Bu komut dosyası hello bulunan *komut dosyaları* hello uygulama projesi klasörü.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="ddcd9-119">Bu makalede, gerçekleştirebilmeleri için komut dosyası yaptıklarını üzerinde arka plan sağlar hello Visual Studio dışında aynı işlemleri.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="ddcd9-120">Toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="ddcd9-120">Connect toohello cluster</span></span>
<span data-ttu-id="ddcd9-121">Bu makaledeki tüm PowerShell komutları çalıştırmadan önce her zaman başlamayı [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric kümesi.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric cluster.</span></span> <span data-ttu-id="ddcd9-122">Merhaba aşağıdaki komutu çalıştırarak tooconnect toohello yerel geliştirme kümesi:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-122">tooconnect toohello local development cluster, run hello following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="ddcd9-123">Bağlantı tooa uzaktan küme veya küme Azure Active Directory, X509 kullanılarak güvenli örnekleri için sertifikalar veya Windows Active Directory bkz [Bağlan tooa güvenli küme](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ddcd9-123">For examples of connecting tooa remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-hello-application-package"></a><span data-ttu-id="ddcd9-124">Merhaba uygulama paketini karşıya yükleyin</span><span class="sxs-lookup"><span data-stu-id="ddcd9-124">Upload hello application package</span></span>
<span data-ttu-id="ddcd9-125">Karşıya yükleme hello uygulama paketi iç Service Fabric bileşenleri tarafından erişilebilen bir konumda koyar.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-125">Uploading hello application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="ddcd9-126">Tooverify hello uygulama paketi yerel olarak istiyorsanız hello kullanın [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-126">If you want tooverify hello application package locally, use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="ddcd9-127">Merhaba [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) karşıya hello uygulama paketi toohello küme Image store komutu.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-127">hello [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads hello application package toohello cluster image store.</span></span>
<span data-ttu-id="ddcd9-128">Merhaba **Get-ImageStoreConnectionStringFromClusterManifest** hello Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet kullanılan tooget hello görüntü olan bağlantı dizesi depolar.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-128">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="ddcd9-129">çalıştırma tooimport hello SDK Modülü:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-129">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="ddcd9-130">Derleme ve adlı bir uygulama paketi varsayalım *MyApplication* Visual Studio 2015'te.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="ddcd9-131">Varsayılan olarak, "MyApplicationType" Merhaba ApplicationManifest.xml listelenen hello uygulama türü adı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-131">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="ddcd9-132">Merhaba hello gerekli uygulama bildirimini, hizmet bildirimlerini ve kod/config/veri paketleri içeren uygulama paketi bulunan *C:\Users\<kullanıcıadı\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-132">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="ddcd9-133">Merhaba aşağıdaki komut hello uygulama paketinin Merhaba içeriğine listeler:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-133">hello following command lists hello contents of hello application package:</span></span>

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

<span data-ttu-id="ddcd9-134">Merhaba uygulama paketi büyük ve/veya birçok dosyaları yoksa, şunları yapabilirsiniz [onu Sıkıştır](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="ddcd9-134">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="ddcd9-135">Merhaba sıkıştırma hello boyutunu ve dosya hello sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-135">hello compression reduces hello size and hello number of files.</span></span>
<span data-ttu-id="ddcd9-136">Merhaba yan etkisi olan, kaydetme ve kayıt hello uygulama türü daha hızlı.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-136">hello side effect is that registering and un-registering hello application type are faster.</span></span> <span data-ttu-id="ddcd9-137">Özellikle hello zaman toocompress hello paketi eklerseniz karşıya yükleme zamanı şu anda, yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-137">Upload time may be slower currently, especially if you include hello time toocompress hello package.</span></span> 

<span data-ttu-id="ddcd9-138">toocompress bir paket kullanım hello aynı [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) komutu.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-138">toocompress a package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="ddcd9-139">Sıkıştırma yapılabilir ayrı karşıya yükleme işlemini hello kullanarak `SkipCopy` bayrak veya hello ile birlikte karşıya yükleme işleminde.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-139">Compression can be done separate from upload, by using hello `SkipCopy` flag, or together with hello upload operation.</span></span> <span data-ttu-id="ddcd9-140">Sıkıştırılmış paketi üzerinde sıkıştırma uygulama yok.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="ddcd9-141">toouncompress kullanımı bir sıkıştırılmış paket hello aynı [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) hello komutunu `UncompressPackage` geçin.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-141">toouncompress a compressed package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with hello `UncompressPackage` switch.</span></span>

<span data-ttu-id="ddcd9-142">Merhaba aşağıdaki cmdlet'i hello paket toohello Image store kopyalamadan sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-142">hello following cmdlet compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="ddcd9-143">Merhaba paket artık hello sıkıştırılmış dosyaları içerir `Code` ve `Config` paketler.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-143">hello package now includes zipped files for hello `Code` and `Config` packages.</span></span> <span data-ttu-id="ddcd9-144">birçok dahili işlemleri (örneğin, paket paylaşımı, belirli doğrulamaları için uygulama türü adı ve sürümü ayıklama) için gerekli olduğu için hello uygulama ve hello hizmet bildirimlerini, daraltılmış değil.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-144">hello application and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="ddcd9-145">Sıkıştırma hello bildirimleri bu işlemleri verimli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-145">Zipping hello manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="ddcd9-146">Büyük uygulama paketlerini hello sıkıştırma zaman alır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-146">For large application packages, hello compression takes time.</span></span> <span data-ttu-id="ddcd9-147">En iyi sonuçlar için hızlı bir SSD sürücüsü kullanın.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="ddcd9-148">Ayrıca Hello sıkıştırma zamanları ve hello sıkıştırılmış paket hello boyutunu hello paket içeriğini göre farklılık.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-148">hello compression times and hello size of hello compressed package also differ based on hello package content.</span></span>
<span data-ttu-id="ddcd9-149">Örneğin, hello ilk göstermek ve hello sıkıştırma süresiyle sıkıştırılmış paket boyutu hello bazı paketler için sıkıştırma istatistikleri aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-149">For example, here is compression statistics for some packages, which show hello initial and hello compressed package size, with hello compression time.</span></span>

|<span data-ttu-id="ddcd9-150">Başlangıç boyutu (MB)</span><span class="sxs-lookup"><span data-stu-id="ddcd9-150">Initial size (MB)</span></span>|<span data-ttu-id="ddcd9-151">Dosya sayısı</span><span class="sxs-lookup"><span data-stu-id="ddcd9-151">File count</span></span>|<span data-ttu-id="ddcd9-152">Sıkıştırma zamanı</span><span class="sxs-lookup"><span data-stu-id="ddcd9-152">Compression Time</span></span>|<span data-ttu-id="ddcd9-153">Sıkıştırılmış paket boyutu (MB)</span><span class="sxs-lookup"><span data-stu-id="ddcd9-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="ddcd9-154">100</span><span class="sxs-lookup"><span data-stu-id="ddcd9-154">100</span></span>|<span data-ttu-id="ddcd9-155">100</span><span class="sxs-lookup"><span data-stu-id="ddcd9-155">100</span></span>|<span data-ttu-id="ddcd9-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="ddcd9-156">00:00:03.3547592</span></span>|<span data-ttu-id="ddcd9-157">60</span><span class="sxs-lookup"><span data-stu-id="ddcd9-157">60</span></span>|
|<span data-ttu-id="ddcd9-158">512</span><span class="sxs-lookup"><span data-stu-id="ddcd9-158">512</span></span>|<span data-ttu-id="ddcd9-159">100</span><span class="sxs-lookup"><span data-stu-id="ddcd9-159">100</span></span>|<span data-ttu-id="ddcd9-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="ddcd9-160">00:00:16.3850303</span></span>|<span data-ttu-id="ddcd9-161">307</span><span class="sxs-lookup"><span data-stu-id="ddcd9-161">307</span></span>|
|<span data-ttu-id="ddcd9-162">1024</span><span class="sxs-lookup"><span data-stu-id="ddcd9-162">1024</span></span>|<span data-ttu-id="ddcd9-163">500</span><span class="sxs-lookup"><span data-stu-id="ddcd9-163">500</span></span>|<span data-ttu-id="ddcd9-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="ddcd9-164">00:00:32.5907950</span></span>|<span data-ttu-id="ddcd9-165">615</span><span class="sxs-lookup"><span data-stu-id="ddcd9-165">615</span></span>|
|<span data-ttu-id="ddcd9-166">2048</span><span class="sxs-lookup"><span data-stu-id="ddcd9-166">2048</span></span>|<span data-ttu-id="ddcd9-167">1000</span><span class="sxs-lookup"><span data-stu-id="ddcd9-167">1000</span></span>|<span data-ttu-id="ddcd9-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="ddcd9-168">00:01:04.3775554</span></span>|<span data-ttu-id="ddcd9-169">1231</span><span class="sxs-lookup"><span data-stu-id="ddcd9-169">1231</span></span>|
|<span data-ttu-id="ddcd9-170">5012</span><span class="sxs-lookup"><span data-stu-id="ddcd9-170">5012</span></span>|<span data-ttu-id="ddcd9-171">100</span><span class="sxs-lookup"><span data-stu-id="ddcd9-171">100</span></span>|<span data-ttu-id="ddcd9-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="ddcd9-172">00:02:45.2951288</span></span>|<span data-ttu-id="ddcd9-173">3074</span><span class="sxs-lookup"><span data-stu-id="ddcd9-173">3074</span></span>|

<span data-ttu-id="ddcd9-174">Bir paket sıkıştırılmış sonra karşıya yüklenen tooone olabilir veya birden çok Service Fabric gerektiği kümeleri.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-174">Once a package is compressed, it can be uploaded tooone or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="ddcd9-175">Merhaba dağıtım için sıkıştırılmış ve sıkıştırılmamış paketleri aynı mekanizmadır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-175">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="ddcd9-176">Hello paket sıkıştırılmışsa, bu nedenle hello küme görüntü deposunda depolanır ve hello uygulamayı çalıştırmadan önce hello düğümde sıkıştırılmamış.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-176">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>


<span data-ttu-id="ddcd9-177">Merhaba aşağıdaki örnek hello paket toohello Image store "MyApplicationV1" adlı bir klasöre yükler:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-177">hello following example uploads hello package toohello image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="ddcd9-178">Merhaba **Get-ImageStoreConnectionStringFromClusterManifest** hello Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet kullanılan tooget hello görüntü olan bağlantı dizesi depolar.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-178">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="ddcd9-179">çalıştırma tooimport hello SDK Modülü:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-179">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="ddcd9-180">Merhaba belirtmezseniz *- ApplicationPackagePathInImageStore* parametresi, hello uygulama paketi hello Image store hello "Hata ayıklama" klasörüne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-180">If you do not specify hello *-ApplicationPackagePathInImageStore* parameter, hello application package is copied into hello "Debug" folder in hello image store.</span></span>

<span data-ttu-id="ddcd9-181">tooupload bir paket hello süresini birden çok faktörlere bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-181">hello time it takes tooupload a package differs depending on multiple factors.</span></span> <span data-ttu-id="ddcd9-182">Bu etkenler hello paketi, başlangıç paket boyutu ve hello dosya boyutları dosya hello sayısı bazılarıdır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-182">Some of these factors are hello number of files in hello package, hello package size, and hello file sizes.</span></span> <span data-ttu-id="ddcd9-183">Merhaba ağ hızı hello kaynak makineyle hello Service Fabric kümesi arasında da hello karşıya yükleme zamanı etkiler.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-183">hello network speed between hello source machine and hello Service Fabric cluster also impacts hello upload time.</span></span> <span data-ttu-id="ddcd9-184">için varsayılan zaman aşımı hello [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 30 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-184">hello default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="ddcd9-185">Bağlı olarak açıklanan faktörleri Merhaba, tooincrease hello zaman aşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-185">Depending on hello described factors, you may have tooincrease hello timeout.</span></span> <span data-ttu-id="ddcd9-186">Merhaba paket hello kopya çağrısında sıkıştırma, tooalso gerekir hello sıkıştırma zaman göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-186">If you are compressing hello package in hello copy call, you need tooalso consider hello compression time.</span></span>

<span data-ttu-id="ddcd9-187">Bkz: [hello görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) için tamamlayıcı bilgiler hakkında hello Image store ve görüntü depolama bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-187">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="ddcd9-188">YAZMAÇ hello uygulama paketi</span><span class="sxs-lookup"><span data-stu-id="ddcd9-188">Register hello application package</span></span>
<span data-ttu-id="ddcd9-189">Merhaba uygulama türü ve sürümü hello uygulama paketi kaydedildikten sonra kullanılabilir hale hello uygulama bildiriminde bildirildi.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-189">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="ddcd9-190">Merhaba sistem hello önceki adımda karşıya yüklenen hello paket okur hello paket doğrular, hello paket içeriğini işler ve işlenen hello paket tooan iç sistem konumuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-190">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="ddcd9-191">Merhaba çalıştırmak [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello hello kümedeki uygulama türü ve dağıtımı için kullanılabilir hale getirin:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-191">Run hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello application type in hello cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="ddcd9-192">"MyApplicationV1" Merhaba uygulama paketinin bulunduğu hello Image store hello klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-192">"MyApplicationV1" is hello folder in hello image store where hello application package is located.</span></span> <span data-ttu-id="ddcd9-193">Merhaba uygulama türü adı "MyApplicationType" Sürüm "1.0.0" (her ikisi de hello uygulama bildiriminde bulunur) ile artık hello kümesinde kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-193">hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) is now registered in hello cluster.</span></span>

<span data-ttu-id="ddcd9-194">Merhaba [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) komut, yalnızca hello sistem başarıyla kaydedildi hello uygulama paketine sahip olduktan sonra döndürür.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-194">hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after hello system has successfully registered hello application package.</span></span> <span data-ttu-id="ddcd9-195">Ne kadar süreyle kayıt alır hello boyutu ve hello uygulama paketinin içeriğini bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-195">How long registration takes depends on hello size and contents of hello application package.</span></span> <span data-ttu-id="ddcd9-196">Gerekirse, hello **- TimeoutSec** parametresi kullanılan toosupply daha uzun bir süre olabilir (Merhaba varsayılan zaman aşımı olan 60 saniye).</span><span class="sxs-lookup"><span data-stu-id="ddcd9-196">If needed, hello **-TimeoutSec** parameter can be used toosupply a longer timeout (hello default timeout is 60 seconds).</span></span>

<span data-ttu-id="ddcd9-197">Paket veya zaman aşımına uğruyor, hello kullanın. büyük bir uygulamanız varsa, **- zaman uyumsuz** parametresi.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-197">If you have a large application package or if you are experiencing timeouts, use hello **-Async** parameter.</span></span> <span data-ttu-id="ddcd9-198">Merhaba komut hello küme hello register komutunun kabul eder ve gerektiği gibi hello işleme devam ettiğinde döndürür.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-198">hello command returns when hello cluster accepts hello register command, and hello processing continues as needed.</span></span>
<span data-ttu-id="ddcd9-199">Merhaba [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) komutu tüm başarıyla kayıtlı uygulama türü sürümleri ve kayıt durumlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-199">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="ddcd9-200">Merhaba kaydı yapıldığında bu komut toodetermine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-200">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a><span data-ttu-id="ddcd9-201">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddcd9-201">Create hello application</span></span>
<span data-ttu-id="ddcd9-202">Bir uygulamadan hello kullanarak başarıyla kaydettirildi herhangi bir uygulama türü sürümü örneği [yeni ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-202">You can instantiate an application from any application type version that has been registered successfully by using hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="ddcd9-203">her uygulamanın Hello adı hello ile başlamalı *"fabric:"* düzen ve her bir uygulama örneği için benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-203">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="ddcd9-204">Hello uygulama bildiriminde hello hedef uygulama türünün tanımlı hiçbir varsayılan hizmetleri de oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-204">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="ddcd9-205">Verilen herhangi bir kayıtlı uygulama türü sürümü için birden çok uygulama örneği oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="ddcd9-206">Her uygulama örneği yalıtımı, kendi çalışma dizini ve işlem ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="ddcd9-207">uygulamalar ve hizmetler olarak adlandırılan toosee hello çalıştırmak hello kümede çalışan [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) ve [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-207">toosee which named apps and services are running in hello cluster, run hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

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

## <a name="remove-an-application"></a><span data-ttu-id="ddcd9-208">Bir uygulamayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="ddcd9-208">Remove an application</span></span>
<span data-ttu-id="ddcd9-209">Uygulama örneğini artık gerekli olmadığında kalıcı olarak hello kullanarak adıyla kaldırabilirsiniz [Kaldır ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-209">When an application instance is no longer needed, you can permanently remove it by name using hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="ddcd9-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) tüm hizmet durumunu da, kalıcı olarak kaldırma toohello uygulama ait tüm hizmetleri otomatik olarak kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="ddcd9-211">Bu işlem geri alınamaz ve uygulama durumu kurtarılamıyor.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="ddcd9-212">Bir uygulama türü kaydını kaldırma</span><span class="sxs-lookup"><span data-stu-id="ddcd9-212">Unregister an application type</span></span>
<span data-ttu-id="ddcd9-213">Belirli bir uygulama türü sürümü artık gerekli olmadığında hello kullanarak hello uygulama türü kaydını kaldırma [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-213">When a particular version of an application type is no longer needed, you should unregister hello application type using hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="ddcd9-214">Merhaba Image store tarafından kullanılan kaydı siliniyor kullanılmayan uygulama türleri sürümleri depolama alanı.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-214">Unregistering unused application types releases storage space used by hello image store.</span></span> <span data-ttu-id="ddcd9-215">Uygulama türü olarak hiçbir uygulamaları karşı oluşturulur ve uygulama Beklemede yükseltmeler, Hayır başvurduğunuzdan sürece kaydı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="ddcd9-216">Çalıştırma [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello uygulama türleri şu anda kayıtlı hello kümede:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello application types currently registered in hello cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="ddcd9-217">Çalıştırma [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister belirli uygulama türü:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="ddcd9-218">Bir uygulama paketi hello görüntü deposundan kaldırır</span><span class="sxs-lookup"><span data-stu-id="ddcd9-218">Remove an application package from hello image store</span></span>
<span data-ttu-id="ddcd9-219">Bir uygulama paketi artık gerekli olmadığında hello görüntü deposu toofree sistem kaynaklarının silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-219">When an application package is no longer needed, you can delete it from hello image store toofree up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="ddcd9-220">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ddcd9-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="ddcd9-221">Kopya ServiceFabricApplicationPackage bir ImageStoreConnectionString için sorar</span><span class="sxs-lookup"><span data-stu-id="ddcd9-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="ddcd9-222">Merhaba Service Fabric SDK ortam zaten hello Varsayılanlarını Ayarla doğru olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-222">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="ddcd9-223">Ancak gerekirse, hello ImageStoreConnectionString tüm komutlar için Service Fabric kümesi kullanarak bu hello hello değeri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-223">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="ddcd9-224">Merhaba küme bildiriminde hello ImageStoreConnectionString bulabilirsiniz hello kullanarak alınan [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) ve Get-ImageStoreConnectionStringFromClusterManifest komutlar:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-224">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="ddcd9-225">Merhaba **Get-ImageStoreConnectionStringFromClusterManifest** hello Service Fabric SDK PowerShell modülünün bir parçası olan cmdlet kullanılan tooget hello görüntü olan bağlantı dizesi depolar.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-225">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="ddcd9-226">çalıştırma tooimport hello SDK Modülü:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-226">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="ddcd9-227">Merhaba ImageStoreConnectionString hello küme bildiriminde bulunur:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-227">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="ddcd9-228">Bkz: [hello görüntü deposu bağlantı dizesi anlamak](service-fabric-image-store-connection-string.md) için tamamlayıcı bilgiler hakkında hello Image store ve görüntü depolama bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-228">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="ddcd9-229">Büyük uygulama paketini dağıtma</span><span class="sxs-lookup"><span data-stu-id="ddcd9-229">Deploy large application package</span></span>
<span data-ttu-id="ddcd9-230">Sorun: [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) büyük uygulama paketi (GB sırasını) için zaman aşımına uğradı.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="ddcd9-231">Deneyin:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-231">Try:</span></span>
- <span data-ttu-id="ddcd9-232">Daha büyük zaman aşımını belirtmek [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) komutu ile `TimeoutSec` parametresi.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="ddcd9-233">Varsayılan olarak, hello zaman aşımı 30 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-233">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="ddcd9-234">Kaynak makine ve küme arasındaki Hello ağ bağlantısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-234">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="ddcd9-235">Merhaba bağlantı yavaş ise, bir makine daha iyi bir ağ bağlantısı ile kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-235">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="ddcd9-236">Merhaba istemci makine hello küme başka bir bölgede ise, bir istemci makine bir daha yakından ya da aynı bölgede hello küme olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-236">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="ddcd9-237">Dış azaltma devreyi olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="ddcd9-238">Örneğin, Hello Image store yapılandırılmış toouse azure depolama olduğunda, karşıya yükleme kısıtlanan.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-238">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="ddcd9-239">Sorun: karşıya yükleme paketi başarıyla tamamlandı ancak [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) zaman aşımına uğradı. Deneyin:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out. Try:</span></span>
- <span data-ttu-id="ddcd9-240">[Merhaba paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) toohello Image store kopyalamadan önce.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-240">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="ddcd9-241">Hello sıkıştırma hello boyutunu azaltır ve hangi sırayla hello trafik miktarını azaltır ve bu Service Fabric çalışma hello dosya sayısı, gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-241">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="ddcd9-242">Merhaba karşıya yükleme işlemi (özellikle hello sıkıştırma zaman eklerseniz) daha yavaş olabilir, ancak daha hızlı kaydedin ve kaydı hello uygulama türü.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-242">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="ddcd9-243">Daha büyük zaman aşımını belirtmek [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) ile `TimeoutSec` parametresi.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-243">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="ddcd9-244">Belirtin `Async` için geçiş [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="ddcd9-244">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="ddcd9-245">Merhaba komut hello küme hello komutu kabul eder ve hello uygulama türü hello kayıt zaman uyumsuz olarak devam ettiğinde döndürür.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-245">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span> <span data-ttu-id="ddcd9-246">Bu nedenle, yoktur gerek toospecify daha yüksek bir zaman aşımı bu durumda.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-246">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="ddcd9-247">Merhaba [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) komutu tüm başarıyla kayıtlı uygulama türü sürümleri ve kayıt durumlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-247">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="ddcd9-248">Merhaba kaydı yapıldığında bu komut toodetermine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-248">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="ddcd9-249">Birçok dosyalarıyla uygulama paketini dağıtma</span><span class="sxs-lookup"><span data-stu-id="ddcd9-249">Deploy application package with many files</span></span>
<span data-ttu-id="ddcd9-250">Sorun: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) zaman aşımına uğraması için uygulama paketi birçok dosyalarla (binlerce sırasını).</span><span class="sxs-lookup"><span data-stu-id="ddcd9-250">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="ddcd9-251">Deneyin:</span><span class="sxs-lookup"><span data-stu-id="ddcd9-251">Try:</span></span>
- <span data-ttu-id="ddcd9-252">[Merhaba paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) toohello Image store kopyalamadan önce.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-252">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="ddcd9-253">Merhaba sıkıştırma dosyaları hello sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-253">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="ddcd9-254">Daha büyük zaman aşımını belirtmek [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) ile `TimeoutSec` parametresi.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-254">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="ddcd9-255">Belirtin `Async` için geçiş [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="ddcd9-255">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="ddcd9-256">Merhaba komut hello küme hello komutu kabul eder ve hello uygulama türü hello kayıt zaman uyumsuz olarak devam ettiğinde döndürür.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-256">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span>
<span data-ttu-id="ddcd9-257">Bu nedenle, yoktur gerek toospecify daha yüksek bir zaman aşımı bu durumda.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-257">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="ddcd9-258">Merhaba [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) komutu tüm başarıyla kayıtlı uygulama türü sürümleri ve kayıt durumlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-258">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="ddcd9-259">Merhaba kaydı yapıldığında bu komut toodetermine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddcd9-259">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="ddcd9-260">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ddcd9-260">Next steps</span></span>
[<span data-ttu-id="ddcd9-261">Service Fabric uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="ddcd9-261">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="ddcd9-262">Service Fabric sistem durumu giriş</span><span class="sxs-lookup"><span data-stu-id="ddcd9-262">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="ddcd9-263">Tanılama ve bir Service Fabric hizmeti sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ddcd9-263">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="ddcd9-264">Service Fabric uygulamada modeli</span><span class="sxs-lookup"><span data-stu-id="ddcd9-264">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
