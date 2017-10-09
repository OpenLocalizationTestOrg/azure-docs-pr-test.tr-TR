---
title: aaaAzure Service Fabric uygulama modeli | Microsoft Docs
description: "Nasıl toomodel ve uygulamaları ve Hizmetleri Service Fabric açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="96b38-103">Service Fabric uygulamada modeli</span><span class="sxs-lookup"><span data-stu-id="96b38-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="96b38-104">Bu makalede hello Azure Service Fabric uygulama modeli ve toodefine bir uygulama ve hizmet aracılığıyla dosyaları nasıl bildirim genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="96b38-104">This article provides an overview of hello Azure Service Fabric application model and how toodefine an application and service via manifest files.</span></span>

## <a name="understand-hello-application-model"></a><span data-ttu-id="96b38-105">Merhaba uygulama modelini anlama</span><span class="sxs-lookup"><span data-stu-id="96b38-105">Understand hello application model</span></span>
<span data-ttu-id="96b38-106">Bir uygulama, belirli bir işlevi veya işlevleri gerçekleştirmek bağlı hizmetler topluluğudur.</span><span class="sxs-lookup"><span data-stu-id="96b38-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="96b38-107">Bir hizmet tam ve tek başına bir işlevi gerçekleştirir ve başlayın ve diğer hizmetler bağımsız olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="96b38-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="96b38-108">Kod, yapılandırma ve verileri bir servis oluşur.</span><span class="sxs-lookup"><span data-stu-id="96b38-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="96b38-109">Her hizmet için kodu hello yürütülebilir ikili dosyaları oluşur, çalışma zamanında yüklenen hizmet ayarlarını yapılandırma oluşur ve rasgele statik verileri toobe hello hizmeti tarafından tüketilen veri oluşur.</span><span class="sxs-lookup"><span data-stu-id="96b38-109">For each service, code consists of hello executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data toobe consumed by hello service.</span></span> <span data-ttu-id="96b38-110">Bu hiyerarşik uygulama modeli her bileşenin bağımsız olarak sürümlü hem de yükseltilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![Merhaba Service Fabric uygulama modeli][appmodel-diagram]

<span data-ttu-id="96b38-112">Uygulama türü, bir uygulamanın bir kategori değil ve hizmet türlerinin bir dizi oluşur.</span><span class="sxs-lookup"><span data-stu-id="96b38-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="96b38-113">Bir hizmetin kategori bir hizmet türüdür.</span><span class="sxs-lookup"><span data-stu-id="96b38-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="96b38-114">Merhaba kategori farklı ayarları ve yapılandırmaları olabilir, ancak aynı hello çekirdek işlevselliğini kalır hello.</span><span class="sxs-lookup"><span data-stu-id="96b38-114">hello categorization can have different settings and configurations, but hello core functionality remains hello same.</span></span> <span data-ttu-id="96b38-115">Merhaba bir hizmet örnekleri olan hello farklı hizmet yapılandırma farklılıkları Merhaba aynı hizmeti türü.</span><span class="sxs-lookup"><span data-stu-id="96b38-115">hello instances of a service are hello different service configuration variations of hello same service type.</span></span>  

<span data-ttu-id="96b38-116">Sınıflar (veya "türleri") uygulamaları ve Hizmetleri XML dosyalarını (uygulama bildirimlerini ve hizmet bildirimlerini) açıklanan.</span><span class="sxs-lookup"><span data-stu-id="96b38-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="96b38-117">Merhaba bildirimleri göre hello kümenin görüntü deposundan uygulamaları oluşturulabilir hello şablonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="96b38-117">hello manifests are hello templates against which applications can be instantiated from hello cluster's image store.</span></span> <span data-ttu-id="96b38-118">Merhaba hello ServiceManifest.xml ve ApplicationManifest.xml dosyası için şema tanımı hello Service Fabric SDK ile yüklenir ve çok Araçları*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="96b38-118">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="96b38-119">Merhaba kodu farklı bir uygulama örnekleri için ayrı işlemlerdeki bile tarafından barındırıldığında aynı Service Fabric düğümü hello gibi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="96b38-119">hello code for different application instances run as separate processes even when hosted by hello same Service Fabric node.</span></span> <span data-ttu-id="96b38-120">Ayrıca, her uygulama örneğinin hello yaşam döngüsü (örneğin yükseltilmiş) yönetilebilir bağımsız olarak.</span><span class="sxs-lookup"><span data-stu-id="96b38-120">Furthermore, hello lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="96b38-121">Merhaba Aşağıdaki diyagramda uygulama türleri sırayla kod, yapılandırma ve veri paketleri oluşan hizmet türlerini tespiti gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="96b38-121">hello following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="96b38-122">toosimplify hello diyagramı, yalnızca hello kod/config/verileri paketler için `ServiceType4` her hizmet türü bazı içerir veya bu tüm paket türlerinin de gösterilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-122">toosimplify hello diagram, only hello code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Service Fabric uygulama türleri ve hizmet türleri][cluster-imagestore-apptypes]

<span data-ttu-id="96b38-124">İki farklı bildirim dosyalarıdır kullanılan toodescribe uygulamalar ve hizmetler: Merhaba hizmet bildirimi ve uygulama bildirimi.</span><span class="sxs-lookup"><span data-stu-id="96b38-124">Two different manifest files are used toodescribe applications and services: hello service manifest and application manifest.</span></span> <span data-ttu-id="96b38-125">Bildirimleri ayrıntılı bölümleri aşağıdaki hello olarak ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96b38-125">Manifests are covered in detail in hello following sections.</span></span>

<span data-ttu-id="96b38-126">Merhaba kümedeki etkin bir hizmet türünün bir veya daha fazla örneğini olabilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-126">There can be one or more instances of a service type active in hello cluster.</span></span> <span data-ttu-id="96b38-127">Örneğin, durum bilgisi olan hizmet örneği veya çoğaltmalar, yüksek güvenilirlik hello kümedeki farklı düğümlerde bulunan çoğaltmalar arasında durumu yineleyerek elde edin.</span><span class="sxs-lookup"><span data-stu-id="96b38-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in hello cluster.</span></span> <span data-ttu-id="96b38-128">Bir kümedeki bir düğümün başarısız olsa bile çoğaltma temelde hello hizmet toobe için artıklık sağlar.</span><span class="sxs-lookup"><span data-stu-id="96b38-128">Replication essentially provides redundancy for hello service toobe available even if one node in a cluster fails.</span></span> <span data-ttu-id="96b38-129">A [bölümlenmiş hizmet](service-fabric-concepts-partitioning.md) daha ayrıntılı olarak böler hello kümedeki düğümler arasında kendi durumu (ve erişimi desenleri toothat durumu).</span><span class="sxs-lookup"><span data-stu-id="96b38-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns toothat state) across nodes in hello cluster.</span></span>

<span data-ttu-id="96b38-130">Merhaba Aşağıdaki diyagramda hello uygulamalar ve hizmet örnekleri, bölümler ve çoğaltmalar arasındaki ilişkiyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="96b38-130">hello following diagram shows hello relationship between applications and service instances, partitions, and replicas.</span></span>

![Bölümler ve çoğaltmalar bir hizmet kapsamındaki][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="96b38-132">Http:// hello Service Fabric Explorer aracını kullanarak bir küme uygulamalarının hello düzeni görüntüleyebileceği&lt;yourclusteraddress&gt;: 19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="96b38-132">You can view hello layout of applications in a cluster using hello Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="96b38-133">Daha fazla bilgi için bkz: [Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="96b38-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="96b38-134">Bir hizmeti açıklayın</span><span class="sxs-lookup"><span data-stu-id="96b38-134">Describe a service</span></span>
<span data-ttu-id="96b38-135">Merhaba hizmet bildirimi hello hizmet türü ve sürümü bildirimli olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="96b38-135">hello service manifest declaratively defines hello service type and version.</span></span> <span data-ttu-id="96b38-136">Hizmet türü, sistem durumu özellikleri, Yük Dengeleme ölçümleri, hizmeti ikili dosyalarını ve yapılandırma dosyaları gibi hizmet meta verilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="96b38-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="96b38-137">Başka bir deyişle, bir hizmet paketi toosupport oluşturan hello kod, yapılandırma ve veri paketleri açıklar bir veya daha fazla hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="96b38-137">Put another way, it describes hello code, configuration, and data packages that compose a service package toosupport one or more service types.</span></span> <span data-ttu-id="96b38-138">Basit bir örnek hizmet bildirimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="96b38-138">Here is a simple example service manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

<span data-ttu-id="96b38-139">**Sürüm** öznitelikleri yapılandırılmamış dizelerdir ve hello sistem tarafından çözümlenmemiş.</span><span class="sxs-lookup"><span data-stu-id="96b38-139">**Version** attributes are unstructured strings and not parsed by hello system.</span></span> <span data-ttu-id="96b38-140">Sürüm öznitelikleri her bileşen yükseltmeler için kullanılan tooversion şunlardır.</span><span class="sxs-lookup"><span data-stu-id="96b38-140">Version attributes are used tooversion each component for upgrades.</span></span>

<span data-ttu-id="96b38-141">**ServiceTypes** hangi hizmet türleri tarafından desteklenen bildirir **CodePackages** bu bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="96b38-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="96b38-142">Bu hizmet türlerinden birini karşı bir hizmet örneği oluşturulduğunda bu bildirimde belirtilen tüm kod paketleri kendi giriş noktaları çalıştırarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="96b38-143">Merhaba elde edilen beklenen tooregister hello desteklenen hizmet türlerinin çalışma zamanında işlemlerdir.</span><span class="sxs-lookup"><span data-stu-id="96b38-143">hello resulting processes are expected tooregister hello supported service types at run time.</span></span> <span data-ttu-id="96b38-144">Hizmet türlerini hello bildirim düzeyinde ve değil hello kod paketi düzeyinde bildirilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-144">Service types are declared at hello manifest level and not hello code package level.</span></span> <span data-ttu-id="96b38-145">Birden çok kod paket olduğunda hello sistem hizmet türleri bildirilen hello herhangi biri için görünür olduğunda bu nedenle bunlar tüm etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-145">So when there are multiple code packages, they are all activated whenever hello system looks for any one of hello declared service types.</span></span>

<span data-ttu-id="96b38-146">**SetupEntryPoint** hello Service Fabric aynı kimlik bilgileri ile çalışan bir ayrıcalıklı giriş noktasıdır (genellikle hello *LocalSystem* hesabı) önce başka bir giriş noktası.</span><span class="sxs-lookup"><span data-stu-id="96b38-146">**SetupEntryPoint** is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="96b38-147">tarafından belirtilen hello yürütülebilir **EntryPoint** genellikle hello uzun süre çalışan hizmet ana bilgisayardır.</span><span class="sxs-lookup"><span data-stu-id="96b38-147">hello executable specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="96b38-148">uzun süre için toorun hello hizmet konağı yüksek ayrıcalıklara sahip olan ayrı Kurulum giriş noktası Hello varlığını önler.</span><span class="sxs-lookup"><span data-stu-id="96b38-148">hello presence of a separate setup entry point avoids having toorun hello service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="96b38-149">tarafından belirtilen hello yürütülebilir **EntryPoint** çalıştırıldıktan **SetupEntryPoint** başarıyla çıkar.</span><span class="sxs-lookup"><span data-stu-id="96b38-149">hello executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="96b38-150">Hello işlemi her zamankinden sonlandırır veya çöküyor hello elde edilen işlem yeniden ve izlendiği (yeniden itibaren **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="96b38-150">If hello process ever terminates or crashes, hello resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="96b38-151">Kullanma için tipik senaryolar **SetupEntryPoint** hello hizmeti başlamadan önce bir yürütülebilir dosyayı çalıştırmak veya yükseltilmiş ayrıcalıklarla bir işlem gerçekleştirdiğinizde durumdadır.</span><span class="sxs-lookup"><span data-stu-id="96b38-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before hello service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="96b38-152">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="96b38-152">For example:</span></span>

* <span data-ttu-id="96b38-153">Ayarlama ve hizmet yürütülebilir gereksinimleri hello ortam değişkenleri başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="96b38-153">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="96b38-154">Bu sınırlı tooonly yürütülebilir dosyalar hello Service Fabric programlama modeli yazılmış değil.</span><span class="sxs-lookup"><span data-stu-id="96b38-154">This is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="96b38-155">Örneğin, bir node.js uygulamasını dağıtmak için yapılandırılmış bazı ortam değişkenleri npm.exe gerekir.</span><span class="sxs-lookup"><span data-stu-id="96b38-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="96b38-156">Güvenlik sertifikaları yükleyerek erişim denetimini ayarlama.</span><span class="sxs-lookup"><span data-stu-id="96b38-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="96b38-157">Konusunda daha fazla ayrıntı için tooconfigure hello **SetupEntryPoint** görmek [hizmet Kurulum giriş noktası için hello ilkesi yapılandırma](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="96b38-157">For more details on how tooconfigure hello **SetupEntryPoint** see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="96b38-158">**EnvironmentVariables** Bu kod paketi için ayarlanan ortam değişkenlerini bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="96b38-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="96b38-159">Environmentment değişkenleri hello geçersiz `ApplicationManifest.xml` tooprovide farklı hizmet örnekleri için farklı değerler.</span><span class="sxs-lookup"><span data-stu-id="96b38-159">Environmentment variables can be overridden in hello `ApplicationManifest.xml` tooprovide different values for different service instances.</span></span> 

<span data-ttu-id="96b38-160">**Nın DataPackage** tarafından hello adlı bir klasör bildirir **adı** çalışma zamanında hello işlem tarafından kullanılan rasgele statik verileri toobe içeren öznitelik.</span><span class="sxs-lookup"><span data-stu-id="96b38-160">**DataPackage** declares a folder, named by hello **Name** attribute, that contains arbitrary static data toobe consumed by hello process at run time.</span></span>

<span data-ttu-id="96b38-161">**ConfigPackage** tarafından hello adlı bir klasör bildirir **adı** içeren öznitelik, bir *Settings.xml* dosya.</span><span class="sxs-lookup"><span data-stu-id="96b38-161">**ConfigPackage** declares a folder, named by hello **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="96b38-162">Hello ayarları dosyası hello işlem geri çalışma zamanında okur kullanıcı tanımlı, anahtar-değer çifti ayarları bölümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="96b38-162">hello settings file contains sections of user-defined, key-value pair settings that hello process reads back at run time.</span></span> <span data-ttu-id="96b38-163">Yalnızca yükseltme sırasında hello **ConfigPackage** **sürüm** değişti, işlem çalışan hello yeniden sonra.</span><span class="sxs-lookup"><span data-stu-id="96b38-163">During an upgrade, if only hello **ConfigPackage** **version** has changed, then hello running process is not restarted.</span></span> <span data-ttu-id="96b38-164">Bunun yerine, bir geri çağırma bunlar dinamik olarak yeniden, böylece yapılandırma ayarlarının değişip hello işlem bildirir.</span><span class="sxs-lookup"><span data-stu-id="96b38-164">Instead, a callback notifies hello process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="96b38-165">İşte bir örnek *Settings.xml* dosyası:</span><span class="sxs-lookup"><span data-stu-id="96b38-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="96b38-166">Bir hizmet bildirimi birden çok kodu, yapılandırma ve veri paketleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="96b38-167">Bunların her biri bağımsız olarak sürümlü olabilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="96b38-168">Bir uygulamayı tanımlayan</span><span class="sxs-lookup"><span data-stu-id="96b38-168">Describe an application</span></span>
<span data-ttu-id="96b38-169">Merhaba uygulama bildirimi bildirimli olarak hello uygulama türü ve sürümü açıklar.</span><span class="sxs-lookup"><span data-stu-id="96b38-169">hello application manifest declaratively describes hello application type and version.</span></span> <span data-ttu-id="96b38-170">Hizmet oluşturma meta veri şema, örnek sayısı/çoğaltma faktörü, güvenlik/yalıtım İlkesi, yerleştirme kısıtlamaları, yapılandırma geçersiz kılmaları ve bağlı hizmet türü bölümleme kararlı adları gibi belirtir.</span><span class="sxs-lookup"><span data-stu-id="96b38-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="96b38-171">Merhaba Yük Dengeleme etki alanları Merhaba uygulaması yerleştirildiği de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96b38-171">hello load-balancing domains into which hello application is placed are also described.</span></span>

<span data-ttu-id="96b38-172">Bu nedenle, bir uygulama bildirimi hello uygulama düzeyinde öğeleri açıklar ve başvuran bir veya daha fazla hizmet uygulama türü toocompose bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="96b38-172">Thus, an application manifest describes elements at hello application level and references one or more service manifests toocompose an application type.</span></span> <span data-ttu-id="96b38-173">Basit bir örnek uygulama bildirimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="96b38-173">Here is a simple example application manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

<span data-ttu-id="96b38-174">Gibi hizmet bildirimlerini **sürüm** öznitelikleri yapılandırılmamış dizelerdir ve hello sistem tarafından çözümlenmemiş.</span><span class="sxs-lookup"><span data-stu-id="96b38-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by hello system.</span></span> <span data-ttu-id="96b38-175">Sürüm öznitelikleri ayrıca her bileşen yükseltmeler için kullanılan tooversion değildir.</span><span class="sxs-lookup"><span data-stu-id="96b38-175">Version attributes are also used tooversion each component for upgrades.</span></span>

<span data-ttu-id="96b38-176">**ServiceManifestImport** bu uygulama türü oluşturan başvurular tooservice bildirimlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="96b38-176">**ServiceManifestImport** contains references tooservice manifests that compose this application type.</span></span> <span data-ttu-id="96b38-177">Alınan hizmet bildirimlerini hangi hizmet türleri içindeki bu uygulama türü geçerli belirler.</span><span class="sxs-lookup"><span data-stu-id="96b38-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="96b38-178">Merhaba ServiceManifestImport içinde ServiceManifest.xml dosyalarında Settings.xml ve ortam değişkenleri içindeki yapılandırma değerleri geçersiz.</span><span class="sxs-lookup"><span data-stu-id="96b38-178">Within hello ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="96b38-179">**DefaultServices** bir uygulama bu uygulama türü karşı örneği olduğunda, otomatik olarak oluşturulan hizmet örnekleri bildirir.</span><span class="sxs-lookup"><span data-stu-id="96b38-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="96b38-180">Varsayılan Hizmetleri yalnızca kolaylık sağlamak ve oluşturulduktan sonra her açısından normal services gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="96b38-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="96b38-181">Bunların yanı sıra diğer hizmetlere hello uygulama örneğinde yükseltilir ve de kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-181">They are upgraded along with any other services in hello application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="96b38-182">Bir uygulama bildirimi birden çok hizmet bildirimi alır ve varsayılan hizmet içerebilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="96b38-183">Her hizmet bildirim alma bağımsız olarak sürümlü olabilir.</span><span class="sxs-lookup"><span data-stu-id="96b38-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="96b38-184">toomaintain farklı uygulama ve hizmet parametreleri tek tek ortamlar için nasıl görürüm toolearn [birden çok ortamlar için uygulama parametreleri yönetme](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="96b38-184">toolearn how toomaintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="96b38-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96b38-185">Next steps</span></span>
<span data-ttu-id="96b38-186">[Bir uygulama paketi](service-fabric-package-apps.md) ve toodeploy kullanıma hazır hale getirin.</span><span class="sxs-lookup"><span data-stu-id="96b38-186">[Package an application](service-fabric-package-apps.md) and make it ready toodeploy.</span></span>

<span data-ttu-id="96b38-187">[Dağıtma ve uygulamaları kaldırma] [ 10] açıklar nasıl toouse PowerShell toomanage uygulama örnekleri.</span><span class="sxs-lookup"><span data-stu-id="96b38-187">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances.</span></span>

<span data-ttu-id="96b38-188">[Birden çok ortamlar için uygulama parametreleri yönetme] [ 11] açıklar nasıl tooconfigure parametreleri ve farklı uygulama örnekleri için ortam değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="96b38-188">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="96b38-189">[Uygulamanız için güvenlik ilkelerini yapılandırmak] [ 12] toorun güvenlik ilkeleri toorestrict erişim'in altında hizmetleri nasıl açıklar.</span><span class="sxs-lookup"><span data-stu-id="96b38-189">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<span data-ttu-id="96b38-190">[Uygulama barındırma modellerini] [ 13] bir dağıtılan hizmet ve hizmet ana bilgisayar işlemi çoğaltmaları (veya örnekleri) arasındaki ilişkiyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="96b38-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
