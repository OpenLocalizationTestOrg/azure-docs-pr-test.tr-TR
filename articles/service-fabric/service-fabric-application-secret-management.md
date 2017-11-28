---
title: "Service Fabric uygulamaları parolalarında yönetme | Microsoft Docs"
description: "Bu makale, Service Fabric uygulaması gizli değerleri güvenli açıklamaktadır."
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
ms.openlocfilehash: d71924cda8bb3bffbe221946d80dba150359e38e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="ef3ab-103">Service Fabric uygulamaları parolaları yönetme</span><span class="sxs-lookup"><span data-stu-id="ef3ab-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="ef3ab-104">Bu kılavuz, Service Fabric uygulaması parolalarında yönetme adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-104">This guide walks you through the steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="ef3ab-105">Gizli depolama bağlantı dizeleri, parolalar veya düz metin olarak işleneceğini olmayan diğer değerleri gibi herhangi bir önemli bilgi olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="ef3ab-106">Bu kılavuz, anahtarları ve gizli anahtarları yönetmek için Azure anahtar kasası kullanır.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-106">This guide uses Azure Key Vault to manage keys and secrets.</span></span> <span data-ttu-id="ef3ab-107">Ancak, *kullanarak* gizli bir uygulamada herhangi bir yerde barındırılan bir kümeye dağıtılacak uygulamalar izin vermek için platform belirsiz bulut.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-107">However, *using* secrets in an application is cloud platform-agnostic to allow applications to be deployed to a cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="ef3ab-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ef3ab-108">Overview</span></span>
<span data-ttu-id="ef3ab-109">Hizmet yapılandırma ayarlarını yönetmek için önerilen yöntem aracılığıyladır [hizmet yapılandırma paketleri][config-package].</span><span class="sxs-lookup"><span data-stu-id="ef3ab-109">The recommended way to manage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="ef3ab-110">Yapılandırma paketleri sürümlü ve sistem durumu doğrulama ve Otomatik geri alma ile yönetilen yükseltmelerini aracılığıyla güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="ef3ab-111">Genel hizmet kesintisi olasılığını azaltır olarak bu genel yapılandırma için tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-111">This is preferred to global configuration as it reduces the chances of a global service outage.</span></span> <span data-ttu-id="ef3ab-112">Şifrelenmiş parolalar hiçbir istisnadır.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="ef3ab-113">Service Fabric şifreleme ve şifre çözme sertifikası şifreleme kullanarak bir yapılandırma paketi Settings.xml dosyasındaki değerleri için yerleşik özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="ef3ab-114">Aşağıdaki diyagramda Service Fabric uygulaması gizli yönetimi için temel akışı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-114">The following diagram illustrates the basic flow for secret management in a Service Fabric application:</span></span>

![Gizli yönetimine genel bakış][overview]

<span data-ttu-id="ef3ab-116">Bu akış dört ana adım vardır:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="ef3ab-117">Veri şifreleme sertifikası alın.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="ef3ab-118">Sertifikayı kümenizdeki yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-118">Install the certificate in your cluster.</span></span>
3. <span data-ttu-id="ef3ab-119">Sertifikayla ilgili bir uygulama dağıtırken gizli değerleri şifreler ve bir hizmetin Settings.xml yapılandırma dosyasına Ekle.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-119">Encrypt secret values when deploying an application with the certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="ef3ab-120">Settings.xml dışında şifrelenmiş değerler ile aynı şifreleme sertifikası şifresini çözerek okuyun.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-120">Read encrypted values out of Settings.xml by decrypting with the same encipherment certificate.</span></span> 

<span data-ttu-id="ef3ab-121">[Azure anahtar kasası] [ key-vault-get-started] burada Azure Service Fabric kümeleri yüklü sertifikaları almak için bir yol ve sertifikalar için bir güvenli depolama konumu olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way to get certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="ef3ab-122">Azure'a dağıtma değil, anahtar kasası Service Fabric uygulamaları parolalarında yönetmek üzere kullanmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-122">If you are not deploying to Azure, you do not need to use Key Vault to manage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="ef3ab-123">Veri şifreleme sertifikası</span><span class="sxs-lookup"><span data-stu-id="ef3ab-123">Data encipherment certificate</span></span>
<span data-ttu-id="ef3ab-124">Veri şifreleme sertifikası kesinlikle şifreleme için kullanılır ve şifre çözme yapılandırmasının bir hizmetin Settings.xml değerleri ve kimlik doğrulaması için kullanılan veya şifre metin imzalama değil.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="ef3ab-125">Sertifikanın aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-125">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="ef3ab-126">Sertifika bir özel anahtar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-126">The certificate must contain a private key.</span></span>
* <span data-ttu-id="ef3ab-127">Sertifikanın bir kişisel bilgi değişimi (.pfx) dosyasına dışarı aktarılabilir olarak, anahtar değişimi için oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-127">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="ef3ab-128">Sertifika anahtar kullanımı veri şifreleme (10) içermelidir ve sunucu kimlik doğrulaması veya istemci kimlik doğrulaması içermemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-128">The certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="ef3ab-129">Örneğin, PowerShell kullanarak otomatik olarak imzalanan sertifika oluşturulurken `KeyUsage` bayrağını ayarlayın, `DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-129">For example, when creating a self-signed certificate using PowerShell, the `KeyUsage` flag must be set to `DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-the-certificate-in-your-cluster"></a><span data-ttu-id="ef3ab-130">Kümenizdeki sertifikayı yükleme</span><span class="sxs-lookup"><span data-stu-id="ef3ab-130">Install the certificate in your cluster</span></span>
<span data-ttu-id="ef3ab-131">Bu sertifika, kümedeki her düğümde yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-131">This certificate must be installed on each node in the cluster.</span></span> <span data-ttu-id="ef3ab-132">Bu çalışma zamanında bir hizmetin Settings.xml depolanan değerleri şifresini çözmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-132">It will be used at runtime to decrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="ef3ab-133">Bkz: [Azure Kaynak Yöneticisi'ni kullanarak bir küme oluşturmak nasıl] [ service-fabric-cluster-creation-via-arm] kurulum yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-133">See [how to create a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="ef3ab-134">Uygulama parolaları şifrelemek</span><span class="sxs-lookup"><span data-stu-id="ef3ab-134">Encrypt application secrets</span></span>
<span data-ttu-id="ef3ab-135">Service Fabric SDK yerleşik gizli şifreleme ve şifre çözme işlevi vardır.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-135">The Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="ef3ab-136">Gizli değerleri yerleşik anda şifrelenmiş şifresi ve program aracılığıyla hizmet kodunda okuyun.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="ef3ab-137">Aşağıdaki PowerShell komutunu bir gizli anahtarı şifrelemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-137">The following PowerShell command is used to encrypt a secret.</span></span> <span data-ttu-id="ef3ab-138">Bu komut, yalnızca değeri şifreler; Mevcut **değil** şifre metnin imzalayın.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-138">This command only encrypts the value; it does **not** sign the cipher text.</span></span> <span data-ttu-id="ef3ab-139">Ciphertext gizli değerleri için üretmek için kümenizdeki yüklü aynı şifreleme sertifikası kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-139">You must use the same encipherment certificate that is installed in your cluster to produce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="ef3ab-140">Sonuçta elde edilen base-64 dizesi hem gizli ciphertext yanı sıra, şifrelemek için kullanılan sertifikayla ilgili bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-140">The resulting base-64 string contains both the secret ciphertext as well as information about the certificate that was used to encrypt it.</span></span>  <span data-ttu-id="ef3ab-141">Base-64 kodlu bir dize hizmetinizin Settings.xml yapılandırma dosyasıyla parametresinde eklenebilir `IsEncrypted` özniteliğini `true`:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-141">The base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with the `IsEncrypted` attribute set to `true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="ef3ab-142">Uygulama örnekleri uygulama parolaları Ekle</span><span class="sxs-lookup"><span data-stu-id="ef3ab-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="ef3ab-143">İdeal olarak, farklı ortamlar için dağıtım olarak otomatik olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-143">Ideally, deployment to different environments should be as automated as possible.</span></span> <span data-ttu-id="ef3ab-144">Bu, gizli şifreleme bir yapı ortamında gerçekleştirme ve uygulama örnekleri oluşturulurken parametre olarak şifrelenmiş parolalar sağlama gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-144">This can be accomplished by performing secret encryption in a build environment and providing the encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="ef3ab-145">Geçersiz kılınabilir parametreler Settings.xml kullanın</span><span class="sxs-lookup"><span data-stu-id="ef3ab-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="ef3ab-146">Settings.xml yapılandırma dosyası uygulama oluşturma sırasında sağlanan geçersiz kılınabilir parametrelere izin verir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-146">The Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="ef3ab-147">Kullanım `MustOverride` parametresi için bir değer sağlamak yerine özniteliği:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-147">Use the `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="ef3ab-148">Settings.xml değerleri geçersiz kılmak için ApplicationManifest.xml hizmeti için bir geçersiz kılma parametresi bildirin:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-148">To override values in Settings.xml, declare an override parameter for the service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="ef3ab-149">Değer olarak belirtilebilir şimdi bir *uygulama parametresi* uygulamasının bir örneğini oluştururken.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-149">Now the value can be specified as an *application parameter* when creating an instance of the application.</span></span> <span data-ttu-id="ef3ab-150">Uygulama örneğini oluşturmak komut dosyasıyla PowerShell kullanarak veya bir derleme işlemindeki kolay tümleştirme için C# ile yazılmış.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="ef3ab-151">PowerShell kullanarak, parametre için sağlanan `New-ServiceFabricApplication` olarak komutunu bir [karma tablosu](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="ef3ab-151">Using PowerShell, the parameter is supplied to the `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="ef3ab-152">C# kullanarak, uygulama parametreleri belirtilen bir `ApplicationDescription` olarak bir `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="ef3ab-153">Hizmet kodundan gizli şifresini çözme</span><span class="sxs-lookup"><span data-stu-id="ef3ab-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="ef3ab-154">Service Fabric Hizmetleri'nde altında ağ hizmeti varsayılan olarak Windows üzerinde çalışan ve bazı ek kurulum olmadan düğümde yüklü olan sertifikalar erişiminiz yok.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access to certificates installed on the node without some extra setup.</span></span>

<span data-ttu-id="ef3ab-155">Ne zaman emin ağ hizmeti yapmanıza gerek veri şifreleme sertifikasını kullanarak veya hangi kullanıcı hizmet hesabı altında çalışan sertifikanın özel anahtarı erişebilir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-155">When using a data encipherment certificate, you need to make sure NETWORK SERVICE or whatever user account the service is running under has access to the certificate's private key.</span></span> <span data-ttu-id="ef3ab-156">Service Fabric, bunu yapmak için yapılandırırsanız erişim hizmetiniz için otomatik olarak verme işleyecek.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-156">Service Fabric will handle granting access for your service automatically if you configure it to do so.</span></span> <span data-ttu-id="ef3ab-157">Bu yapılandırma, kullanıcılar ve sertifikalar için güvenlik ilkelerini tanımlayarak ApplicationManifest.xml yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="ef3ab-158">Aşağıdaki örnekte, ağ hizmeti hesabının, parmak izi tarafından tanımlanan bir sertifika okuma erişimi verilir:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-158">In the following example, the NETWORK SERVICE account is given read access to a certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="ef3ab-159">Sertifika parmak izi sertifika deposu ek bileşeninden Windows kopyalarken görünmeyen bir karakter parmak izi dizenin başında yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-159">When copying a certificate thumbprint from the certificate store snap-in on Windows, an invisible character is placed at the beginning of the thumbprint string.</span></span> <span data-ttu-id="ef3ab-160">Bu görünmez karakter çalışırken bir sertifika parmak izi tarafından bulmak için bu nedenle bu ek karakter silmek istediğinizden emin bir hata neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-160">This invisible character can cause an error when trying to locate a certificate by thumbprint, so be sure to delete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="ef3ab-161">Uygulama parolaları hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="ef3ab-161">Use application secrets in service code</span></span>
<span data-ttu-id="ef3ab-162">Kolay olan değerleri şifresini çözmek için bir yapılandırma paketi Settings.xml yapılandırma değerlerini erişmek için API sağlar `IsEncrypted` özniteliği kümesine `true`.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-162">The API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have the `IsEncrypted` attribute set to `true`.</span></span> <span data-ttu-id="ef3ab-163">Şifrelenmiş metin şifreleme için kullanılan sertifikayla ilgili bilgileri içerdiğinden, el ile Sertifika Bul gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-163">Since the encrypted text contains information about the certificate used for encryption, you do not need to manually find the certificate.</span></span> <span data-ttu-id="ef3ab-164">Sertifika yalnızca hizmet üzerinde çalıştığı düğüm üzerinde yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef3ab-164">The certificate just needs to be installed on the node that the service is running on.</span></span> <span data-ttu-id="ef3ab-165">Basit Arama `DecryptValue()` yöntemi özgün gizli değer almak için:</span><span class="sxs-lookup"><span data-stu-id="ef3ab-165">Simply call the `DecryptValue()` method to retrieve the original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="ef3ab-166">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ef3ab-166">Next Steps</span></span>
<span data-ttu-id="ef3ab-167">Daha fazla bilgi edinmek [farklı güvenlik izinleriyle çalışan uygulamalar](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="ef3ab-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
