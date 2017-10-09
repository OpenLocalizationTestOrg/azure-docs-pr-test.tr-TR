---
title: "aaaManage birden çok ortamlarda Service Fabric | Microsoft Docs"
description: "Service Fabric uygulamaları bir makine toothousands makinelerin boyutu aralık kümeleri üzerinde çalıştırılabilir. Bazı durumlarda, uygulamanız bu çeşitli ortamlar için farklı tooconfigure isteyeceksiniz. Bu makalede yer almaktadır nasıl ortamı başına toodefine farklı uygulama parametreleri."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="964ea-105">Birden çok ortamlar için uygulama parametreleri yönetme</span><span class="sxs-lookup"><span data-stu-id="964ea-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="964ea-106">Herhangi bir yerden bir toomany makinelerin binlerce kullanarak Azure Service Fabric kümeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="964ea-106">You can create Azure Service Fabric clusters by using anywhere from one toomany thousands of machines.</span></span> <span data-ttu-id="964ea-107">Uygulama ikili dosyaları değişiklik yapmadan bu paylaşılabilen çok sayıda ortamlar arasında çalıştırılabilir olsa da, genellikle tooconfigure Merhaba uygulaması farklı makineler için dağıtıyorsunuz hello sayısı bağlı olarak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="964ea-107">While application binaries can run without modification across this wide spectrum of environments, you often want tooconfigure hello application differently, depending on hello number of machines you're deploying to.</span></span>

<span data-ttu-id="964ea-108">Basit bir örnek olarak göz önünde bulundurun `InstanceCount` durumsuz bir hizmet için.</span><span class="sxs-lookup"><span data-stu-id="964ea-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="964ea-109">Azure uygulamalarını çalıştırırken bu parametre toohello özel "-1 değeri" genellikle tooset istersiniz.</span><span class="sxs-lookup"><span data-stu-id="964ea-109">When you are running applications in Azure, you generally want tooset this parameter toohello special value of "-1".</span></span> <span data-ttu-id="964ea-110">Bu yapılandırma, hizmetiniz hello küme (veya bir yerleştirme kısıtlaması ayarlarsanız hello düğüm türü kümedeki her düğüm) kümedeki her düğüm üzerinde çalıştığını sağlar.</span><span class="sxs-lookup"><span data-stu-id="964ea-110">This configuration ensures that your service is running on every node in hello cluster (or every node in hello node type if you have set a placement constraint).</span></span> <span data-ttu-id="964ea-111">Birden çok işlem aynı hello üzerinde dinleme olamaz bu yana ancak, bu yapılandırma bir tek makineli küme için uygun değil tek bir makinede uç noktası.</span><span class="sxs-lookup"><span data-stu-id="964ea-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on hello same endpoint on a single machine.</span></span> <span data-ttu-id="964ea-112">Bunun yerine, genellikle ayarladığınız `InstanceCount` çok "1".</span><span class="sxs-lookup"><span data-stu-id="964ea-112">Instead, you typically set `InstanceCount` too"1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="964ea-113">Ortama özgü parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="964ea-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="964ea-114">Merhaba çözüm toothis yapılandırma sorunu parametreli varsayılan Hizmetleri ve belirli bir ortam için bu parametre değerlerini doldurun uygulama parametreleri dosyalarını kümesidir.</span><span class="sxs-lookup"><span data-stu-id="964ea-114">hello solution toothis configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="964ea-115">Varsayılan hizmet ve uygulama parametreleri hello uygulamada yapılandırılır ve bildirimleri hizmet.</span><span class="sxs-lookup"><span data-stu-id="964ea-115">Default services and application parameters are configured in hello application and service manifests.</span></span> <span data-ttu-id="964ea-116">Merhaba hello ServiceManifest.xml ve ApplicationManifest.xml dosyaları için şema tanımı hello Service Fabric SDK ile yüklenir ve çok Araçları*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="964ea-116">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml files is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="964ea-117">Varsayılan Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="964ea-117">Default services</span></span>
<span data-ttu-id="964ea-118">Service Fabric uygulamaları hizmet örnekleri koleksiyonu yapılır.</span><span class="sxs-lookup"><span data-stu-id="964ea-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="964ea-119">Toocreate için boş bir uygulama mümkündür ve tüm hizmet örnekleri dinamik olarak oluşturmak olsa da, çoğu uygulamayı hello uygulama örneği oluşturulduğunda, her zaman oluşturulması gereken Çekirdek Hizmetleri kümesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="964ea-119">While it is possible for you toocreate an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when hello application is instantiated.</span></span> <span data-ttu-id="964ea-120">Başvurulan tooas "varsayılan Hizmetleri" bunlar.</span><span class="sxs-lookup"><span data-stu-id="964ea-120">These are referred tooas "default services".</span></span> <span data-ttu-id="964ea-121">Köşeli parantez içine dahil ortamı başına yapılandırması yer tutucular ile Merhaba uygulama bildiriminde belirtilir:</span><span class="sxs-lookup"><span data-stu-id="964ea-121">They are specified in hello application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="964ea-122">Her adlandırılmış parametreleri hello hello uygulama bildiriminin hello parametreleri öğesi içinde tanımlanmış olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="964ea-122">Each of hello named parameters must be defined within hello Parameters element of hello application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="964ea-123">Daha fazla özel parametre hello olmaması durumunda belirli bir ortam için kullanılan hello değeri toobe Hello DefaultValue özniteliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="964ea-123">hello DefaultValue attribute specifies hello value toobe used in hello absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="964ea-124">Tüm hizmet örneği parametreleri ortamı başına yapılandırması için uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="964ea-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="964ea-125">Merhaba yukarıdaki örnekte, LowKey hello ve hello bölüm aralığı işlevi hello veri etki alanının değil hello ortamı olduğundan hello hizmetin bölümleme düzeni HighKey değerlerini açıkça hizmetin tüm örneklerine ait hello için tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="964ea-125">In hello example above, hello LowKey and HighKey values for hello service's partitioning scheme are explicitly defined for all instances of hello service since hello partition range is a function of hello data domain, not hello environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="964ea-126">Ortam başına hizmet yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="964ea-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="964ea-127">Merhaba [Service Fabric uygulama modeli](service-fabric-application-model.md) Hizmetleri çalışma zamanında okunabilir özel anahtar-değer çiftleri içeren tooinclude yapılandırma paketlerini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="964ea-127">hello [Service Fabric application model](service-fabric-application-model.md) enables services tooinclude configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="964ea-128">Bu ayarların Hello değerleri ayrıca Ayrıştırılan ortamı tarafından belirterek bir `ConfigOverride` hello uygulama bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="964ea-128">hello values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in hello application manifest.</span></span>

<span data-ttu-id="964ea-129">Ayar hello için hello Config\Settings.xml dosyasında aşağıdaki hello olduğunu varsayalım `Stateful1` hizmeti:</span><span class="sxs-lookup"><span data-stu-id="964ea-129">Suppose that you have hello following setting in hello Config\Settings.xml file for hello `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="964ea-130">Bu değer için bir özel uygulama/ortamı çifti toooverride oluşturmak bir `ConfigOverride` hello hizmet bildirimi hello uygulama bildiriminde aktardığınızda.</span><span class="sxs-lookup"><span data-stu-id="964ea-130">toooverride this value for a specific application/environment pair, create a `ConfigOverride` when you import hello service manifest in hello application manifest.</span></span>

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="964ea-131">Bu parametre yukarıda gösterildiği gibi ortamı tarafından sonra yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="964ea-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="964ea-132">Bunu hello Parametreler bölümünde hello uygulama bildiriminin bildirme ve ortama özgü değerleri hello uygulama parametresi dosyalarında belirterek yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="964ea-132">You can do this by declaring it in hello parameters section of hello application manifest and specifying environment-specific values in hello application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="964ea-133">Hizmet yapılandırma ayarlarını Hello durumda olduğu bir anahtarın değerini hello ayarlanabilir üç yerde vardır: hello hizmeti yapılandırma paketi, hello uygulama bildirimi ve hello uygulama parametre dosyası.</span><span class="sxs-lookup"><span data-stu-id="964ea-133">In hello case of service configuration settings, there are three places where hello value of a key can be set: hello service configuration package, hello application manifest, and hello application parameter file.</span></span> <span data-ttu-id="964ea-134">Service Fabric her zaman hello uygulama parametre dosyasından ilk (belirtilmişse) seçin, sonra uygulama bildirimi hello ve son olarak yapılandırma paketi hello.</span><span class="sxs-lookup"><span data-stu-id="964ea-134">Service Fabric will always choose from hello application parameter file first (if specified), then hello application manifest, and finally hello configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="964ea-135">Ayarlama ve ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="964ea-135">Setting and using environment variables</span></span> 
<span data-ttu-id="964ea-136">Belirtin ve hello ServiceManifest.xml dosyasında ortam değişkenlerini ayarlama ve daha sonra bu örneği başına temelinde hello ApplicationManifest.xml dosyasında geçersiz.</span><span class="sxs-lookup"><span data-stu-id="964ea-136">You can specify and set environment variables in hello ServiceManifest.xml file and then override these in hello ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="964ea-137">bir değerle ayarlayın ve hello diğer geçersiz kılınır Hello örnekte iki ortam değişkenleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="964ea-137">hello example below shows two environment variables, one with a value set and hello other is overridden.</span></span> <span data-ttu-id="964ea-138">Tooset ortam değişkenleri değerleri hello aynı şekilde, bu yapılandırma geçersiz kılma işlemleri için kullanılan uygulama parametrelerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="964ea-138">You can use application parameters tooset environment variables values in hello same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="964ea-139">Merhaba ApplicationManifest.xml, başvuru hello kod hello ServiceManifest hello ile paketinde toooverride hello ortam değişkenleri `EnvironmentOverrides` öğesi.</span><span class="sxs-lookup"><span data-stu-id="964ea-139">toooverride hello environment variables in hello ApplicationManifest.xml, reference hello code package in hello ServiceManifest with hello `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="964ea-140">Merhaba adlı hizmet örneği oluşturulduktan sonra koddan hello ortam değişkenlerine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="964ea-140">Once hello named service instance is created you can access hello environment variables from code.</span></span> <span data-ttu-id="964ea-141">Örneğin, C# yapabileceğiniz hello aşağıdaki</span><span class="sxs-lookup"><span data-stu-id="964ea-141">e.g. In C# you can do hello following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="964ea-142">Service Fabric ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="964ea-142">Service Fabric environment variables</span></span>
<span data-ttu-id="964ea-143">Service Fabric kümesi her hizmet örneği için ortam değişkenleri içindeki oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="964ea-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="964ea-144">Merhaba ortam değişkenlerinin tam listesi olduğu aşağıda hello olanları kalın olan, hizmetiniz, kullanacağınız olanları hello burada hello diğer olan Service Fabric çalışma zamanı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="964ea-144">hello full list of environment variables is below, where hello ones in bold are hello ones that you will use in your service, hello other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="964ea-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="964ea-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="964ea-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="964ea-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="964ea-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="964ea-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="964ea-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="964ea-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="964ea-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="964ea-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="964ea-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="964ea-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="964ea-151">**Fabric_Endpoint_ [YourServiceName] TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="964ea-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="964ea-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="964ea-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="964ea-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="964ea-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="964ea-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="964ea-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="964ea-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="964ea-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="964ea-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="964ea-156">Fabric_NodeId</span></span>
* <span data-ttu-id="964ea-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="964ea-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="964ea-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="964ea-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="964ea-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="964ea-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="964ea-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="964ea-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="964ea-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="964ea-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="964ea-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="964ea-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="964ea-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="964ea-163">FabricPackageFileName</span></span>

<span data-ttu-id="964ea-164">Merhaba kod belows nasıl toolist hello Service Fabric ortam değişkenleri gösterir</span><span class="sxs-lookup"><span data-stu-id="964ea-164">hello code belows shows how toolist hello Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="964ea-165">Merhaba adlı bir uygulama türü için ortam değişkenleri örnekleri verilmiştir `GuestExe.Application` hizmet türü ile adlı `FrontEndService` yerel geliştirme makinenizde çalıştırdığınızda.</span><span class="sxs-lookup"><span data-stu-id="964ea-165">hello following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="964ea-166">**Fabric_ApplicationName fabric:/GuestExe.Application =**</span><span class="sxs-lookup"><span data-stu-id="964ea-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="964ea-167">**Fabric_CodePackageName kodu =**</span><span class="sxs-lookup"><span data-stu-id="964ea-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="964ea-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="964ea-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="964ea-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="964ea-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="964ea-170">**Fabric_NodeName _Node_2 =**</span><span class="sxs-lookup"><span data-stu-id="964ea-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="964ea-171">Uygulama parametre dosyaları</span><span class="sxs-lookup"><span data-stu-id="964ea-171">Application parameter files</span></span>
<span data-ttu-id="964ea-172">Merhaba Service Fabric uygulaması projesi bir veya daha fazla uygulama parametreleri dosyalarını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="964ea-172">hello Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="964ea-173">Bunların her birini hello belirli değerleri hello uygulama bildiriminde tanımlanan hello parametreleri tanımlar:</span><span class="sxs-lookup"><span data-stu-id="964ea-173">Each of them defines hello specific values for hello parameters that are defined in hello application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="964ea-174">Varsayılan olarak, yeni bir uygulama Local.1Node.xml, Local.5Node.xml ve Cloud.xml adlı üç uygulama parametreleri dosyalarını içerir:</span><span class="sxs-lookup"><span data-stu-id="964ea-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Çözüm Gezgini'nde uygulama parametre dosyaları][app-parameters-solution-explorer]

<span data-ttu-id="964ea-176">toocreate bir parametre dosyası yalnızca kopyalayın ve mevcut bir yapıştırın ve yeni bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="964ea-176">toocreate a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="964ea-177">Dağıtım sırasında ortama özgü parametreleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="964ea-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="964ea-178">Dağıtım sırasında uygulamanızla toochoose hello uygun parametre dosyası tooapply gerekir.</span><span class="sxs-lookup"><span data-stu-id="964ea-178">At deployment time, you need toochoose hello appropriate parameter file tooapply with your application.</span></span> <span data-ttu-id="964ea-179">Visual Studio'da hello Yayımla iletişim kutusu veya PowerShell aracılığıyla bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="964ea-179">You can do this through hello Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="964ea-180">Visual Studio'dan dağıtma</span><span class="sxs-lookup"><span data-stu-id="964ea-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="964ea-181">Visual Studio'da uygulamanız yayımladığınızda hello kullanılabilir parametre dosyalar listesinden seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="964ea-181">You can choose from hello list of available parameter files when you publish your application in Visual Studio.</span></span>

![Merhaba Yayımla iletişim kutusunda bir parametre dosyası seçin][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="964ea-183">Powershell'den dağıtma</span><span class="sxs-lookup"><span data-stu-id="964ea-183">Deploy from PowerShell</span></span>
<span data-ttu-id="964ea-184">Merhaba `Deploy-FabricApplication.ps1` hello uygulama projesi şablona dahil edilen PowerShell betiğini bir yayımlama profili bir parametre olarak kabul eder ve hello PublishProfile bir başvuru toohello uygulama parametreler dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="964ea-184">hello `Deploy-FabricApplication.ps1` PowerShell script included in hello application project template accepts a publish profile as a parameter and hello PublishProfile contains a reference toohello application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="964ea-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="964ea-185">Next steps</span></span>
<span data-ttu-id="964ea-186">Bu konuda, açıklanan hello temel kavramlar bazıları hakkında daha fazla toolearn hello bkz [Service Fabric teknik genel bakış](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="964ea-186">toolearn more about some of hello core concepts that are discussed in this topic, see hello [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="964ea-187">Visual Studio'da kullanılabilir olan diğer uygulama yönetim özellikleri hakkında daha fazla bilgi için bkz: [Visual Studio'da, Service Fabric uygulamaları yönetmek](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="964ea-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
