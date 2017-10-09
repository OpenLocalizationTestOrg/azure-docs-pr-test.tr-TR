---
title: Azure Windows VM aaaEncrypt disklerde | Microsoft Docs
description: "Nasıl tooencrypt sanal diskler için bir Windows VM üzerinde Gelişmiş Güvenlik Azure PowerShell'i kullanma"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="786dd-103">Nasıl bir Windows VM üzerindeki tooencrypt sanal diskler</span><span class="sxs-lookup"><span data-stu-id="786dd-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="786dd-104">Geliştirilmiş sanal makine (VM) güvenlik ve uyumluluk için Azure sanal diskleri şifrelenebilir.</span><span class="sxs-lookup"><span data-stu-id="786dd-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="786dd-105">Diskleri, bir Azure anahtar kasası güvenli şifreleme anahtarları kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="786dd-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="786dd-106">Bu şifreleme anahtarları denetlemek ve bunların kullanılması denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="786dd-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="786dd-107">Bu makale ayrıntıları nasıl Windows Azure PowerShell kullanarak bir VM sanal disklerde tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="786dd-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="786dd-108">Ayrıca [hello Azure CLI 2.0 kullanarak bir Linux VM şifrelemek](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="786dd-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="786dd-109">Disk şifrelemesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="786dd-109">Overview of disk encryption</span></span>
<span data-ttu-id="786dd-110">Windows sanal makineleri sanal disklerde Bitlocker kullanılarak bekleme sırasında şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="786dd-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="786dd-111">Azure sanal diskleri şifreleme ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="786dd-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="786dd-112">Şifreleme anahtarları yazılım koruması'nı kullanarak Azure anahtar kasası içinde depolanır veya içe aktarmak ya da anahtarlarınızı tooFIPS sertifikalı donanım güvenlik modüllerinde (HSM'ler) 140-2 Düzey 2 standartları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="786dd-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="786dd-113">Bu şifreleme anahtarlar kullanılan tooencrypt ve sanal diskleri ekli tooyour VM şifresini.</span><span class="sxs-lookup"><span data-stu-id="786dd-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="786dd-114">Bu şifreleme anahtarları denetimin korumak ve kullanımlarını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="786dd-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="786dd-115">Bir Azure Active Directory Hizmet sorumlusu VM'ler açma ve kapatma gücü gibi bu şifreleme anahtarları verme için güvenli bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="786dd-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="786dd-116">bir VM şifrelemek için hello işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="786dd-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="786dd-117">Bir şifreleme anahtarının bir Azure anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="786dd-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="786dd-118">Merhaba şifreleme anahtar toobe diskleri şifrelemek için kullanılabilir yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="786dd-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="786dd-119">tooread hello şifreleme anahtarını hello Azure anahtar kasası oluşturma bir Azure Active Directory hizmet asıl hello uygun izinlere sahip.</span><span class="sxs-lookup"><span data-stu-id="786dd-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="786dd-120">Merhaba komutu tooencrypt hello Azure Active Directory hizmet asıl ve uygun şifreleme anahtar toobe kullanılan belirtme, sanal diskler gönderin.</span><span class="sxs-lookup"><span data-stu-id="786dd-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="786dd-121">Hello Azure Active Directory hizmet asıl istekleri Azure anahtar kasası gerekli şifreleme anahtarından hello.</span><span class="sxs-lookup"><span data-stu-id="786dd-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="786dd-122">Merhaba sanal diskler sağlanan hello şifreleme anahtarı kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="786dd-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="786dd-123">Şifreleme işlemi</span><span class="sxs-lookup"><span data-stu-id="786dd-123">Encryption process</span></span>
<span data-ttu-id="786dd-124">Disk şifrelemesi ek bileşenler aşağıdaki hello üzerinde dayanır:</span><span class="sxs-lookup"><span data-stu-id="786dd-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="786dd-125">**Azure anahtar kasası** -kullanılan toosafeguard şifreleme anahtarları ve gizli anahtarları hello disk şifreleme/şifre çözme işlemi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="786dd-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="786dd-126">Varsa, mevcut bir Azure anahtar kasası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="786dd-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="786dd-127">Bir anahtar kasası tooencrypting disk toodedicate sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="786dd-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="786dd-128">tooseparate yönetim sınırlarını ve anahtar görünürlük, ayrılmış bir anahtar kasası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="786dd-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="786dd-129">**Azure Active Directory** - tanıtıcıları hello gerekli şifreleme anahtarlarını güvenli değişimi ve kimlik doğrulaması için istenen eylemler.</span><span class="sxs-lookup"><span data-stu-id="786dd-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="786dd-130">Genellikle, uygulamanızı barındırmak için var olan bir Azure Active Directory örneğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="786dd-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="786dd-131">Merhaba hizmet sorumlusu hello uygun şifreleme anahtarları verilmesi ve güvenli mekanizması toorequest sağlar.</span><span class="sxs-lookup"><span data-stu-id="786dd-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="786dd-132">Azure Active Directory ile tümleşen gerçek uygulama geliştirme değil.</span><span class="sxs-lookup"><span data-stu-id="786dd-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="786dd-133">Gereksinimler ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="786dd-133">Requirements and limitations</span></span>
<span data-ttu-id="786dd-134">Desteklenen senaryolar ve disk şifrelemesi için gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="786dd-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="786dd-135">Yeni Windows sanal makineleri Azure Market görüntülerini veya özel VHD görüntüsü üzerinde şifrelemeyi etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="786dd-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="786dd-136">Var olan Windows sanal makineleri Azure üzerinde şifrelemeyi etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="786dd-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="786dd-137">Depolama alanları kullanılarak yapılandırılan Windows VM'ler üzerinde şifrelemeyi etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="786dd-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="786dd-138">İşletim sistemi ve veri şifreleme devre dışı bırakma Windows VM'ler için sürücüleri.</span><span class="sxs-lookup"><span data-stu-id="786dd-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="786dd-139">Tüm kaynaklar (örneğin, anahtar kasası, depolama hesabı ve VM) hello olmalıdır aynı Azure bölgesinde ve abonelik.</span><span class="sxs-lookup"><span data-stu-id="786dd-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="786dd-140">Standart katmanı VM'ler D, DS, G ve GS serisi VM'ler gibi.</span><span class="sxs-lookup"><span data-stu-id="786dd-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="786dd-141">Disk şifrelemesi senaryoları aşağıdaki hello şu anda desteklenmiyor:</span><span class="sxs-lookup"><span data-stu-id="786dd-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="786dd-142">Temel katman VM'ler.</span><span class="sxs-lookup"><span data-stu-id="786dd-142">Basic tier VMs.</span></span>
* <span data-ttu-id="786dd-143">Merhaba Klasik dağıtım modeli kullanılarak oluşturulan VM'ler.</span><span class="sxs-lookup"><span data-stu-id="786dd-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="786dd-144">Merhaba şifreleme anahtarları zaten şifrelenmiş VM'de güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="786dd-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="786dd-145">Şirket içi anahtar yönetimi hizmeti ile tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="786dd-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="786dd-146">Azure anahtar kasası ve anahtarları oluşturma</span><span class="sxs-lookup"><span data-stu-id="786dd-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="786dd-147">Başlamadan önce o hello en son sürümünü hello Azure PowerShell modülünün yüklü emin olun.</span><span class="sxs-lookup"><span data-stu-id="786dd-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="786dd-148">Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="786dd-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="786dd-149">Merhaba komut örnekleri tüm örnek parametreleri kendi adları, konum ve anahtar değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="786dd-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="786dd-150">Merhaba aşağıdaki örnekleri kullanmak, bir kural *myResourceGroup*, *myKeyVault*, *myVM*, vb..</span><span class="sxs-lookup"><span data-stu-id="786dd-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="786dd-151">Merhaba ilk adımı şifreleme anahtarlarınızı toocreate Azure anahtar kasası toostore değil.</span><span class="sxs-lookup"><span data-stu-id="786dd-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="786dd-152">Azure anahtar kasası anahtarları, gizli depolayabilir veya toosecurely izin parolalar, uygulama ve hizmetlerinize uygulamadan.</span><span class="sxs-lookup"><span data-stu-id="786dd-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="786dd-153">Sanal disk şifrelemesi için bir anahtar kasası toostore kullanılan tooencrypt bir şifreleme anahtarı oluşturun veya sanal diskleri şifresini.</span><span class="sxs-lookup"><span data-stu-id="786dd-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="786dd-154">Azure aboneliğinizle içinde Hello Azure anahtar kasası sağlayıcısını etkinleştir [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), sahip bir kaynak grubu oluşturma [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="786dd-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="786dd-155">Merhaba aşağıdaki örnekte oluşturur bir kaynak grubu adı *myResourceGroup* hello içinde *Doğu ABD* konumu:</span><span class="sxs-lookup"><span data-stu-id="786dd-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="786dd-156">depolama ve hello VM kendisini gibi kaynakları bulunmalıdır Hello Azure anahtar kasası içeren hello şifreleme anahtarlarını ve ilişkili işlem aynı bölgede hello.</span><span class="sxs-lookup"><span data-stu-id="786dd-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="786dd-157">Bir Azure anahtar kasası ile oluşturma [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) ve hello anahtar kasası disk şifrelemesi ile kullanılmak üzere etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="786dd-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="786dd-158">İçin benzersiz bir anahtar kasası adı belirtmeniz *keyVaultName* gibi:</span><span class="sxs-lookup"><span data-stu-id="786dd-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="786dd-159">Yazılım veya donanım güvenlik modeli (HSM) koruması kullanarak şifreleme anahtarlarını depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="786dd-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="786dd-160">HSM kullanmanın premium anahtar kasası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="786dd-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="786dd-161">Premium yazılım korumalı anahtarlar depolar standart anahtar kasası yerine anahtar kasası ek maliyet toocreating yoktur.</span><span class="sxs-lookup"><span data-stu-id="786dd-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="786dd-162">toocreate adım önceki hello bir Premium'da anahtar kasası eklemek hello *- Sku "Premium"* parametreleri.</span><span class="sxs-lookup"><span data-stu-id="786dd-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="786dd-163">Standart bir anahtar kasası oluşturduğumuz beri hello aşağıdaki örnek yazılım korumalı anahtarlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="786dd-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="786dd-164">Her iki koruma modelleri için erişim toorequest hello şifreleme anahtarları hello VM toodecrypt hello sanal diskler önyüklendiğinde verilen toobe hello Azure platformu gerekir.</span><span class="sxs-lookup"><span data-stu-id="786dd-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="786dd-165">Anahtar kasası ile bir şifreleme anahtarı oluşturmak [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="786dd-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="786dd-166">Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar *myKey*:</span><span class="sxs-lookup"><span data-stu-id="786dd-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="786dd-167">Azure Active Directory hizmet asıl Hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="786dd-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="786dd-168">Sanal diskler şifrelenmiş veya şifresi olduğunda bir hesabı toohandle hello kimlik doğrulaması ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi belirtin.</span><span class="sxs-lookup"><span data-stu-id="786dd-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="786dd-169">Bu hesabı, bir Azure Active Directory hizmet asıl hello Azure platformu toorequest hello uygun şifreleme anahtarları hello VM adına izin verir.</span><span class="sxs-lookup"><span data-stu-id="786dd-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="786dd-170">Birçok kuruluş Azure Active Directory dizinleri ayrılmış olsa, aboneliğinizde varsayılan Azure Active Directory örneği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="786dd-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="786dd-171">Azure Active Directory ile bir hizmet sorumlusu oluşturma [yeni AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="786dd-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="786dd-172">toospecify güvenli bir parola izleyin hello [parola ilkeleri ve kısıtlamaları Azure Active Directory'de](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="786dd-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="786dd-173">toosuccessfully şifrelemek veya şifresini sanal diskler, anahtar kasasında depolanan hello şifreleme anahtarı üzerindeki izinleri kümesi toopermit hello Azure Active Directory hizmet asıl tooread hello anahtarları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="786dd-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="786dd-174">Anahtar kasası ile üzerindeki izinleri ayarla [kümesi AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span><span class="sxs-lookup"><span data-stu-id="786dd-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="786dd-175">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="786dd-175">Create virtual machine</span></span>
<span data-ttu-id="786dd-176">tootest Merhaba şifreleme işlemi, bir VM oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="786dd-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="786dd-177">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* kullanarak bir *Windows Server 2016 Datacenter* görüntü:</span><span class="sxs-lookup"><span data-stu-id="786dd-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="786dd-178">Sanal makine şifrele</span><span class="sxs-lookup"><span data-stu-id="786dd-178">Encrypt virtual machine</span></span>
<span data-ttu-id="786dd-179">tooencrypt hello sanal diskler, tüm hello önceki bileşenleri birlikte getirin:</span><span class="sxs-lookup"><span data-stu-id="786dd-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="786dd-180">Hello Azure Active Directory hizmet asıl ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="786dd-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="786dd-181">Şifrelenmiş disklerinizi Hello anahtar kasası toostore hello meta verileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="786dd-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="786dd-182">Merhaba şifreleme anahtarları toouse hello gerçek şifreleme ve şifre çözme için belirtin.</span><span class="sxs-lookup"><span data-stu-id="786dd-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="786dd-183">Tooencrypt hello işletim sistemi diski, hello veri diskleri veya tüm isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="786dd-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="786dd-184">VM ile şifrelemek [kümesi AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) hello Azure anahtar kasası anahtar ve Azure Active Directory hizmet asıl kimlik bilgilerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="786dd-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="786dd-185">Merhaba aşağıdaki örnekte tüm hello anahtar bilgilerini alır sonra hello adlı VM şifreler *myVM*:</span><span class="sxs-lookup"><span data-stu-id="786dd-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

<span data-ttu-id="786dd-186">Merhaba komut istemi toocontinue hello VM şifrelemeli kabul edin.</span><span class="sxs-lookup"><span data-stu-id="786dd-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="786dd-187">Merhaba VM hello işlemi sırasında yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="786dd-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="786dd-188">Merhaba şifreleme işlemi tamamlandıktan sonra hello VM yeniden başlattı, hello şifreleme durumuna sahip gözden [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="786dd-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="786dd-189">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="786dd-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="786dd-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="786dd-190">Next steps</span></span>
* <span data-ttu-id="786dd-191">Azure anahtar kasası yönetme hakkında daha fazla bilgi için bkz: [sanal makineler için anahtar kasasını oluşturup](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="786dd-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="786dd-192">Bir şifrelenmiş özel VM tooupload tooAzure, hazırlama gibi disk şifrelemesi hakkında daha fazla bilgi için bkz: [Azure Disk şifrelemesi](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="786dd-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
