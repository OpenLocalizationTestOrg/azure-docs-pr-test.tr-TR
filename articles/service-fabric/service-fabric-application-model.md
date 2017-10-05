---
title: Azure Service Fabric uygulama modeli | Microsoft Docs
description: "Nasıl model ve uygulamaları ve Hizmetleri Service Fabric açıklanmaktadır."
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
ms.openlocfilehash: e30482427b88eb3e58d39075c7f0734664b79aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="98f43-103">Service Fabric uygulamada modeli</span><span class="sxs-lookup"><span data-stu-id="98f43-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="98f43-104">Bu makalede Azure Service Fabric uygulama modeli ve bir uygulama ve hizmet bildirim dosyaları aracılığıyla nasıl tanımlanacağı genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="98f43-104">This article provides an overview of the Azure Service Fabric application model and how to define an application and service via manifest files.</span></span>

## <a name="understand-the-application-model"></a><span data-ttu-id="98f43-105">Uygulama modeli anlama</span><span class="sxs-lookup"><span data-stu-id="98f43-105">Understand the application model</span></span>
<span data-ttu-id="98f43-106">Bir uygulama, belirli bir işlevi veya işlevleri gerçekleştirmek bağlı hizmetler topluluğudur.</span><span class="sxs-lookup"><span data-stu-id="98f43-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="98f43-107">Bir hizmet tam ve tek başına bir işlevi gerçekleştirir ve başlayın ve diğer hizmetler bağımsız olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="98f43-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="98f43-108">Kod, yapılandırma ve verileri bir servis oluşur.</span><span class="sxs-lookup"><span data-stu-id="98f43-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="98f43-109">Her hizmet için kodu yürütülebilir ikili dosyaları oluşur, çalışma zamanında yüklenen hizmet ayarlarını yapılandırma oluşur ve veri hizmeti tarafından kullanılacak rasgele statik verileri oluşur.</span><span class="sxs-lookup"><span data-stu-id="98f43-109">For each service, code consists of the executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data to be consumed by the service.</span></span> <span data-ttu-id="98f43-110">Bu hiyerarşik uygulama modeli her bileşenin bağımsız olarak sürümlü hem de yükseltilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![Service Fabric uygulama modeli][appmodel-diagram]

<span data-ttu-id="98f43-112">Uygulama türü, bir uygulamanın bir kategori değil ve hizmet türlerinin bir dizi oluşur.</span><span class="sxs-lookup"><span data-stu-id="98f43-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="98f43-113">Bir hizmetin kategori bir hizmet türüdür.</span><span class="sxs-lookup"><span data-stu-id="98f43-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="98f43-114">Kategori farklı ayarları ve yapılandırmaları olabilir, ancak temel işlevleri aynı kalır.</span><span class="sxs-lookup"><span data-stu-id="98f43-114">The categorization can have different settings and configurations, but the core functionality remains the same.</span></span> <span data-ttu-id="98f43-115">Farklı hizmet yapılandırma farklılıkları aynı hizmet türünün hizmet örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="98f43-115">The instances of a service are the different service configuration variations of the same service type.</span></span>  

<span data-ttu-id="98f43-116">Sınıflar (veya "türleri") uygulamaları ve Hizmetleri XML dosyalarını (uygulama bildirimlerini ve hizmet bildirimlerini) açıklanan.</span><span class="sxs-lookup"><span data-stu-id="98f43-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="98f43-117">Bildirimler, kümenin görüntü deposundan göre uygulamaları oluşturulabilir şablonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="98f43-117">The manifests are the templates against which applications can be instantiated from the cluster's image store.</span></span> <span data-ttu-id="98f43-118">ServiceManifest.xml ve ApplicationManifest.xml dosyası için şema tanımı Service Fabric SDK ile birlikte yüklenir ve araçların *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="98f43-118">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="98f43-119">Farklı uygulama örnekleri için kod bile aynı Service Fabric düğümüne barındırıldığında ayrı işlemler olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="98f43-119">The code for different application instances run as separate processes even when hosted by the same Service Fabric node.</span></span> <span data-ttu-id="98f43-120">Ayrıca, her uygulama örneği yaşam döngüsü (örneğin yükseltilmiş) yönetilebilir bağımsız olarak.</span><span class="sxs-lookup"><span data-stu-id="98f43-120">Furthermore, the lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="98f43-121">Aşağıdaki diyagramda uygulama türleri sırayla kod, yapılandırma ve veri paketleri oluşan hizmet türlerini tespiti gösterir.</span><span class="sxs-lookup"><span data-stu-id="98f43-121">The following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="98f43-122">Diyagram basitleştirmek için yalnızca kod/config/verileri paketler için `ServiceType4` her hizmet türü bazı içerir veya bu tüm paket türlerinin de gösterilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-122">To simplify the diagram, only the code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Service Fabric uygulama türleri ve hizmet türleri][cluster-imagestore-apptypes]

<span data-ttu-id="98f43-124">İki farklı bildirim dosyası, uygulamaları ve hizmetleri tanımlamak için kullanılır: hizmet bildirimi ve uygulama bildirimi.</span><span class="sxs-lookup"><span data-stu-id="98f43-124">Two different manifest files are used to describe applications and services: the service manifest and application manifest.</span></span> <span data-ttu-id="98f43-125">Bildirimler, aşağıdaki bölümlerde ayrıntılı olarak ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="98f43-125">Manifests are covered in detail in the following sections.</span></span>

<span data-ttu-id="98f43-126">Kümedeki etkin bir hizmet türünün bir veya daha fazla örneğini olabilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-126">There can be one or more instances of a service type active in the cluster.</span></span> <span data-ttu-id="98f43-127">Örneğin, durum bilgisi olan hizmet örneği veya çoğaltmalar, yüksek güvenilirlik kümedeki farklı düğümlerde bulunan çoğaltmalar arasında durumu yineleyerek elde edin.</span><span class="sxs-lookup"><span data-stu-id="98f43-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in the cluster.</span></span> <span data-ttu-id="98f43-128">Çoğaltma temelde hizmetinin bir kümedeki bir düğümün başarısız olsa bile kullanılabilir olması artıklık sağlar.</span><span class="sxs-lookup"><span data-stu-id="98f43-128">Replication essentially provides redundancy for the service to be available even if one node in a cluster fails.</span></span> <span data-ttu-id="98f43-129">A [bölümlenmiş hizmet](service-fabric-concepts-partitioning.md) daha fazla kümedeki düğümler arasında alt durumu (ve bu durum için erişim düzenlerini) böler.</span><span class="sxs-lookup"><span data-stu-id="98f43-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns to that state) across nodes in the cluster.</span></span>

<span data-ttu-id="98f43-130">Aşağıdaki diyagram, uygulamaları ve hizmet örnekleri, bölümler ve çoğaltmalar arasındaki ilişkiyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="98f43-130">The following diagram shows the relationship between applications and service instances, partitions, and replicas.</span></span>

![Bölümler ve çoğaltmalar bir hizmet kapsamındaki][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="98f43-132">Http:// kullanılabilir Service Fabric Explorer aracını kullanarak bir küme uygulamalarının düzeni görüntüleyebileceği&lt;yourclusteraddress&gt;: 19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="98f43-132">You can view the layout of applications in a cluster using the Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="98f43-133">Daha fazla bilgi için bkz: [Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="98f43-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="98f43-134">Bir hizmeti açıklayın</span><span class="sxs-lookup"><span data-stu-id="98f43-134">Describe a service</span></span>
<span data-ttu-id="98f43-135">Hizmet bildirimi bildirimli olarak hizmet türü ve sürümü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="98f43-135">The service manifest declaratively defines the service type and version.</span></span> <span data-ttu-id="98f43-136">Hizmet türü, sistem durumu özellikleri, Yük Dengeleme ölçümleri, hizmeti ikili dosyalarını ve yapılandırma dosyaları gibi hizmet meta verilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="98f43-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="98f43-137">Başka bir deyişle, bir veya daha fazla hizmet türlerini desteklemek için bir hizmet paketi oluşturan kod, yapılandırma ve veri paketleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="98f43-137">Put another way, it describes the code, configuration, and data packages that compose a service package to support one or more service types.</span></span> <span data-ttu-id="98f43-138">Basit bir örnek hizmet bildirimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="98f43-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="98f43-139">**Sürüm** öznitelikleri yapılandırılmamış dizelerdir ve sistem tarafından çözümlenmemiş.</span><span class="sxs-lookup"><span data-stu-id="98f43-139">**Version** attributes are unstructured strings and not parsed by the system.</span></span> <span data-ttu-id="98f43-140">Sürüm öznitelikleri sürüme her bileşenin yükseltmeleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98f43-140">Version attributes are used to version each component for upgrades.</span></span>

<span data-ttu-id="98f43-141">**ServiceTypes** hangi hizmet türleri tarafından desteklenen bildirir **CodePackages** bu bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="98f43-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="98f43-142">Bu hizmet türlerinden birini karşı bir hizmet örneği oluşturulduğunda bu bildirimde belirtilen tüm kod paketleri kendi giriş noktaları çalıştırarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="98f43-143">Sonuçta elde edilen işlemleri çalışma zamanında desteklenen hizmet türlerinin kaydetmek beklenir.</span><span class="sxs-lookup"><span data-stu-id="98f43-143">The resulting processes are expected to register the supported service types at run time.</span></span> <span data-ttu-id="98f43-144">Hizmet türlerini, bildirim düzeyini ve kod paketi düzeyinde bildirilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-144">Service types are declared at the manifest level and not the code package level.</span></span> <span data-ttu-id="98f43-145">Birden çok kod paket olduğunda bildirilen hizmet türleri herhangi biri için sistem bakar olduğunda bu nedenle bunlar tüm etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-145">So when there are multiple code packages, they are all activated whenever the system looks for any one of the declared service types.</span></span>

<span data-ttu-id="98f43-146">**SetupEntryPoint** Service Fabric kimlik bilgileriyle çalışır ayrıcalıklı giriş noktasıdır (genellikle *LocalSystem* hesabı) önce başka bir giriş noktası.</span><span class="sxs-lookup"><span data-stu-id="98f43-146">**SetupEntryPoint** is a privileged entry point that runs with the same credentials as Service Fabric (typically the *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="98f43-147">Tarafından belirtilen yürütülebilir **EntryPoint** genellikle uzun süre çalışan hizmet yöneticisidir.</span><span class="sxs-lookup"><span data-stu-id="98f43-147">The executable specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="98f43-148">Ayrı Kurulum giriş noktası varlığını hizmet konağı yüksek ayrıcalıklara sahip uzun süre için çalıştırmanız gereğini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="98f43-148">The presence of a separate setup entry point avoids having to run the service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="98f43-149">Tarafından belirtilen yürütülebilir **EntryPoint** çalıştırıldıktan **SetupEntryPoint** başarıyla çıkar.</span><span class="sxs-lookup"><span data-stu-id="98f43-149">The executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="98f43-150">İşlemin her zamankinden sonlandırır veya çöküyor, sonuçta elde edilen işlem yeniden ve izlendiği (yeniden itibaren **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="98f43-150">If the process ever terminates or crashes, the resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="98f43-151">Kullanma için tipik senaryolar **SetupEntryPoint** hizmeti başlamadan önce bir yürütülebilir dosyayı çalıştırmak veya yükseltilmiş ayrıcalıklarla bir işlem gerçekleştirdiğinizde durumdadır.</span><span class="sxs-lookup"><span data-stu-id="98f43-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before the service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="98f43-152">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="98f43-152">For example:</span></span>

* <span data-ttu-id="98f43-153">Ayarlama ve hizmeti yürütülebilir dosyası gerekli ortam değişkenleri başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="98f43-153">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="98f43-154">Bu, yalnızca Service Fabric programlama modeli yazılmış yürütülebilir dosyalar için sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="98f43-154">This is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="98f43-155">Örneğin, bir node.js uygulamasını dağıtmak için yapılandırılmış bazı ortam değişkenleri npm.exe gerekir.</span><span class="sxs-lookup"><span data-stu-id="98f43-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="98f43-156">Güvenlik sertifikaları yükleyerek erişim denetimini ayarlama.</span><span class="sxs-lookup"><span data-stu-id="98f43-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="98f43-157">Nasıl yapılandırılacağı hakkında daha fazla ayrıntı için **SetupEntryPoint** görmek [hizmet Kurulum giriş noktası için ilkeyi yapılandırın](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="98f43-157">For more details on how to configure the **SetupEntryPoint** see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="98f43-158">**EnvironmentVariables** Bu kod paketi için ayarlanan ortam değişkenlerini bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="98f43-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="98f43-159">Environmentment değişkenleri geçersiz kılınmış içinde `ApplicationManifest.xml` farklı hizmet örnekleri için farklı değerler sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="98f43-159">Environmentment variables can be overridden in the `ApplicationManifest.xml` to provide different values for different service instances.</span></span> 

<span data-ttu-id="98f43-160">**Nın DataPackage** tarafından adlı bir klasör bildirir **adı** işlem tarafından çalışma zamanında kullanılacak rastgele statik verileri içeren öznitelik.</span><span class="sxs-lookup"><span data-stu-id="98f43-160">**DataPackage** declares a folder, named by the **Name** attribute, that contains arbitrary static data to be consumed by the process at run time.</span></span>

<span data-ttu-id="98f43-161">**ConfigPackage** tarafından adlı bir klasör bildirir **adı** içeren öznitelik, bir *Settings.xml* dosya.</span><span class="sxs-lookup"><span data-stu-id="98f43-161">**ConfigPackage** declares a folder, named by the **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="98f43-162">Ayarlar dosyası işlemi geri çalışma zamanında okur kullanıcı tanımlı, anahtar-değer çifti ayarları bölümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="98f43-162">The settings file contains sections of user-defined, key-value pair settings that the process reads back at run time.</span></span> <span data-ttu-id="98f43-163">Yalnızca yükseltme sırasında **ConfigPackage** **sürüm** değişti, çalışan işlem yeniden sonra.</span><span class="sxs-lookup"><span data-stu-id="98f43-163">During an upgrade, if only the **ConfigPackage** **version** has changed, then the running process is not restarted.</span></span> <span data-ttu-id="98f43-164">Bunun yerine, bir geri çağırma bunlar dinamik olarak yeniden yüklendi için yapılandırma ayarları değişti işlem bildirir.</span><span class="sxs-lookup"><span data-stu-id="98f43-164">Instead, a callback notifies the process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="98f43-165">İşte bir örnek *Settings.xml* dosyası:</span><span class="sxs-lookup"><span data-stu-id="98f43-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="98f43-166">Bir hizmet bildirimi birden çok kodu, yapılandırma ve veri paketleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="98f43-167">Bunların her biri bağımsız olarak sürümlü olabilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="98f43-168">Bir uygulamayı tanımlayan</span><span class="sxs-lookup"><span data-stu-id="98f43-168">Describe an application</span></span>
<span data-ttu-id="98f43-169">Uygulama bildirimini bildirimli olarak uygulama türü ve sürümü açıklar.</span><span class="sxs-lookup"><span data-stu-id="98f43-169">The application manifest declaratively describes the application type and version.</span></span> <span data-ttu-id="98f43-170">Hizmet oluşturma meta veri şema, örnek sayısı/çoğaltma faktörü, güvenlik/yalıtım İlkesi, yerleştirme kısıtlamaları, yapılandırma geçersiz kılmaları ve bağlı hizmet türü bölümleme kararlı adları gibi belirtir.</span><span class="sxs-lookup"><span data-stu-id="98f43-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="98f43-171">Uygulama üzerine yerleştirilen yük dengeleyici etki alanları da açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="98f43-171">The load-balancing domains into which the application is placed are also described.</span></span>

<span data-ttu-id="98f43-172">Bu nedenle, bir uygulama bildirimi uygulama düzeyinde öğeleri açıklar ve uygulama türü oluşturmak için bir veya daha fazla hizmet bildirimlerini başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="98f43-172">Thus, an application manifest describes elements at the application level and references one or more service manifests to compose an application type.</span></span> <span data-ttu-id="98f43-173">Basit bir örnek uygulama bildirimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="98f43-173">Here is a simple example application manifest:</span></span>

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

<span data-ttu-id="98f43-174">Gibi hizmet bildirimlerini **sürüm** öznitelikleri yapılandırılmamış dizelerdir ve sistem tarafından çözümlenmemiş.</span><span class="sxs-lookup"><span data-stu-id="98f43-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by the system.</span></span> <span data-ttu-id="98f43-175">Sürüm öznitelikleridir de sürüme her bileşenin yükseltmeleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98f43-175">Version attributes are also used to version each component for upgrades.</span></span>

<span data-ttu-id="98f43-176">**ServiceManifestImport** bu uygulama türü oluşturan hizmet bildirimlerini başvurular içeriyor.</span><span class="sxs-lookup"><span data-stu-id="98f43-176">**ServiceManifestImport** contains references to service manifests that compose this application type.</span></span> <span data-ttu-id="98f43-177">Alınan hizmet bildirimlerini hangi hizmet türleri içindeki bu uygulama türü geçerli belirler.</span><span class="sxs-lookup"><span data-stu-id="98f43-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="98f43-178">ServiceManifestImport içinde ServiceManifest.xml dosyalarında Settings.xml ve ortam değişkenleri içindeki yapılandırma değerleri geçersiz.</span><span class="sxs-lookup"><span data-stu-id="98f43-178">Within the ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="98f43-179">**DefaultServices** bir uygulama bu uygulama türü karşı örneği olduğunda, otomatik olarak oluşturulan hizmet örnekleri bildirir.</span><span class="sxs-lookup"><span data-stu-id="98f43-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="98f43-180">Varsayılan Hizmetleri yalnızca kolaylık sağlamak ve oluşturulduktan sonra her açısından normal services gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="98f43-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="98f43-181">Bunlar, herhangi bir uygulama örneği Hizmetleri'nde birlikte yükseltilir ve de kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-181">They are upgraded along with any other services in the application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="98f43-182">Bir uygulama bildirimi birden çok hizmet bildirimi alır ve varsayılan hizmet içerebilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="98f43-183">Her hizmet bildirim alma bağımsız olarak sürümlü olabilir.</span><span class="sxs-lookup"><span data-stu-id="98f43-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="98f43-184">Farklı bir uygulama ve hizmet parametreleri tek tek ortamlar için korumak öğrenmek için bkz: [birden çok ortamlar için uygulama parametreleri yönetme](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="98f43-184">To learn how to maintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="98f43-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98f43-185">Next steps</span></span>
<span data-ttu-id="98f43-186">[Bir uygulama paketi](service-fabric-package-apps.md) ve dağıtmak hazır olun.</span><span class="sxs-lookup"><span data-stu-id="98f43-186">[Package an application](service-fabric-package-apps.md) and make it ready to deploy.</span></span>

<span data-ttu-id="98f43-187">[Dağıtma ve uygulamaları kaldırma] [ 10] uygulama örnekleri yönetmek için PowerShell kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="98f43-187">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances.</span></span>

<span data-ttu-id="98f43-188">[Birden çok ortamlar için uygulama parametreleri yönetme] [ 11] parametreleri ve farklı uygulama örnekleri için ortam değişkenleri nasıl yapılandırılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="98f43-188">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="98f43-189">[Uygulamanız için güvenlik ilkelerini yapılandırmak] [ 12] erişimi kısıtlamak için güvenlik ilkeleri altında hizmetlerini çalıştırmak açıklar.</span><span class="sxs-lookup"><span data-stu-id="98f43-189">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<span data-ttu-id="98f43-190">[Uygulama barındırma modellerini] [ 13] bir dağıtılan hizmet ve hizmet ana bilgisayar işlemi çoğaltmaları (veya örnekleri) arasındaki ilişkiyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="98f43-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
