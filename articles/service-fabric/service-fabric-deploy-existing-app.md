---
title: "Varolan bir yürütülebilir tooAzure Service Fabric aaaDeploy | Microsoft Docs"
description: "Var olan bir uygulamayı, böylece bir konuk yürütülebilir olarak toopackage tooa Service Fabric kümesi nasıl dağıtılacağını üzerinde gözden geçirme"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="6ed24-103">Bir konuk yürütülebilir tooService doku dağıtma</span><span class="sxs-lookup"><span data-stu-id="6ed24-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="6ed24-104">Azure Service Fabric kod, Node.js, Java ya da C++ gibi herhangi bir türde bir hizmet olarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="6ed24-105">Service Fabric toothese türlerdeki Hizmetleri Konuk yürütülebilir dosyalar ifade eder.</span><span class="sxs-lookup"><span data-stu-id="6ed24-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="6ed24-106">Konuk yürütülebilir dosyalar gibi durum bilgisi olmayan hizmetler Service Fabric tarafından kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="6ed24-107">Sonuç olarak, bunlar kullanılabilirlik ve diğer ölçümleri temelinde, bir kümedeki düğümlere yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="6ed24-108">Bu makalede nasıl toopackage ve Visual Studio veya komut satırı yardımcı programını kullanarak bir konuk yürütülebilir tooa Service Fabric kümesi dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="6ed24-109">Bu makalede, hello adımları toopackage yürütülebilir Konuk kapsar ve tooService doku dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="6ed24-110">Service Fabric yürütülebilir Konuk çalıştıran avantajları</span><span class="sxs-lookup"><span data-stu-id="6ed24-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="6ed24-111">Bir Service Fabric kümesi yürütülebilir Konuk birkaç avantaj toorunning vardır:</span><span class="sxs-lookup"><span data-stu-id="6ed24-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="6ed24-112">Yüksek kullanılabilirlik.</span><span class="sxs-lookup"><span data-stu-id="6ed24-112">High availability.</span></span> <span data-ttu-id="6ed24-113">Service Fabric çalışan uygulamaları yüksek oranda kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="6ed24-114">Service Fabric uygulaması örneğini çalıştırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ed24-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="6ed24-115">Sistem durumu izleme.</span><span class="sxs-lookup"><span data-stu-id="6ed24-115">Health monitoring.</span></span> <span data-ttu-id="6ed24-116">Service Fabric sistem durumu izleme uygulama çalışıp çalışmadığını ve bir hata olduğunda tanılama bilgileri sağlayan olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="6ed24-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="6ed24-117">Uygulama yaşam döngüsü yönetimi.</span><span class="sxs-lookup"><span data-stu-id="6ed24-117">Application lifecycle management.</span></span> <span data-ttu-id="6ed24-118">Yükseltme sırasında bildirilen hatalı sistem durumu olayı ise yükseltmeler kapalı kalma süresi ile sağlamanın yanı sıra, Service Fabric otomatik geri alma toohello önceki sürümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ed24-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="6ed24-119">Yoğunluğu.</span><span class="sxs-lookup"><span data-stu-id="6ed24-119">Density.</span></span> <span data-ttu-id="6ed24-120">Her uygulama toorun kendi donanımda hello ihtiyacını ortadan kaldıran bir kümede birden çok uygulama çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="6ed24-121">Bulunabilirliği: REST kullanarak hello kümedeki diğer hizmetler hello Service Fabric adlandırma hizmeti toofind çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="6ed24-122">Örnekler</span><span class="sxs-lookup"><span data-stu-id="6ed24-122">Samples</span></span>
* [<span data-ttu-id="6ed24-123">Paketleme ve dağıtma bir konuk yürütülebilir dosyası için örnek</span><span class="sxs-lookup"><span data-stu-id="6ed24-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="6ed24-124">İki Konuk yürütülebilir dosyalar (C# ve nodejs) iletişim REST kullanarak hello Adlandırma Hizmeti örnek</span><span class="sxs-lookup"><span data-stu-id="6ed24-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="6ed24-125">Uygulama ve hizmet bildirim dosyaları'na genel bakış</span><span class="sxs-lookup"><span data-stu-id="6ed24-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="6ed24-126">Bir konuk yürütülebilir dağıtma bir parçası olarak yararlı toounderstand hello Service Fabric paketleme ve dağıtım modeli açıklandığı gibi olmasından [uygulama modeli](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="6ed24-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="6ed24-127">Hello Service Fabric paketleme model üzerinde iki XML dosyasını kullanır: uygulama ve hizmet bildirimlerini hello.</span><span class="sxs-lookup"><span data-stu-id="6ed24-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="6ed24-128">Merhaba şema tanımı hello ApplicationManifest.xml ve ServiceManifest.xml dosyaları yüklü olduğunda ile Merhaba Service Fabric SDK içine *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="6ed24-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="6ed24-129">**Uygulama bildirimini** hello uygulama bildirimidir kullanılan toodescribe Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6ed24-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="6ed24-130">Onu oluşturan hello Hizmetleri ve örnek hello sayısı gibi nasıl bir veya daha fazla hizmet dağıtılmalıdır kullanılan toodefine olan diğer parametreleri listeler.</span><span class="sxs-lookup"><span data-stu-id="6ed24-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="6ed24-131">Service Fabric bir uygulama dağıtımı ve yükseltmesi birimidir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="6ed24-132">Bir uygulama olası hataları ve olası düzeyine yönetildiği tek bir birim olarak yükseltilebilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="6ed24-133">Service Fabric garanti hello yükseltme işlemi şunlardan biri olduğundan başarılı ya da hello yükseltme başarısız olursa Merhaba uygulaması bilinmeyen veya kararsız bir durumda bırakmaz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="6ed24-134">**Hizmet bildirimi** hello hizmet bildirimi hello hizmet bileşenlerinin açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ed24-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="6ed24-135">Merhaba adı ve hizmet türü gibi veri ve kod ve yapılandırma içerir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="6ed24-136">Merhaba hizmet bildirimi de olabilecek bazı ek parametreleri içeren tooconfigure hello hizmet dağıtıldıktan sonra kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="6ed24-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="6ed24-137">Uygulama paketi dosya yapısı</span><span class="sxs-lookup"><span data-stu-id="6ed24-137">Application package file structure</span></span>
<span data-ttu-id="6ed24-138">bir uygulama tooService doku toodeploy Merhaba uygulaması tanımlanmış dizin yapısına uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6ed24-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="6ed24-139">Merhaba, bu yapıyı örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-139">hello following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="6ed24-140">Merhaba ApplicationPackageRoot Merhaba uygulaması tanımlayan hello ApplicationManifest.xml dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="6ed24-141">Merhaba uygulamasına dahil edilen her hizmet için bir alt tüm hello hizmeti gerektiren yapıları hello kullanılan toocontain ' dir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="6ed24-142">Bu alt dizinlere hello ServiceManifest.xml ve genellikle aşağıdaki hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6ed24-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="6ed24-143">*Kod*.</span><span class="sxs-lookup"><span data-stu-id="6ed24-143">*Code*.</span></span> <span data-ttu-id="6ed24-144">Bu dizin hello servis kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="6ed24-145">*Config*. Bu dizin, hello hizmeti çalışma zamanı tooretrieve belirli yapılandırma ayarları erişebilmesini Settings.xml dosya (ve gerekirse diğer dosyaları) içerir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="6ed24-146">*Veri*.</span><span class="sxs-lookup"><span data-stu-id="6ed24-146">*Data*.</span></span> <span data-ttu-id="6ed24-147">Merhaba hizmeti gereken bir ek dizin toostore ek yerel veri budur.</span><span class="sxs-lookup"><span data-stu-id="6ed24-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="6ed24-148">Veri kullanılan toostore yalnızca geçici veri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="6ed24-149">Merhaba hizmetinin (örneğin, yük devretme sırasında) yeniden konumlandırılmasını toobe gerekirse Service Fabric değil kopyalama veya çoğaltılacak değişiklikleri toohello veri dizini yok.</span><span class="sxs-lookup"><span data-stu-id="6ed24-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="6ed24-150">Toocreate hello yok `config` ve `data` ihtiyaç duymuyorsanız dizinleri.</span><span class="sxs-lookup"><span data-stu-id="6ed24-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="6ed24-151">Paketin var olan bir yürütülebilir dosya</span><span class="sxs-lookup"><span data-stu-id="6ed24-151">Package an existing executable</span></span>
<span data-ttu-id="6ed24-152">Bir konuk yürütülebilir paketleme, Visual Studio Proje şablonu ya da toouse seçebilirsiniz veya çok[hello uygulama paketini el ile oluşturmak](#manually).</span><span class="sxs-lookup"><span data-stu-id="6ed24-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="6ed24-153">Visual Studio kullanarak, uygulama paketinin yapısı hello ve bildirim dosyası hello yeni proje şablonu tarafından sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6ed24-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="6ed24-154">Merhaba en kolay yolu toopackage bir hizmete yürütülebilir bir mevcut Windows olduğu toouse Visual Studio ve Linux toouse Yeoman</span><span class="sxs-lookup"><span data-stu-id="6ed24-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="6ed24-155">Visual Studio toopackage kullanın ve var olan bir yürütülebilir dosya dağıtma</span><span class="sxs-lookup"><span data-stu-id="6ed24-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="6ed24-156">Visual Studio Service Fabric Konuk yürütülebilir tooa Service Fabric küme dağıtma hizmet şablonu toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ed24-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="6ed24-157">Seçin **dosya** > **yeni proje**ve bir Service Fabric uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ed24-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="6ed24-158">Seçin **Konuk yürütülebilir** hello hizmet şablonu olarak.</span><span class="sxs-lookup"><span data-stu-id="6ed24-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="6ed24-159">Tıklatın **Gözat** tooselect hello klasörüyle çalıştırılabilir ve hello rest hello parametreleri toocreate hello hizmetinin doldurun.</span><span class="sxs-lookup"><span data-stu-id="6ed24-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="6ed24-160">*Kod paketi davranış*.</span><span class="sxs-lookup"><span data-stu-id="6ed24-160">*Code Package Behavior*.</span></span> <span data-ttu-id="6ed24-161">Set toocopy hello yürütülebilir değişmezse faydalı olan, klasör toohello Visual Studio projesi, tüm başlangıç içeriğini olabilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="6ed24-162">Hello yürütülebilir toochange beklediğiniz ve dinamik olarak hello özelliği toopick yeni yapılar yedeklemek istiyorsanız, bunun yerine toolink toohello klasör seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="6ed24-163">Visual Studio'da hello uygulama projesi oluştururken, bağlantılı klasörleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="6ed24-164">Bu toohello kaynak konumdan yürütülebilir kaynak hedefine, tooupdate hello Konuk için olası kolaylaştırarak hello projede bağlar.</span><span class="sxs-lookup"><span data-stu-id="6ed24-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="6ed24-165">Bu güncelleştirmeler derlemede hello uygulama paketinin parçası haline gelir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="6ed24-166">*Program* toostart hello hizmet çalıştırılmalıdır hello yürütülebilir dosya belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="6ed24-167">*Bağımsız değişkenler* toohello yürütülebilir iletilmesi gereken hello bağımsız değişkenlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="6ed24-168">Bağımsız değişkenlerle parametrelerin listesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="6ed24-169">*WorkingFolder* başlatılan toobe geçiyor hello işlem hello çalışma dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="6ed24-170">Üç değerleri belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6ed24-170">You can specify three values:</span></span>
     * <span data-ttu-id="6ed24-171">`CodeBase`Bu hello çalışma dizini toobe hello uygulama paketinde toohello kod dizini ayarlanmış olduğuna belirtir (`Code` dosya yapısı önceki hello gösterilen dizin).</span><span class="sxs-lookup"><span data-stu-id="6ed24-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="6ed24-172">`CodePackage`Bu hello çalışma dizini toobe ayarlamak toohello kök hello uygulama paketinin olduğuna belirtir (`GuestService1Pkg` dosya yapısı önceki hello gösterilen).</span><span class="sxs-lookup"><span data-stu-id="6ed24-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="6ed24-173">`Work`Merhaba dosyaları iş adlı bir alt dizinde yerleştirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="6ed24-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="6ed24-174">Hizmetinize bir ad verin ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="6ed24-175">Hizmet iletişimi için bir uç nokta gerekiyorsa, artık hello protokolü, bağlantı noktası ve türü toohello ServiceManifest.xml dosya ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="6ed24-176">Örneğin: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="6ed24-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="6ed24-177">Şimdi, hello paketini kullanmak ve eylem hello çözümü Visual Studio'da hata ayıklama yerel kümenizdeki karşı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="6ed24-178">Hazır olduğunuzda, yayımlama hello uygulama tooa uzaktan küme veya hello çözüm toosource denetiminde denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6ed24-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="6ed24-179">Bu makale toosee toohello sonuna nasıl Git tooview Service Fabric Explorer'da çalıştıran Konuk yürütülebilir hizmetinizi.</span><span class="sxs-lookup"><span data-stu-id="6ed24-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="6ed24-180">Yoeman toopackage kullanın ve var olan bir yürütülebilir dosya Linux'ta dağıtma</span><span class="sxs-lookup"><span data-stu-id="6ed24-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="6ed24-181">oluşturma ve dağıtma Linux'ta yürütülebilir Konuk hello yordamı olduğu hello csharp veya java uygulamasını dağıtma aynı.</span><span class="sxs-lookup"><span data-stu-id="6ed24-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="6ed24-182">Bir terminal penceresinde `yo azuresfguest` yazın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="6ed24-183">Uygulamanızı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-183">Name your application.</span></span>
3. <span data-ttu-id="6ed24-184">Hizmet adı ve hello yürütülebilir dosya yolu ve hello parametreleri ile çağrılmalıdır gibi hello ayrıntıları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="6ed24-185">Yeoman hello uygun uygulama ile bir uygulama paketi oluşturur ve bildirim dosyası ile birlikte yüklemek ve komut dosyaları kaldırmak.</span><span class="sxs-lookup"><span data-stu-id="6ed24-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="6ed24-186">El ile paketini ve varolan yürütülebilir bir dağıtma</span><span class="sxs-lookup"><span data-stu-id="6ed24-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="6ed24-187">bir konuk yürütülebilir dosyayı el ile paketleme hello işlemi aşağıdaki genel adımları hello üzerinde dayanır:</span><span class="sxs-lookup"><span data-stu-id="6ed24-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="6ed24-188">Merhaba paket dizin yapısını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ed24-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="6ed24-189">Merhaba uygulamanın kod ve yapılandırma dosyalarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6ed24-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="6ed24-190">Merhaba hizmet bildirim dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="6ed24-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="6ed24-191">Merhaba uygulama bildirim dosyasının düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="6ed24-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="6ed24-192">Merhaba paket dizin yapısını oluşturun</span><span class="sxs-lookup"><span data-stu-id="6ed24-192">Create hello package directory structure</span></span>
<span data-ttu-id="6ed24-193">Merhaba dizin yapısını oluşturarak bölümünde, önceki hello açıklandığı gibi başlatabilirsiniz "Uygulama paketi dosya yapısı."</span><span class="sxs-lookup"><span data-stu-id="6ed24-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="6ed24-194">Merhaba uygulamanın kod ve yapılandırma dosyaları Ekle</span><span class="sxs-lookup"><span data-stu-id="6ed24-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="6ed24-195">Merhaba dizin yapısını oluşturduktan sonra hello kod ve yapılandırma dizinleri altında hello uygulamanın kod ve yapılandırma dosyaları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="6ed24-196">Ek dizinler veya hello kod veya yapılandırma dizinleri alt dizinler de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="6ed24-197">Service Fabric mu bir `xcopy` hello içeriğiyle nedenle iki üst dizini, kod ve ayarları oluşturma dışında hiçbir önceden tanımlanmış yapısı toouse hello uygulama kök dizini.</span><span class="sxs-lookup"><span data-stu-id="6ed24-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="6ed24-198">(Dilerseniz farklı adlar seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-198">(You can pick different names if you want.</span></span> <span data-ttu-id="6ed24-199">Daha fazla ayrıntı hello sonraki bölümünde bulunur.)</span><span class="sxs-lookup"><span data-stu-id="6ed24-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="6ed24-200">Tüm hello dosyaları ve uygulama gereksinimlerini hello bağımlılıkları eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="6ed24-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="6ed24-201">Service Fabric hello uygulamanın Hizmetleri dağıtılan giderek toobe nerede hello kümede hello tüm düğümlerde hello uygulama paketi içeriği kopyalar.</span><span class="sxs-lookup"><span data-stu-id="6ed24-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="6ed24-202">Merhaba paket Merhaba uygulaması toorun ihtiyaç duyduğu tüm hello kodu içermelidir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="6ed24-203">Merhaba bağımlılıkları zaten kurulu olduğunu varsayın değil.</span><span class="sxs-lookup"><span data-stu-id="6ed24-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="6ed24-204">Merhaba hizmet bildirim dosyasını düzenleyin</span><span class="sxs-lookup"><span data-stu-id="6ed24-204">Edit hello service manifest file</span></span>
<span data-ttu-id="6ed24-205">Hello sonraki adıma tooedit hello hizmet bildirim dosyası tooinclude hello bilgi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="6ed24-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="6ed24-206">Merhaba hizmet türünün Hello adı.</span><span class="sxs-lookup"><span data-stu-id="6ed24-206">hello name of hello service type.</span></span> <span data-ttu-id="6ed24-207">Bu, Service Fabric tooidentify bir hizmeti kullanan bir kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="6ed24-208">Merhaba komutu toouse toolaunch hello uygulaması (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="6ed24-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="6ed24-209">Toobe gereken komut dosyaları tooset hello uygulamasının (SetupEntrypoint) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="6ed24-210">Merhaba örneği aşağıdadır bir `ServiceManifest.xml` dosyası:</span><span class="sxs-lookup"><span data-stu-id="6ed24-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="6ed24-211">Aşağıdaki bölümlerde hello hello farklı kısımlarını tooupdate gerektiğini hello dosya gidin.</span><span class="sxs-lookup"><span data-stu-id="6ed24-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="6ed24-212">Güncelleştirme ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="6ed24-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="6ed24-213">İstediğiniz herhangi bir ad seçin `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="6ed24-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="6ed24-214">Merhaba değeri hello kullanılan `ApplicationManifest.xml` dosya tooidentify hello hizmeti.</span><span class="sxs-lookup"><span data-stu-id="6ed24-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="6ed24-215">Belirtin `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="6ed24-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="6ed24-216">Bu öznitelik Service Fabric söyler hello hizmeti kendi başına bir uygulama üzerinde temel, gerekli tüm Service Fabric toolaunch toodo olduğundan bir işlem olarak ve durumunu izleyin.</span><span class="sxs-lookup"><span data-stu-id="6ed24-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="6ed24-217">CodePackage güncelleştir</span><span class="sxs-lookup"><span data-stu-id="6ed24-217">Update CodePackage</span></span>
<span data-ttu-id="6ed24-218">Merhaba CodePackage öğesi hello hizmetin kod hello konumu (ve sürüm) belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="6ed24-219">Merhaba `Name` öğesidir hello directory hello uygulama hello hizmetin kodu içeren bir paket içinde kullanılan toospecify hello adı.</span><span class="sxs-lookup"><span data-stu-id="6ed24-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="6ed24-220">`CodePackage`Ayrıca hello sahip `version` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="6ed24-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="6ed24-221">Bu kullanılan toospecify hello hello kod sürümü olabilir ve aynı zamanda potansiyel olabilir Service Fabric hello uygulama yaşam döngüsü yönetimi altyapısını kullanarak tooupgrade hello hizmetin kod kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6ed24-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="6ed24-222">İsteğe bağlı: Güncelleştirme SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="6ed24-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="6ed24-223">Merhaba SetupEntryPoint öğesi kullanılan toospecify hello hizmetin kod başlatılmadan önce yürütülüp herhangi çalıştırılabilir veya toplu iş dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="6ed24-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="6ed24-224">Başlatma gerekli ise dahil toobe gerek kalmayacak şekilde isteğe bağlı bir adım var.</span><span class="sxs-lookup"><span data-stu-id="6ed24-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="6ed24-225">Merhaba hizmeti her başlatıldığında hello SetupEntryPoint yürütülür.</span><span class="sxs-lookup"><span data-stu-id="6ed24-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="6ed24-226">Olmadığından tek SetupEntryPoint Kurulum betikleri hello uygulamanın kurulum birden çok komut dosyası gerektiriyorsa tek toplu iş dosyasında gruplandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="6ed24-227">Merhaba SetupEntryPoint tüm dosya türlerinin yürütebilirsiniz: yürütülebilir dosyaları, toplu iş dosyaları ve PowerShell cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="6ed24-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="6ed24-228">Daha fazla ayrıntı için bkz: [yapılandırma SetupEntryPoint](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="6ed24-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="6ed24-229">Örnek önceki hello hello SetupEntryPoint adlı bir toplu iş dosyasını çalıştırır `LaunchConfig.cmd` diğer bir deyişle bulunan hello `scripts` alt hello kod dizini (Merhaba WorkingFolder öğesi tooCodeBase ayarlanmış olduğu varsayılarak).</span><span class="sxs-lookup"><span data-stu-id="6ed24-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="6ed24-230">EntryPoint güncelleştir</span><span class="sxs-lookup"><span data-stu-id="6ed24-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="6ed24-231">Merhaba `EntryPoint` hello hizmet bildirim dosyasında öğedir kullanılan toospecify nasıl toolaunch hello hizmet.</span><span class="sxs-lookup"><span data-stu-id="6ed24-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="6ed24-232">Merhaba `ExeHost` öğesi belirttiğinden hello yürütülebilir (ve bağımsız değişkenler) olması gereken toolaunch hello hizmeti kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6ed24-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="6ed24-233">`Program`Merhaba hello hizmet başlaması gereken hello yürütülebilir dosyanın adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="6ed24-234">`Arguments`toohello yürütülebilir iletilmesi gereken hello bağımsız değişkenlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="6ed24-235">Bağımsız değişkenlerle parametrelerin listesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="6ed24-236">`WorkingFolder`başlatılan toobe geçiyor hello işlem Hello çalışma dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="6ed24-237">Üç değerleri belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6ed24-237">You can specify three values:</span></span>
  * <span data-ttu-id="6ed24-238">`CodeBase`Bu hello çalışma dizini toobe hello uygulama paketinde toohello kod dizini ayarlanmış olduğuna belirtir (`Code` dosya yapısı önceki hello dizin).</span><span class="sxs-lookup"><span data-stu-id="6ed24-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="6ed24-239">`CodePackage`Bu hello çalışma dizini toobe ayarlamak toohello kök hello uygulama paketinin olduğuna belirtir (`GuestService1Pkg` dosya yapısı önceki hello içinde).</span><span class="sxs-lookup"><span data-stu-id="6ed24-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="6ed24-240">`Work`Merhaba dosyaları iş adlı bir alt dizinde yerleştirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="6ed24-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="6ed24-241">Merhaba WorkingFolder yararlı tooset hello doğru çalışma dizini, böylelikle göreli yollar ya da hello uygulama veya başlatma komut dosyaları tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="6ed24-242">Uç noktaları güncelleştirin ve iletişim için adlandırma hizmetine kaydetme</span><span class="sxs-lookup"><span data-stu-id="6ed24-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="6ed24-243">Örnek önceki hello hello `Endpoint` öğesi Merhaba uygulaması üzerinde dinleme hello uç noktalarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="6ed24-244">Bu örnekte, hello Node.js uygulaması HTTP 3000 bağlantı noktasında dinler.</span><span class="sxs-lookup"><span data-stu-id="6ed24-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="6ed24-245">Ayrıca diğer hizmetler hello uç noktası adresi toothis hizmeti bulabilir şekilde Bu uç nokta toohello Naming Service Service Fabric toopublish sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="6ed24-246">Bu, Konuk yürütülebilir hizmetleri arasında toobe mümkün toocommunicate sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ed24-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="6ed24-247">Merhaba yayımlanan uç noktası adresi hello biçimidir `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="6ed24-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="6ed24-248">`UriScheme`ve `PathSuffix` isteğe bağlı öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="6ed24-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="6ed24-249">`IPAddressOrFQDN`IP adresi veya tam etki alanı adı bu yürütülebilir dosya üzerine yerleştirilen hello düğümünün hello ve sizin için hesaplanır ' dir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="6ed24-250">Merhaba aşağıdaki örnekte, bir kez hello hizmet dağıtılır, Service Fabric Explorer'da benzer bir uç nokta çok gördüğünüz`http://10.1.4.92:3000/myapp/` hello hizmet örneği için yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="6ed24-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="6ed24-251">Veya yerel makine varsa gördüğünüz `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="6ed24-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="6ed24-252">Bu adresleri ile kullanabileceğiniz [ters proxy](service-fabric-reverseproxy.md) toocommunicate hizmetleri arasında.</span><span class="sxs-lookup"><span data-stu-id="6ed24-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="6ed24-253">Merhaba uygulama bildirim dosyasının Düzenle</span><span class="sxs-lookup"><span data-stu-id="6ed24-253">Edit hello application manifest file</span></span>
<span data-ttu-id="6ed24-254">Merhaba yapılandırdıktan sonra `Servicemanifest.xml` dosya, bazı değişiklikler toohello toomake gerek `ApplicationManifest.xml` hello tooensure doğru hizmet türü ve adı kullanılan dosya.</span><span class="sxs-lookup"><span data-stu-id="6ed24-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="6ed24-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="6ed24-255">ServiceManifestImport</span></span>
<span data-ttu-id="6ed24-256">Merhaba, `ServiceManifestImport` öğesi hello uygulamasında tooinclude istediğiniz bir veya daha fazla hizmet belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="6ed24-257">Hizmetleri ile başvurulan `ServiceManifestName`, hello burada hello hello dizinin adını belirtir `ServiceManifest.xml` dosyasının bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="6ed24-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="6ed24-258">Günlük ayarlama</span><span class="sxs-lookup"><span data-stu-id="6ed24-258">Set up logging</span></span>
<span data-ttu-id="6ed24-259">Hello uygulama ve yapılandırma betikleri hataları göster Konuk yürütülebilir dosyaları için bu yararlı toobe mümkün toosee konsol günlükleri toofind çıkışı olur.</span><span class="sxs-lookup"><span data-stu-id="6ed24-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="6ed24-260">Konsol yeniden yönlendirmesi hello yapılandırılabilir `ServiceManifest.xml` hello kullanarak dosyayı `ConsoleRedirection` öğesi.</span><span class="sxs-lookup"><span data-stu-id="6ed24-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="6ed24-261">Hiçbir zaman bu hello uygulama yük devretme etkileyebileceğinden üretimde dağıtılan bir uygulamada hello konsol yeniden yönlendirme ilkesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="6ed24-262">*Yalnızca* bunu yerel geliştirme ve hata ayıklama amacıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-262">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="6ed24-263">`ConsoleRedirection`kullanılan tooredirect konsol çıkış (stdout ve stderr) tooa çalışma dizini olabilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="6ed24-264">Bu hatalar hiçbir hello Kurulum veya hello Service Fabric kümesi hello uygulamada yürütülmesi sırasında hello özelliği tooverify sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ed24-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="6ed24-265">`FileRetentionCount`kaç tane dosyaları hello çalışma dizinindeki kaydedilir belirler.</span><span class="sxs-lookup"><span data-stu-id="6ed24-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="6ed24-266">Örneğin, 5, değeri hello önceki beş yürütmeleri için hello günlük dosyalarını hello çalışma dizininde depolanır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="6ed24-267">`FileMaxSizeInKb`Merhaba hello günlük dosyalarının en büyük boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="6ed24-268">Günlük dosyaları hello hizmetin çalışma dizinleri birinde kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="6ed24-269">Merhaba dosyalarının bulunduğu toodetermine hangi düğümün hello hizmetinin çalıştığını ve hangi çalışma dizini kullanılan Service Fabric Explorer toodetermine kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="6ed24-270">Bu işlem, bu makalenin sonraki bölümlerinde ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6ed24-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="6ed24-271">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="6ed24-271">Deployment</span></span>
<span data-ttu-id="6ed24-272">Merhaba son adımdır çok[uygulamanızı dağıtmak](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="6ed24-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="6ed24-273">PowerShell komut dosyası gösterilmektedir nasıl aşağıdaki hello toodeploy uygulama toohello yerel geliştirme küme ve yeni bir Service Fabric hizmetini başlatın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="6ed24-274">[Merhaba paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) hello paketi büyük veya çok sayıda dosya varsa toohello Image store kopyalamadan önce.</span><span class="sxs-lookup"><span data-stu-id="6ed24-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="6ed24-275">Daha fazla bilgi [burada](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="6ed24-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="6ed24-276">Service Fabric hizmeti çeşitli "yapılandırmalarında." dağıtılabilir</span><span class="sxs-lookup"><span data-stu-id="6ed24-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="6ed24-277">Örneğin, tek veya birden çok örneği dağıtılabilir veya hello Service Fabric kümesinin her bir düğümde hello Hizmeti'nin bir örneğini olduğunu şekilde dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="6ed24-278">Merhaba `InstanceCount` hello parametresinin `New-ServiceFabricService` cmdlet'tir kullanılan toospecify kaç tane hello hizmet örneğinin hello Service Fabric kümesi içinde başlatılan.</span><span class="sxs-lookup"><span data-stu-id="6ed24-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="6ed24-279">Merhaba ayarlayabilirsiniz `InstanceCount` hello dağıtmakta olduğunuz uygulama türüne bağlı olarak değeri.</span><span class="sxs-lookup"><span data-stu-id="6ed24-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="6ed24-280">Merhaba iki en yaygın senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6ed24-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="6ed24-281">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="6ed24-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="6ed24-282">Bu durumda, hello hizmetinin yalnızca bir örneğini hello kümede dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="6ed24-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="6ed24-283">Service Fabric'ın Zamanlayıcı hangi düğüm hello hizmeti dağıtılan toobe geçiyor belirler.</span><span class="sxs-lookup"><span data-stu-id="6ed24-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="6ed24-284">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="6ed24-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="6ed24-285">Bu durumda, hello Hizmeti'nin bir örneğini hello Service Fabric kümedeki her düğümde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="6ed24-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="6ed24-286">Merhaba sonuç hello hizmetinin her düğüm için bir (ve yalnızca bir) örneğini hello kümede yaşıyor.</span><span class="sxs-lookup"><span data-stu-id="6ed24-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="6ed24-287">İstemci uygulamaları çok "Merhaba küme toouse hello uç noktası hello düğümler tooany bağlanmak" ön uç uygulamalar (örneğin, bir REST uç noktası), için kullanışlı bir yapılandırma olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="6ed24-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="6ed24-288">Merhaba Service Fabric kümesinin tüm düğümlerine bağlı tooa yük dengeleyici olduğunda, örneğin, bu yapılandırma de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="6ed24-289">İstemci trafiğini sonra hello kümedeki tüm düğümler üzerinde çalışan hello hizmeti üzerinden dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ed24-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="6ed24-290">Çalışan uygulamanızı denetleyin</span><span class="sxs-lookup"><span data-stu-id="6ed24-290">Check your running application</span></span>
<span data-ttu-id="6ed24-291">Service Fabric Explorer'da hello hizmetinin çalıştığı hello düğümü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="6ed24-292">Bu örnekte, Düğüm1 üzerinde çalışır:</span><span class="sxs-lookup"><span data-stu-id="6ed24-292">In this example, it runs on Node1:</span></span>

![Hizmetinin çalıştığı düğüm](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="6ed24-294">Toohello düğümüne gidin ve toohello uygulama göz atın, diskteki konumuna dahil olmak üzere hello temel düğüm bilgileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![Disk konumu](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="6ed24-296">Sunucu Gezgini kullanarak toohello dizin göz atarsanız, hello ekran aşağıdaki gösterildiği gibi hello çalışma dizinini ve hello hizmetin Günlük klasörü bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6ed24-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![Günlük konumu](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="6ed24-298">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6ed24-298">Next steps</span></span>
<span data-ttu-id="6ed24-299">Bu makalede, öğrendiğiniz nasıl toopackage Konuk çalıştırılabilir ve tooService doku dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6ed24-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="6ed24-300">Merhaba makaleler ilgili bilgi ve görevler için bkz.</span><span class="sxs-lookup"><span data-stu-id="6ed24-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="6ed24-301">[Paketleme ve dağıtma bir konuk yürütülebilir dosyası için örnek](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), bağlantı toohello yayın öncesi hello paketleme Aracı'nın dahil</span><span class="sxs-lookup"><span data-stu-id="6ed24-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="6ed24-302">İki Konuk yürütülebilir dosyalar (C# ve nodejs) iletişim REST kullanarak hello Adlandırma Hizmeti örnek</span><span class="sxs-lookup"><span data-stu-id="6ed24-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="6ed24-303">Konuk tarafından yürütülebilir birden çok uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="6ed24-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="6ed24-304">Visual Studio kullanarak ilk Service Fabric uygulamanızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ed24-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
