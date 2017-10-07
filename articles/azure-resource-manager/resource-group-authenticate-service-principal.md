---
title: "PowerShell ile Azure uygulaması için aaaCreate kimlik | Microsoft Docs"
description: "Toouse Azure PowerShell toocreate bir Azure Active Directory uygulaması ve hizmet sorumlusu ve rol tabanlı erişim, erişim tooresources nasıl kontrol açıklar. Bunu gösterir nasıl tooauthenticate uygulamayla bir parola veya sertifika."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: c534360799b590054a051e4426e5e27dccb559b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a>Bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanın

Bir uygulama ya da tooaccess kaynakları gereken komut dosyası varsa, kendi kimlik bilgileriyle hello uygulamanın kimlik doğrulamasını ve hello uygulama için bir kimlik ayarlayın. Bu kimlik, bir hizmet sorumlusu bilinir. Bu yaklaşım sağlar:

* İzinleri kendi izinlerinizi farklı toohello uygulama kimliği atayın. Genellikle, bu kısıtlı tooexactly hangi hello uygulamanın toodo ihtiyacı izinlerdir.
* Sertifika kimlik doğrulaması için Katılımsız betik yürütülürken kullanın.

Bu konu, nasıl gösterir toouse [Azure PowerShell](/powershell/azure/overview) tooset kendi kimlik bilgilerini ve kimlik altında bir uygulama toorun için ihtiyaç duyduğunuz her şeyi ayarlama.

## <a name="required-permissions"></a>Gerekli izinler
toocomplete bu konuda, Azure Active Directory ve Azure aboneliğinize yeterli izniniz olması gerekir. Özellikle, mümkün toocreate hello Azure Active Directory içinde bir uygulama olabilir. ve hello hizmet asıl tooa rolünü atamanız gerekir. 

hesabınızın yeterli izinlere sahip olup olmadığı hello portalıdır hello en kolay yolu toocheck. Bkz: [gerekli izni denetleyin](resource-group-create-service-principal-portal.md#required-permissions).

Şimdi, ile kimlik doğrulaması için tooa bölüm devam edin:

* [Parola](#create-service-principal-with-password)
* [otomatik olarak imzalanan sertifika](#create-service-principal-with-self-signed-certificate)
* [Sertifika yetkilisinden sertifika](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>PowerShell komutları

tooset bir hizmet sorumlusu yukarı kullanın:

| Komut | Açıklama |
| ------- | ----------- | 
| [AzureRmADServicePrincipal yeni](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Bir Azure Active Directory Hizmet sorumlusu oluşturur |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | Atar hello RBAC rolü toohello belirtilen asıl belirtilen, kapsam hello sırasında belirtilen. |


## <a name="create-service-principal-with-password"></a>Parola ile hizmet sorumlusu oluşturma

toocreate hello katkıda bulunan rolü, aboneliğiniz için hizmet sorumlusuyla kullanın: 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

Merhaba örneği için 20 saniye tooallow hello yeni hizmet asıl toopropagate Azure Active Directory boyunca biraz zaman uyku moduna geçer. Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} hello dizininde yok."

Merhaba aşağıdaki betiği toospecify hello varsayılan abonelik dışında bir kapsam sağlar ve bir hata oluşursa, yeniden deneme rol ataması hello:

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
)

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 
 # Create Service Principal for hello AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Merhaba komut dosyasıyla ilgili bazı öğeleri toonote:

* toogrant hello kimlik erişim toohello varsayılan abonelik, gereksinim tooprovide ResourceGroup veya Subscriptionıd parametreleri.
* Yalnızca toolimit hello hello rol ataması tooa kaynak grubu kapsamını istediğinizde hello ResourceGroup parametresini belirtin.
*  Bu örnekte, hello hizmet asıl toohello katkıda bulunan rolü ekleyin. Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).
* Hello komut dosyası için 15 saniye tooallow hello yeni hizmet asıl toopropagate Azure Active Directory boyunca biraz zaman uyku moduna geçer. Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} hello dizininde yok."
* Toogrant hello hizmet asıl erişim toomore abonelik veya kaynak grupları gerekiyorsa, hello çalıştırmak `New-AzureRMRoleAssignment` farklı kapsamlar yeniden cmdlet'iyle.


### <a name="provide-credentials-through-powershell"></a>PowerShell ile kimlik bilgileri sağlayın
Şimdi, hello uygulaması tooperform işlemleri toolog de gerekir. Merhaba kullanıcı adı için hello kullan `ApplicationId` Merhaba uygulaması için oluşturduğunuz. Merhaba parolasını hello hello hesabı oluşturulurken belirtilen birinin kullanın. 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

Merhaba Kiracı kimliği hassas, olmadığından doğrudan komut dosyanıza ekleme. Tooretrieve hello Kiracı kimliği gerekiyorsa kullanın:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>Hizmet sorumlusu ile otomatik olarak imzalanan sertifika oluşturma

toocreate otomatik olarak imzalanan sertifika ve hello katkıda bulunan rolü, aboneliğiniz için bir hizmet sorumlusu kullanın: 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

Merhaba örneği için 20 saniye tooallow hello yeni hizmet asıl toopropagate Azure Active Directory boyunca biraz zaman uyku moduna geçer. Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} hello dizininde yok."

Merhaba aşağıdaki betiği toospecify hello varsayılan abonelik dışında bir kapsam sağlar ve bir hata oluşursa, yeniden deneme rol ataması hello. Windows 10 veya Windows Server 2016 Azure PowerShell 2.0 yüklü olmalıdır.

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Merhaba komut dosyasıyla ilgili bazı öğeleri toonote:

* toogrant hello kimlik erişim toohello varsayılan abonelik, gereksinim tooprovide ResourceGroup veya Subscriptionıd parametreleri.
* Yalnızca toolimit hello hello rol ataması tooa kaynak grubu kapsamını istediğinizde hello ResourceGroup parametresini belirtin.
* Bu örnekte, hello hizmet asıl toohello katkıda bulunan rolü ekleyin. Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).
* Hello komut dosyası için 15 saniye tooallow hello yeni hizmet asıl toopropagate Azure Active Directory boyunca biraz zaman uyku moduna geçer. Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} hello dizininde yok."
* Toogrant hello hizmet asıl erişim toomore abonelik veya kaynak grupları gerekiyorsa, hello çalıştırmak `New-AzureRMRoleAssignment` farklı kapsamlar yeniden cmdlet'iyle.

Varsa, **Windows 10 veya Windows Server 2016 Technical Preview gerekmez**, toodownload hello gereksinim [otomatik olarak imzalanan sertifika Oluşturucu](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) Microsoft Script Center gelen. İçeriğini ayıklayın ve ihtiyacınız hello cmdlet'i içeri aktarın.

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
Hello komut dosyasında, aşağıdaki iki satır toogenerate hello sertifika hello yerine koyun.
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>Otomatik PowerShell komut dosyası aracılığıyla sertifikası sağlayın
Bir hizmet sorumlusu oturum olduğunda, AD uygulamanız için hello dizininin tooprovide hello Kiracı kimliği gerekir. Bir kiracı, Azure Active Directory örneğidir. Yalnızca bir aboneliğiniz varsa, kullanabilirsiniz:

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

Merhaba uygulama kimliği ve Kiracı kimliği olmayan hassas, doğrudan komut dosyanıza katıştırmak için. Tooretrieve hello Kiracı kimliği gerekiyorsa kullanın:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Tooretrieve hello uygulama kimliği gerekiyorsa kullanın:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>Sertifika yetkilisinden sertifika ile hizmet sorumlusu oluşturma
toouse verilen sertifika, sertifika yetkilisi toocreate hizmet sorumlusu, aşağıdaki komut dosyası kullan hello:

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -KeyCredentials $keyCredential
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

Merhaba komut dosyasıyla ilgili bazı öğeleri toonote:

* Kapsamlı toohello abonelik erişilebilir.
* Bu örnekte, hello hizmet asıl toohello katkıda bulunan rolü ekleyin. Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).
* Hello komut dosyası için 15 saniye tooallow hello yeni hizmet asıl toopropagate Azure Active Directory boyunca biraz zaman uyku moduna geçer. Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} hello dizininde yok."
* Toogrant hello hizmet asıl erişim toomore abonelik veya kaynak grupları gerekiyorsa, hello çalıştırmak `New-AzureRMRoleAssignment` farklı kapsamlar yeniden cmdlet'iyle.

### <a name="provide-certificate-through-automated-powershell-script"></a>Otomatik PowerShell komut dosyası aracılığıyla sertifikası sağlayın
Bir hizmet sorumlusu oturum olduğunda, AD uygulamanız için hello dizininin tooprovide hello Kiracı kimliği gerekir. Bir kiracı, Azure Active Directory örneğidir.

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

Merhaba uygulama kimliği ve Kiracı kimliği olmayan hassas, doğrudan komut dosyanıza katıştırmak için. Tooretrieve hello Kiracı kimliği gerekiyorsa kullanın:

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Tooretrieve hello uygulama kimliği gerekiyorsa kullanın:

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>Kimlik bilgilerini değiştirme

ya da güvenliğinin aşılması veya bir kimlik bilgisi sona erme nedeniyle, bir AD uygulaması için toochange hello kimlik hello kullan [Kaldır AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) ve [yeni AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlet'leri.

tooremove bir uygulama için tüm hello kimlik bilgilerini kullan:

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

tooadd bir parola kullanın:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

tooadd sertifika değeri, bu konu başlığı altında gösterildiği gibi otomatik olarak imzalanan bir sertifika oluşturun. Ardından, kullanın:

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a>Erişim belirteci toosimplify oturum Kaydet
içinde toolog gereken her zaman tooavoid hello hizmet asıl kimlik bilgileri sağlama, hello erişim belirteci kaydedebilirsiniz.

toouse hello geçerli erişim belirteci bir sonraki oturumunda hello profil kaydedin.
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
Hello profil açın ve içeriğini inceleyin. Bir erişim belirteci içerdiğine dikkat edin. El ile yeniden oturum açmayı yerine, yalnızca hello profili yükleyin.
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> Merhaba belirtecin geçerli olduğu sürece kaydedilmiş bir profil kullanarak yalnızca çalıştığı şekilde hello erişim belirtecinin süresi.
>  

Alternatif olarak, PowerShell toolog REST işlemlerini çağırabilirsiniz. Merhaba kimlik doğrulaması yanıttan hello erişim belirteci diğer işlemleri ile kullanılmak üzere alabilir. REST işlemlerini çağırarak hello erişim belirteci alma bir örnek için bkz: [bir erişim belirteci oluşturma](resource-manager-rest-api.md#generating-an-access-token).

## <a name="debug"></a>Hata ayıklama

Bir hizmet sorumlusu oluşturma sırasında aşağıdaki hatalar hello karşılaşabilirsiniz:

* **"Authentication_Unauthorized"** veya **"abonelik hello bağlamda bulunamadı."** -Hesabınızı hello olmadığında bu hatayı gördüğünüz [gerekli izinleri](#required-permissions) hello Azure Active Directory tooregister bir uygulama üzerinde. Yalnızca yönetici kullanıcıların Azure Active Directory'de uygulamaları kaydedebilirsiniz ve hesabınızın bir yönetici değil, bu hata genellikle, bakın Yönetici tooeither atamak, tooan Yönetici rolü ya da tooenable kullanıcılar tooregister uygulamaları isteyin.

* Hesabınızı **"yetkilendirme tooperform eylemi 'Microsoft.Authorization/roleAssignments/write' kapsamı üzerinde '/ subscriptions / {GUID}' yok."**  -Hesabınızı rol tooan kimlik yeterli izinleri tooassign olmadığında bu hatayı bakın. Abonelik Yöneticisi tooadd isteyin, tooUser erişim Yönetici rolü.

## <a name="sample-applications"></a>Örnek uygulamalar
Farklı platformlarda üzerinden hello uygulama olarak oturum açma hakkında daha fazla bilgi için bkz:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Sonraki adımlar
* Kaynakları yönetmek için Azure'da bir uygulamayı tümleştirme ayrıntılı adımlar için bkz: [Geliştirici Kılavuzu tooauthorization hello Azure Kaynak Yöneticisi API'si ile](resource-manager-api-authentication.md).
* Uygulamalar ve hizmet asıl adı daha ayrıntılı bir açıklaması için bkz: [uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md). 
* Azure Active Directory kimlik doğrulaması hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](../active-directory/active-directory-authentication-scenarios.md).
* Verilen veya toousers reddedilen kullanılabilir eylemler listesi için bkz: [Azure Resource Manager kaynak sağlayıcısı işlemleri](../active-directory/role-based-access-control-resource-provider-operations.md).

