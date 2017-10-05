---
title: "PowerShell ile Azure uygulama kimliği oluşturma | Microsoft Docs"
description: "Bir Azure Active Directory uygulaması ve hizmet sorumlusu oluşturmak ve rol tabanlı erişim denetimi aracılığıyla kaynaklara erişim izni için Azure PowerShell kullanmayı açıklar. Uygulama ile bir parola veya sertifika kimlik doğrulaması yapmayı gösterir."
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
ms.openlocfilehash: 55e83b0742652abbb42100a11a468bc13a7a8aed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-powershell-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="c0815-104">Kaynaklara erişmek üzere hizmet sorumlusu oluşturmak için Azure PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="c0815-104">Use Azure PowerShell to create a service principal to access resources</span></span>

<span data-ttu-id="c0815-105">Bir uygulama ya da kaynaklara erişmek için gereken komut dosyası varsa, uygulamanın kendi kimlik bilgileriyle kimlik doğrulamasını ve uygulama için bir kimlik ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c0815-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="c0815-106">Bu kimlik, bir hizmet sorumlusu bilinir.</span><span class="sxs-lookup"><span data-stu-id="c0815-106">This identity is known as a service principal.</span></span> <span data-ttu-id="c0815-107">Bu yaklaşım sağlar:</span><span class="sxs-lookup"><span data-stu-id="c0815-107">This approach enables you to:</span></span>

* <span data-ttu-id="c0815-108">Kendi izinlerinizi farklı uygulama kimliği için izinleri atayın.</span><span class="sxs-lookup"><span data-stu-id="c0815-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="c0815-109">Genellikle, bu izinleri tam olarak hangi uygulama yapması gereken için kısıtlanır.</span><span class="sxs-lookup"><span data-stu-id="c0815-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="c0815-110">Sertifika kimlik doğrulaması için Katılımsız betik yürütülürken kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0815-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="c0815-111">Bu konuda nasıl kullanılacağını gösterir [Azure PowerShell](/powershell/azure/overview) kendi kimlik bilgilerini ve kimlik altında çalıştırmak bir uygulama için gereksinim duyduğunuz her şeyi ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="c0815-111">This topic shows you how to use [Azure PowerShell](/powershell/azure/overview) to set up everything you need for an application to run under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="c0815-112">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="c0815-112">Required permissions</span></span>
<span data-ttu-id="c0815-113">Bu konuda tamamlamak için Azure Active Directory ve Azure aboneliğinize yeterli izniniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0815-113">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="c0815-114">Özellikle, Azure Active Directory'de bir uygulama oluşturun ve hizmet sorumlusu rol atama mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0815-114">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="c0815-115">Hesabınızın yeterli izinlere sahip olup olmadığını denetlemenin en kolay yolu portalı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="c0815-115">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="c0815-116">Bkz: [gerekli izni denetleyin](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="c0815-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="c0815-117">Şimdi, ile kimlik doğrulaması için bir bölüm için devam edin:</span><span class="sxs-lookup"><span data-stu-id="c0815-117">Now, proceed to a section for authenticating with:</span></span>

* [<span data-ttu-id="c0815-118">Parola</span><span class="sxs-lookup"><span data-stu-id="c0815-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="c0815-119">otomatik olarak imzalanan sertifika</span><span class="sxs-lookup"><span data-stu-id="c0815-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="c0815-120">Sertifika yetkilisinden sertifika</span><span class="sxs-lookup"><span data-stu-id="c0815-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="c0815-121">PowerShell komutları</span><span class="sxs-lookup"><span data-stu-id="c0815-121">PowerShell commands</span></span>

<span data-ttu-id="c0815-122">Bir hizmet sorumlusu ayarlamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-122">To set up a service principal, you use:</span></span>

| <span data-ttu-id="c0815-123">Komut</span><span class="sxs-lookup"><span data-stu-id="c0815-123">Command</span></span> | <span data-ttu-id="c0815-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c0815-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="c0815-125">AzureRmADServicePrincipal yeni</span><span class="sxs-lookup"><span data-stu-id="c0815-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="c0815-126">Bir Azure Active Directory Hizmet sorumlusu oluşturur</span><span class="sxs-lookup"><span data-stu-id="c0815-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="c0815-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="c0815-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="c0815-128">Belirtilen kapsamda belirtilen asıl belirtilen RBAC rolü atar.</span><span class="sxs-lookup"><span data-stu-id="c0815-128">Assigns the specified RBAC role to the specified principal, at the specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="c0815-129">Parola ile hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0815-129">Create service principal with password</span></span>

<span data-ttu-id="c0815-130">Aboneliğiniz için katılımcı rolü ile bir hizmet sorumlusu oluşturmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-130">To create a service principal with the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="c0815-131">Örneğin yeni hizmet için bir süre Azure Active Directory yaymak için asıl izin vermek 20 saniye için uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="c0815-131">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="c0815-132">Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} dizininde yok."</span><span class="sxs-lookup"><span data-stu-id="c0815-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="c0815-133">Aşağıdaki komut dosyası varsayılan abonelik dışında bir kapsam belirtmenize olanak sağlar ve bir hata oluşursa rol atamasını yeniden deneme sayısı:</span><span class="sxs-lookup"><span data-stu-id="c0815-133">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs:</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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

 
 # Create Service Principal for the AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="c0815-134">Komut dosyası hakkında dikkat edilecek bazı öğeler için:</span><span class="sxs-lookup"><span data-stu-id="c0815-134">A few items to note about the script:</span></span>

* <span data-ttu-id="c0815-135">Varsayılan abonelik kimliği erişimi vermek için ResourceGroup veya Subscriptionıd parametreleri sağlamak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c0815-135">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="c0815-136">Yalnızca bir kaynak grubu için rol ataması kapsamını sınırlamak istediğinizde ResourceGroup parametresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c0815-136">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
*  <span data-ttu-id="c0815-137">Bu örnekte, hizmet sorumlusu katkıda bulunan rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c0815-137">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="c0815-138">Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c0815-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="c0815-139">Komut dosyasını yeni hizmet için bir süre Azure Active Directory yaymak için asıl izin vermek 15 saniye için uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="c0815-139">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="c0815-140">Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} dizininde yok."</span><span class="sxs-lookup"><span data-stu-id="c0815-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="c0815-141">Daha fazla abonelik veya kaynak grupları için hizmet asıl erişimi vermeniz gerekiyorsa, çalıştırmak `New-AzureRMRoleAssignment` farklı kapsamlar yeniden cmdlet'iyle.</span><span class="sxs-lookup"><span data-stu-id="c0815-141">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="c0815-142">PowerShell ile kimlik bilgileri sağlayın</span><span class="sxs-lookup"><span data-stu-id="c0815-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="c0815-143">Şimdi, işlemleri gerçekleştirmek için uygulama olarak oturum açmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0815-143">Now, you need to log in as the application to perform operations.</span></span> <span data-ttu-id="c0815-144">Kullanıcı adı için `ApplicationId` uygulama için oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="c0815-144">For the user name, use the `ApplicationId` that you created for the application.</span></span> <span data-ttu-id="c0815-145">Parola için hesabı oluşturulurken belirtilen bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0815-145">For the password, use the one you specified when creating the account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="c0815-146">Kiracı kimliği hassas, olmadığından doğrudan komut dosyanıza ekleme.</span><span class="sxs-lookup"><span data-stu-id="c0815-146">The tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="c0815-147">Kiracı Kimliği almak gereken durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-147">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="c0815-148">Hizmet sorumlusu ile otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0815-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="c0815-149">Kendinden imzalı bir sertifika ve aboneliğiniz için katılımcı rolü ile bir hizmet sorumlusu oluşturmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-149">To create a service principal with a self-signed certificate and the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="c0815-150">Örneğin yeni hizmet için bir süre Azure Active Directory yaymak için asıl izin vermek 20 saniye için uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="c0815-150">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="c0815-151">Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} dizininde yok."</span><span class="sxs-lookup"><span data-stu-id="c0815-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="c0815-152">Aşağıdaki komut dosyasında varsayılan abonelik dışında bir kapsam belirtmenize olanak sağlar ve bir hata oluşursa rol atamasını yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="c0815-152">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs.</span></span> <span data-ttu-id="c0815-153">Windows 10 veya Windows Server 2016 Azure PowerShell 2.0 yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c0815-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="c0815-154">Komut dosyası hakkında dikkat edilecek bazı öğeler için:</span><span class="sxs-lookup"><span data-stu-id="c0815-154">A few items to note about the script:</span></span>

* <span data-ttu-id="c0815-155">Varsayılan abonelik kimliği erişimi vermek için ResourceGroup veya Subscriptionıd parametreleri sağlamak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c0815-155">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="c0815-156">Yalnızca bir kaynak grubu için rol ataması kapsamını sınırlamak istediğinizde ResourceGroup parametresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c0815-156">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
* <span data-ttu-id="c0815-157">Bu örnekte, hizmet sorumlusu katkıda bulunan rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c0815-157">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="c0815-158">Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c0815-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="c0815-159">Komut dosyasını yeni hizmet için bir süre Azure Active Directory yaymak için asıl izin vermek 15 saniye için uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="c0815-159">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="c0815-160">Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} dizininde yok."</span><span class="sxs-lookup"><span data-stu-id="c0815-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="c0815-161">Daha fazla abonelik veya kaynak grupları için hizmet asıl erişimi vermeniz gerekiyorsa, çalıştırmak `New-AzureRMRoleAssignment` farklı kapsamlar yeniden cmdlet'iyle.</span><span class="sxs-lookup"><span data-stu-id="c0815-161">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="c0815-162">Varsa, **Windows 10 veya Windows Server 2016 Technical Preview gerekmez**, karşıdan yüklemek gereken [otomatik olarak imzalanan sertifika Oluşturucu](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) Microsoft Script Center gelen.</span><span class="sxs-lookup"><span data-stu-id="c0815-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need to download the [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="c0815-163">İçeriğini ayıklayın ve ihtiyacınız cmdlet'i içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="c0815-163">Extract its contents and import the cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="c0815-164">Komut dosyasında, sertifikayı oluşturmak için aşağıdaki iki satırı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c0815-164">In the script, substitute the following two lines to generate the certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="c0815-165">Otomatik PowerShell komut dosyası aracılığıyla sertifikası sağlayın</span><span class="sxs-lookup"><span data-stu-id="c0815-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="c0815-166">Bir hizmet sorumlusu oturum olduğunda, Kiracı kimliği dizininin AD uygulamanız için sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0815-166">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="c0815-167">Bir kiracı, Azure Active Directory örneğidir.</span><span class="sxs-lookup"><span data-stu-id="c0815-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="c0815-168">Yalnızca bir aboneliğiniz varsa, kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c0815-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="c0815-169">Doğrudan komut dosyanıza katıştırmak için uygulama kimliği ve Kiracı kimliği harfe duyarlı değildir.</span><span class="sxs-lookup"><span data-stu-id="c0815-169">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="c0815-170">Kiracı Kimliği almak gereken durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-170">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="c0815-171">Uygulama Kimliğini almak gereken durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-171">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="c0815-172">Sertifika yetkilisinden sertifika ile hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0815-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="c0815-173">Hizmet sorumlusu oluşturmak için bir sertifika yetkilisi tarafından verilen bir sertifika kullanmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-173">To use a certificate issued from a Certificate Authority to create service principal, use the following script:</span></span>

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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

<span data-ttu-id="c0815-174">Komut dosyası hakkında dikkat edilecek bazı öğeler için:</span><span class="sxs-lookup"><span data-stu-id="c0815-174">A few items to note about the script:</span></span>

* <span data-ttu-id="c0815-175">Erişim aboneliği kapsamlıdır.</span><span class="sxs-lookup"><span data-stu-id="c0815-175">Access is scoped to the subscription.</span></span>
* <span data-ttu-id="c0815-176">Bu örnekte, hizmet sorumlusu katkıda bulunan rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c0815-176">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="c0815-177">Diğer roller için bkz: [RBAC: yerleşik roller](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c0815-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="c0815-178">Komut dosyasını yeni hizmet için bir süre Azure Active Directory yaymak için asıl izin vermek 15 saniye için uyku moduna geçer.</span><span class="sxs-lookup"><span data-stu-id="c0815-178">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="c0815-179">Kodunuzu yetecek kadar uzun süre beklemez belirten bir hata görürsünüz: "PrincipalNotFound: asıl {id} dizininde yok."</span><span class="sxs-lookup"><span data-stu-id="c0815-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="c0815-180">Daha fazla abonelik veya kaynak grupları için hizmet asıl erişimi vermeniz gerekiyorsa, çalıştırmak `New-AzureRMRoleAssignment` farklı kapsamlar yeniden cmdlet'iyle.</span><span class="sxs-lookup"><span data-stu-id="c0815-180">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="c0815-181">Otomatik PowerShell komut dosyası aracılığıyla sertifikası sağlayın</span><span class="sxs-lookup"><span data-stu-id="c0815-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="c0815-182">Bir hizmet sorumlusu oturum olduğunda, Kiracı kimliği dizininin AD uygulamanız için sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0815-182">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="c0815-183">Bir kiracı, Azure Active Directory örneğidir.</span><span class="sxs-lookup"><span data-stu-id="c0815-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="c0815-184">Doğrudan komut dosyanıza katıştırmak için uygulama kimliği ve Kiracı kimliği harfe duyarlı değildir.</span><span class="sxs-lookup"><span data-stu-id="c0815-184">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="c0815-185">Kiracı Kimliği almak gereken durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-185">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="c0815-186">Uygulama Kimliğini almak gereken durumlarda kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-186">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="c0815-187">Kimlik bilgilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="c0815-187">Change credentials</span></span>

<span data-ttu-id="c0815-188">Ya da güvenliğinin aşılması veya bir kimlik bilgisi sona erme nedeniyle, bir AD uygulaması için kimlik bilgilerini değiştirmek için kullanın [Kaldır AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) ve [yeni AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="c0815-188">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use the [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="c0815-189">Bir uygulama için tüm kimlik bilgilerini kaldırmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-189">To remove all the credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="c0815-190">Bir parola eklemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-190">To add a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="c0815-191">Bir sertifika değer eklemek için bu konudaki gösterildiği gibi otomatik olarak imzalanan bir sertifika oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0815-191">To add a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="c0815-192">Ardından, kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0815-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-to-simplify-log-in"></a><span data-ttu-id="c0815-193">Oturum açma basitleştirmek için erişim belirteci Kaydet</span><span class="sxs-lookup"><span data-stu-id="c0815-193">Save access token to simplify log in</span></span>
<span data-ttu-id="c0815-194">Oturum açmak gereken her zaman hizmet asıl kimlik bilgilerini sağlayan önlemek için erişim belirteci kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0815-194">To avoid providing the service principal credentials every time it needs to log in, you can save the access token.</span></span>

<span data-ttu-id="c0815-195">Bir sonraki oturumda geçerli erişim belirtecini kullanmak için profil kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c0815-195">To use the current access token in a later session, save the profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="c0815-196">Profil açın ve içeriğini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="c0815-196">Open the profile and examine its contents.</span></span> <span data-ttu-id="c0815-197">Bir erişim belirteci içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c0815-197">Notice that it contains an access token.</span></span> <span data-ttu-id="c0815-198">El ile yeniden oturum açmayı yerine, yalnızca profili yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c0815-198">Instead of manually logging in again, simply load the profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="c0815-199">Belirtecin geçerli olduğu sürece kaydedilmiş bir profil kullanarak yalnızca çalıştığı şekilde erişim belirtecinin süresi.</span><span class="sxs-lookup"><span data-stu-id="c0815-199">The access token expires, so using a saved profile only works for as long as the token is valid.</span></span>
>  

<span data-ttu-id="c0815-200">Alternatif olarak, oturum açmak için PowerShell REST işlemlerini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0815-200">Alternatively, you can invoke REST operations from PowerShell to log in.</span></span> <span data-ttu-id="c0815-201">Kimlik doğrulaması yanıtından, diğer işlemleri ile kullanmak için erişim belirtecini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0815-201">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="c0815-202">REST işlemlerini çağırarak erişim belirtecini alma bir örnek için bkz: [bir erişim belirteci oluşturma](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="c0815-202">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="c0815-203">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="c0815-203">Debug</span></span>

<span data-ttu-id="c0815-204">Bir hizmet sorumlusu oluşturma sırasında şu hatalarla karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c0815-204">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="c0815-205">**"Authentication_Unauthorized"** veya **"abonelik bağlamda bulunamadı."**</span><span class="sxs-lookup"><span data-stu-id="c0815-205">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="c0815-206">Hesabınızı olmadığı zaman-bu hatayı görmek [gerekli izinleri](#required-permissions) uygulama kaydetmek için Azure Active Directory üzerinde.</span><span class="sxs-lookup"><span data-stu-id="c0815-206">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="c0815-207">Yalnızca yönetici kullanıcıların Azure Active Directory'de uygulamaları kaydedebilirsiniz ve hesabınızın bir yönetici değil, bu hata genellikle, bakın</span><span class="sxs-lookup"><span data-stu-id="c0815-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="c0815-208">Ya da bir yönetici rolü atayın veya kullanıcıların uygulamaları kaydetmek yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="c0815-208">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="c0815-209">Hesabınızı **"kapsamı '/ subscriptions / {GUID}' üzerinde 'Microsoft.Authorization/roleAssignments/write' işlemini gerçekleştirme yetkisi yok."**  -Hesabınız için bir kimlik rol atamak için yeterli izinlere sahip olmadığında bu hataya bakın.</span><span class="sxs-lookup"><span data-stu-id="c0815-209">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="c0815-210">Kullanıcı erişimi Yöneticisi rolüne eklemek için abonelik yöneticinize başvurun.</span><span class="sxs-lookup"><span data-stu-id="c0815-210">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="c0815-211">Örnek uygulamalar</span><span class="sxs-lookup"><span data-stu-id="c0815-211">Sample applications</span></span>
<span data-ttu-id="c0815-212">Farklı platformlarda üzerinden uygulama olarak oturum açma hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="c0815-212">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="c0815-213">.NET</span><span class="sxs-lookup"><span data-stu-id="c0815-213">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="c0815-214">Java</span><span class="sxs-lookup"><span data-stu-id="c0815-214">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="c0815-215">Node.js</span><span class="sxs-lookup"><span data-stu-id="c0815-215">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="c0815-216">Python</span><span class="sxs-lookup"><span data-stu-id="c0815-216">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="c0815-217">Ruby</span><span class="sxs-lookup"><span data-stu-id="c0815-217">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="c0815-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0815-218">Next steps</span></span>
* <span data-ttu-id="c0815-219">Kaynakları yönetmek için Azure'da bir uygulamayı tümleştirme ayrıntılı adımlar için bkz: [Geliştirici Kılavuzu'na yetkilendirme Azure Kaynak Yöneticisi API'si ile](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c0815-219">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="c0815-220">Uygulamalar ve hizmet asıl adı daha ayrıntılı bir açıklaması için bkz: [uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="c0815-220">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="c0815-221">Azure Active Directory kimlik doğrulaması hakkında daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="c0815-221">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="c0815-222">Verilen veya kullanıcılar için reddedilen kullanılabilir eylemler listesi için bkz: [Azure Resource Manager kaynak sağlayıcısı işlemleri](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="c0815-222">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

