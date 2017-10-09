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
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="66229-103">Service Fabric uygulamaları parolaları yönetme</span><span class="sxs-lookup"><span data-stu-id="66229-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="66229-104">Bu kılavuzda, Service Fabric uygulaması parolalarında yönetme hello adımlar anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="66229-104">This guide walks you through hello steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="66229-105">Gizli depolama bağlantı dizeleri, parolalar veya düz metin olarak işleneceğini olmayan diğer değerleri gibi herhangi bir önemli bilgi olabilir.</span><span class="sxs-lookup"><span data-stu-id="66229-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="66229-106">Bu kılavuz, Azure anahtar kasası toomanage anahtarları ve gizli anahtarları kullanır.</span><span class="sxs-lookup"><span data-stu-id="66229-106">This guide uses Azure Key Vault toomanage keys and secrets.</span></span> <span data-ttu-id="66229-107">Ancak, *kullanarak* gizli bir uygulamada olduğu herhangi bir yerde barındırılan bulut platformu belirsiz tooallow uygulamaları toobe dağıtılan tooa küme.</span><span class="sxs-lookup"><span data-stu-id="66229-107">However, *using* secrets in an application is cloud platform-agnostic tooallow applications toobe deployed tooa cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="66229-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="66229-108">Overview</span></span>
<span data-ttu-id="66229-109">Merhaba önerilen yöntem toomanage hizmeti yapılandırma ayarları olan aracılığıyla [hizmet yapılandırma paketleri][config-package].</span><span class="sxs-lookup"><span data-stu-id="66229-109">hello recommended way toomanage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="66229-110">Yapılandırma paketleri sürümlü ve sistem durumu doğrulama ve Otomatik geri alma ile yönetilen yükseltmelerini aracılığıyla güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="66229-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="66229-111">Genel hizmet kesintisi hello olasılığını azaltır olarak tercih edilen tooglobal yapılandırma budur.</span><span class="sxs-lookup"><span data-stu-id="66229-111">This is preferred tooglobal configuration as it reduces hello chances of a global service outage.</span></span> <span data-ttu-id="66229-112">Şifrelenmiş parolalar hiçbir istisnadır.</span><span class="sxs-lookup"><span data-stu-id="66229-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="66229-113">Service Fabric şifreleme ve şifre çözme sertifikası şifreleme kullanarak bir yapılandırma paketi Settings.xml dosyasındaki değerleri için yerleşik özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="66229-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="66229-114">Merhaba Aşağıdaki diyagramda bir Service Fabric uygulaması gizli yönetimi için temel akış hello gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="66229-114">hello following diagram illustrates hello basic flow for secret management in a Service Fabric application:</span></span>

![Gizli yönetimine genel bakış][overview]

<span data-ttu-id="66229-116">Bu akış dört ana adım vardır:</span><span class="sxs-lookup"><span data-stu-id="66229-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="66229-117">Veri şifreleme sertifikası alın.</span><span class="sxs-lookup"><span data-stu-id="66229-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="66229-118">Kümenizdeki Hello sertifikası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="66229-118">Install hello certificate in your cluster.</span></span>
3. <span data-ttu-id="66229-119">Bir uygulamayı hello sertifikayla dağıtırken gizli değerleri şifrelemek ve bir hizmetin Settings.xml yapılandırma dosyasına Ekle.</span><span class="sxs-lookup"><span data-stu-id="66229-119">Encrypt secret values when deploying an application with hello certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="66229-120">İle şifre çözme tarafından şifrelenmiş okuma değerleri Settings.xml dışında aynı şifreleme sertifikası hello.</span><span class="sxs-lookup"><span data-stu-id="66229-120">Read encrypted values out of Settings.xml by decrypting with hello same encipherment certificate.</span></span> 

<span data-ttu-id="66229-121">[Azure anahtar kasası] [ key-vault-get-started] burada yolu tooget ve sertifikalar için bir güvenli depolama konumu olarak kullanılan Azure Service Fabric kümeleri üzerinde yüklü olan sertifikalar.</span><span class="sxs-lookup"><span data-stu-id="66229-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way tooget certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="66229-122">TooAzure değil dağıtıyorsanız, Service Fabric uygulamaları toouse anahtar kasası toomanage parolalarında gerekmez.</span><span class="sxs-lookup"><span data-stu-id="66229-122">If you are not deploying tooAzure, you do not need toouse Key Vault toomanage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="66229-123">Veri şifreleme sertifikası</span><span class="sxs-lookup"><span data-stu-id="66229-123">Data encipherment certificate</span></span>
<span data-ttu-id="66229-124">Veri şifreleme sertifikası kesinlikle şifreleme için kullanılır ve şifre çözme yapılandırmasının bir hizmetin Settings.xml değerleri ve kimlik doğrulaması için kullanılan veya şifre metin imzalama değil.</span><span class="sxs-lookup"><span data-stu-id="66229-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="66229-125">Merhaba sertifika hello aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="66229-125">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="66229-126">Merhaba sertifika özel anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="66229-126">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="66229-127">anahtar değişimi için dışarı aktarılabilir tooa kişisel bilgi değişimi (.pfx) dosyasını Hello sertifika oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="66229-127">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="66229-128">Merhaba sertifika anahtar kullanımı veri şifreleme (10) içermelidir ve sunucu kimlik doğrulaması veya istemci kimlik doğrulaması içermemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="66229-128">hello certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="66229-129">Örneğin, PowerShell kullanarak otomatik olarak imzalanan bir sertifika oluştururken hello `KeyUsage` bayrağı çok ayarlanmalıdır`DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="66229-129">For example, when creating a self-signed certificate using PowerShell, hello `KeyUsage` flag must be set too`DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a><span data-ttu-id="66229-130">Kümenizdeki Hello sertifika yükleme</span><span class="sxs-lookup"><span data-stu-id="66229-130">Install hello certificate in your cluster</span></span>
<span data-ttu-id="66229-131">Bu sertifika, hello kümedeki her düğümde yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="66229-131">This certificate must be installed on each node in hello cluster.</span></span> <span data-ttu-id="66229-132">Bir hizmetin Settings.xml depolanan çalışma zamanı toodecrypt değerleri kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="66229-132">It will be used at runtime toodecrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="66229-133">Bkz: [nasıl toocreate Azure Kaynak Yöneticisi'ni kullanarak bir küme] [ service-fabric-cluster-creation-via-arm] kurulum yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="66229-133">See [how toocreate a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="66229-134">Uygulama parolaları şifrelemek</span><span class="sxs-lookup"><span data-stu-id="66229-134">Encrypt application secrets</span></span>
<span data-ttu-id="66229-135">Merhaba Service Fabric SDK yerleşik gizli şifreleme ve şifre çözme işlevi vardır.</span><span class="sxs-lookup"><span data-stu-id="66229-135">hello Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="66229-136">Gizli değerleri yerleşik anda şifrelenmiş şifresi ve program aracılığıyla hizmet kodunda okuyun.</span><span class="sxs-lookup"><span data-stu-id="66229-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="66229-137">PowerShell komutunu aşağıdaki hello kullanılan tooencrypt gizli ' dir.</span><span class="sxs-lookup"><span data-stu-id="66229-137">hello following PowerShell command is used tooencrypt a secret.</span></span> <span data-ttu-id="66229-138">Bu komut, yalnızca hello değeri şifreler; Mevcut **değil** oturum hello şifreli metin.</span><span class="sxs-lookup"><span data-stu-id="66229-138">This command only encrypts hello value; it does **not** sign hello cipher text.</span></span> <span data-ttu-id="66229-139">Merhaba kullanmalısınız gizli değerleri için küme tooproduce ciphertext yüklü aynı şifreleme sertifikası:</span><span class="sxs-lookup"><span data-stu-id="66229-139">You must use hello same encipherment certificate that is installed in your cluster tooproduce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="66229-140">Merhaba sonuç base-64 dizesi hem hello gizli ciphertext, hem de kullanılan tooencrypt edildi hello sertifikayla ilgili bilgileri içeren.</span><span class="sxs-lookup"><span data-stu-id="66229-140">hello resulting base-64 string contains both hello secret ciphertext as well as information about hello certificate that was used tooencrypt it.</span></span>  <span data-ttu-id="66229-141">Merhaba base 64 kodlu bir dize parametresi hizmetinizin Settings.xml yapılandırma dosyasındaki hello ile eklenebilir `IsEncrypted` özniteliği ayarlanmış çok`true`:</span><span class="sxs-lookup"><span data-stu-id="66229-141">hello base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with hello `IsEncrypted` attribute set too`true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="66229-142">Uygulama örnekleri uygulama parolaları Ekle</span><span class="sxs-lookup"><span data-stu-id="66229-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="66229-143">İdeal olarak, dağıtım toodifferent ortamları gibi otomatik olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="66229-143">Ideally, deployment toodifferent environments should be as automated as possible.</span></span> <span data-ttu-id="66229-144">Bu, gizli şifreleme bir yapı ortamında gerçekleştirme ve şifrelenmiş hello gizli parametre olarak uygulama örnekleri oluşturulurken sağlama gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="66229-144">This can be accomplished by performing secret encryption in a build environment and providing hello encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="66229-145">Geçersiz kılınabilir parametreler Settings.xml kullanın</span><span class="sxs-lookup"><span data-stu-id="66229-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="66229-146">Merhaba Settings.xml yapılandırma dosyası uygulama oluşturma sırasında sağlanan geçersiz kılınabilir parametrelere izin verir.</span><span class="sxs-lookup"><span data-stu-id="66229-146">hello Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="66229-147">Kullanım hello `MustOverride` parametresi için bir değer sağlamak yerine özniteliği:</span><span class="sxs-lookup"><span data-stu-id="66229-147">Use hello `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="66229-148">Settings.xml, toooverride değerleri ApplicationManifest.xml hello hizmeti için bir geçersiz kılma parametresi bildirin:</span><span class="sxs-lookup"><span data-stu-id="66229-148">toooverride values in Settings.xml, declare an override parameter for hello service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="66229-149">Merhaba değeri olarak belirtilebilir şimdi bir *uygulama parametresi* hello uygulamasının bir örneğini oluştururken.</span><span class="sxs-lookup"><span data-stu-id="66229-149">Now hello value can be specified as an *application parameter* when creating an instance of hello application.</span></span> <span data-ttu-id="66229-150">Uygulama örneğini oluşturmak komut dosyasıyla PowerShell kullanarak veya bir derleme işlemindeki kolay tümleştirme için C# ile yazılmış.</span><span class="sxs-lookup"><span data-stu-id="66229-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="66229-151">PowerShell kullanarak hello sağlanan toohello parametredir `New-ServiceFabricApplication` olarak komutunu bir [karma tablosu](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="66229-151">Using PowerShell, hello parameter is supplied toohello `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="66229-152">C# kullanarak, uygulama parametreleri belirtilen bir `ApplicationDescription` olarak bir `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="66229-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="66229-153">Hizmet kodundan gizli şifresini çözme</span><span class="sxs-lookup"><span data-stu-id="66229-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="66229-154">Service Fabric Hizmetleri'nde altında ağ hizmeti varsayılan olarak Windows üzerinde çalışan ve erişim toocertificates yüklenmemiş bazı ek kurulum olmadan hello düğümde.</span><span class="sxs-lookup"><span data-stu-id="66229-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access toocertificates installed on hello node without some extra setup.</span></span>

<span data-ttu-id="66229-155">Veri şifreleme sertifikasını kullanırken toomake erişim toohello sertifikanın özel anahtarı ağ hizmeti veya seçtiğiniz kullanıcı hesabı hello hizmetinin altında çalışmakta olduğundan emin gerekir.</span><span class="sxs-lookup"><span data-stu-id="66229-155">When using a data encipherment certificate, you need toomake sure NETWORK SERVICE or whatever user account hello service is running under has access toohello certificate's private key.</span></span> <span data-ttu-id="66229-156">Service Fabric toodo şekilde yapılandırmanız varsa erişim hizmetiniz için otomatik olarak verme işleyecek.</span><span class="sxs-lookup"><span data-stu-id="66229-156">Service Fabric will handle granting access for your service automatically if you configure it toodo so.</span></span> <span data-ttu-id="66229-157">Bu yapılandırma, kullanıcılar ve sertifikalar için güvenlik ilkelerini tanımlayarak ApplicationManifest.xml yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="66229-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="66229-158">Aşağıdaki örneğine hello hello NETWORK SERVICE hesabının okuma erişimi tooa sertifika, parmak izi tarafından tanımlanan verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="66229-158">In hello following example, hello NETWORK SERVICE account is given read access tooa certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="66229-159">Sertifika parmak izi kopyalarken Windows hello Sertifika ek bileşenini depolamak, görünmeyen bir karakter hello hello parmak izi dize başında yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="66229-159">When copying a certificate thumbprint from hello certificate store snap-in on Windows, an invisible character is placed at hello beginning of hello thumbprint string.</span></span> <span data-ttu-id="66229-160">Bu görünmez karakteri hata toolocate çalışırken bir sertifika neden olabilir parmak izi tarafından bu ek karakter böylece emin toodelete olması.</span><span class="sxs-lookup"><span data-stu-id="66229-160">This invisible character can cause an error when trying toolocate a certificate by thumbprint, so be sure toodelete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="66229-161">Uygulama parolaları hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="66229-161">Use application secrets in service code</span></span>
<span data-ttu-id="66229-162">yapılandırma değerlerini Settings.xml bir yapılandırma paketi erişmek için API hello verir hello olan değerleri kolay şifresini çözmek için `IsEncrypted` özniteliği ayarlanmış çok`true`.</span><span class="sxs-lookup"><span data-stu-id="66229-162">hello API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have hello `IsEncrypted` attribute set too`true`.</span></span> <span data-ttu-id="66229-163">Merhaba şifreli metin şifreleme için kullanılan hello sertifikayla ilgili bilgileri içerdiğinden toomanually Bul hello sertifika gerekmez.</span><span class="sxs-lookup"><span data-stu-id="66229-163">Since hello encrypted text contains information about hello certificate used for encryption, you do not need toomanually find hello certificate.</span></span> <span data-ttu-id="66229-164">Merhaba sertifikanın yalnızca hello Hizmeti'nin çalıştığı hello düğümde yüklü toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="66229-164">hello certificate just needs toobe installed on hello node that hello service is running on.</span></span> <span data-ttu-id="66229-165">Yalnızca hello çağrı `DecryptValue()` yöntemi tooretrieve hello özgün gizli değer:</span><span class="sxs-lookup"><span data-stu-id="66229-165">Simply call hello `DecryptValue()` method tooretrieve hello original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="66229-166">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="66229-166">Next Steps</span></span>
<span data-ttu-id="66229-167">Daha fazla bilgi edinmek [farklı güvenlik izinleriyle çalışan uygulamalar](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="66229-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
