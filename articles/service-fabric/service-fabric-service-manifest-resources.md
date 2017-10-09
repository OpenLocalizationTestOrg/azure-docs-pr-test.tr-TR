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
# <a name="specify-resources-in-a-service-manifest"></a>Bir hizmet bildiriminde kaynakları belirtme
## <a name="overview"></a>Genel Bakış
Merhaba hizmet bildirimi hello hizmet toobe tarafından bildirilen ve değiştirilen derlenmiş hello kodunu değiştirmeden kullanılan kaynakları sağlar. Azure Service Fabric hello hizmeti için uç nokta kaynakların yapılandırmasını destekler. Merhaba erişimine toohello hello hizmet bildiriminde belirtilen hello güvenlik grubuna hello uygulama bildiriminde aracılığıyla denetlenebilir. kaynakları Hello bildirimi hello hizmet toointroduce yeni bir yapılandırma mekanizması gerekmez anlamına dağıtım sırasında değiştirilmiş bu kaynakları toobe sağlar. Merhaba hello ServiceManifest.xml dosyası için şema tanımı hello Service Fabric SDK ile yüklenir ve çok Araçları*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

## <a name="endpoints"></a>Uç Noktalar
Bir uç nokta kaynağının hello hizmet bildiriminde tanımlandığında, Service Fabric bir bağlantı noktası açıkça belirtilmediğinde ayrılmış hello uygulama bağlantı noktası aralığından bağlantı noktaları atar. Örneğin, hello uç noktada arayın *ServiceEndpoint1* sonra bu paragraf sağlanan hello bildirim parçacığı belirtildi. Ayrıca, hizmetleri da belirli bir bağlantı noktasını bir kaynak isteğinde bulunabilirsiniz. Aynı düğüm paylaşımı hello bağlantı üzerinde çalışan bir hizmetin çoğaltmaları hello sırada hizmet çoğaltmaları farklı küme düğümleri üzerinde çalışan farklı bağlantı noktası numaraları atanabilir. Hello hizmet çoğaltmaları ardından bu bağlantı noktaları gerektiği için çoğaltma ve istemci isteklerini dinlemeye kullanabilirsiniz.

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

Çok başvuran[durum bilgisi olan güvenilir hizmetler yapılandırma](service-fabric-reliable-services-configuration.md) tooread uç noktaları hello yapılandırma paketi ayarları dosyasından (settings.xml) başvuran hakkında daha fazla bilgi.

## <a name="example-specifying-an-http-endpoint-for-your-service"></a>Örnek: hizmetiniz için bir HTTP uç noktası belirtme
Merhaba aşağıdaki hizmet bildirimi bir TCP uç nokta kaynağının ve iki HTTP uç noktası kaynakları hello tanımlar &lt;kaynakları&gt; öğesi.

HTTP otomatik olarak Service Fabric tarafından ACL misiniz noktalarıdır.

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

## <a name="example-specifying-an-https-endpoint-for-your-service"></a>Örnek: hizmetiniz için bir HTTPS uç noktası belirtme
Hello HTTPS protokolünü sunucu kimlik doğrulaması sağlar ve ayrıca istemci-sunucu iletişimi şifrelemek için kullanılır. Service Fabric hizmetinizi üzerinde tooenable HTTPS hello hello protokolü belirtmek *kaynakları uç noktaları -> Endpoint ->* hello uç noktası için daha önce gösterildiği gibi hello hizmet bildirimi bölümünü *ServiceEndpoint3* .

> [!NOTE]
> Bir hizmetin Protokolü uygulama yükseltme sırasında değiştirilemez. Yükseltme sırasında değiştirilir, önemli bir değişiklik olur.
> 
> 

HTTPS için tooset gerekir ApplicationManifest örnek aşağıda verilmiştir. Merhaba, sertifika parmak izi sağlanmalıdır. Merhaba EndpointRef ServiceManifest hello HTTPS protokolünü ayarlama içinde bir başvuru tooEndpointResource ' dir. Birden fazla EndpointCertificate ekleyebilirsiniz.  

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

## <a name="overriding-endpoints-in-servicemanifestxml"></a>ServiceManifest.xml uç noktalarını geçersiz kılma

Merhaba ApplicationManifest eşdüzey tooConfigOverrides bölümünde olacağı bir ResourceOverrides bölümü ekleyin. Bu bölümde hello hizmet bildiriminde belirtilen hello kaynaklar bölümünde hello uç noktalar bölümü için hello geçersiz kılma belirtebilirsiniz.

Sipariş toooverride ApplicationParameters değişikliği kullanarak ServiceManifest uç içinde aşağıdaki gibi ApplicationManifest hello:

Yeni bir bölüm "ResourceOverrides" Merhaba ServiceManifestImport Bölüm Ekle

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

Hello aşağıda parametreleri ekleyin:

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

Merhaba uygulamayı şimdi dağıtırken bu değerleri ApplicationParameters örneğin geçirebilirsiniz:

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

Not: Merhaba ApplicationParameters boş olan hello değerleri sağlarsanız, biz toohello varsayılan dön hello ServiceManifest EndPointName karşılık gelen hello için sağlanan değer.

Örneğin:

Merhaba belirttiğiniz ServiceManifest içindeki IF

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

Port1 hello ve Protocol1 ilgili uygulama parametreleri null veya boş değer. başlangıç bağlantı noktası hala ServiceFabric tarafından belirlenir. Ve hello protokol tcp olur.

Yanlış bir değer belirtin varsayalım. Gibi bağlantı noktası için bir dize değeri "Foo" yerine int belirttiğiniz  ServiceFabricApplication yeni komutu bir hata ile başarısız olur: Bölüm 'ResourceOverrides' name 'ServiceEndpoint1' özniteliğinde 'Port1' hello geçersiz kılma parametresi geçersiz. Belirtilen hello değeri 'Foo' ve gerekli 'int'.
