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
# <a name="model-an-application-in-service-fabric"></a>Service Fabric uygulamada modeli
Bu makalede hello Azure Service Fabric uygulama modeli ve toodefine bir uygulama ve hizmet aracılığıyla dosyaları nasıl bildirim genel bakış sağlar.

## <a name="understand-hello-application-model"></a>Merhaba uygulama modelini anlama
Bir uygulama, belirli bir işlevi veya işlevleri gerçekleştirmek bağlı hizmetler topluluğudur. Bir hizmet tam ve tek başına bir işlevi gerçekleştirir ve başlayın ve diğer hizmetler bağımsız olarak çalışır.  Kod, yapılandırma ve verileri bir servis oluşur. Her hizmet için kodu hello yürütülebilir ikili dosyaları oluşur, çalışma zamanında yüklenen hizmet ayarlarını yapılandırma oluşur ve rasgele statik verileri toobe hello hizmeti tarafından tüketilen veri oluşur. Bu hiyerarşik uygulama modeli her bileşenin bağımsız olarak sürümlü hem de yükseltilmiş olabilir.

![Merhaba Service Fabric uygulama modeli][appmodel-diagram]

Uygulama türü, bir uygulamanın bir kategori değil ve hizmet türlerinin bir dizi oluşur. Bir hizmetin kategori bir hizmet türüdür. Merhaba kategori farklı ayarları ve yapılandırmaları olabilir, ancak aynı hello çekirdek işlevselliğini kalır hello. Merhaba bir hizmet örnekleri olan hello farklı hizmet yapılandırma farklılıkları Merhaba aynı hizmeti türü.  

Sınıflar (veya "türleri") uygulamaları ve Hizmetleri XML dosyalarını (uygulama bildirimlerini ve hizmet bildirimlerini) açıklanan.  Merhaba bildirimleri göre hello kümenin görüntü deposundan uygulamaları oluşturulabilir hello şablonlarıdır. Merhaba hello ServiceManifest.xml ve ApplicationManifest.xml dosyası için şema tanımı hello Service Fabric SDK ile yüklenir ve çok Araçları*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

Merhaba kodu farklı bir uygulama örnekleri için ayrı işlemlerdeki bile tarafından barındırıldığında aynı Service Fabric düğümü hello gibi çalıştırın. Ayrıca, her uygulama örneğinin hello yaşam döngüsü (örneğin yükseltilmiş) yönetilebilir bağımsız olarak. Merhaba Aşağıdaki diyagramda uygulama türleri sırayla kod, yapılandırma ve veri paketleri oluşan hizmet türlerini tespiti gösterilmektedir. toosimplify hello diyagramı, yalnızca hello kod/config/verileri paketler için `ServiceType4` her hizmet türü bazı içerir veya bu tüm paket türlerinin de gösterilir.

![Service Fabric uygulama türleri ve hizmet türleri][cluster-imagestore-apptypes]

İki farklı bildirim dosyalarıdır kullanılan toodescribe uygulamalar ve hizmetler: Merhaba hizmet bildirimi ve uygulama bildirimi. Bildirimleri ayrıntılı bölümleri aşağıdaki hello olarak ele alınmaktadır.

Merhaba kümedeki etkin bir hizmet türünün bir veya daha fazla örneğini olabilir. Örneğin, durum bilgisi olan hizmet örneği veya çoğaltmalar, yüksek güvenilirlik hello kümedeki farklı düğümlerde bulunan çoğaltmalar arasında durumu yineleyerek elde edin. Bir kümedeki bir düğümün başarısız olsa bile çoğaltma temelde hello hizmet toobe için artıklık sağlar. A [bölümlenmiş hizmet](service-fabric-concepts-partitioning.md) daha ayrıntılı olarak böler hello kümedeki düğümler arasında kendi durumu (ve erişimi desenleri toothat durumu).

Merhaba Aşağıdaki diyagramda hello uygulamalar ve hizmet örnekleri, bölümler ve çoğaltmalar arasındaki ilişkiyi gösterir.

![Bölümler ve çoğaltmalar bir hizmet kapsamındaki][cluster-application-instances]

> [!TIP]
> Http:// hello Service Fabric Explorer aracını kullanarak bir küme uygulamalarının hello düzeni görüntüleyebileceği&lt;yourclusteraddress&gt;: 19080/Explorer. Daha fazla bilgi için bkz: [Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).
> 
> 

## <a name="describe-a-service"></a>Bir hizmeti açıklayın
Merhaba hizmet bildirimi hello hizmet türü ve sürümü bildirimli olarak tanımlar. Hizmet türü, sistem durumu özellikleri, Yük Dengeleme ölçümleri, hizmeti ikili dosyalarını ve yapılandırma dosyaları gibi hizmet meta verilerini belirtir.  Başka bir deyişle, bir hizmet paketi toosupport oluşturan hello kod, yapılandırma ve veri paketleri açıklar bir veya daha fazla hizmet türü. Basit bir örnek hizmet bildirimi şöyledir:

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

**Sürüm** öznitelikleri yapılandırılmamış dizelerdir ve hello sistem tarafından çözümlenmemiş. Sürüm öznitelikleri her bileşen yükseltmeler için kullanılan tooversion şunlardır.

**ServiceTypes** hangi hizmet türleri tarafından desteklenen bildirir **CodePackages** bu bildiriminde. Bu hizmet türlerinden birini karşı bir hizmet örneği oluşturulduğunda bu bildirimde belirtilen tüm kod paketleri kendi giriş noktaları çalıştırarak etkinleştirilir. Merhaba elde edilen beklenen tooregister hello desteklenen hizmet türlerinin çalışma zamanında işlemlerdir. Hizmet türlerini hello bildirim düzeyinde ve değil hello kod paketi düzeyinde bildirilir. Birden çok kod paket olduğunda hello sistem hizmet türleri bildirilen hello herhangi biri için görünür olduğunda bu nedenle bunlar tüm etkinleştirilir.

**SetupEntryPoint** hello Service Fabric aynı kimlik bilgileri ile çalışan bir ayrıcalıklı giriş noktasıdır (genellikle hello *LocalSystem* hesabı) önce başka bir giriş noktası. tarafından belirtilen hello yürütülebilir **EntryPoint** genellikle hello uzun süre çalışan hizmet ana bilgisayardır. uzun süre için toorun hello hizmet konağı yüksek ayrıcalıklara sahip olan ayrı Kurulum giriş noktası Hello varlığını önler. tarafından belirtilen hello yürütülebilir **EntryPoint** çalıştırıldıktan **SetupEntryPoint** başarıyla çıkar. Hello işlemi her zamankinden sonlandırır veya çöküyor hello elde edilen işlem yeniden ve izlendiği (yeniden itibaren **SetupEntryPoint**).  

Kullanma için tipik senaryolar **SetupEntryPoint** hello hizmeti başlamadan önce bir yürütülebilir dosyayı çalıştırmak veya yükseltilmiş ayrıcalıklarla bir işlem gerçekleştirdiğinizde durumdadır. Örneğin:

* Ayarlama ve hizmet yürütülebilir gereksinimleri hello ortam değişkenleri başlatılıyor. Bu sınırlı tooonly yürütülebilir dosyalar hello Service Fabric programlama modeli yazılmış değil. Örneğin, bir node.js uygulamasını dağıtmak için yapılandırılmış bazı ortam değişkenleri npm.exe gerekir.
* Güvenlik sertifikaları yükleyerek erişim denetimini ayarlama.

Konusunda daha fazla ayrıntı için tooconfigure hello **SetupEntryPoint** görmek [hizmet Kurulum giriş noktası için hello ilkesi yapılandırma](service-fabric-application-runas-security.md)

**EnvironmentVariables** Bu kod paketi için ayarlanan ortam değişkenlerini bir listesini sağlar. Environmentment değişkenleri hello geçersiz `ApplicationManifest.xml` tooprovide farklı hizmet örnekleri için farklı değerler. 

**Nın DataPackage** tarafından hello adlı bir klasör bildirir **adı** çalışma zamanında hello işlem tarafından kullanılan rasgele statik verileri toobe içeren öznitelik.

**ConfigPackage** tarafından hello adlı bir klasör bildirir **adı** içeren öznitelik, bir *Settings.xml* dosya. Hello ayarları dosyası hello işlem geri çalışma zamanında okur kullanıcı tanımlı, anahtar-değer çifti ayarları bölümleri içerir. Yalnızca yükseltme sırasında hello **ConfigPackage** **sürüm** değişti, işlem çalışan hello yeniden sonra. Bunun yerine, bir geri çağırma bunlar dinamik olarak yeniden, böylece yapılandırma ayarlarının değişip hello işlem bildirir. İşte bir örnek *Settings.xml* dosyası:

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> Bir hizmet bildirimi birden çok kodu, yapılandırma ve veri paketleri içerebilir. Bunların her biri bağımsız olarak sürümlü olabilir.
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

## <a name="describe-an-application"></a>Bir uygulamayı tanımlayan
Merhaba uygulama bildirimi bildirimli olarak hello uygulama türü ve sürümü açıklar. Hizmet oluşturma meta veri şema, örnek sayısı/çoğaltma faktörü, güvenlik/yalıtım İlkesi, yerleştirme kısıtlamaları, yapılandırma geçersiz kılmaları ve bağlı hizmet türü bölümleme kararlı adları gibi belirtir. Merhaba Yük Dengeleme etki alanları Merhaba uygulaması yerleştirildiği de açıklanmaktadır.

Bu nedenle, bir uygulama bildirimi hello uygulama düzeyinde öğeleri açıklar ve başvuran bir veya daha fazla hizmet uygulama türü toocompose bildirimleri. Basit bir örnek uygulama bildirimi şöyledir:

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

Gibi hizmet bildirimlerini **sürüm** öznitelikleri yapılandırılmamış dizelerdir ve hello sistem tarafından çözümlenmemiş. Sürüm öznitelikleri ayrıca her bileşen yükseltmeler için kullanılan tooversion değildir.

**ServiceManifestImport** bu uygulama türü oluşturan başvurular tooservice bildirimlerini içerir. Alınan hizmet bildirimlerini hangi hizmet türleri içindeki bu uygulama türü geçerli belirler. Merhaba ServiceManifestImport içinde ServiceManifest.xml dosyalarında Settings.xml ve ortam değişkenleri içindeki yapılandırma değerleri geçersiz. 


**DefaultServices** bir uygulama bu uygulama türü karşı örneği olduğunda, otomatik olarak oluşturulan hizmet örnekleri bildirir. Varsayılan Hizmetleri yalnızca kolaylık sağlamak ve oluşturulduktan sonra her açısından normal services gibi davranır. Bunların yanı sıra diğer hizmetlere hello uygulama örneğinde yükseltilir ve de kaldırılabilir.

> [!NOTE]
> Bir uygulama bildirimi birden çok hizmet bildirimi alır ve varsayılan hizmet içerebilir. Her hizmet bildirim alma bağımsız olarak sürümlü olabilir.
> 
> 

toomaintain farklı uygulama ve hizmet parametreleri tek tek ortamlar için nasıl görürüm toolearn [birden çok ortamlar için uygulama parametreleri yönetme](service-fabric-manage-multiple-environment-app-configuration.md).

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Sonraki adımlar
[Bir uygulama paketi](service-fabric-package-apps.md) ve toodeploy kullanıma hazır hale getirin.

[Dağıtma ve uygulamaları kaldırma] [ 10] açıklar nasıl toouse PowerShell toomanage uygulama örnekleri.

[Birden çok ortamlar için uygulama parametreleri yönetme] [ 11] açıklar nasıl tooconfigure parametreleri ve farklı uygulama örnekleri için ortam değişkenleri.

[Uygulamanız için güvenlik ilkelerini yapılandırmak] [ 12] toorun güvenlik ilkeleri toorestrict erişim'in altında hizmetleri nasıl açıklar.

[Uygulama barındırma modellerini] [ 13] bir dağıtılan hizmet ve hizmet ana bilgisayar işlemi çoğaltmaları (veya örnekleri) arasındaki ilişkiyi açıklar.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
