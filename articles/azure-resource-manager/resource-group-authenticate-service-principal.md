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
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="a8cc5-104">Bir hizmet asıl tooaccess kaynakları Azure PowerShell toocreate kullanın</span><span class="sxs-lookup"><span data-stu-id="a8cc5-104">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="a8cc5-105">Bir uygulama ya da tooaccess kaynakları gereken komut dosyası varsa, kendi kimlik bilgileriyle hello uygulamanın kimlik doğrulamasını ve hello uygulama için bir kimlik ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="a8cc5-106">Bu kimlik, bir hizmet sorumlusu bilinir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-106">This identity is known as a service principal.</span></span> <span data-ttu-id="a8cc5-107">Bu yaklaşım sağlar:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-107">This approach enables you to:</span></span>

* <span data-ttu-id="a8cc5-108">İzinleri kendi izinlerinizi farklı toohello uygulama kimliği atayın.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="a8cc5-109">Genellikle, bu kısıtlı tooexactly hangi hello uygulamanın toodo ihtiyacı izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="a8cc5-110">Sertifika kimlik doğrulaması için Katılımsız betik yürütülürken kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="a8cc5-111">Bu konu, nasıl gösterir toouse [Azure PowerShell](/powershell/azure/overview) tooset kendi kimlik bilgilerini ve kimlik altında bir uygulama toorun için ihtiyaç duyduğunuz her şeyi ayarlama.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-111">This topic shows you how toouse [Azure PowerShell](/powershell/azure/overview) tooset up everything you need for an application toorun under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="a8cc5-112">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="a8cc5-112">Required permissions</span></span>
<span data-ttu-id="a8cc5-113">toocomplete bu konuda, Azure Active Directory ve Azure aboneliğinize yeterli izniniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-113">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="a8cc5-114">Özellikle, mümkün toocreate hello Azure Active Directory içinde bir uygulama olabilir. ve hello hizmet asıl tooa rolünü atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-114">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="a8cc5-115">hesabınızın yeterli izinlere sahip olup olmadığı hello portalıdır hello en kolay yolu toocheck.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-115">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="a8cc5-116">Bkz: [gerekli izni denetleyin](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="a8cc5-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="a8cc5-117">Şimdi, ile kimlik doğrulaması için tooa bölüm devam edin:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-117">Now, proceed tooa section for authenticating with:</span></span>

* [<span data-ttu-id="a8cc5-118">Parola</span><span class="sxs-lookup"><span data-stu-id="a8cc5-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="a8cc5-119">otomatik olarak imzalanan sertifika</span><span class="sxs-lookup"><span data-stu-id="a8cc5-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="a8cc5-120">Sertifika yetkilisinden sertifika</span><span class="sxs-lookup"><span data-stu-id="a8cc5-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="a8cc5-121">PowerShell komutları</span><span class="sxs-lookup"><span data-stu-id="a8cc5-121">PowerShell commands</span></span>

<span data-ttu-id="a8cc5-122">tooset bir hizmet sorumlusu yukarı kullanın:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-122">tooset up a service principal, you use:</span></span>

| <span data-ttu-id="a8cc5-123">Komut</span><span class="sxs-lookup"><span data-stu-id="a8cc5-123">Command</span></span> | <span data-ttu-id="a8cc5-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a8cc5-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="a8cc5-125">AzureRmADServicePrincipal yeni</span><span class="sxs-lookup"><span data-stu-id="a8cc5-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="a8cc5-126">Bir Azure Active Directory Hizmet sorumlusu oluşturur</span><span class="sxs-lookup"><span data-stu-id="a8cc5-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="a8cc5-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="a8cc5-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="a8cc5-128">Atar hello RBAC rolü toohello belirtilen asıl belirtilen, kapsam hello sırasında belirtilen.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-128">Assigns hello specified RBAC role toohello specified principal, at hello specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="a8cc5-129">Parola ile hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8cc5-129">Create service principal with password</span></span>

<span data-ttu-id="a8cc5-130">toocreate hello katkıda bulunan rolü, aboneliğiniz için hizmet sorumlusuyla kullanın:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-130">toocreate a service principal with hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="a8cc5-131">Merhaba örneği için 20 saniye tooallow hello yeni hizmet asıl toopropagate Azure Active Directory boyunca biraz zaman uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-131">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="a8cc5-132">Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} hello dizininde yok."</span><span class="sxs-lookup"><span data-stu-id="a8cc5-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="a8cc5-133">Merhaba aşağıdaki betiği toospecify hello varsayılan abonelik dışında bir kapsam sağlar ve bir hata oluşursa, yeniden deneme rol ataması hello:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-133">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs:</span></span>

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

<span data-ttu-id="a8cc5-134">Merhaba komut dosyasıyla ilgili bazı öğeleri toonote:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-134">A few items toonote about hello script:</span></span>

* <span data-ttu-id="a8cc5-135">toogrant hello kimlik erişim toohello varsayılan abonelik, gereksinim tooprovide ResourceGroup veya Subscriptionıd parametreleri.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-135">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="a8cc5-136">Yalnızca toolimit hello hello rol ataması tooa kaynak grubu kapsamını istediğinizde hello ResourceGroup parametresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-136">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
*  <span data-ttu-id="a8cc5-137">Bu örnekte, hello hizmet asıl toohello katkıda bulunan rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-137">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="a8cc5-138">Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a8cc5-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="a8cc5-139">Hello komut dosyası için 15 saniye tooallow hello yeni hizmet asıl toopropagate Azure Active Directory boyunca biraz zaman uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-139">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="a8cc5-140">Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} hello dizininde yok."</span><span class="sxs-lookup"><span data-stu-id="a8cc5-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="a8cc5-141">Toogrant hello hizmet asıl erişim toomore abonelik veya kaynak grupları gerekiyorsa, hello çalıştırmak `New-AzureRMRoleAssignment` farklı kapsamlar yeniden cmdlet'iyle.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-141">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="a8cc5-142">PowerShell ile kimlik bilgileri sağlayın</span><span class="sxs-lookup"><span data-stu-id="a8cc5-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="a8cc5-143">Şimdi, hello uygulaması tooperform işlemleri toolog de gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-143">Now, you need toolog in as hello application tooperform operations.</span></span> <span data-ttu-id="a8cc5-144">Merhaba kullanıcı adı için hello kullan `ApplicationId` Merhaba uygulaması için oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-144">For hello user name, use hello `ApplicationId` that you created for hello application.</span></span> <span data-ttu-id="a8cc5-145">Merhaba parolasını hello hello hesabı oluşturulurken belirtilen birinin kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-145">For hello password, use hello one you specified when creating hello account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="a8cc5-146">Merhaba Kiracı kimliği hassas, olmadığından doğrudan komut dosyanıza ekleme.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-146">hello tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="a8cc5-147">Tooretrieve hello Kiracı kimliği gerekiyorsa kullanın:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-147">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="a8cc5-148">Hizmet sorumlusu ile otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8cc5-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="a8cc5-149">toocreate otomatik olarak imzalanan sertifika ve hello katkıda bulunan rolü, aboneliğiniz için bir hizmet sorumlusu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-149">toocreate a service principal with a self-signed certificate and hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="a8cc5-150">Merhaba örneği için 20 saniye tooallow hello yeni hizmet asıl toopropagate Azure Active Directory boyunca biraz zaman uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-150">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="a8cc5-151">Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} hello dizininde yok."</span><span class="sxs-lookup"><span data-stu-id="a8cc5-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="a8cc5-152">Merhaba aşağıdaki betiği toospecify hello varsayılan abonelik dışında bir kapsam sağlar ve bir hata oluşursa, yeniden deneme rol ataması hello.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-152">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs.</span></span> <span data-ttu-id="a8cc5-153">Windows 10 veya Windows Server 2016 Azure PowerShell 2.0 yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

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

<span data-ttu-id="a8cc5-154">Merhaba komut dosyasıyla ilgili bazı öğeleri toonote:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-154">A few items toonote about hello script:</span></span>

* <span data-ttu-id="a8cc5-155">toogrant hello kimlik erişim toohello varsayılan abonelik, gereksinim tooprovide ResourceGroup veya Subscriptionıd parametreleri.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-155">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="a8cc5-156">Yalnızca toolimit hello hello rol ataması tooa kaynak grubu kapsamını istediğinizde hello ResourceGroup parametresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-156">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
* <span data-ttu-id="a8cc5-157">Bu örnekte, hello hizmet asıl toohello katkıda bulunan rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-157">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="a8cc5-158">Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a8cc5-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="a8cc5-159">Hello komut dosyası için 15 saniye tooallow hello yeni hizmet asıl toopropagate Azure Active Directory boyunca biraz zaman uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-159">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="a8cc5-160">Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} hello dizininde yok."</span><span class="sxs-lookup"><span data-stu-id="a8cc5-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="a8cc5-161">Toogrant hello hizmet asıl erişim toomore abonelik veya kaynak grupları gerekiyorsa, hello çalıştırmak `New-AzureRMRoleAssignment` farklı kapsamlar yeniden cmdlet'iyle.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-161">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="a8cc5-162">Varsa, **Windows 10 veya Windows Server 2016 Technical Preview gerekmez**, toodownload hello gereksinim [otomatik olarak imzalanan sertifika Oluşturucu](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) Microsoft Script Center gelen.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need toodownload hello [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="a8cc5-163">İçeriğini ayıklayın ve ihtiyacınız hello cmdlet'i içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-163">Extract its contents and import hello cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="a8cc5-164">Hello komut dosyasında, aşağıdaki iki satır toogenerate hello sertifika hello yerine koyun.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-164">In hello script, substitute hello following two lines toogenerate hello certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="a8cc5-165">Otomatik PowerShell komut dosyası aracılığıyla sertifikası sağlayın</span><span class="sxs-lookup"><span data-stu-id="a8cc5-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="a8cc5-166">Bir hizmet sorumlusu oturum olduğunda, AD uygulamanız için hello dizininin tooprovide hello Kiracı kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-166">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="a8cc5-167">Bir kiracı, Azure Active Directory örneğidir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="a8cc5-168">Yalnızca bir aboneliğiniz varsa, kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="a8cc5-169">Merhaba uygulama kimliği ve Kiracı kimliği olmayan hassas, doğrudan komut dosyanıza katıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-169">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="a8cc5-170">Tooretrieve hello Kiracı kimliği gerekiyorsa kullanın:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-170">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="a8cc5-171">Tooretrieve hello uygulama kimliği gerekiyorsa kullanın:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-171">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="a8cc5-172">Sertifika yetkilisinden sertifika ile hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8cc5-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="a8cc5-173">toouse verilen sertifika, sertifika yetkilisi toocreate hizmet sorumlusu, aşağıdaki komut dosyası kullan hello:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-173">toouse a certificate issued from a Certificate Authority toocreate service principal, use hello following script:</span></span>

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

<span data-ttu-id="a8cc5-174">Merhaba komut dosyasıyla ilgili bazı öğeleri toonote:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-174">A few items toonote about hello script:</span></span>

* <span data-ttu-id="a8cc5-175">Kapsamlı toohello abonelik erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-175">Access is scoped toohello subscription.</span></span>
* <span data-ttu-id="a8cc5-176">Bu örnekte, hello hizmet asıl toohello katkıda bulunan rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-176">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="a8cc5-177">Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="a8cc5-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="a8cc5-178">Hello komut dosyası için 15 saniye tooallow hello yeni hizmet asıl toopropagate Azure Active Directory boyunca biraz zaman uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-178">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="a8cc5-179">Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} hello dizininde yok."</span><span class="sxs-lookup"><span data-stu-id="a8cc5-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="a8cc5-180">Toogrant hello hizmet asıl erişim toomore abonelik veya kaynak grupları gerekiyorsa, hello çalıştırmak `New-AzureRMRoleAssignment` farklı kapsamlar yeniden cmdlet'iyle.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-180">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="a8cc5-181">Otomatik PowerShell komut dosyası aracılığıyla sertifikası sağlayın</span><span class="sxs-lookup"><span data-stu-id="a8cc5-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="a8cc5-182">Bir hizmet sorumlusu oturum olduğunda, AD uygulamanız için hello dizininin tooprovide hello Kiracı kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-182">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="a8cc5-183">Bir kiracı, Azure Active Directory örneğidir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="a8cc5-184">Merhaba uygulama kimliği ve Kiracı kimliği olmayan hassas, doğrudan komut dosyanıza katıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-184">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="a8cc5-185">Tooretrieve hello Kiracı kimliği gerekiyorsa kullanın:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-185">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="a8cc5-186">Tooretrieve hello uygulama kimliği gerekiyorsa kullanın:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-186">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="a8cc5-187">Kimlik bilgilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="a8cc5-187">Change credentials</span></span>

<span data-ttu-id="a8cc5-188">ya da güvenliğinin aşılması veya bir kimlik bilgisi sona erme nedeniyle, bir AD uygulaması için toochange hello kimlik hello kullan [Kaldır AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) ve [yeni AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-188">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="a8cc5-189">tooremove bir uygulama için tüm hello kimlik bilgilerini kullan:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-189">tooremove all hello credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="a8cc5-190">tooadd bir parola kullanın:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-190">tooadd a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="a8cc5-191">tooadd sertifika değeri, bu konu başlığı altında gösterildiği gibi otomatik olarak imzalanan bir sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-191">tooadd a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="a8cc5-192">Ardından, kullanın:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a><span data-ttu-id="a8cc5-193">Erişim belirteci toosimplify oturum Kaydet</span><span class="sxs-lookup"><span data-stu-id="a8cc5-193">Save access token toosimplify log in</span></span>
<span data-ttu-id="a8cc5-194">içinde toolog gereken her zaman tooavoid hello hizmet asıl kimlik bilgileri sağlama, hello erişim belirteci kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-194">tooavoid providing hello service principal credentials every time it needs toolog in, you can save hello access token.</span></span>

<span data-ttu-id="a8cc5-195">toouse hello geçerli erişim belirteci bir sonraki oturumunda hello profil kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-195">toouse hello current access token in a later session, save hello profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="a8cc5-196">Hello profil açın ve içeriğini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-196">Open hello profile and examine its contents.</span></span> <span data-ttu-id="a8cc5-197">Bir erişim belirteci içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-197">Notice that it contains an access token.</span></span> <span data-ttu-id="a8cc5-198">El ile yeniden oturum açmayı yerine, yalnızca hello profili yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-198">Instead of manually logging in again, simply load hello profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="a8cc5-199">Merhaba belirtecin geçerli olduğu sürece kaydedilmiş bir profil kullanarak yalnızca çalıştığı şekilde hello erişim belirtecinin süresi.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-199">hello access token expires, so using a saved profile only works for as long as hello token is valid.</span></span>
>  

<span data-ttu-id="a8cc5-200">Alternatif olarak, PowerShell toolog REST işlemlerini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-200">Alternatively, you can invoke REST operations from PowerShell toolog in.</span></span> <span data-ttu-id="a8cc5-201">Merhaba kimlik doğrulaması yanıttan hello erişim belirteci diğer işlemleri ile kullanılmak üzere alabilir.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-201">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="a8cc5-202">REST işlemlerini çağırarak hello erişim belirteci alma bir örnek için bkz: [bir erişim belirteci oluşturma](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="a8cc5-202">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="a8cc5-203">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="a8cc5-203">Debug</span></span>

<span data-ttu-id="a8cc5-204">Bir hizmet sorumlusu oluşturma sırasında aşağıdaki hatalar hello karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-204">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="a8cc5-205">**"Authentication_Unauthorized"** veya **"abonelik hello bağlamda bulunamadı."**</span><span class="sxs-lookup"><span data-stu-id="a8cc5-205">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="a8cc5-206">-Hesabınızı hello olmadığında bu hatayı gördüğünüz [gerekli izinleri](#required-permissions) hello Azure Active Directory tooregister bir uygulama üzerinde.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-206">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="a8cc5-207">Yalnızca yönetici kullanıcıların Azure Active Directory'de uygulamaları kaydedebilirsiniz ve hesabınızın bir yönetici değil, bu hata genellikle, bakın Yönetici tooeither atamak, tooan Yönetici rolü ya da tooenable kullanıcılar tooregister uygulamaları isteyin.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="a8cc5-208">Hesabınızı **"yetkilendirme tooperform eylemi 'Microsoft.Authorization/roleAssignments/write' kapsamı üzerinde '/ subscriptions / {GUID}' yok."**  -Hesabınızı rol tooan kimlik yeterli izinleri tooassign olmadığında bu hatayı bakın.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-208">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="a8cc5-209">Abonelik Yöneticisi tooadd isteyin, tooUser erişim Yönetici rolü.</span><span class="sxs-lookup"><span data-stu-id="a8cc5-209">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="a8cc5-210">Örnek uygulamalar</span><span class="sxs-lookup"><span data-stu-id="a8cc5-210">Sample applications</span></span>
<span data-ttu-id="a8cc5-211">Farklı platformlarda üzerinden hello uygulama olarak oturum açma hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="a8cc5-211">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="a8cc5-212">.NET</span><span class="sxs-lookup"><span data-stu-id="a8cc5-212">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="a8cc5-213">Java</span><span class="sxs-lookup"><span data-stu-id="a8cc5-213">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="a8cc5-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="a8cc5-214">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="a8cc5-215">Python</span><span class="sxs-lookup"><span data-stu-id="a8cc5-215">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="a8cc5-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="a8cc5-216">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="a8cc5-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8cc5-217">Next steps</span></span>
* <span data-ttu-id="a8cc5-218">Kaynakları yönetmek için Azure'da bir uygulamayı tümleştirme ayrıntılı adımlar için bkz: [Geliştirici Kılavuzu tooauthorization hello Azure Kaynak Yöneticisi API'si ile](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a8cc5-218">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="a8cc5-219">Uygulamalar ve hizmet asıl adı daha ayrıntılı bir açıklaması için bkz: [uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="a8cc5-219">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="a8cc5-220">Azure Active Directory kimlik doğrulaması hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="a8cc5-220">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="a8cc5-221">Verilen veya toousers reddedilen kullanılabilir eylemler listesi için bkz: [Azure Resource Manager kaynak sağlayıcısı işlemleri](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a8cc5-221">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

