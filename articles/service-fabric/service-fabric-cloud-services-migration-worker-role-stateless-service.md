---
title: "Azure Cloud Services uygulamalarını toomicroservices aaaConvert | Microsoft Docs"
description: "Bu kılavuz bulut Hizmetleri Web karşılaştırır ve çalışan rolleri ve Service Fabric durum bilgisi olmayan hizmetler toohelp bulut Hizmetleri tooService doku ' geçirme."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a>Tooconverting Web ve çalışan rolleri tooService doku durum bilgisi olmayan hizmetler Kılavuzu
Bu makalede nasıl toomigrate, bulut Hizmetleri Web ve çalışan rolleri tooService doku durum bilgisi olmayan hizmetler. Uygulamalar, genel mimarisi toostay kabaca gittiği aynı hello için bulut Hizmetleri tooService doku hello en basit geçiş yolu budur.

## <a name="cloud-service-project-tooservice-fabric-application-project"></a>Bulut hizmeti projesi tooService doku uygulama projesi
 Uygulamanızı dağıtılan toorun hello tam paket uygulamanız - diğer bir deyişle, bunların her tanımlamak için bir bulut hizmeti projesi ve bir Service Fabric uygulaması projesi benzer bir yapıya ve her iki temsil hello dağıtım birimi sahiptir. Bir bulut hizmeti projesi, bir veya daha fazla Web veya çalışan rolleri içerir. Benzer şekilde, bir Service Fabric uygulaması projesi bir veya daha fazla hizmet içeriyor. 

Merhaba Service Fabric uygulaması projesi yalnızca dağıtılacak bir uygulama tanımlar ancak hello hello bulut hizmeti projesi tüm çiftler VM dağıtımı ile uygulama dağıtımı hello ve bu nedenle, VM yapılandırma ayarlarını içeren farktır Service Fabric kümesindeki var olan VM'ler tooa kümesi. hello Azure portal veya bir Resource Manager şablonu aracılığıyla ve birden çok Service Fabric uygulamaları kullanılabilecek tooit dağıtıldığında hello Service Fabric kümesi kendisi yalnızca dağıtılır.

![Service Fabric ve Cloud Services proje karşılaştırma][3]

## <a name="worker-role-toostateless-service"></a>Çalışan rolü toostateless hizmeti
Kavramsal olarak, bir çalışan rolü hello iş yükü, her örneği aynıdır ve istekleri yönlendirilmiş tooany örnek herhangi bir zamanda olabilir anlamına durum bilgisiz iş yükünü temsil eder. Her bir örnek beklenen tooremember hello önceki isteği değil. Merhaba iş yükü çalışır durum üzerinde Azure Table Storage veya Azure belge DB gibi bir dış durum depolama alanını tarafından yönetilir. Service Fabric iş yükü bu tür bir durum bilgisiz hizmeti tarafından temsil edilir. Merhaba basit bir yaklaşım toomigrating çalışan rolü tooService doku çalışan rolü kodunu tooa durum bilgisiz hizmet dönüştürme yapılabilir.

![Çalışan rolü tooStateless hizmeti][4]

## <a name="web-role-toostateless-service"></a>Web rolü toostateless hizmeti
Benzer tooWorker rolü, Web rolü ayrıca durum bilgisiz iş yükünü temsil eder ve bu nedenle kavramsal çok eşlenen tooa Service Fabric durum bilgisiz hizmet olabilir. Ancak, Web rolünden farklı olarak, IIS Service Fabric desteklemez. toomigrate bir web uygulaması Web rolü tooa durum bilgisiz hizmetinden kendi kendini barındırır ve IIS veya ASP.NET Core 1 gibi System.Web bağlı olmayan ilk taşıma tooa web framework gerektirir.

| **Uygulama** | **Destekleniyor** | **Geçiş yolu** |
| --- | --- | --- |
| ASP.NET Web formları |Hayır |Dönüştürme tooASP.NET 1 MVC çekirdek |
| ASP.NET MVC |İle geçiş |Yükseltme tooASP.NET 1 MVC çekirdek |
| ASP.NET Web API'si |İle geçiş |Kendini barındıran sunucu veya ASP.NET Core 1 kullanın |
| ASP.NET Core 1 |Evet |Yok |

## <a name="entry-point-api-and-lifecycle"></a>Giriş noktası API ve yaşam döngüsü
Çalışan rolü ve Service Fabric API'leri teklif benzer giriş noktaları hizmeti: 

| **Giriş noktası** | **Çalışan rolü** | **Service Fabric hizmeti** |
| --- | --- | --- |
| İşleme |`Run()` |`RunAsync()` |
| VM Başlat |`OnStart()` |Yok |
| VM'yi Durdur |`OnStop()` |Yok |
| İstemci istekleri için açık dinleyicisi |Yok |<ul><li> `CreateServiceInstanceListener()`için durum bilgisiz</li><li>`CreateServiceReplicaListener()`durum bilgisi için</li></ul> |

### <a name="worker-role"></a>Çalışan rolü
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a>Doku durum bilgisiz hizmeti
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

Hem birincil "Çalıştır" geçersiz kılma hangi toobegin işlemede sahiptir. Service Fabric Hizmetleri birleştirme `Run`, `Start`, ve `Stop` tek bir giriş noktasına `RunAsync`. Hizmetinizi ne zaman çalışmaya başlaması gereken `RunAsync` başlar ve hello çalışma durması gerektiğini `RunAsync` yöntemin CancellationToken durdurulma. 

Merhaba yaşam döngüsü ve çalışan rolleri ve Service Fabric Hizmetleri ömrü arasında birkaç temel farklılıklar vardır:

* **Yaşam döngüsü:** çalışan rolü VM ve bu nedenle, yaşam döngüsü olduğunu bağlı toohello zaman hello VM başlatır ve durdurur olaylarını içerir VM hello büyük fark vardır. Service Fabric hizmeti, birbiriyle ilgili olmayan gibi hello zaman konak VM veya makine başlar ve durdurun, olayları içermez böylece hello VM döngüsü, ayrı bir yaşam döngüsü sahiptir.
* **Yaşam süresi:** çalışan rolü örneği hello varsa geri `Run` yöntemi çıkar. Merhaba `RunAsync` bir Service Fabric hizmeti yönteminde ancak çalıştırabilirsiniz toocompletion ve hello hizmet örneği oluşturan kalacak. 

Service Fabric, istemci isteklerini dinlemek Hizmetleri için isteğe bağlı iletişim Kurulum giriş noktası sağlar. Merhaba RunAsync ve iletişim giriş noktası hello RunAsync yöntemi olmadan tooexit izin - hizmetiniz tooonly dinleme tooclient istekleri seçin veya yalnızca bir işleme döngüsü ya da her ikisini de Çalıştır - Service Fabric hizmetlerini isteğe bağlı bir geçersiz kılma olan istemci istekleri için toolisten devam çünkü hello hizmet örneği, yeniden başlatılıyor.

## <a name="application-api-and-environment"></a>Uygulama API ve ortam
Merhaba bulut Hizmetleri ortam API bilgi ve işlevsellik hello geçerli VM örneği yanı sıra diğer VM rolü örneklerini hakkında bilgi sağlar. Service Fabric tooits çalışma zamanı ile ilgili bilgiler ve hello düğüm hizmet hakkındaki bazı bilgileri şu anda çalışan sağlar. 

| **Ortam görev** | **Cloud Services** | **Service Fabric** |
| --- | --- | --- |
| Yapılandırma ayarları ve değişiklik bildirimi |`RoleEnvironment` |`CodePackageActivationContext` |
| Yerel Depolama |`RoleEnvironment` |`CodePackageActivationContext` |
| Uç nokta bilgileri |`RoleInstance` <ul><li>Geçerli örnek:`RoleEnvironment.CurrentRoleInstance`</li><li>Diğer roller ve örneği:`RoleEnvironment.Roles`</li> |<ul><li>`NodeContext`Geçerli düğüm adresi</li><li>`FabricClient`ve `ServicePartitionResolver` hizmet uç noktası bulma</li> |
| Ortam öykünmesi |`RoleEnvironment.IsEmulated` |Yok |
| Eşzamanlı değişiklik olayı |`RoleEnvironment` |Yok |

## <a name="configuration-settings"></a>Yapılandırma ayarları
Bulut hizmetleri yapılandırma ayarlarında bir VM rolü için ayarlanır ve bu VM rolü örneklerini tooall uygulayın. Bu ayarlar, anahtar-değer çiftleri ServiceConfiguration.*.cscfg dosyalarında ayarlamak ve doğrudan RoleEnvironment erişilebilir. Bir VM birden çok hizmet ve uygulamaları barındırmak için Service Fabric içinde ayarlarını ayrı ayrı tooa VM yazmak yerine tooeach hizmetini ve tooeach uygulama uygulayın. Bir hizmet üç paketlerini oluşur:

* **Kod:** hello hizmeti yürütülebilir dosyaları, ikili dosyaları, DLL'ler ve diğer dosyaları içeren bir hizmet toorun gerekiyor.
* **Config:** tüm yapılandırma dosyalarını ve ayarlarını bir hizmet için.
* **Veri:** hello hizmetiyle ilişkili statik veri dosyaları.

Bu paketleri her bağımsız olarak sürümlü hem de yükseltilmiş olabilir. Benzer tooCloud Hizmetleri, bir yapılandırma paketi bir API aracılığıyla programlı olarak erişilebilir ve bir yapılandırma paketi değişikliği kullanılabilir toonotify hello hizmetine olaylardır. Settings.xml dosyası anahtar-değer yapılandırma ve programlı erişim benzer toohello uygulama ayarları bölümünde bir App.config dosyası için kullanılabilir. Ancak, XML, JSON, YAML veya özel bir ikili biçimi olup bulut Hizmetleri, herhangi bir biçimdeki tüm yapılandırma dosyalarını bir Service Fabric yapılandırma paketi içerebilir. 

### <a name="accessing-configuration"></a>Erişimi yapılandırma
#### <a name="cloud-services"></a>Cloud Services
Yapılandırma ayarları ServiceConfiguration.*.cscfg üzerinden erişilebilir `RoleEnvironment`. Bu ayarları hello genel olarak kullanılabilir tooall rol örnekleri olan aynı bulut hizmeti dağıtımı.

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a>Service Fabric
Her hizmetin kendi tek tek bir yapılandırma paketi vardır. Hiçbir yerleşik mekanizması olduğunu genel yapılandırma ayarları için erişilebilir bir kümedeki tüm uygulamalar tarafından. Service Fabric'ın özel Settings.xml yapılandırma dosyasının bir yapılandırma paketi içinde kullanırken, uygulama düzeyinde yapılandırma ayarlarını edinerek hello uygulama düzeyinde Settings.xml değerlerde üzerine yazılabilir.

Yapılandırma ayarları hello hizmetin aracılığıyla her hizmet örneği içinde erişimleri olan `CodePackageActivationContext`.

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a>Yapılandırma güncelleştirme olayları
#### <a name="cloud-services"></a>Cloud Services
Merhaba `RoleEnvironment.Changed` tüm rol örneklerinin bir değişiklik olduğunda oluşur bir yapılandırma değişikliği gibi hello ortamda kullanılan toonotify bir olaydır. Rol örnekleri geri dönüştürme ya da bir çalışan işleminin yeniden başlatmadan olmadan kullanılan tooconsume yapılandırma güncelleştirmeleri budur.

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a>Service Fabric
Bir hizmette - kod, yapılandırma ve verileri - hello üç paket türlerinin her biri bir paket güncelleştirildi, eklenen veya kaldırılan bir hizmet örneği bildir olayları vardır. Bir hizmet birden çok paket her tür içerebilir. Örneğin, bir hizmet birden çok yapılandırma paketleri, tek tek her sürümü tutulan ve yükseltilebilir olabilir. 

Bu olaylar, hello hizmet örneği başlatmadan hizmet paketleri, kullanılabilir tooconsume değişir.

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a>Başlangıç görevi
Başlatma, bir uygulama başlatılmadan önce gerçekleştirilen eylemler görevlerdir. Yükseltilmiş ayrıcalıklar kullanarak genellikle kullanılan toorun Kurulum betikleri bir başlangıç görevdir. Bulut Hizmetleri ve Service Fabric başlangıç görevleri destekler. Merhaba temel fark söz konusu bulut Hizmetleri, bir rol örneği bir parçası olduğundan Service Fabric bağlı tooany değil bağlı tooa hizmet başlangıç görevi iken bir başlangıç görevi bağlı tooa VM belirli VM.

| Cloud Services | Service Fabric |
| --- | --- | --- |
| Yapılandırma konumu |ServiceDefinition.csdef |
| Ayrıcalıkları |"sınırlı" veya "yükseltilmiş" |
| Sıralama |"Basit", "arka plan", "ön" |

### <a name="cloud-services"></a>Cloud Services
Bulut Hizmetleri başlatma giriş noktası ServiceDefinition.csdef rol başına yapılandırılır. 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a>Service Fabric
Service Fabric başlangıç giriş noktası ServiceManifest.xml hizmetinde başına yapılandırılır:

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a>Geliştirme ortamı hakkında bir Not
Bulut Hizmetleri ve Service Fabric tümleşik ile Visual Studio Proje şablonları ve hata ayıklama, yapılandırma ve her ikisi de yerel olarak dağıtma desteği ve tooAzure. Service Fabric ve bulut hizmetlerini de bir yerel geliştirme çalışma zamanı ortamı sağlar. Merhaba, farktır sırada hello bulut hizmeti geliştirme çalışma zamanı öykünür Merhaba, çalıştığı Azure ortamı, Service Fabric bir öykünücü kullanmaz - hello tam Service Fabric çalışma zamanını kullanır. Merhaba Service Fabric, yerel geliştirme makinenizde çalıştırma ortamıdır hello üretimde çalışan aynı ortamı.

## <a name="next-steps"></a>Sonraki adımlar
Service Fabric Reliable Services ve hello bulut Hizmetleri ve Service Fabric uygulama mimarisi toounderstand hello tam tootake avantajlarından Service Fabric özelliklerinin nasıl ayarlanacağını arasındaki temel farklar hakkında daha fazlasını okuyun.

* [Service Fabric Reliable Services ile çalışmaya başlama](service-fabric-reliable-services-quick-start.md)
* [Bulut Hizmetleri ve Service Fabric arasındaki kavramsal Kılavuzu toohello farklar](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
