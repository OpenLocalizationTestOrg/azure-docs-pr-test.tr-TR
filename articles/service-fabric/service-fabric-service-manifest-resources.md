---
title: "aaaSpecifying Service Fabric hizmet uç noktaları | Microsoft Docs"
description: "Nasıl toodescribe uç noktası bir hizmette, nasıl dahil olmak üzere bildirim kaynakları tooset HTTPS uç noktalarının ayarlama"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="ea049-103">Bir hizmet bildiriminde kaynakları belirtme</span><span class="sxs-lookup"><span data-stu-id="ea049-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="ea049-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ea049-104">Overview</span></span>
<span data-ttu-id="ea049-105">Merhaba hizmet bildirimi hello hizmet toobe tarafından bildirilen ve değiştirilen derlenmiş hello kodunu değiştirmeden kullanılan kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea049-105">hello service manifest allows resources that are used by hello service toobe declared/changed without changing hello compiled code.</span></span> <span data-ttu-id="ea049-106">Azure Service Fabric hello hizmeti için uç nokta kaynakların yapılandırmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ea049-106">Azure Service Fabric supports configuration of endpoint resources for hello service.</span></span> <span data-ttu-id="ea049-107">Merhaba erişimine toohello hello hizmet bildiriminde belirtilen hello güvenlik grubuna hello uygulama bildiriminde aracılığıyla denetlenebilir.</span><span class="sxs-lookup"><span data-stu-id="ea049-107">hello access toohello resources that are specified in hello service manifest can be controlled via hello SecurityGroup in hello application manifest.</span></span> <span data-ttu-id="ea049-108">kaynakları Hello bildirimi hello hizmet toointroduce yeni bir yapılandırma mekanizması gerekmez anlamına dağıtım sırasında değiştirilmiş bu kaynakları toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea049-108">hello declaration of resources allows these resources toobe changed at deployment time, meaning hello service doesn't need toointroduce a new configuration mechanism.</span></span> <span data-ttu-id="ea049-109">Merhaba hello ServiceManifest.xml dosyası için şema tanımı hello Service Fabric SDK ile yüklenir ve çok Araçları*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="ea049-109">hello schema definition for hello ServiceManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="ea049-110">Uç Noktalar</span><span class="sxs-lookup"><span data-stu-id="ea049-110">Endpoints</span></span>
<span data-ttu-id="ea049-111">Bir uç nokta kaynağının hello hizmet bildiriminde tanımlandığında, Service Fabric bir bağlantı noktası açıkça belirtilmediğinde ayrılmış hello uygulama bağlantı noktası aralığından bağlantı noktaları atar.</span><span class="sxs-lookup"><span data-stu-id="ea049-111">When an endpoint resource is defined in hello service manifest, Service Fabric assigns ports from hello reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="ea049-112">Örneğin, hello uç noktada arayın *ServiceEndpoint1* sonra bu paragraf sağlanan hello bildirim parçacığı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ea049-112">For example, look at hello endpoint *ServiceEndpoint1* specified in hello manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="ea049-113">Ayrıca, hizmetleri da belirli bir bağlantı noktasını bir kaynak isteğinde bulunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea049-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="ea049-114">Aynı düğüm paylaşımı hello bağlantı üzerinde çalışan bir hizmetin çoğaltmaları hello sırada hizmet çoğaltmaları farklı küme düğümleri üzerinde çalışan farklı bağlantı noktası numaraları atanabilir.</span><span class="sxs-lookup"><span data-stu-id="ea049-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on hello same node share hello port.</span></span> <span data-ttu-id="ea049-115">Hello hizmet çoğaltmaları ardından bu bağlantı noktaları gerektiği için çoğaltma ve istemci isteklerini dinlemeye kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea049-115">hello service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="ea049-116">Çok başvuran[durum bilgisi olan güvenilir hizmetler yapılandırma](service-fabric-reliable-services-configuration.md) tooread uç noktaları hello yapılandırma paketi ayarları dosyasından (settings.xml) başvuran hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="ea049-116">Refer too[Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread more about referencing endpoints from hello config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="ea049-117">Örnek: hizmetiniz için bir HTTP uç noktası belirtme</span><span class="sxs-lookup"><span data-stu-id="ea049-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="ea049-118">Merhaba aşağıdaki hizmet bildirimi bir TCP uç nokta kaynağının ve iki HTTP uç noktası kaynakları hello tanımlar &lt;kaynakları&gt; öğesi.</span><span class="sxs-lookup"><span data-stu-id="ea049-118">hello following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in hello &lt;Resources&gt; element.</span></span>

<span data-ttu-id="ea049-119">HTTP otomatik olarak Service Fabric tarafından ACL misiniz noktalarıdır.</span><span class="sxs-lookup"><span data-stu-id="ea049-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="ea049-120">Örnek: hizmetiniz için bir HTTPS uç noktası belirtme</span><span class="sxs-lookup"><span data-stu-id="ea049-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="ea049-121">Hello HTTPS protokolünü sunucu kimlik doğrulaması sağlar ve ayrıca istemci-sunucu iletişimi şifrelemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ea049-121">hello HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="ea049-122">Service Fabric hizmetinizi üzerinde tooenable HTTPS hello hello protokolü belirtmek *kaynakları uç noktaları -> Endpoint ->* hello uç noktası için daha önce gösterildiği gibi hello hizmet bildirimi bölümünü *ServiceEndpoint3* .</span><span class="sxs-lookup"><span data-stu-id="ea049-122">tooenable HTTPS on your Service Fabric service, specify hello protocol in hello *Resources -> Endpoints -> Endpoint* section of hello service manifest, as shown earlier for hello endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="ea049-123">Bir hizmetin Protokolü uygulama yükseltme sırasında değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="ea049-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="ea049-124">Yükseltme sırasında değiştirilir, önemli bir değişiklik olur.</span><span class="sxs-lookup"><span data-stu-id="ea049-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="ea049-125">HTTPS için tooset gerekir ApplicationManifest örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ea049-125">Here is an example ApplicationManifest that you need tooset for HTTPS.</span></span> <span data-ttu-id="ea049-126">Merhaba, sertifika parmak izi sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea049-126">hello thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="ea049-127">Merhaba EndpointRef ServiceManifest hello HTTPS protokolünü ayarlama içinde bir başvuru tooEndpointResource ' dir.</span><span class="sxs-lookup"><span data-stu-id="ea049-127">hello EndpointRef is a reference tooEndpointResource in ServiceManifest, for which you set hello HTTPS protocol.</span></span> <span data-ttu-id="ea049-128">Birden fazla EndpointCertificate ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea049-128">You can add more than one EndpointCertificate.</span></span>  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="ea049-129">ServiceManifest.xml uç noktalarını geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="ea049-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="ea049-130">Merhaba ApplicationManifest eşdüzey tooConfigOverrides bölümünde olacağı bir ResourceOverrides bölümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea049-130">In hello ApplicationManifest add a ResourceOverrides section which will be a sibling tooConfigOverrides section.</span></span> <span data-ttu-id="ea049-131">Bu bölümde hello hizmet bildiriminde belirtilen hello kaynaklar bölümünde hello uç noktalar bölümü için hello geçersiz kılma belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea049-131">In this section you can specify hello override for hello Endpoints section in hello resources section specified in hello Service manifest.</span></span>

<span data-ttu-id="ea049-132">Sipariş toooverride ApplicationParameters değişikliği kullanarak ServiceManifest uç içinde aşağıdaki gibi ApplicationManifest hello:</span><span class="sxs-lookup"><span data-stu-id="ea049-132">In order toooverride EndPoint in ServiceManifest using ApplicationParameters change hello ApplicationManifest as following:</span></span>

<span data-ttu-id="ea049-133">Yeni bir bölüm "ResourceOverrides" Merhaba ServiceManifestImport Bölüm Ekle</span><span class="sxs-lookup"><span data-stu-id="ea049-133">In hello ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

<span data-ttu-id="ea049-134">Hello aşağıda parametreleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea049-134">In hello Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="ea049-135">Merhaba uygulamayı şimdi dağıtırken bu değerleri ApplicationParameters örneğin geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ea049-135">While deploying hello application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="ea049-136">Not: Merhaba ApplicationParameters boş olan hello değerleri sağlarsanız, biz toohello varsayılan dön hello ServiceManifest EndPointName karşılık gelen hello için sağlanan değer.</span><span class="sxs-lookup"><span data-stu-id="ea049-136">Note: If hello values provide for hello ApplicationParameters is empty we go back toohello default value provided in hello ServiceManifest for hello corresponding EndPointName.</span></span>

<span data-ttu-id="ea049-137">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ea049-137">For example:</span></span>

<span data-ttu-id="ea049-138">Merhaba belirttiğiniz ServiceManifest içindeki IF</span><span class="sxs-lookup"><span data-stu-id="ea049-138">If in hello ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="ea049-139">Port1 hello ve Protocol1 ilgili uygulama parametreleri null veya boş değer.</span><span class="sxs-lookup"><span data-stu-id="ea049-139">And hello Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="ea049-140">başlangıç bağlantı noktası hala ServiceFabric tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="ea049-140">hello port is still decided by ServiceFabric.</span></span> <span data-ttu-id="ea049-141">Ve hello protokol tcp olur.</span><span class="sxs-lookup"><span data-stu-id="ea049-141">And hello Protocol will tcp.</span></span>

<span data-ttu-id="ea049-142">Yanlış bir değer belirtin varsayalım.</span><span class="sxs-lookup"><span data-stu-id="ea049-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="ea049-143">Gibi bağlantı noktası için bir dize değeri "Foo" yerine int belirttiğiniz  ServiceFabricApplication yeni komutu bir hata ile başarısız olur: Bölüm 'ResourceOverrides' name 'ServiceEndpoint1' özniteliğinde 'Port1' hello geçersiz kılma parametresi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="ea049-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : hello override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="ea049-144">Belirtilen hello değeri 'Foo' ve gerekli 'int'.</span><span class="sxs-lookup"><span data-stu-id="ea049-144">hello value specified is 'Foo' and required is 'int'.</span></span>
