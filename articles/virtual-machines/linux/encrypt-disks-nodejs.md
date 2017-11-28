---
title: "Bir Linux VM Azure CLI 1.0 ile disklerde şifrelemek | Microsoft Docs"
description: "Azure CLI 1.0 ve Resource Manager dağıtım modeli kullanarak bir Linux VM disklerde şifreleme"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: b436f2d43c41000f4385889edb3fa3983d4a8c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="71b8c-103">Azure CLI 1.0 kullanarak bir Linux VM disklerde şifrele</span><span class="sxs-lookup"><span data-stu-id="71b8c-103">Encrypt disks on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="71b8c-104">Geliştirilmiş sanal makine (VM) güvenlik ve uyumluluk için Azure sanal diskleri bekleyen şifrelenebilir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="71b8c-105">Diskleri, bir Azure anahtar kasası güvenli şifreleme anahtarları kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="71b8c-106">Bu şifreleme anahtarları denetlemek ve bunların kullanılması denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71b8c-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="71b8c-107">Bu makalede Azure CLI 1.0 ve Resource Manager dağıtım modeli kullanarak bir Linux VM sanal disklerde şifrelemek nasıl ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 1.0 and the Resource Manager deployment model.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="71b8c-108">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="71b8c-108">CLI versions to complete the task</span></span>
<span data-ttu-id="71b8c-109">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="71b8c-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="71b8c-110">[Azure CLI 1.0](#quick-commands) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="71b8c-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="71b8c-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="71b8c-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="71b8c-112">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="71b8c-112">Quick commands</span></span>
<span data-ttu-id="71b8c-113">VM sanal disklerde şifrelemek için hızlı bir şekilde, aşağıdaki bölümde ayrıntıları temel görevi gerekiyorsa komutları.</span><span class="sxs-lookup"><span data-stu-id="71b8c-113">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="71b8c-114">Her adım, belgenin geri kalanında bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="71b8c-114">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="71b8c-115">Gereksinim duyduğunuz [en son Azure CLI 1.0](../../xplat-cli-install.md) yüklü ve Resource Manager modunu aşağıdaki gibi kullanarak oturum:</span><span class="sxs-lookup"><span data-stu-id="71b8c-115">You need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="71b8c-116">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-116">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="71b8c-117">Örnek parametre adlarında `myResourceGroup`, `myKeyVault`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="71b8c-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="71b8c-118">İlk olarak, Azure aboneliğinizde içinde Azure anahtar kasası Sağlayıcısı'nı etkinleştirin ve bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71b8c-118">First, enable the Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="71b8c-119">Aşağıdaki örnek, bir kaynak grubu adı oluşturur `myResourceGroup` içinde `WestUS` konumu:</span><span class="sxs-lookup"><span data-stu-id="71b8c-119">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="71b8c-120">Azure anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71b8c-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="71b8c-121">Aşağıdaki örnek adlı bir anahtar kasası oluşturur `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="71b8c-121">The following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="71b8c-122">Bir şifreleme anahtarı anahtar kasanızı oluşturmak ve disk şifrelemesi için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="71b8c-123">Aşağıdaki örnek adlı bir anahtar oluşturur `myKey`:</span><span class="sxs-lookup"><span data-stu-id="71b8c-123">The following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="71b8c-124">Kimlik doğrulama işleme ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi için Azure Active Directory'yi kullanarak bir uç nokta oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71b8c-124">Create an endpoint using Azure Active Directory for handling the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="71b8c-125">`--home-page` Ve `--identifier-uris` gerçek yönlendirilebilir adresi olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="71b8c-125">The `--home-page` and `--identifier-uris` do not need to be actual routable address.</span></span> <span data-ttu-id="71b8c-126">Yüksek düzeyde güvenlik için istemci gizli yerine parolalar kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="71b8c-126">For the highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="71b8c-127">Azure CLI istemci gizli şu anda oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="71b8c-127">The Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="71b8c-128">İstemci gizli yalnızca Azure portalında oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-128">Client secrets can only be generated in the Azure portal.</span></span> <span data-ttu-id="71b8c-129">Aşağıdaki örnek adlı bir Azure Active Directory uç nokta oluşturuyor `myAADApp` ve bir parola kullanıyorsa `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="71b8c-129">The following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="71b8c-130">Kendi parolanızı aşağıdaki gibi belirtin:</span><span class="sxs-lookup"><span data-stu-id="71b8c-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="71b8c-131">Not `applicationId` yukarıdaki komut çıktısı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-131">Note the `applicationId` shown in the output from the preceding command.</span></span> <span data-ttu-id="71b8c-132">Bu uygulama kimliği, aşağıdaki adımlarda kullanılır:</span><span class="sxs-lookup"><span data-stu-id="71b8c-132">This application ID is used in the following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="71b8c-133">Bir veri diski için mevcut bir VM'yi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-133">Add a data disk to an existing VM.</span></span> <span data-ttu-id="71b8c-134">Aşağıdaki örnek, adlı VM için bir veri diski ekler `myVM`:</span><span class="sxs-lookup"><span data-stu-id="71b8c-134">The following example adds a data disk to a VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="71b8c-135">Anahtar kasası ve oluşturduğunuz anahtarı için ayrıntıları inceleyin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-135">Review the details for your Key Vault and the key you created.</span></span> <span data-ttu-id="71b8c-136">Anahtar kasası kimliği, URI ve anahtar gerek son adımda URL.</span><span class="sxs-lookup"><span data-stu-id="71b8c-136">You need the Key Vault ID, URI, and key URL in the final step.</span></span> <span data-ttu-id="71b8c-137">Aşağıdaki örnek ayrıntıları adlı bir anahtar kasası için incelemeleri `myKeyVault` ve adlı anahtar `myKey`:</span><span class="sxs-lookup"><span data-stu-id="71b8c-137">The following example reviews the details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="71b8c-138">Disklerinizi gibi kendi parametre adları boyunca girme şifrelemek:</span><span class="sxs-lookup"><span data-stu-id="71b8c-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="71b8c-139">Azure CLI ayrıntılı hataları şifreleme işlemi sırasında sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="71b8c-139">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="71b8c-140">Ek sorun giderme bilgileri için inceleyin `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="71b8c-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="71b8c-141">Yukarıdaki komut birçok değişkeni yok ve işlem neden başarısız konusunda kadar göstergesi alamayabilirsiniz gibi tam komut örneği aşağıdaki gibi olur:</span><span class="sxs-lookup"><span data-stu-id="71b8c-141">As the preceding command has many variables and you may not get much indication as to why the process fails, a complete command example would be as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="71b8c-142">Son olarak, sanal diskler artık şifrelenmiş olduğunu onaylamak için yeniden şifreleme durumunu gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-142">Finally, review the encryption status again to confirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="71b8c-143">Aşağıdaki örnek adlı bir VM'den durumunu denetler `myVM` içinde `myResourceGroup` kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="71b8c-143">The following example checks the status of a VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="71b8c-144">Disk şifrelemesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="71b8c-144">Overview of disk encryption</span></span>
<span data-ttu-id="71b8c-145">Linux sanal makineleri sanal disklerde rest kullanarak şifrelenir [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="71b8c-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="71b8c-146">Azure sanal diskleri şifreleme ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="71b8c-147">Şifreleme anahtarları yazılım koruması'nı kullanarak Azure anahtar kasası içinde depolanır veya içe aktarmak ya da anahtarlarınızı FIPS 140-2 Düzey 2 standartları sertifikalı donanım güvenlik modüllerinde (HSM'ler) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="71b8c-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="71b8c-148">Bu şifreleme anahtarları denetimin korumak ve kullanımlarını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71b8c-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="71b8c-149">Bu şifreleme anahtarlarını şifrelemek ve şifresini çözmek, VM'ye bağlı sanal diskler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="71b8c-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="71b8c-150">Bir Azure Active Directory uç nokta VM'ler açma ve kapatma gücü gibi bu şifreleme anahtarları verme için güvenli bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="71b8c-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="71b8c-151">Bir VM şifreleme işlemi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="71b8c-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="71b8c-152">Bir şifreleme anahtarının bir Azure anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71b8c-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="71b8c-153">Diskleri şifrelemek için kullanılabilmesi için şifreleme anahtarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="71b8c-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="71b8c-154">Şifreleme anahtarı Azure anahtar Kasası'okumak için Azure Active Directory'yi kullanarak uygun izinlere sahip bir uç nokta oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71b8c-154">To read the cryptographic key from the Azure Key Vault, create an endpoint using Azure Active Directory with the appropriate permissions.</span></span>
4. <span data-ttu-id="71b8c-155">Kullanılacak uygun şifreleme anahtarını ve Azure Active Directory uç noktası belirterek, sanal diskler şifrelemek için komutu yürütün.</span><span class="sxs-lookup"><span data-stu-id="71b8c-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory endpoint and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="71b8c-156">Azure Active Directory uç nokta gereken şifreleme anahtarını Azure anahtar Kasası'ister.</span><span class="sxs-lookup"><span data-stu-id="71b8c-156">The Azure Active Directory endpoint requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="71b8c-157">Sanal diskler sağlanan şifreleme anahtarı kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="71b8c-158">Destek Hizmetleri ve şifreleme işlemi</span><span class="sxs-lookup"><span data-stu-id="71b8c-158">Supporting services and encryption process</span></span>
<span data-ttu-id="71b8c-159">Disk şifrelemesi aşağıdaki ek bileşenlerini dayanır:</span><span class="sxs-lookup"><span data-stu-id="71b8c-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="71b8c-160">**Azure anahtar kasası** - şifreleme anahtarları ve gizli anahtarları disk şifreleme/şifre çözme işlemi için kullanılan korumak için kullanılan.</span><span class="sxs-lookup"><span data-stu-id="71b8c-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="71b8c-161">Varsa, mevcut bir Azure anahtar kasası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71b8c-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="71b8c-162">Diskleri şifrelemek için bir anahtar kasası ayrılması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="71b8c-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="71b8c-163">Yönetim sınırlarını ve anahtar görünürlük ayırmak için ayrılmış bir anahtar kasası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71b8c-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="71b8c-164">**Azure Active Directory** -güvenli değişimi gerekli şifreleme anahtarlarını ve kimlik doğrulaması istenen eylemler için işler.</span><span class="sxs-lookup"><span data-stu-id="71b8c-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="71b8c-165">Genellikle, uygulamanızı barındırmak için var olan bir Azure Active Directory örneğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71b8c-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="71b8c-166">Daha fazla istemek ve uygun şifreleme anahtarları verilen anahtar kasası ve sanal makine Hizmetleri için bir uç nokta uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="71b8c-166">The application is more of an endpoint for the Key Vault and Virtual Machine services to request and get issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="71b8c-167">Azure Active Directory ile tümleşen gerçek uygulama geliştirme değil.</span><span class="sxs-lookup"><span data-stu-id="71b8c-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="71b8c-168">Gereksinimler ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="71b8c-168">Requirements and limitations</span></span>
<span data-ttu-id="71b8c-169">Desteklenen senaryolar ve disk şifrelemesi için gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="71b8c-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="71b8c-170">Aşağıdaki Linux sunucusu SKU'ları - Ubuntu ve CentOS, SUSE ve SUSE Linux Enterprise Server (SLES) ve Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="71b8c-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="71b8c-171">Tüm kaynaklar (örneğin, anahtar kasası, depolama hesabı ve VM) aynı Azure bölgesinde ve abonelik olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="71b8c-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="71b8c-172">Standart bir, D, DS, G ve GS serisi VM'ler.</span><span class="sxs-lookup"><span data-stu-id="71b8c-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="71b8c-173">Disk şifrelemesi aşağıdaki senaryolarda şu anda desteklenmiyor:</span><span class="sxs-lookup"><span data-stu-id="71b8c-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="71b8c-174">Temel katman VM'ler.</span><span class="sxs-lookup"><span data-stu-id="71b8c-174">Basic tier VMs.</span></span>
* <span data-ttu-id="71b8c-175">Klasik dağıtım modeli kullanılarak oluşturulan VM'ler.</span><span class="sxs-lookup"><span data-stu-id="71b8c-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="71b8c-176">İşletim sistemi disk şifrelemesi Linux sanal makineleri üzerinde devre dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="71b8c-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="71b8c-177">Zaten şifrelenmiş bir Linux VM üzerinde şifreleme anahtarlarını güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="71b8c-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-the-azure-key-vault-and-keys"></a><span data-ttu-id="71b8c-178">Azure anahtar kasası ve anahtarları oluşturma</span><span class="sxs-lookup"><span data-stu-id="71b8c-178">Create the Azure Key Vault and keys</span></span>
<span data-ttu-id="71b8c-179">Bu kılavuz kalanını tamamlamak için ihtiyacınız [en son Azure CLI 1.0](../../xplat-cli-install.md) yüklü ve Resource Manager modunu aşağıdaki gibi kullanarak oturum:</span><span class="sxs-lookup"><span data-stu-id="71b8c-179">To complete the remainder of this guide, you need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="71b8c-180">Komut örnekleri tüm örnek parametreleri kendi adları, konum ve anahtar değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-180">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="71b8c-181">Aşağıdaki örnekler, bir kuralı kullanmak `myResourceGroup`, `myKeyVault`, `myAADApp`vb..</span><span class="sxs-lookup"><span data-stu-id="71b8c-181">The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="71b8c-182">İlk adım, şifreleme anahtarlarını depolamak için bir Azure anahtar kasası oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="71b8c-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="71b8c-183">Azure anahtar kasası anahtarları, gizli ya da, uygulama ve hizmetlerinize güvenli bir şekilde uygulamak izin parolaları depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71b8c-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="71b8c-184">Sanal disk şifreleme için şifreleme veya şifrelerini çözme, sanal diskler için kullanılan bir şifreleme anahtarı depolamak için anahtar kasası kullanın.</span><span class="sxs-lookup"><span data-stu-id="71b8c-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="71b8c-185">Azure aboneliğinizde Azure anahtar kasası sağlayıcısını etkinleştirin, ardından bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71b8c-185">Enable the Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="71b8c-186">Aşağıdaki örnek, bir kaynak grubu oluşturur `myResourceGroup` içinde `WestUS` konumu:</span><span class="sxs-lookup"><span data-stu-id="71b8c-186">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="71b8c-187">Şifreleme anahtarlarını ve depolama ve VM gibi ilişkili işlem kaynakları içeren Azure anahtar kasası aynı bölgede bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="71b8c-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="71b8c-188">Aşağıdaki örnek, bir Azure anahtar kasası adlı oluşturur `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="71b8c-188">The following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="71b8c-189">Yazılım veya donanım güvenlik modeli (HSM) koruması kullanarak şifreleme anahtarlarını depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71b8c-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="71b8c-190">HSM kullanmanın premium anahtar kasası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="71b8c-191">Premium yazılım korumalı anahtarlar depolar standart anahtar kasası yerine anahtar kasası oluşturmak için ek bir maliyet yoktur.</span><span class="sxs-lookup"><span data-stu-id="71b8c-191">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="71b8c-192">Premium anahtar kasası oluşturmak için önceki adımda ekleyin `--sku Premium` komutu.</span><span class="sxs-lookup"><span data-stu-id="71b8c-192">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="71b8c-193">Aşağıdaki örnek, standart bir anahtar kasası oluşturduğumuz bu yana yazılım korumalı anahtarlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="71b8c-193">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="71b8c-194">Her iki koruma modeli için Azure platformu VM sanal diskleri şifresini çözmek için önyüklendiğinde şifreleme anahtarları istemek için erişim verilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-194">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="71b8c-195">Bir şifreleme anahtarı, anahtar kasası içinde oluşturun, sonra sanal disk şifrelemesi ile kullanmak için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="71b8c-196">Aşağıdaki örnek adlı bir anahtar oluşturur `myKey` ve disk şifrelemesi için sağlar:</span><span class="sxs-lookup"><span data-stu-id="71b8c-196">The following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-the-azure-active-directory-application"></a><span data-ttu-id="71b8c-197">Azure Active Directory uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="71b8c-197">Create the Azure Active Directory application</span></span>
<span data-ttu-id="71b8c-198">Sanal diskler şifrelenmiş veya şifresi, kimlik doğrulama ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi işlemek için bir uç nokta kullanın.</span><span class="sxs-lookup"><span data-stu-id="71b8c-198">When virtual disks are encrypted or decrypted, you use an endpoint to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="71b8c-199">Bu uç noktası, bir Azure Active Directory uygulaması VM adına uygun şifreleme anahtarları istemek Azure platformu sağlar.</span><span class="sxs-lookup"><span data-stu-id="71b8c-199">This endpoint, an Azure Active Directory application, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="71b8c-200">Birçok kuruluş Azure Active Directory dizinleri ayrılmış olsa, aboneliğinizde varsayılan Azure Active Directory örneği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="71b8c-201">Tam bir Azure Active Directory Uygulama oluşturmadığınızı gibi `--home-page` ve `--identifier-uris` parametreleri aşağıdaki örnekte gerçek yönlendirilebilir adresi olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="71b8c-201">As you are not creating a full Azure Active Directory application, the `--home-page` and `--identifier-uris` parameters in the following example do not need to be actual routable address.</span></span> <span data-ttu-id="71b8c-202">Aşağıdaki örnek, ayrıca Azure portal oluşturma anahtarları yerine bir parola tabanlı gizlilik belirtir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-202">The following example also specifies a password-based secret rather than generating keys from within the Azure portal.</span></span> <span data-ttu-id="71b8c-203">Bu sürede anahtarlar oluşturma Azure CLI üzerinden yapılamaz.</span><span class="sxs-lookup"><span data-stu-id="71b8c-203">As this time, generating keys cannot be done from the Azure CLI.</span></span>

<span data-ttu-id="71b8c-204">Azure Active Directory uygulamanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71b8c-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="71b8c-205">Aşağıdaki örnek adlı bir uygulama oluşturur `myAADApp` ve bir parola kullanıyorsa `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="71b8c-205">The following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="71b8c-206">Kendi parolanızı aşağıdaki gibi belirtin:</span><span class="sxs-lookup"><span data-stu-id="71b8c-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="71b8c-207">Not `applicationId` döndürülen çıktıda önceki komutu.</span><span class="sxs-lookup"><span data-stu-id="71b8c-207">Make a note of the `applicationId` that is returned in the output from the preceding command.</span></span> <span data-ttu-id="71b8c-208">Bu uygulama kimliği kalan adımları bazıları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="71b8c-208">This application ID is used in some of the remaining steps.</span></span> <span data-ttu-id="71b8c-209">Ardından, uygulama ortamınızda erişilebilir olmasını sağlamak bir hizmet asıl adı (SPN) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="71b8c-209">Next, create a service principal name (SPN) so that the application is accessible within your environment.</span></span> <span data-ttu-id="71b8c-210">Başarılı bir şekilde şifrelemek veya sanal diskleri şifresini çözmek için anahtar kasasında depolanan şifreleme anahtarı üzerindeki izinleri anahtarları okumak için Azure Active Directory Uygulama izin verecek şekilde ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71b8c-210">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory application to read the keys.</span></span>

<span data-ttu-id="71b8c-211">SPN oluşturmak ve uygun izinleri aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="71b8c-211">Create the SPN and set the appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="71b8c-212">Sanal bir disk ekleyin ve şifreleme durumunu gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="71b8c-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="71b8c-213">Bazı sanal diskler gerçekte şifrelemek için bir disk eklemek için mevcut bir VM'yi olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="71b8c-213">To actually encrypt some virtual disks, lets add a disk to an existing VM.</span></span> <span data-ttu-id="71b8c-214">5 Gb veri diski için mevcut bir VM'yi aşağıdaki şekilde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="71b8c-214">Add a 5Gb data disk to an existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="71b8c-215">Sanal diskleri şu anda şifrelenmez.</span><span class="sxs-lookup"><span data-stu-id="71b8c-215">The virtual disks are not currently encrypted.</span></span> <span data-ttu-id="71b8c-216">VM geçerli şifreleme durumunu aşağıdaki gibi gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="71b8c-216">Review the current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="71b8c-217">Sanal diskler şifrele</span><span class="sxs-lookup"><span data-stu-id="71b8c-217">Encrypt virtual disks</span></span>
<span data-ttu-id="71b8c-218">Şimdi sanal diskleri şifrelemek için birlikte tüm önceki bileşenleri getirin:</span><span class="sxs-lookup"><span data-stu-id="71b8c-218">To now encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="71b8c-219">Azure Active Directory uygulaması ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-219">Specify the Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="71b8c-220">Şifrelenmiş diskleriniz için meta verileri depolamak için anahtar kasası belirtin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-220">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="71b8c-221">Gerçek şifreleme ve şifre çözme için kullanılacak şifreleme anahtarları belirtin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-221">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="71b8c-222">İşletim sistemi diski, veri diskleri veya tüm şifrelemek isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="71b8c-222">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="71b8c-223">Azure anahtar kasası ve URI, anahtar kasası kimliği gerekir ve ardından son adım URL anahtar olarak, oluşturulan anahtarın ayrıntıları incelemenizi sağlar:</span><span class="sxs-lookup"><span data-stu-id="71b8c-223">Lets review the details for your Azure Key Vault and the key you created, as you need the Key Vault ID, URI, and then key URL in the final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="71b8c-224">Çıktısını kullanarak, sanal disklere şifrelemek `azure keyvault show` ve `azure keyvault key show` gibi komutlar:</span><span class="sxs-lookup"><span data-stu-id="71b8c-224">Encrypt your virtual disks using the output from the `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="71b8c-225">Yukarıdaki komut birçok değişken taşıdığından, tam komut başvurusu için aşağıdaki örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="71b8c-225">As the preceding command has many variables, the following example is the complete command for reference:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="71b8c-226">Azure CLI ayrıntılı hataları şifreleme işlemi sırasında sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="71b8c-226">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="71b8c-227">Ek sorun giderme bilgileri için inceleyin `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` şifreleme VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="71b8c-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on the VM you are encrypting.</span></span>

<span data-ttu-id="71b8c-228">Son olarak, sanal diskler artık şifrelenmiş olduğunu onaylamak için yeniden şifreleme durumunu gözden olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="71b8c-228">Finally, lets review the encryption status again to confirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="71b8c-229">Ek veri disklerinin ekleme</span><span class="sxs-lookup"><span data-stu-id="71b8c-229">Add additional data disks</span></span>
<span data-ttu-id="71b8c-230">Veri disklerinizi şifrelenmiş sonra daha sonra ek sanal diskleri VM'nize eklemek ve de şifreleme.</span><span class="sxs-lookup"><span data-stu-id="71b8c-230">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="71b8c-231">Çalıştırdığınızda `azure vm enable-disk-encryption` komutu, dizisi sürümü kullanılarak Artır `--sequence-version` parametresi.</span><span class="sxs-lookup"><span data-stu-id="71b8c-231">When you run the `azure vm enable-disk-encryption` command, increment the sequence version using the `--sequence-version` parameter.</span></span> <span data-ttu-id="71b8c-232">Bu sıra sürüm parametresi aynı VM üzerinde yinelenen işlemler gerçekleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="71b8c-232">This sequence version parameter allows you to perform repeated operations on the same VM.</span></span>

<span data-ttu-id="71b8c-233">Örneğin, ikinci bir sanal disk VM'nize aşağıdaki şekilde ekleyin olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="71b8c-233">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="71b8c-234">Sanal diskler şifrelemek için komutu yeniden çalıştırın bu zaman ekleme `--sequence-version` parametresi ve değeri bizim ilk çalıştırma gibi artırma:</span><span class="sxs-lookup"><span data-stu-id="71b8c-234">Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="71b8c-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="71b8c-235">Next steps</span></span>
* <span data-ttu-id="71b8c-236">Azure anahtar kasası, şifreleme anahtarlarını ve kasa, silme de dahil olmak üzere yönetme hakkında daha fazla bilgi için bkz: [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="71b8c-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="71b8c-237">Azure için karşıya yüklemek için şifrelenmiş bir özel VM hazırlama gibi disk şifrelemesi hakkında daha fazla bilgi için bkz: [Azure Disk şifrelemesi](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="71b8c-237">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
