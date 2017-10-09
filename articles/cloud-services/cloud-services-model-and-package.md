---
title: aaaWhat olan bir bulut hizmeti modeli ve paket | Microsoft Docs
description: "Merhaba bulut hizmeti modeli (.csdef, .cscfg) ve Azure paketine (.cspkg) açıklanır"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a>Merhaba bulut hizmeti modeli nedir ve nasıl paket?
Bir bulut hizmeti üç bileşenlerini hello hizmet tanımı oluşturulur *(.csdef)*, hizmet yapılandırması hello *(.cscfg)*ve bir hizmet paketi *(.cspkg)*. Her iki hello **ServiceDefinition.csdef** ve **ServiceConfig.cscfg** dosyaları XML tabanlı ve topluca hello modeli olarak adlandırılan hello bulut hizmeti ve nasıl yapılandırılır; hello yapısını açıklar. Merhaba **ServicePackage.cspkg** hello oluşturulan bir zip dosyası **ServiceDefinition.csdef** ve bunun yanı sıra, tüm gerekli hello ikili tabanlı bağımlılıkları içerir. Azure, her iki hello bir bulut hizmeti oluşturur **ServicePackage.cspkg** ve hello **ServiceConfig.cscfg**.

Azure'da Hello bulut hizmeti çalışır duruma geldiğinde hello yeniden yapılandırabilirsiniz **ServiceConfig.cscfg** dosyası, ancak hello tanımı alter olamaz.

## <a name="what-would-you-like-tooknow-more-about"></a>Ne hakkında daha fazla tooknow istiyorsunuz?
* Merhaba hakkında daha fazla tooknow istediğiniz [ServiceDefinition.csdef](#csdef) ve [ServiceConfig.cscfg](#cscfg) dosyaları.
* Zaten bu hakkında bilebilirim ver [bazı örnekler](#next-steps) üzerinde ne ı yapılandırabilirsiniz.
* Toocreate hello istediğiniz [ServicePackage.cspkg](#cspkg).
* Visual Studio kullanarak ve istiyorum...
  * [Bir bulut hizmeti oluştur][vs_create]
  * [Var olan bir bulut hizmetini yeniden yapılandırın][vs_reconfigure]
  * [Bir bulut hizmeti projesini dağıtma][vs_deploy]
  * [Bir bulut hizmeti örneği içine Uzak Masaüstü][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
Merhaba **ServiceDefinition.csdef** dosyayı belirtir Azure tooconfigure tarafından kullanılan hello ayarları bir bulut hizmeti. Merhaba [Azure Hizmet tanım Şeması (.csdef dosyası)](https://msdn.microsoft.com/library/azure/ee758711.aspx) hello izin verilen biçim için bir hizmet tanımı dosyası sağlar. Merhaba aşağıdaki örnek hello Web ve çalışan rolleri için tanımlanan hello ayarlarını gösterir:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

Toohello başvurabilir [Hizmet tanım Şeması](https://msdn.microsoft.com/library/azure/ee758711.aspx) daha iyi burada kullanılan hello XML Şeması anlamak için Bununla birlikte, İşte bazı hello öğeleri hızlı bir açıklaması:

**Siteleri**  
IIS7'de barındırılan Web siteleri veya web uygulamaları için Hello tanımlarını içerir.

**InputEndpoints**  
Uç noktalar için Hello tanımları içeren toocontact hello bulut hizmeti kullanılır.

**InternalEndpoints**  
Rol örnekleri toocommunicate birbirleriyle tarafından kullanılan uç noktaları için Hello tanımlarını içerir.

**ConfigurationSettings**  
Belirli bir rol özellikleri için Hello ayarı tanımlarını içerir.

**Sertifikalar**  
Bir rol için gerekli sertifikaları için Hello tanımlarını içerir. Merhaba önceki kod örneğinde hello yapılandırmasını Azure bağlanmak için kullanılan bir sertifika gösterilmektedir.

**LocalResources**  
Yerel depolama kaynaklarını Hello tanımlarını içerir. Yerel depolama kaynağı hello sanal makinenin bir rol örneği çalıştığı hello dosya sisteminde ayrılmış bir dizindir.

**İçeri aktarmalar**  
İçeri aktarılan modüller Hello tanımlarını içerir. Hello önceki kod örneğinde, Uzak Masaüstü Bağlantısı ve Azure bağlanmak için hello modülleri gösterir.

**Başlangıç**  
Merhaba rol başladığında çalıştırılan görevleri içerir. Merhaba görevler bir .cmd veya yürütülebilir dosya içinde tanımlanır.

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>ServiceConfiguration.cscfg
Bulut hizmetiniz için hello ayarlarının Hello yapılandırmasını hello başlangıç değerleri belirlenir **ServiceConfiguration.cscfg** dosya. Bu dosyadaki her rol için toodeploy istediğiniz örneklerinin hello sayısını belirtin. Merhaba değerleri hello hizmet tanımı dosyasında tanımlanan hello yapılandırma ayarları için toohello hizmet yapılandırma dosyası eklenir. Merhaba bulut hizmetiyle ilişkili tüm yönetim sertifikaları için Hello parmak izleri toohello dosya de eklenir. Merhaba [Azure hizmet yapılandırma şeması (.cscfg dosyası)](https://msdn.microsoft.com/library/azure/ee758710.aspx) hello izin verilen biçim için bir hizmet yapılandırma dosyası sağlar.

Merhaba hizmet yapılandırma dosyası Merhaba uygulaması ile paketlenmiştir değil ancak ayrı bir dosya olarak karşıya yüklenen tooAzure olduğu ve kullanılan tooconfigure hello bulut hizmeti. Bulut hizmetinizi gerek olmadan yeni bir hizmet yapılandırma dosyası karşıya yükleyebilirsiniz. Merhaba bulut hizmeti çalışırken hello yapılandırma değerlerini hello bulut hizmeti için değiştirilebilir. Merhaba aşağıdaki örnek hello Web ve çalışan rolleri için tanımlanan hello yapılandırma ayarlarını gösterir:

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

Toohello başvurabilir [hizmet yapılandırma şeması](https://msdn.microsoft.com/library/azure/ee758710.aspx) burada kullanılan daha iyi anlamak hello XML Şeması, ancak hello öğeleri hızlı bir açıklaması aşağıda verilmiştir:

**Örnekleri**  
Örnekleri hello rol için çalışan sayısı hello yapılandırır. tooprevent, bulut hizmet olası yükseltmeleri sırasında kullanılamaz hale gelmesini web dönük rollerinizi birden fazla örneğini dağıtmanız önerilir. Birden fazla örneği dağıtarak hello toohello yönergeleri uymak [Azure işlem hizmet düzeyi sözleşmesi (SLA)](http://azure.microsoft.com/support/legal/sla/), Internet'e yönelik rolleri, iki %99,95 harici bağlantı garanti eder ya da daha fazla rol örnekleri için bir hizmet dağıtılır.

**ConfigurationSettings**  
Çalışan rolü için örnekler hello Hello ayarlarını yapılandırır. Merhaba Hello adını `<Setting>` öğeleri hello Ayar tanımlarına hello hizmet tanımı dosyasında eşleşmesi gerekir.

**Sertifikalar**  
Merhaba hizmeti tarafından kullanılan hello sertifikaları yapılandırır. Merhaba önceki kod örneğinde nasıl toodefine hello hello RemoteAccess modülü için sertifika gösterilmektedir. Merhaba hello değerini *parmak izi* toohello parmak izi hello sertifika toouse özniteliği ayarlanmalıdır.

<p/>

> [!NOTE]
> Merhaba sertifika parmak izi Hello toohello yapılandırma dosyasını bir metin düzenleyicisi kullanarak eklenebilir. Ya da hello değer üzerinde hello eklenebilir **sertifikaları** hello sekmesinde **özellikleri** Visual Studio'da hello rolünün sayfası.
> 
> 

## <a name="defining-ports-for-role-instances"></a>Rol örnekleri için bağlantı noktalarını tanımlama
Azure yalnızca bir giriş noktası tooa web rolü sağlar. Tüm trafiği aracılığıyla bir IP adresi oluştuğunu anlamına gelir. Merhaba ana bilgisayar üstbilgisi toodirect hello isteği toohello doğru konuma yapılandırarak, Web siteleri tooshare bir bağlantı noktası yapılandırabilirsiniz. Başlangıç IP adresi uygulamaları toolisten toowell bilinen bağlantı noktalarını da yapılandırabilirsiniz.

Merhaba aşağıdaki örnek bir Web sitesi ve web uygulaması içeren bir web rolü için başlangıç yapılandırmasını gösterir. Hello Web sitesi bağlantı noktası 80 üzerinde hello varsayılan giriş konumu olarak yapılandırılır ve hello web uygulamalardır yapılandırılmış tooreceive isteklerinden "mail.mysite.cloudapp.net" adlı bir alternatif ana bilgisayar üstbilgisi.

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a>Bir rolün Hello yapılandırmasını değiştirme
Azure'da hello hizmet çevrimdışı bırakmadan çalışırken, bulut hizmetinizin hello yapılandırma güncelleştirebilirsiniz. toochange yapılandırma bilgilerini, yeni bir yapılandırma dosyası ya da yükleyebilir veya düzenleme hello yapılandırma dosyasında yerleştirin ve hizmetini çalıştıran tooyour uygulayın. Merhaba aşağıdaki değişiklikleri hizmet toohello yapılandırmasını yapılabilir:

* **Merhaba değerleri yapılandırma ayarlarını değiştirme**  
  Bir yapılandırma ayarı değişiklikleri, bir rol örneği hello örneği çevrimiçi durumdayken tooapply hello değişiklik veya toorecycle hello örnek düzgün biçimde seçin ve hello örneği çevrimdışı durumdayken hello değişikliği uygulamak.
* **Merhaba Hizmeti topolojisi rol örneklerinin değiştirme**  
  Topolojisi değişiklikleri bir örneği burada kaldırılmakta dışında çalışan örneklerini etkilemez. Tüm kalan örnekleri geri dönüşüm toobe genellikle gerekmez; Ancak, rol örnekleri toorecycle yanıt tooa topoloji değişikliği seçebilirsiniz.
* **Merhaba sertifika parmak izi değiştirme**  
  Rol örneği çevrimdışı olduğunda, yalnızca bir sertifika güncelleştirebilirsiniz. Bir sertifika eklenmiş, silinmiş veya rol örneği çevrimiçi durumdayken değişti, Azure düzgün biçimde hello örneği çevrimdışı tooupdate hello sertifika alır ve hello değişiklik tamamlandıktan sonra yeniden çevrimiçi duruma getirin.

### <a name="handling-configuration-changes-with-service-runtime-events"></a>Yapılandırma değişiklikleriyle hizmeti çalışma zamanı olayları işleme
Merhaba [Azure çalışma zamanı kitaplığı](https://msdn.microsoft.com/library/azure/mt419365.aspx) hello içeren [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) ad alanı bir rolden Azure ortamı hello ile etkileşim kurmaya yönelik sınıflar sağlar. Merhaba [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) sınıfı önce ve sonra bir yapılandırma değişikliği yükseltilmiş olayları aşağıdaki hello tanımlar:

* **[Değiştirme](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) olayı**  
  Merhaba yapılandırma değişikliği uygulanan tooa belirtilen gerekirse fırsat tootake hello rol örnekleri aşağı vermiş bir rol örneği önce gerçekleşir.
* **[Değiştirilen](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) olayı**  
  Merhaba yapılandırma değişikliği uygulanan tooa belirtilen bir rol örneği olduğunda oluşur.

> [!NOTE]
> Sertifika değişiklikleri her zaman bir rolün örnekleri hello çevrimdışına çünkü hello RoleEnvironment.Changing veya RoleEnvironment.Changed olayları yükseltmeyin.
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
bir uygulamayı Azure bulut hizmeti olarak toodeploy, ilk paketi Merhaba uygulaması hello uygun biçimde gerekir. Merhaba kullanabilirsiniz **CSPack** komut satırı aracı (Merhaba ile yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/)) toocreate hello paket dosyası alternatif bir tooVisual Studio olarak.

**CSPack** kullanır hello hello hizmet tanımı dosya ve hizmet yapılandırma dosyası toodefine hello hello paketinin içeriğini içeriğini. **CSPack** hello kullanarak bir uygulama paketi dosyası (.cspkg tooAzure yükleyebilirsiniz) oluşturur [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy). Varsayılan olarak, adlı hello paket `[ServiceDefinitionFileName].cspkg`, ancak hello kullanarak farklı bir ad belirtebilirsiniz `/out` seçeneği **CSPack**.

**CSPack** bulunur  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> CSPack.exe (windows üzerinde) kullanılabilir hello çalıştırarak **Microsoft Azure komut istemi** hello SDK ile yüklenen kısayol.  
> 
> Hello CSPack.exe programını tek başına toosee belgelerine tüm hello olası anahtarları ve komutları çalıştırın.
> 
> 

<p />

> [!TIP]
> Bulut hizmetinizi yerel olarak çalıştırma hello **Microsoft Azure işlem öykünücüsü**, hello kullan **/copyonly** seçeneği. Bu seçenek hello hello uygulama tooa dizin düzenini içinden hello işlem öykünücüsü çalıştırılabilmesi için ikili dosyaları kopyalar.
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a>Örnek komut toopackage bir bulut hizmeti
Merhaba aşağıdaki örnek bir web rolü hello bilgilerini içeren bir uygulama paketi oluşturur. Merhaba hizmet tanımı dosyası toouse Hello komutu belirtir, ikili dosyaları burada olabilir hello dizin bulundu ve hello paket dosyasının adı hello.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

Merhaba uygulama bir web rolü ve çalışan rolü içeriyorsa, hello aşağıdaki komutu kullanılır:

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

Burada hello değişkenleri şunlardır:

| Değişken | Değer |
| --- | --- |
| \[DirectoryName\] |Merhaba alt hello .csdef dosyası hello Azure projesi, içerir hello kök proje dizini altında. |
| \[ServiceDefinition\] |Merhaba hizmet tanımı dosyası Hello adı. Varsayılan olarak, bu dosyayı ServiceDefinition.csdef olarak adlandırılır. |
| \[Çıkışdosyaadı\] |Merhaba adı hello için paket dosyası oluşturulur. Genellikle, bu Merhaba uygulaması toohello adına ayarlanır. Hiçbir dosya adı belirtilirse, hello uygulama paketi olarak oluşturuldu \[ApplicationName\].cspkg. |
| \[Rol adı\] |Merhaba hizmet tanımı dosyasında tanımlanan hello rolünün Hello adı. |
| \[RoleBinariesDirectory] |hello ikili dosyaları hello rolü için başlangıç konumu. |
| \[VirtualPath\] |Merhaba hello siteler bölümünde hello hizmet tanımı tanımlanan her sanal yol için fiziksel dizinler. |
| \[PhysicalPath\] |Merhaba hello site düğümünde hello hizmet tanımı tanımlanan her sanal yol için hello içeriğinin fiziksel dizinleri. |
| \[RoleAssemblyName\] |Merhaba rolü için ikili dosya hello Hello adı. |

## <a name="next-steps"></a>Sonraki adımlar
Bulut hizmeti paket oluşturma ve istiyorum...

* [Bir bulut hizmet örneği için Kurulum Uzak Masaüstü][remotedesktop]
* [Bir bulut hizmeti projesini dağıtma][deploy]

Visual Studio kullanarak ve istiyorum...

* [Yeni bir bulut hizmeti oluştur][vs_create]
* [Var olan bir bulut hizmetini yeniden yapılandırın][vs_reconfigure]
* [Bir bulut hizmeti projesini dağıtma][vs_deploy]
* [Bir bulut hizmet örneği için Kurulum Uzak Masaüstü][vs_remote]

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
