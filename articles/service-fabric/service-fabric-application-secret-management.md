---
title: "Service Fabric uygulamaları aaaManaging parolalarında | Microsoft Docs"
description: "Bu makalede nasıl toosecure gizli bir Service Fabric uygulaması değerleri açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a>Service Fabric uygulamaları parolaları yönetme
Bu kılavuzda, Service Fabric uygulaması parolalarında yönetme hello adımlar anlatılmaktadır. Gizli depolama bağlantı dizeleri, parolalar veya düz metin olarak işleneceğini olmayan diğer değerleri gibi herhangi bir önemli bilgi olabilir.

Bu kılavuz, Azure anahtar kasası toomanage anahtarları ve gizli anahtarları kullanır. Ancak, *kullanarak* gizli bir uygulamada olduğu herhangi bir yerde barındırılan bulut platformu belirsiz tooallow uygulamaları toobe dağıtılan tooa küme. 

## <a name="overview"></a>Genel Bakış
Merhaba önerilen yöntem toomanage hizmeti yapılandırma ayarları olan aracılığıyla [hizmet yapılandırma paketleri][config-package]. Yapılandırma paketleri sürümlü ve sistem durumu doğrulama ve Otomatik geri alma ile yönetilen yükseltmelerini aracılığıyla güncelleştirilebilir. Genel hizmet kesintisi hello olasılığını azaltır olarak tercih edilen tooglobal yapılandırma budur. Şifrelenmiş parolalar hiçbir istisnadır. Service Fabric şifreleme ve şifre çözme sertifikası şifreleme kullanarak bir yapılandırma paketi Settings.xml dosyasındaki değerleri için yerleşik özellikler vardır.

Merhaba Aşağıdaki diyagramda bir Service Fabric uygulaması gizli yönetimi için temel akış hello gösterilmektedir:

![Gizli yönetimine genel bakış][overview]

Bu akış dört ana adım vardır:

1. Veri şifreleme sertifikası alın.
2. Kümenizdeki Hello sertifikası yükleyin.
3. Bir uygulamayı hello sertifikayla dağıtırken gizli değerleri şifrelemek ve bir hizmetin Settings.xml yapılandırma dosyasına Ekle.
4. İle şifre çözme tarafından şifrelenmiş okuma değerleri Settings.xml dışında aynı şifreleme sertifikası hello. 

[Azure anahtar kasası] [ key-vault-get-started] burada yolu tooget ve sertifikalar için bir güvenli depolama konumu olarak kullanılan Azure Service Fabric kümeleri üzerinde yüklü olan sertifikalar. TooAzure değil dağıtıyorsanız, Service Fabric uygulamaları toouse anahtar kasası toomanage parolalarında gerekmez.

## <a name="data-encipherment-certificate"></a>Veri şifreleme sertifikası
Veri şifreleme sertifikası kesinlikle şifreleme için kullanılır ve şifre çözme yapılandırmasının bir hizmetin Settings.xml değerleri ve kimlik doğrulaması için kullanılan veya şifre metin imzalama değil. Merhaba sertifika hello aşağıdaki gereksinimleri karşılamalıdır:

* Merhaba sertifika özel anahtar içermelidir.
* anahtar değişimi için dışarı aktarılabilir tooa kişisel bilgi değişimi (.pfx) dosyasını Hello sertifika oluşturulması gerekir.
* Merhaba sertifika anahtar kullanımı veri şifreleme (10) içermelidir ve sunucu kimlik doğrulaması veya istemci kimlik doğrulaması içermemesi gerekir. 
  
  Örneğin, PowerShell kullanarak otomatik olarak imzalanan bir sertifika oluştururken hello `KeyUsage` bayrağı çok ayarlanmalıdır`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>Kümenizdeki Hello sertifika yükleme
Bu sertifika, hello kümedeki her düğümde yüklenmelidir. Bir hizmetin Settings.xml depolanan çalışma zamanı toodecrypt değerleri kullanılacaktır. Bkz: [nasıl toocreate Azure Kaynak Yöneticisi'ni kullanarak bir küme] [ service-fabric-cluster-creation-via-arm] kurulum yönergeleri. 

## <a name="encrypt-application-secrets"></a>Uygulama parolaları şifrelemek
Merhaba Service Fabric SDK yerleşik gizli şifreleme ve şifre çözme işlevi vardır. Gizli değerleri yerleşik anda şifrelenmiş şifresi ve program aracılığıyla hizmet kodunda okuyun. 

PowerShell komutunu aşağıdaki hello kullanılan tooencrypt gizli ' dir. Bu komut, yalnızca hello değeri şifreler; Mevcut **değil** oturum hello şifreli metin. Merhaba kullanmalısınız gizli değerleri için küme tooproduce ciphertext yüklü aynı şifreleme sertifikası:

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

Merhaba sonuç base-64 dizesi hem hello gizli ciphertext, hem de kullanılan tooencrypt edildi hello sertifikayla ilgili bilgileri içeren.  Merhaba base 64 kodlu bir dize parametresi hizmetinizin Settings.xml yapılandırma dosyasındaki hello ile eklenebilir `IsEncrypted` özniteliği ayarlanmış çok`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>Uygulama örnekleri uygulama parolaları Ekle
İdeal olarak, dağıtım toodifferent ortamları gibi otomatik olmalıdır. Bu, gizli şifreleme bir yapı ortamında gerçekleştirme ve şifrelenmiş hello gizli parametre olarak uygulama örnekleri oluşturulurken sağlama gerçekleştirilebilir.

#### <a name="use-overridable-parameters-in-settingsxml"></a>Geçersiz kılınabilir parametreler Settings.xml kullanın
Merhaba Settings.xml yapılandırma dosyası uygulama oluşturma sırasında sağlanan geçersiz kılınabilir parametrelere izin verir. Kullanım hello `MustOverride` parametresi için bir değer sağlamak yerine özniteliği:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

Settings.xml, toooverride değerleri ApplicationManifest.xml hello hizmeti için bir geçersiz kılma parametresi bildirin:

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

Merhaba değeri olarak belirtilebilir şimdi bir *uygulama parametresi* hello uygulamasının bir örneğini oluştururken. Uygulama örneğini oluşturmak komut dosyasıyla PowerShell kullanarak veya bir derleme işlemindeki kolay tümleştirme için C# ile yazılmış.

PowerShell kullanarak hello sağlanan toohello parametredir `New-ServiceFabricApplication` olarak komutunu bir [karma tablosu](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

C# kullanarak, uygulama parametreleri belirtilen bir `ApplicationDescription` olarak bir `NameValueCollection`:

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a>Hizmet kodundan gizli şifresini çözme
Service Fabric Hizmetleri'nde altında ağ hizmeti varsayılan olarak Windows üzerinde çalışan ve erişim toocertificates yüklenmemiş bazı ek kurulum olmadan hello düğümde.

Veri şifreleme sertifikasını kullanırken toomake erişim toohello sertifikanın özel anahtarı ağ hizmeti veya seçtiğiniz kullanıcı hesabı hello hizmetinin altında çalışmakta olduğundan emin gerekir. Service Fabric toodo şekilde yapılandırmanız varsa erişim hizmetiniz için otomatik olarak verme işleyecek. Bu yapılandırma, kullanıcılar ve sertifikalar için güvenlik ilkelerini tanımlayarak ApplicationManifest.xml yapılabilir. Aşağıdaki örneğine hello hello NETWORK SERVICE hesabının okuma erişimi tooa sertifika, parmak izi tarafından tanımlanan verilmiştir:

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> Sertifika parmak izi kopyalarken Windows hello Sertifika ek bileşenini depolamak, görünmeyen bir karakter hello hello parmak izi dize başında yerleştirilir. Bu görünmez karakteri hata toolocate çalışırken bir sertifika neden olabilir parmak izi tarafından bu ek karakter böylece emin toodelete olması.
> 
> 

### <a name="use-application-secrets-in-service-code"></a>Uygulama parolaları hizmetini kullanma
yapılandırma değerlerini Settings.xml bir yapılandırma paketi erişmek için API hello verir hello olan değerleri kolay şifresini çözmek için `IsEncrypted` özniteliği ayarlanmış çok`true`. Merhaba şifreli metin şifreleme için kullanılan hello sertifikayla ilgili bilgileri içerdiğinden toomanually Bul hello sertifika gerekmez. Merhaba sertifikanın yalnızca hello Hizmeti'nin çalıştığı hello düğümde yüklü toobe gerekir. Yalnızca hello çağrı `DecryptValue()` yöntemi tooretrieve hello özgün gizli değer:

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>Sonraki Adımlar
Daha fazla bilgi edinmek [farklı güvenlik izinleriyle çalışan uygulamalar](service-fabric-application-runas-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
