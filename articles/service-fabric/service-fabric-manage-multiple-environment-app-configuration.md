---
title: "Service Fabric birden çok ortamlarında yönetme | Microsoft Docs"
description: "Service Fabric uygulamaları bir makine boyutu makineler binlerce aralık kümeleri üzerinde çalıştırılabilir. Bazı durumlarda, uygulamanız bu çeşitli ortamlar için farklı yapılandırma isteyeceksiniz. Bu makalede, ortam başına farklı uygulama parametrelerini tanımlamak alınmaktadır."
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
ms.openlocfilehash: 9317b3f0b7984e795c4205360ed58e2c4f3fbcb1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="0784a-105">Birden çok ortamlar için uygulama parametreleri yönetme</span><span class="sxs-lookup"><span data-stu-id="0784a-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="0784a-106">Bir binlerce makineler için herhangi bir yerde kullanarak Azure Service Fabric kümeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0784a-106">You can create Azure Service Fabric clusters by using anywhere from one to many thousands of machines.</span></span> <span data-ttu-id="0784a-107">Uygulama ikili dosyaları değişiklik yapmadan bu paylaşılabilen çok sayıda ortamlar arasında çalıştırılabilir olsa da, genellikle uygulama için dağıtımı makineler sayısına bağlı olarak farklı şekilde, yapılandırmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="0784a-107">While application binaries can run without modification across this wide spectrum of environments, you often want to configure the application differently, depending on the number of machines you're deploying to.</span></span>

<span data-ttu-id="0784a-108">Basit bir örnek olarak göz önünde bulundurun `InstanceCount` durumsuz bir hizmet için.</span><span class="sxs-lookup"><span data-stu-id="0784a-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="0784a-109">Azure uygulamalarını çalıştırırken genellikle "-1" özel değeri için bu parametreyi ayarlayın istersiniz.</span><span class="sxs-lookup"><span data-stu-id="0784a-109">When you are running applications in Azure, you generally want to set this parameter to the special value of "-1".</span></span> <span data-ttu-id="0784a-110">Bu yapılandırma, hizmetiniz her düğümde Küme (veya bir yerleştirme kısıtlaması ayarlarsanız düğüm türü kümedeki her düğüm) çalıştığını sağlar.</span><span class="sxs-lookup"><span data-stu-id="0784a-110">This configuration ensures that your service is running on every node in the cluster (or every node in the node type if you have set a placement constraint).</span></span> <span data-ttu-id="0784a-111">Ancak, birden çok işlem tek bir makinede aynı uç noktasında dinleme olamaz beri bu yapılandırma bir tek makineli küme için uygun değil.</span><span class="sxs-lookup"><span data-stu-id="0784a-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on the same endpoint on a single machine.</span></span> <span data-ttu-id="0784a-112">Bunun yerine, genellikle ayarladığınız `InstanceCount` "1".</span><span class="sxs-lookup"><span data-stu-id="0784a-112">Instead, you typically set `InstanceCount` to "1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="0784a-113">Ortama özgü parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="0784a-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="0784a-114">Bu yapılandırma sorunun çözümü, parametreli varsayılan Hizmetleri ve belirli bir ortam için bu parametre değerlerini doldurun uygulama parametreleri dosyalarını kümesidir.</span><span class="sxs-lookup"><span data-stu-id="0784a-114">The solution to this configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="0784a-115">Varsayılan hizmet ve uygulama parametreleri uygulama ve hizmet bildirimleri yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="0784a-115">Default services and application parameters are configured in the application and service manifests.</span></span> <span data-ttu-id="0784a-116">Şema tanımı ServiceManifest.xml ve ApplicationManifest.xml dosyaları için Service Fabric SDK'sı ile yüklenir ve araçların *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="0784a-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml files is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="0784a-117">Varsayılan Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="0784a-117">Default services</span></span>
<span data-ttu-id="0784a-118">Service Fabric uygulamaları hizmet örnekleri koleksiyonu yapılır.</span><span class="sxs-lookup"><span data-stu-id="0784a-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="0784a-119">Boş bir uygulama oluşturun ve tüm hizmet örnekleri dinamik olarak oluşturmak mümkün olsa da, uygulamaların çoğu uygulama örneği oluşturulduğunda, her zaman oluşturulması gereken Çekirdek Hizmetleri kümesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0784a-119">While it is possible for you to create an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when the application is instantiated.</span></span> <span data-ttu-id="0784a-120">Bunlar, "varsayılan Hizmetleri" adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="0784a-120">These are referred to as "default services".</span></span> <span data-ttu-id="0784a-121">Uygulama bildiriminde köşeli parantez içine dahil ortamı başına yapılandırması yer tutucular ile belirtilir:</span><span class="sxs-lookup"><span data-stu-id="0784a-121">They are specified in the application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

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

<span data-ttu-id="0784a-122">Her adlandırılmış parametreleri uygulama bildirimi parametreleri öğe içinde tanımlanmış olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="0784a-122">Each of the named parameters must be defined within the Parameters element of the application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="0784a-123">DefaultValue özniteliği belirli bir ortam için daha özel parametre olmaması durumunda kullanılacak değeri belirtir.</span><span class="sxs-lookup"><span data-stu-id="0784a-123">The DefaultValue attribute specifies the value to be used in the absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="0784a-124">Tüm hizmet örneği parametreleri ortamı başına yapılandırması için uygun değildir.</span><span class="sxs-lookup"><span data-stu-id="0784a-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="0784a-125">Yukarıdaki örnekte, hizmetin bölümleme düzeni LowKey ve HighKey değerlerini bölüm aralığı ortam veri etki alanının işlev olduğundan tüm hizmet örnekleri için açık olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="0784a-125">In the example above, the LowKey and HighKey values for the service's partitioning scheme are explicitly defined for all instances of the service since the partition range is a function of the data domain, not the environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="0784a-126">Ortam başına hizmet yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="0784a-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="0784a-127">[Service Fabric uygulama modeli](service-fabric-application-model.md) çalışma zamanında okunabilir özel anahtar-değer çiftleri içeren yapılandırma paketleri eklenecek hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="0784a-127">The [Service Fabric application model](service-fabric-application-model.md) enables services to include configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="0784a-128">Bu ayarları değerlerini de ortamı tarafından belirterek Ayrıştırılan bir `ConfigOverride` uygulama bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="0784a-128">The values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in the application manifest.</span></span>

<span data-ttu-id="0784a-129">Config\Settings.xml dosyasında aşağıdaki ayar olduğunu varsayalım `Stateful1` hizmeti:</span><span class="sxs-lookup"><span data-stu-id="0784a-129">Suppose that you have the following setting in the Config\Settings.xml file for the `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="0784a-130">Bu değer belirli bir uygulama/ortamı çifti için geçersiz kılmak için oluşturma bir `ConfigOverride` içeri aktardığınızda uygulama bildiriminde hizmet bildirimi.</span><span class="sxs-lookup"><span data-stu-id="0784a-130">To override this value for a specific application/environment pair, create a `ConfigOverride` when you import the service manifest in the application manifest.</span></span>

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
<span data-ttu-id="0784a-131">Bu parametre yukarıda gösterildiği gibi ortamı tarafından sonra yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="0784a-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="0784a-132">Bu uygulama bildirimi Parametreler bölümünde bildirme ve ortama özgü değerleri uygulama parametresi dosyalarında belirterek yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0784a-132">You can do this by declaring it in the parameters section of the application manifest and specifying environment-specific values in the application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="0784a-133">Hizmet yapılandırma ayarları söz konusu olduğunda, burada bir anahtarın değerini ayarlanabilir üç yerde vardır: hizmeti yapılandırma paketi, uygulama bildirimi ve uygulama parametre dosyası.</span><span class="sxs-lookup"><span data-stu-id="0784a-133">In the case of service configuration settings, there are three places where the value of a key can be set: the service configuration package, the application manifest, and the application parameter file.</span></span> <span data-ttu-id="0784a-134">Service Fabric her zaman uygulama parametre dosyasından seçin (belirtilmişse) ilk sonra uygulama bildirimi ve son olarak yapılandırma paketi.</span><span class="sxs-lookup"><span data-stu-id="0784a-134">Service Fabric will always choose from the application parameter file first (if specified), then the application manifest, and finally the configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="0784a-135">Ayarlama ve ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="0784a-135">Setting and using environment variables</span></span> 
<span data-ttu-id="0784a-136">Belirtin ve ServiceManifest.xml dosyasında ortam değişkenlerini ayarlama ve daha sonra bu örneği başına temelinde ApplicationManifest.xml dosyasında geçersiz.</span><span class="sxs-lookup"><span data-stu-id="0784a-136">You can specify and set environment variables in the ServiceManifest.xml file and then override these in the ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="0784a-137">Aşağıdaki örnek, iki ortam değişkenleri, bir değer kümesiyle gösterir ve diğer geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="0784a-137">The example below shows two environment variables, one with a value set and the other is overridden.</span></span> <span data-ttu-id="0784a-138">Bu yapılandırma geçersiz kılma işlemleri için kullanılan aynı şekilde ortam değişkenlerinin değerlerini ayarlamak için uygulama parametreleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0784a-138">You can use application parameters to set environment variables values in the same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="0784a-139">Ortam değişkenleri ApplicationManifest.xml geçersiz kılmak için ServiceManifest ile kod paketinde başvuru `EnvironmentOverrides` öğesi.</span><span class="sxs-lookup"><span data-stu-id="0784a-139">To override the environment variables in the ApplicationManifest.xml, reference the code package in the ServiceManifest with the `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="0784a-140">Adlı hizmet örneği oluşturulduktan sonra ortam değişkenleri koddan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0784a-140">Once the named service instance is created you can access the environment variables from code.</span></span> <span data-ttu-id="0784a-141">Örneğin C# ile şunları yapabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0784a-141">e.g. In C# you can do the following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="0784a-142">Service Fabric ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="0784a-142">Service Fabric environment variables</span></span>
<span data-ttu-id="0784a-143">Service Fabric kümesi her hizmet örneği için ortam değişkenleri içindeki oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="0784a-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="0784a-144">Ortam değişkenlerinin tam listesi aşağıdadır, burada Listedekilerin kalın hizmetinizde, diğer Service Fabric çalışma zamanı tarafından kullanılan kullanacağınız olanlar.</span><span class="sxs-lookup"><span data-stu-id="0784a-144">The full list of environment variables is below, where the ones in bold are the ones that you will use in your service, the other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="0784a-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="0784a-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="0784a-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="0784a-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="0784a-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="0784a-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="0784a-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="0784a-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="0784a-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="0784a-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="0784a-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="0784a-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="0784a-151">**Fabric_Endpoint_ [YourServiceName] TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="0784a-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="0784a-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="0784a-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="0784a-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="0784a-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="0784a-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="0784a-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="0784a-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="0784a-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="0784a-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="0784a-156">Fabric_NodeId</span></span>
* <span data-ttu-id="0784a-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="0784a-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="0784a-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="0784a-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="0784a-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="0784a-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="0784a-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="0784a-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="0784a-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="0784a-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="0784a-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="0784a-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="0784a-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="0784a-163">FabricPackageFileName</span></span>

<span data-ttu-id="0784a-164">Kod belows Service Fabric ortam değişkenleri listesinde gösterilmiştir</span><span class="sxs-lookup"><span data-stu-id="0784a-164">The code belows shows how to list the Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="0784a-165">Adlı bir uygulama türü için ortam değişkenleri örnekleri aşağıda verilmiştir `GuestExe.Application` hizmet türü ile adlı `FrontEndService` yerel geliştirme makinenizde çalıştırdığınızda.</span><span class="sxs-lookup"><span data-stu-id="0784a-165">The following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="0784a-166">**Fabric_ApplicationName fabric:/GuestExe.Application =**</span><span class="sxs-lookup"><span data-stu-id="0784a-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="0784a-167">**Fabric_CodePackageName kodu =**</span><span class="sxs-lookup"><span data-stu-id="0784a-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="0784a-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="0784a-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="0784a-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="0784a-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="0784a-170">**Fabric_NodeName _Node_2 =**</span><span class="sxs-lookup"><span data-stu-id="0784a-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="0784a-171">Uygulama parametre dosyaları</span><span class="sxs-lookup"><span data-stu-id="0784a-171">Application parameter files</span></span>
<span data-ttu-id="0784a-172">Service Fabric uygulaması projesi bir veya daha fazla uygulama parametreleri dosyalarını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0784a-172">The Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="0784a-173">Bunların her birini, uygulama bildiriminde tanımlanan parametreler için özel değerler tanımlar:</span><span class="sxs-lookup"><span data-stu-id="0784a-173">Each of them defines the specific values for the parameters that are defined in the application manifest:</span></span>

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
<span data-ttu-id="0784a-174">Varsayılan olarak, yeni bir uygulama Local.1Node.xml, Local.5Node.xml ve Cloud.xml adlı üç uygulama parametreleri dosyalarını içerir:</span><span class="sxs-lookup"><span data-stu-id="0784a-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![Çözüm Gezgini'nde uygulama parametre dosyaları][app-parameters-solution-explorer]

<span data-ttu-id="0784a-176">Bir parametre dosyası oluşturmak için yalnızca kopyalayıp mevcut bir yapıştırın ve yeni bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="0784a-176">To create a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="0784a-177">Dağıtım sırasında ortama özgü parametreleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="0784a-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="0784a-178">Dağıtım sırasında uygulamanızla uygulamak için uygun parametre dosyası seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0784a-178">At deployment time, you need to choose the appropriate parameter file to apply with your application.</span></span> <span data-ttu-id="0784a-179">Visual Studio'da yayımlama iletişim kutusunu veya PowerShell aracılığıyla bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0784a-179">You can do this through the Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="0784a-180">Visual Studio'dan dağıtma</span><span class="sxs-lookup"><span data-stu-id="0784a-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="0784a-181">Visual Studio'da uygulamanız yayımladığınızda kullanılabilir parametre dosyalar listesinden seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0784a-181">You can choose from the list of available parameter files when you publish your application in Visual Studio.</span></span>

![Yayımla iletişim kutusunda bir parametre dosyası seçin][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="0784a-183">Powershell'den dağıtma</span><span class="sxs-lookup"><span data-stu-id="0784a-183">Deploy from PowerShell</span></span>
<span data-ttu-id="0784a-184">`Deploy-FabricApplication.ps1` Uygulama projesi şablona dahil PowerShell betiğini bir yayımlama profili bir parametre olarak kabul eder ve PublishProfile uygulama parametreler dosyası için bir başvuru içeriyor.</span><span class="sxs-lookup"><span data-stu-id="0784a-184">The `Deploy-FabricApplication.ps1` PowerShell script included in the application project template accepts a publish profile as a parameter and the PublishProfile contains a reference to the application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="0784a-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0784a-185">Next steps</span></span>
<span data-ttu-id="0784a-186">Bu konuda açıklanan kavramları bazıları hakkında daha fazla bilgi için bkz: [Service Fabric teknik genel bakış](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0784a-186">To learn more about some of the core concepts that are discussed in this topic, see the [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="0784a-187">Visual Studio'da kullanılabilir olan diğer uygulama yönetim özellikleri hakkında daha fazla bilgi için bkz: [Visual Studio'da, Service Fabric uygulamaları yönetmek](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="0784a-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
