---
title: Azure Service Fabric uygulama aaaPackage | Microsoft Docs
description: "Nasıl toopackage tooa küme dağıtmadan önce bir Service Fabric uygulaması."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a><span data-ttu-id="822d6-103">Bir uygulama paketi</span><span class="sxs-lookup"><span data-stu-id="822d6-103">Package an application</span></span>
<span data-ttu-id="822d6-104">Bu makalede nasıl toopackage Service Fabric uygulama ve dağıtım için hazır olun.</span><span class="sxs-lookup"><span data-stu-id="822d6-104">This article describes how toopackage a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="822d6-105">Paket düzeni</span><span class="sxs-lookup"><span data-stu-id="822d6-105">Package layout</span></span>
<span data-ttu-id="822d6-106">Hello uygulama bildirimi, bir veya daha fazla hizmet bildirimleri ve diğer gerekli paketi dosyaları bir Service Fabric kümesi içine dağıtımı için belirli bir düzende düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="822d6-106">hello application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="822d6-107">Bu makalede Hello örnek bildirimleri aşağıdaki dizin yapısını hello düzenlenmiş toobe gerekir:</span><span class="sxs-lookup"><span data-stu-id="822d6-107">hello example manifests in this article would need toobe organized in hello following directory structure:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

<span data-ttu-id="822d6-108">Merhaba klasörleri toomatch hello adlı **adı** karşılık gelen her öğenin öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="822d6-108">hello folders are named toomatch hello **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="822d6-109">Örneğin, hello hizmet bildirimi hello adlara sahip iki farklı kod paketi içerdiği **MyCodeA** ve **MyCodeB**, her kod için gerekli ikili dosyaları aynı adları içerecektir hello iki klasörlerle hello sonra Paket.</span><span class="sxs-lookup"><span data-stu-id="822d6-109">For example, if hello service manifest contained two code packages with hello names **MyCodeA** and **MyCodeB**, then two folders with hello same names would contain hello necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="822d6-110">SetupEntryPoint kullanın</span><span class="sxs-lookup"><span data-stu-id="822d6-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="822d6-111">Kullanma için tipik senaryolar **SetupEntryPoint** toorun hello hizmet başlatılmadan önce yürütülebilir gerekir veya yükseltilmiş ayrıcalıklarla bir işlem tooperform ihtiyacınız olduğunda durumdadır.</span><span class="sxs-lookup"><span data-stu-id="822d6-111">Typical scenarios for using **SetupEntryPoint** are when you need toorun an executable before hello service starts or you need tooperform an operation with elevated privileges.</span></span> <span data-ttu-id="822d6-112">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="822d6-112">For example:</span></span>

* <span data-ttu-id="822d6-113">Ayarlama ve hizmet yürütülebilir gereksinimleri hello ortam değişkenleri başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="822d6-113">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="822d6-114">Bu sınırlı tooonly yürütülebilir dosyalar hello Service Fabric programlama modeli yazılmış değil.</span><span class="sxs-lookup"><span data-stu-id="822d6-114">It is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="822d6-115">Örneğin, bir node.js uygulamasını dağıtmak için yapılandırılmış bazı ortam değişkenleri npm.exe gerekir.</span><span class="sxs-lookup"><span data-stu-id="822d6-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="822d6-116">Güvenlik sertifikaları yükleyerek erişim denetimini ayarlama.</span><span class="sxs-lookup"><span data-stu-id="822d6-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="822d6-117">Hakkında daha fazla bilgi için tooconfigure hello **SetupEntryPoint**, bkz: [hizmet Kurulum giriş noktası için hello ilkesi yapılandırma](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="822d6-117">For more information on how tooconfigure hello **SetupEntryPoint**, see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="822d6-118">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="822d6-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="822d6-119">Visual Studio kullanarak bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="822d6-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="822d6-120">Visual Studio 2015 toocreate uygulamanızı kullanıyorsanız hello paket komutu tooautomatically yukarıda açıklanan hello düzeni eşleşen bir paket oluştur kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="822d6-120">If you use Visual Studio 2015 toocreate your application, you can use hello Package command tooautomatically create a package that matches hello layout described above.</span></span>

<span data-ttu-id="822d6-121">toocreate bir paket, Çözüm Gezgini'nde hello uygulama projesine sağ tıklayın ve aşağıda gösterildiği gibi hello Paketi komutu seçin:</span><span class="sxs-lookup"><span data-stu-id="822d6-121">toocreate a package, right-click hello application project in Solution Explorer and choose hello Package command, as shown below:</span></span>

![Visual Studio ile bir uygulama paketleme][vs-package-command]

<span data-ttu-id="822d6-123">Paketleme tamamlandığında hello paketi hello konumu hello bulabilirsiniz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="822d6-123">When packaging is complete, you can find hello location of hello package in hello **Output** window.</span></span> <span data-ttu-id="822d6-124">Visual Studio uygulamanızda hata ayıklama veya dağıttığınızda hello paketleme adım otomatik olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="822d6-124">hello packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="822d6-125">Komut satırı tarafından bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="822d6-125">Build a package by command line</span></span>
<span data-ttu-id="822d6-126">Ayrıca kullanarak uygulamanızı kurma olası tooprogrammatically paketi olan `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="822d6-126">It is also possible tooprogrammatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="822d6-127">Merhaba çıktı aynı olacak şekilde hello başlık altında Visual Studio çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="822d6-127">Under hello hood, Visual Studio is running it so hello output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a><span data-ttu-id="822d6-128">Sınama hello paketi</span><span class="sxs-lookup"><span data-stu-id="822d6-128">Test hello package</span></span>
<span data-ttu-id="822d6-129">Hello kullanarak yerel olarak PowerShell aracılığıyla hello paket yapısı doğrulayabilirsiniz [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) komutu.</span><span class="sxs-lookup"><span data-stu-id="822d6-129">You can verify hello package structure locally through PowerShell by using hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="822d6-130">Bu komut için bildirimi ayrıştırma sorunları denetler ve tüm başvuruları doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="822d6-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="822d6-131">Bu komut, yalnızca hello dizinleri ve dosyaları hello paketindeki yapısal doğruluğunu hello doğrular.</span><span class="sxs-lookup"><span data-stu-id="822d6-131">This command only verifies hello structural correctness of hello directories and files in hello package.</span></span>
<span data-ttu-id="822d6-132">Tüm gerekli dosyaların mevcut olduğunu denetleme ötesinde hello kod veya veri paket içeriğini hiçbirini doğrulamak değil.</span><span class="sxs-lookup"><span data-stu-id="822d6-132">It doesn't verify any of hello code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="822d6-133">Bu hello bu hatayı gösterir *MySetup.bat* hello hizmet bildiriminde başvurulan dosya **SetupEntryPoint** hello kod paketi eksik.</span><span class="sxs-lookup"><span data-stu-id="822d6-133">This error shows that hello *MySetup.bat* file referenced in hello service manifest **SetupEntryPoint** is missing from hello code package.</span></span> <span data-ttu-id="822d6-134">Merhaba eksik dosya eklendikten sonra hello uygulama doğrulama geçirir:</span><span class="sxs-lookup"><span data-stu-id="822d6-134">After hello missing file is added, hello application verification passes:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

<span data-ttu-id="822d6-135">Uygulamanız varsa, [uygulama parametreleri](service-fabric-manage-multiple-environment-app-configuration.md) tanımlanan, bunları geçirebilirsiniz [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) uygun doğrulama için.</span><span class="sxs-lookup"><span data-stu-id="822d6-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="822d6-136">Merhaba uygulaması dağıtılacağı hello küme biliyorsanız, hello geçirdiğiniz önerilir `ImageStoreConnectionString` parametresi.</span><span class="sxs-lookup"><span data-stu-id="822d6-136">If you know hello cluster where hello application will be deployed, it is recommended you pass in hello `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="822d6-137">Bu durumda, hello paketi de hello kümede çalışmakta olan önceki sürümlerini Merhaba uygulaması doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="822d6-137">In this case, hello package is also validated against previous versions of hello application that are already running in hello cluster.</span></span> <span data-ttu-id="822d6-138">Örneğin, hello doğrulama bir paket olup olmadığını tespit edebilirsiniz hello ile aynı sürümü ancak farklı içerik zaten dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="822d6-138">For example, hello validation can detect whether a package with hello same version but different content was already deployed.</span></span>  

<span data-ttu-id="822d6-139">Merhaba uygulaması doğru paketlenir ve doğrulama başarılı sonra değerlendirme sıkıştırma gerekirse hello boyutu ve dosya hello sayısı göre.</span><span class="sxs-lookup"><span data-stu-id="822d6-139">Once hello application is packaged correctly and passes validation, evaluate based on hello size and hello number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="822d6-140">Bir paket Sıkıştır</span><span class="sxs-lookup"><span data-stu-id="822d6-140">Compress a package</span></span>
<span data-ttu-id="822d6-141">Bir paket çok büyük veya çok sayıda dosya sahip olduğunda, daha hızlı dağıtımı için sıkıştırın.</span><span class="sxs-lookup"><span data-stu-id="822d6-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="822d6-142">Sıkıştırma, dosyaları ve başlangıç paket boyutu hello sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="822d6-142">Compression reduces hello number of files and hello package size.</span></span>
<span data-ttu-id="822d6-143">Sıkıştırılmış uygulama paketi için [Uploading hello uygulama paketi](service-fabric-deploy-remove-applications.md#upload-the-application-package) (özel sıkıştırma zaman hesaba katıldığında varsa) artık karşılaştırılan toouploading hello sıkıştırılmamış paketi sürebilir ancak [kaydetme](service-fabric-deploy-remove-applications.md#register-the-application-package) ve [kayıt hello uygulama türü](service-fabric-deploy-remove-applications.md#unregister-an-application-type) sıkıştırılmış uygulama paketi için daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="822d6-143">For a compressed application package, [Uploading hello application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared toouploading hello uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering hello application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="822d6-144">Merhaba dağıtım için sıkıştırılmış ve sıkıştırılmamış paketleri aynı mekanizmadır.</span><span class="sxs-lookup"><span data-stu-id="822d6-144">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="822d6-145">Hello paket sıkıştırılmışsa, bu nedenle hello küme görüntü deposunda depolanır ve hello uygulamayı çalıştırmadan önce hello düğümde sıkıştırılmamış.</span><span class="sxs-lookup"><span data-stu-id="822d6-145">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>
<span data-ttu-id="822d6-146">Merhaba sıkıştırma hello geçerli Service Fabric paketi hello sıkıştırılmış sürümüyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="822d6-146">hello compression replaces hello valid Service Fabric package with hello compressed version.</span></span> <span data-ttu-id="822d6-147">Başlangıç klasörü yazma izni izin vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="822d6-147">hello folder must allow write permissions.</span></span> <span data-ttu-id="822d6-148">Sıkıştırma zaten sıkıştırılmış bir paketi çalıştıran herhangi bir değişiklik verir.</span><span class="sxs-lookup"><span data-stu-id="822d6-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="822d6-149">Merhaba Powershell komutunu çalıştırarak bir paket sıkıştırabilirsiniz [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) ile `CompressPackage` geçin.</span><span class="sxs-lookup"><span data-stu-id="822d6-149">You can compress a package by running hello Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="822d6-150">Merhaba sıkıştırmasını hello ile aynı paketini komutunu `UncompressPackage` geçin.</span><span class="sxs-lookup"><span data-stu-id="822d6-150">You can uncompress hello package with hello same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="822d6-151">Merhaba aşağıdaki komutu hello paket toohello Image store kopyalamadan sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="822d6-151">hello following command compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="822d6-152">Kullanarak, gerektiği kadar bir sıkıştırılmış paket tooone veya daha fazla Service Fabric kümeleri kopyalayabilirsiniz [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) hello olmadan `SkipCopy` bayrağı.</span><span class="sxs-lookup"><span data-stu-id="822d6-152">You can copy a compressed package tooone or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without hello `SkipCopy` flag.</span></span>
<span data-ttu-id="822d6-153">Merhaba paket artık hello sıkıştırılmış dosyaları içerir `code`, `config`, ve `data` paketler.</span><span class="sxs-lookup"><span data-stu-id="822d6-153">hello package now includes zipped files for hello `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="822d6-154">birçok dahili işlemleri (örneğin, paket paylaşımı, belirli doğrulamaları için uygulama türü adı ve sürümü ayıklama) için gerekli olduğu için hello uygulama bildirimi ve hello hizmeti bildirimleri, daraltılmış değil.</span><span class="sxs-lookup"><span data-stu-id="822d6-154">hello application manifest and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="822d6-155">Sıkıştırma hello bildirimleri bu işlemleri verimli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="822d6-155">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

<span data-ttu-id="822d6-156">Alternatif olarak, sıkıştırma ve kopyalama hello paketiyle [kopya ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) tek bir adımda.</span><span class="sxs-lookup"><span data-stu-id="822d6-156">Alternatively, you can compress and copy hello package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="822d6-157">Merhaba paket büyükse hello paket sıkıştırma ve hello karşıya yükleme toohello küme için yeterince zaman aşımı tooallow zaman sağlar.</span><span class="sxs-lookup"><span data-stu-id="822d6-157">If hello package is large, provide a high enough timeout tooallow time for both hello package compression and hello upload toohello cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="822d6-158">Dahili olarak, Service Fabric sağlama toplamı doğrulaması için hello uygulama paketleri için hesaplar.</span><span class="sxs-lookup"><span data-stu-id="822d6-158">Internally, Service Fabric computes checksums for hello application packages for validation.</span></span> <span data-ttu-id="822d6-159">Sıkıştırma kullanırken hello sağlama her paketi sürümleri daraltılmış hello üzerinde hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="822d6-159">When using compression, hello checksums are computed on hello zipped versions of each package.</span></span>
<span data-ttu-id="822d6-160">Sıkıştırılmamış bir uygulama paketinizi kopyalanır ve hello toouse sıkıştırma istiyorsanız aynı paketin hello hello sürümleri değiştirmelisiniz `code`, `config`, ve `data` paketleri tooavoid sağlama toplamı eşleşmezliği.</span><span class="sxs-lookup"><span data-stu-id="822d6-160">If you copied an uncompressed version of your application package, and you want toouse compression for hello same package, you must change hello versions of hello `code`, `config`, and `data` packages tooavoid checksum mismatch.</span></span> <span data-ttu-id="822d6-161">Merhaba paketleri, hello sürümünü değiştirme yerine, değişmeden varsa, kullanabileceğiniz [fark sağlama](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="822d6-161">If hello packages are unchanged, instead of changing hello version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="822d6-162">Bu seçenek ile Merhaba değişmeden paket dahil etmeyin yerine hello hizmet bildirimden başvuru.</span><span class="sxs-lookup"><span data-stu-id="822d6-162">With this option, do not include hello unchanged package instead reference it from hello service manifest.</span></span>

<span data-ttu-id="822d6-163">Benzer şekilde, hello paketin sıkıştırılmış bir sürümünü karşıya ve sıkıştırılmamış bir paket toouse istediğiniz hello sürümleri tooavoid hello sağlama toplamı eşleşmezliği güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="822d6-163">Similarly, if you uploaded a compressed version of hello package and you want toouse an uncompressed package, you must update hello versions tooavoid hello checksum mismatch.</span></span>

<span data-ttu-id="822d6-164">Merhaba paket artık doğru paketlenmiş doğrulandı ve için hazır olması için (gerekirse), sıkıştırılmış [dağıtım](service-fabric-deploy-remove-applications.md) tooone ya da daha fazla Service Fabric kümeleri.</span><span class="sxs-lookup"><span data-stu-id="822d6-164">hello package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) tooone or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="822d6-165">Visual Studio kullanarak dağıtırken paketleri Sıkıştır</span><span class="sxs-lookup"><span data-stu-id="822d6-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="822d6-166">Merhaba ekleyerek dağıtım, Visual Studio toocompress paketleri söyleyebilirsiniz `CopyPackageParameters` öğesi tooyour yayımlama profili ve ayarlama hello `CompressPackage` çok öznitelik`true`.</span><span class="sxs-lookup"><span data-stu-id="822d6-166">You can instruct Visual Studio toocompress packages on deployment, by adding hello `CopyPackageParameters` element tooyour publish profile, and set hello `CompressPackage` attribute too`true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="822d6-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="822d6-167">Next steps</span></span>
<span data-ttu-id="822d6-168">[Dağıtma ve uygulamaları kaldırma] [ 10] açıklar nasıl toouse PowerShell toomanage uygulama örnekleri</span><span class="sxs-lookup"><span data-stu-id="822d6-168">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances</span></span>

<span data-ttu-id="822d6-169">[Birden çok ortamlar için uygulama parametreleri yönetme] [ 11] açıklar nasıl tooconfigure parametreleri ve farklı uygulama örnekleri için ortam değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="822d6-169">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="822d6-170">[Uygulamanız için güvenlik ilkelerini yapılandırmak] [ 12] toorun güvenlik ilkeleri toorestrict erişim'in altında hizmetleri nasıl açıklar.</span><span class="sxs-lookup"><span data-stu-id="822d6-170">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
