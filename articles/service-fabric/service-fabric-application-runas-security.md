---
title: "Azure mikro güvenlik ilkeleri hakkında aaaLearn | Microsoft Docs"
description: "Başlamadan önce nasıl eylem burada bir uygulamanın tooperform bazı ihtiyacı hello SetupEntry noktası dahil toorun sistem ve yerel güvenlik hesapları altından bir Service Fabric uygulaması, ayrıcalıklı bir genel bakış"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a>Uygulamanıza yönelik güvenlik ilkeleri yapılandırma
Azure Service Fabric kullanarak hello kümedeki farklı kullanıcı hesabı altında çalışan uygulamaları güvenliğini sağlayabilirsiniz. Service Fabric ayrıca uygulamalar tarafından hello kullanıcı hesapları altında--dağıtımının hello zamanında örneğin kullanılan güvenli hello kaynakları, dizinleri ve dosyaları sertifikaları yardımcı olur. Bu çalışan uygulamaları bile paylaşılan bir barındırılan ortamda, diğerinden daha güvenli hale getirir.

Varsayılan olarak, Service Fabric uygulamaları hello Fabric.exe işlemin altında çalıştığı hello hesap altında çalışır. Service Fabric, aynı zamanda bir yerel kullanıcı hesabı veya hello uygulama bildirimi içinde belirtilen yerel sistem hesabı altında toorun uygulamaları hello yeteneği sağlar. Desteklenen yerel sistem hesabı türleri **YerelKullanıcı**, **NetworkService**, **Yerelhizmet**, ve **LocalSystem**.

 Merhaba tek başına yükleyici kullanarak, veri merkezinizde Windows Server'da Service Fabric çalıştırıyorsanız, Grup yönetilen hizmet hesapları dahil olmak üzere Active Directory etki alanı hesaplarını kullanabilirsiniz.

Tanımlayabilir ve kullanıcı grupları oluşturun, böylece bir veya daha fazla kullanıcı birlikte yönetilen tooeach Grup toobe eklenebilir. Bu, farklı hizmet giriş noktaları için birden çok kullanıcı ve bunlar toohave hello grup düzeyinde kullanılabilen ortak belirli ayrıcalıklara gerektiğinde kullanışlıdır.

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a>Bir hizmet Kurulum giriş noktası için Hello ilkesi yapılandırma
Hello açıklandığı gibi [uygulama modeli](service-fabric-application-model.md), hello Kurulum giriş noktası **SetupEntryPoint**, hello Service Fabric aynı kimlik bilgileri ile çalışan bir ayrıcalıklı giriş noktasıdır (genellikle hello *NetworkService* hesabı) önce başka bir giriş noktası. tarafından belirtilen hello yürütülebilir **EntryPoint** genellikle hello uzun süre çalışan hizmet ana bilgisayardır. Bu nedenle ayrı Kurulum giriş noktası sahip uzun süre için toorun hello hizmet konağı yüksek ayrıcalıklara sahip yürütülebilir belirlemeyi önler. Merhaba yürütülebilir, **EntryPoint** belirtir çalıştırıldıktan **SetupEntryPoint** başarıyla çıkar. Merhaba elde edilen işlem izlenen ve yeniden ve yeniden ile başlayan **SetupEntryPoint** hiç sonlandırır veya çöküyor.

Merhaba aşağıda gösterildiği SetupEntryPoint hello ve hello hizmeti için ana EntryPoint hello bir basit hizmeti bildirim örnek verilmiştir.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a>Yerel bir hesap kullanarak Hello ilkesi yapılandırma
Merhaba hizmet toohave Kurulum giriş noktası yapılandırdıktan sonra hello uygulama bildiriminde altında çalıştığı hello güvenlik izinlerini değiştirebilirsiniz. Aşağıdaki örneğine hello nasıl tooconfigure hello hizmet toorun kullanıcı yönetici hesabının ayrıcalıklarını altında gösterilir.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

İlk olarak, oluşturma bir **sorumluları** SetupAdminUser gibi bir kullanıcı adı bölümü. Bu hello kullanıcı hello yöneticiler sistem grubunun bir üyesi olduğunu gösterir.

Sonraki hello altında **ServiceManifestImport** bölümünde, bir ilke tooapply bu asıl çok yapılandırmak**SetupEntryPoint**. Bu Service Fabric, hello zaman söyler **MySetup.bat** dosyasını çalıştırın, olmalıdır `RunAs` yönetici ayrıcalıklarına sahip. Sahip olduğunuz o *değil* uygulanan bir ilke toohello ana giriş noktası, hello kodda **MyServiceHost.exe** hello sisteminde çalışıyor **NetworkService** hesabı. Bu, tüm hizmet giriş noktaları olarak çalıştırılan hello varsayılan hesaptır.

Şimdi hello dosya MySetup.bat toohello Visual Studio Proje tootest hello yönetici ayrıcalıkları ekleyelim. Visual Studio'da hello hizmeti projesine sağ tıklayın ve MySetup.bat adlı yeni bir dosya ekleyin.

Ardından, o hello MySetup.bat dosya hello hizmet paketinde bulunduğundan emin olun. Varsayılan olarak, bu değil. Hello dosya seçin, tooget hello bağlam menüsü sağ tıklayın ve **özellikleri**. Merhaba Özellikleri iletişim kutusunda emin **tooOutput dizin kopyalama** çok ayarlanır**yeniyse Kopyala**. Aşağıdaki ekran görüntüsü hello bakın.

![SetupEntryPoint toplu iş dosyası için Visual Studio CopyToOutput][image1]

Şimdi hello MySetup.bat dosyasını açın ve aşağıdaki komutları hello ekleyin:

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

Ardından, yapı ve hello çözüm tooa yerel geliştirme kümesi dağıtabilirsiniz. Service Fabric Explorer'da gösterildiği gibi Hello hizmeti başlatıldıktan sonra bu hello MySetup.bat dosyasını iki yolla başarılı olduğunu görebilirsiniz. Bir PowerShell komut istemi açıp türü:

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

Ardından, burada hello hizmet dağıtıldı ve Service Fabric Explorer'da--Örneğin, düğüm 2 başlatılan hello düğümü hello adını not edin. Ardından, hello değerini gösteren toohello uygulama örneği çalışma klasörü toofind hello out.txt dosyasını gidin **TestVariable**. Bu hizmet dağıtılan tooNode 2 olduysa, örneğin, daha sonra hello toothis yolu geçebilir **MyApplicationType**:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a>Yerel Sistem hesapları kullanarak Hello ilkesi yapılandırma
Genellikle, bir yönetici hesabı yerine yerel sistem hesabı kullanarak tercih toorun hello başlangıç komut dosyasıdır. Yöneticiler grubunun da makineler kullanıcı erişim denetimi (UAC) varsayılan olarak etkin olduğundan genellikle işe yaramazsa hello üyesi olarak Hello RunAs İlkesi çalışıyor. Böyle durumlarda, **hello önerilir toorun hello LocalSystem olarak SetupEntryPoint yerine yerel kullanıcı eklenen tooAdministrators grup olarak**. Merhaba aşağıdaki örnekte ayarı hello SetupEntryPoint toorun LocalSystem olarak gösterilmektedir:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>PowerShell komutlarını bir Kurulum giriş noktasından Başlat
Merhaba gelen PowerShell toorun **SetupEntryPoint** noktası çalıştırabilirsiniz **PowerShell.exe** tooa PowerShell işaret eden bir toplu iş dosyasında dosya. İlk olarak, PowerShell dosya toohello hizmet projesi--Örneğin, ekleyin **MySetup.ps1**. Tooset hello unutmayın *yeniyse Kopyala* hello dosyayı ayrıca hello hizmet paketine dahil şekilde özelliği. Merhaba aşağıdaki örnek olarak adlandırılan bir sistem ortam değişkenini ayarlar MySetup.ps1 adlı bir PowerShell dosya başlayan bir örnek toplu iş dosyası gösterir **TestVariable**.

MySetup.bat toostart PowerShell dosyası:

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

Merhaba PowerShell dosyasında tooset bir sistem ortam değişkeni aşağıdaki hello ekleyin:

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> Merhaba toplu iş dosyası çalıştığında, varsayılan olarak, hello uygulama klasörü adlı görünüyor **iş** dosyaları için. MySetup.bat çalıştığında, bu durumda, bu toofind hello MySetup.ps1 dosya hello aynı istiyoruz hello uygulama klasörü **kod paketi** klasör. toochange bu klasör, kümesi hello çalışma klasörü:
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a>Yerel hata ayıklama için konsolu yeniden yönlendirmeyi kullanma
Bazen, yararlı toosee hello konsol çıkışı'hata ayıklama amacıyla bir komut dosyası çalıştırılarak yapılır. toodo bunu hello çıkış tooa dosyasını yazar konsol yeniden yönlendirme ilkesi ayarlayabilirsiniz. Merhaba yazılı toohello uygulama klasörü adlı çıkış dosyası **günlük** burada hello uygulamanın dağıtıldığı ve Çalıştır hello düğümde. (Where bkz toofind Bu örnek önceki hello.)

> [!WARNING]
> Hiçbir zaman bu hello uygulama yük devretme etkileyebileceğinden üretimde dağıtılan bir uygulamada hello konsol yeniden yönlendirme ilkesi kullanın. *Yalnızca* bunu yerel geliştirme ve hata ayıklama amacıyla kullanın.  
> 
> 

Merhaba aşağıdaki örnek ayarı hello konsol yeniden yönlendirmesi FileRetentionCount değeriyle gösterir:

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

Merhaba MySetup.ps1 dosya toowrite şimdi değiştirirseniz bir **Echo** komutu, bu hata ayıklama amacıyla toohello çıktı dosyasına yazma:

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

**Bu konsol yeniden yönlendirme ilkesi, komut dosyası hata ayıklama sonra hemen kaldırın**.

## <a name="configure-a-policy-for-service-code-packages"></a>Hizmet kodu paketleri için bir ilke yapılandırın
Önceki adımları hello gördüğünüz nasıl tooapply RunAs İlkesi tooSetupEntryPoint. Olarak uygulanan toocreate farklı ilkeleri ilkeler nasıl hizmet uygulamasına biraz daha derin bir göz atalım.

### <a name="create-local-user-groups"></a>Yerel kullanıcı grupları oluşturun
Tanımlamak ve bir izin kullanıcı grupları oluşturun veya daha fazla kullanıcı toobe tooa Grup eklenmiştir. Bu, birden çok kullanıcı için farklı hizmet giriş noktaları vardır ve bunlar toohave hello grup düzeyinde kullanılabilen bazı ortak ayrıcalıklarına sahip olmanız gerekir yararlıdır. Merhaba aşağıdaki örnekte gösterilir adlı bir yerel grup **LocalAdminGroup** yönetici ayrıcalıklarına sahip. İki kullanıcılar, Customer1 ve Customer2, bu yerel grubun üyesi yapılır.

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a>Yerel kullanıcılar oluşturma
Bir hizmet Merhaba uygulaması içinde kullanılan toohelp güvenli olabilir yerel bir kullanıcı oluşturabilirsiniz. Zaman bir **YerelKullanıcı** hesap türü belirtilen hello ilkeleri bölümünde hello uygulama bildiriminin, Service Fabric hello uygulamanın dağıtıldığı makinelerde yerel kullanıcı hesaplarını oluşturur. Varsayılan olarak, bu hesapları (örneğin, aşağıdaki örnek hello Customer3) hello uygulamada belirtilenlerle aynı adları bildirim hello sahip değilsiniz. Bunun yerine, dinamik olarak oluşturulur ve rastgele parolalara sahip.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

Bir uygulama hello kullanıcı hesabı ve parolası (örneğin, tooenable NTLM kimlik doğrulaması) tüm makinelerde aynı olmasını gerektirir, hello küme bildiriminde NTLMAuthenticationEnabled tootrue ayarlamanız gerekir. Merhaba küme bildirimi de kullanılan bir NTLMAuthenticationPasswordSecret belirtmelisiniz toogenerate tüm makinelerde aynı parola hello.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a>Hizmet kodu paketleri ilkeleri toohello atayın
Merhaba **RunAsPolicy** bölümünde bir **ServiceManifestImport** kullanılan toorun kod paketi olmalıdır hello sorumluları bölümünden hello hesabını belirtir. Ayrıca hello ilkeleri bölümünde kullanıcı hesaplarıyla hello hizmet paketlerinden bildirim kodu ilişkilendirir. Bu hello Kurulum veya ana giriş noktaları için belirtebilirsiniz veya belirtebilirsiniz `All` tooapply, tooboth. Merhaba aşağıdaki örnek uygulanan farklı ilkeleri gösterir:

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

Varsa **EntryPointType** belirtilmezse, hello varsayılan tooEntryPointType Ayarla "Ana" =. Belirtme **SetupEntryPoint** belirli yüksek ayrıcalıklı kurulum işlemlerini sistem hesabı altında toorun istediğinizde kullanışlıdır. Merhaba gerçek hizmet kodu düşük ayrıcalıklı hesap altında çalışır.

### <a name="apply-a-default-policy-tooall-service-code-packages"></a>Bir varsayılan ilke tooall hizmet kod paketleri Uygula
Merhaba kullandığınız **DefaultRunAsPolicy** bölüm toospecify belirli bir sahip olmayan tüm kod paketler için varsayılan bir kullanıcı hesabı **RunAsPolicy** tanımlanmış. Bir uygulama tarafından kullanılan hello hizmet bildiriminde belirtilen hello kod paketleri çoğunu toorun altında gerekiyorsa aynı kullanıcı hello hello uygulama yalnızca, kullanıcı hesabı ile varsayılan bir RunAs ilke tanımlayın. kod paketi yoksa hello aşağıdaki örnek belirleyen bir **RunAsPolicy** belirtilen hello kod paketi hello altında çalışması gerektiğini **MyDefaultAccount** hello ilkeleri bölümünde belirtilen.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Bir Active Directory etki alanı grubu veya kullanıcı kullanın
Merhaba tek başına yükleyici kullanarak Windows sunucusuna yüklenen Service Fabric bir örneği için Active Directory kullanıcı veya grup hesabına ait hello hizmeti hello kimlik bilgileri altında çalışabilir. Bu içi etki alanınızda Active Directory ve Azure Active Directory (Azure AD) değil. Bir etki alanı kullanıcısı veya grubu kullanarak (örneğin, dosya paylaşımları) hello etki alanındaki izinleri verilmiş diğer kaynaklara erişebilir.

Merhaba aşağıdaki örnekte gösterilir adlı bir Active Directory kullanıcı *TestUser* kendi etki alanı ile bir sertifika kullanılarak şifrelenmiş parola adlı *MyCert*. Merhaba kullanabilirsiniz `Invoke-ServiceFabricEncryptText` PowerShell komut toocreate hello gizli şifreli metin. Bkz: [Service Fabric uygulamaları parolalarında yönetme](service-fabric-application-secret-management.md) Ayrıntılar için.

Bir bant dışı yöntem kullanarak özel anahtarı hello sertifika toodecrypt hello parola toohello yerel makine hello dağıtmanız gerekir (Azure'da, Azure Resource Manager aracılığıyla budur). Ardından, Service Fabric hello hizmet paketi toohello makine dağıtırken mümkün toodecrypt hello parolası ve (Merhaba kullanıcı adı ile birlikte) bu kimlik bilgileri altında Active Directory toorun ile kimlik doğrulaması.

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a>Grup yönetilen hizmet hesabı.
Merhaba tek başına yükleyici kullanarak Windows sunucusuna yüklenen Service Fabric bir örneği için bir grup olarak yönetilen hizmet hesabı (gMSA) hello hizmeti çalışabilir. Bu Active Directory olduğuna dikkat edin, etki alanı içinde şirket içi ve Azure Active Directory (Azure AD) ile değil. Bir gmsa'yı kullanarak parola veya yoktur hello depolanan şifrelenmiş parola `Application Manifest`.

Merhaba aşağıdaki örnekte nasıl toocreate gMSA hesabı olarak adlandırılan gösterir *svc Test$*; toodeploy yönetilen nasıl hizmet hesabı toohello küme düğümleri; ve nasıl tooconfigure hello kullanıcı asıl adı.

##### <a name="prerequisites"></a>Önkoşullar.
- Merhaba etki alanı bir KDS kök anahtarı gerekir.
- Windows Server 2012 veya sonraki işlev düzeyinde toobe Hello etki alanı gerekir.

##### <a name="example"></a>Örnek
1. Hello kullanarak Grup yönetilen hizmet hesabı oluşturma bir active directory etki alanı yöneticisi olan `New-ADServiceAccount` komutunu ve o hello olun `PrincipalsAllowedToRetrieveManagedPassword` hello service fabric küme düğümlerinin tümü içerir. Unutmayın `AccountName`, `DnsHostName`, ve `ServicePrincipalName` benzersiz olması gerekir.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. Her hello service fabric küme düğümlerinin (örneğin, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`) yükleyin ve hello gMSA sınayın.
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. Merhaba kullanıcı asıl yapılandırmak ve hello RunAsPolicy tooreference hello kullanıcı yapılandırın.
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>HTTP ve HTTPS uç noktaları için bir güvenlik erişim ilkesi atama
Bir RunAs İlkesi tooa hizmeti uygulamak ve hello hizmet bildirimi uç noktası kaynakları hello HTTP protokolü ile bildirir, belirtmelisiniz bir **SecurityAccessPolicy** tooensure bağlantı noktalarını toothese uç noktaları ayrılmış olan doğru erişim denetimi için hello hello hizmetinin altında çalıştığı RunAs kullanıcı hesabı listelenir. Aksi takdirde, **http.sys** erişim toohello hizmeti gerekmemesi ve hello istemciden çağrıları hatalarıyla alın. Merhaba aşağıdaki örnek uygular hello Customer1 hesap tooan uç nokta adı verilen **EndpointName**, sağlayan, tam erişim hakları.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Merhaba HTTPS uç noktası için aynı zamanda hello sertifika tooreturn toohello istemcisi tooindicate hello adına sahip. Kullanarak bunu yapabilirsiniz **EndpointBindingPolicy**, hello uygulama bildirimi sertifikaları bölümünde tanımlanan hello sertifikayla.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>Https uç noktaları birden çok uygulama yükseltme
Toobe dikkatli ihtiyacınız olmayan toouse hello **aynı bağlantı noktasını** hello farklı örnekleri için http kullanırken aynı uygulama**s**. Merhaba Service Fabric hello uygulama örnekleri biri için mümkün tooupgrade hello sertifika olmayacaktır nedenidir. Örneğin, 1 veya uygulama 2 her iki uygulamanın kendi sertifikası 1 toocert 2 tooupgrade istiyorsanız. Merhaba yükseltme gerçekleştiğinde hello diğer uygulama hala bu kullanıyor olsa da Service Fabric http.sys hello sertifikası 1 kaydı yukarı temizlendi. tooprevent Bu, Service Fabric algılar zaten var olduğu hello sertifikasıyla hello noktasında kayıtlı başka bir uygulama örneği (son toohttp.sys) ve hello işlemi başarısız olur.

Bu nedenle Service Fabric kullanan iki farklı hizmet yükseltmeyi desteklemez **hello aynı bağlantı noktasını** farklı uygulama durumlarda. Diğer bir deyişle, hello farklı Services'de üzerinde aynı sertifika hello kullanamazsınız aynı bağlantı noktası. Toohave gerekiyorsa paylaşılan sertifika hello üzerinde aynı bağlantı noktası, hizmetleri yerleştirme kısıtlamalarına sahip farklı makinelerde yerleştirilir bu hello tooensure gerekir. Veya her uygulama örneği her hizmet için Service Fabric dinamik bağlantı noktaları mümkünse kullanmayı düşünün. 

Https ile yükseltme bir hata görürseniz "Merhaba Windows HTTP Sunucusu API desteği yok birden çok sertifika bir bağlantı noktasını paylaşmak uygulamalar için." bildiren bir hata uyarısı

## <a name="a-complete-application-manifest-example"></a>Tam uygulama bildirim örneği
uygulama bildirimini izleyerek hello hello birçoğu farklı ayarları gösterilmektedir:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba uygulama modelini anlama](service-fabric-application-model.md)
* [Bir hizmet bildirimi kaynakları belirtme](service-fabric-service-manifest-resources.md)
* [Bir uygulamayı dağıtma](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
