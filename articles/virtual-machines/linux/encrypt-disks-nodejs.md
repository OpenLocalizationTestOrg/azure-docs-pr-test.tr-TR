---
title: bir Linux VM hello Azure CLI 1.0 ile aaaEncrypt disklerde | Microsoft Docs
description: "Azure CLI 1.0 ve hello Resource Manager dağıtım modeli kullanarak bir Linux VM tooencrypt disklerde nasıl hello"
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
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="e7b70-103">Hello Azure CLI 1.0 kullanarak bir Linux VM disklerde şifrele</span><span class="sxs-lookup"><span data-stu-id="e7b70-103">Encrypt disks on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="e7b70-104">Geliştirilmiş sanal makine (VM) güvenlik ve uyumluluk için Azure sanal diskleri bekleyen şifrelenebilir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="e7b70-105">Diskleri, bir Azure anahtar kasası güvenli şifreleme anahtarları kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="e7b70-106">Bu şifreleme anahtarları denetlemek ve bunların kullanılması denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7b70-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="e7b70-107">Bu makalede, Azure CLI 1.0 ve hello Resource Manager dağıtım modeli kullanarak bir Linux VM sanal disklerde tooencrypt nasıl hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="e7b70-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 1.0 and hello Resource Manager deployment model.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e7b70-108">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="e7b70-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e7b70-109">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="e7b70-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e7b70-110">[Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="e7b70-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e7b70-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="e7b70-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="e7b70-112">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="e7b70-112">Quick commands</span></span>
<span data-ttu-id="e7b70-113">Tooquickly gerekiyorsa hello görevi, VM'yi sanal disklerde tooencrypt hello bölüm ayrıntıları hello temel aşağıdaki komutları.</span><span class="sxs-lookup"><span data-stu-id="e7b70-113">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="e7b70-114">Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="e7b70-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="e7b70-115">Merhaba gereksinim [en son Azure CLI 1.0](../../xplat-cli-install.md) yüklü ve aşağıdaki gibi hello Resource Manager modunu kullanarak oturum:</span><span class="sxs-lookup"><span data-stu-id="e7b70-115">You need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e7b70-116">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-116">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e7b70-117">Örnek parametre adlarında `myResourceGroup`, `myKeyVault`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e7b70-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="e7b70-118">İlk olarak, Azure aboneliğinizde içinde hello Azure anahtar kasası sağlayıcısı etkinleştirin ve bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7b70-118">First, enable hello Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="e7b70-119">Merhaba aşağıdaki örnekte oluşturur bir kaynak grubu adı `myResourceGroup` hello içinde `WestUS` konumu:</span><span class="sxs-lookup"><span data-stu-id="e7b70-119">hello following example creates a resource group name `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="e7b70-120">Azure anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7b70-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="e7b70-121">Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar kasası `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="e7b70-121">hello following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="e7b70-122">Bir şifreleme anahtarı anahtar kasanızı oluşturmak ve disk şifrelemesi için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="e7b70-123">Merhaba aşağıdaki örnek adlı bir anahtar oluşturur `myKey`:</span><span class="sxs-lookup"><span data-stu-id="e7b70-123">hello following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="e7b70-124">İşleme hello kimlik doğrulama ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi için Azure Active Directory'yi kullanarak bir uç nokta oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7b70-124">Create an endpoint using Azure Active Directory for handling hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="e7b70-125">Merhaba `--home-page` ve `--identifier-uris` gerek kalmaz toobe gerçek yönlendirilebilir adres.</span><span class="sxs-lookup"><span data-stu-id="e7b70-125">hello `--home-page` and `--identifier-uris` do not need toobe actual routable address.</span></span> <span data-ttu-id="e7b70-126">Merhaba yüksek düzeyde güvenlik için istemci gizli yerine parolalar kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e7b70-126">For hello highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="e7b70-127">Hello Azure CLI istemci gizli şu anda oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="e7b70-127">hello Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="e7b70-128">İstemci gizli yalnızca hello Azure portal oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-128">Client secrets can only be generated in hello Azure portal.</span></span> <span data-ttu-id="e7b70-129">Merhaba aşağıdaki örnek adlı bir Azure Active Directory uç nokta oluşturuyor `myAADApp` ve bir parola kullanıyorsa `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="e7b70-129">hello following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="e7b70-130">Kendi parolanızı aşağıdaki gibi belirtin:</span><span class="sxs-lookup"><span data-stu-id="e7b70-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="e7b70-131">Not hello `applicationId` komutu önceki hello hello çıktısını gösterilen.</span><span class="sxs-lookup"><span data-stu-id="e7b70-131">Note hello `applicationId` shown in hello output from hello preceding command.</span></span> <span data-ttu-id="e7b70-132">Bu uygulama kimliği, aşağıdaki adımları hello kullanılır:</span><span class="sxs-lookup"><span data-stu-id="e7b70-132">This application ID is used in hello following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="e7b70-133">VM varolan bir veri diski tooan ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-133">Add a data disk tooan existing VM.</span></span> <span data-ttu-id="e7b70-134">Merhaba aşağıdaki örnek, bir veri diski tooa adlı VM `myVM`:</span><span class="sxs-lookup"><span data-stu-id="e7b70-134">hello following example adds a data disk tooa VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="e7b70-135">Oluşturduğunuz anahtar kasası ve hello anahtarınızı Hello ayrıntılarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-135">Review hello details for your Key Vault and hello key you created.</span></span> <span data-ttu-id="e7b70-136">Anahtar kasası kimliği, URI ve anahtar hello hello son adımda URL.</span><span class="sxs-lookup"><span data-stu-id="e7b70-136">You need hello Key Vault ID, URI, and key URL in hello final step.</span></span> <span data-ttu-id="e7b70-137">Merhaba aşağıdaki örnek hello ayrıntılarını adlı bir anahtar kasası için gözden geçiriyor `myKeyVault` ve adlı anahtar `myKey`:</span><span class="sxs-lookup"><span data-stu-id="e7b70-137">hello following example reviews hello details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="e7b70-138">Disklerinizi gibi kendi parametre adları boyunca girme şifrelemek:</span><span class="sxs-lookup"><span data-stu-id="e7b70-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="e7b70-139">Hello Azure CLI ayrıntılı hataları hello şifreleme işlemi sırasında sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="e7b70-139">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="e7b70-140">Ek sorun giderme bilgileri için inceleyin `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="e7b70-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="e7b70-141">Hello komut önceki birçok değişkeni yok ve kadar göstergesi toowhy hello işlemi başarısız olarak alamayabilirsiniz, tam komut örneği aşağıdaki gibi olur:</span><span class="sxs-lookup"><span data-stu-id="e7b70-141">As hello preceding command has many variables and you may not get much indication as toowhy hello process fails, a complete command example would be as follows:</span></span>

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

<span data-ttu-id="e7b70-142">Son olarak, gözden geçirme hello şifreleme durumu yeniden sanal diskler şimdi şifrelendikten tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="e7b70-142">Finally, review hello encryption status again tooconfirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="e7b70-143">Merhaba aşağıdaki örnek hello durumunu adlı bir VM denetler `myVM` hello içinde `myResourceGroup` kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="e7b70-143">hello following example checks hello status of a VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="e7b70-144">Disk şifrelemesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="e7b70-144">Overview of disk encryption</span></span>
<span data-ttu-id="e7b70-145">Linux sanal makineleri sanal disklerde rest kullanarak şifrelenir [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="e7b70-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="e7b70-146">Azure sanal diskleri şifreleme ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="e7b70-147">Şifreleme anahtarları yazılım koruması'nı kullanarak Azure anahtar kasası içinde depolanır veya içe aktarmak ya da anahtarlarınızı tooFIPS sertifikalı donanım güvenlik modüllerinde (HSM'ler) 140-2 Düzey 2 standartları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e7b70-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="e7b70-148">Bu şifreleme anahtarları denetimin korumak ve kullanımlarını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7b70-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="e7b70-149">Bu şifreleme anahtarlar kullanılan tooencrypt ve sanal diskleri ekli tooyour VM şifresini.</span><span class="sxs-lookup"><span data-stu-id="e7b70-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="e7b70-150">Bir Azure Active Directory uç nokta VM'ler açma ve kapatma gücü gibi bu şifreleme anahtarları verme için güvenli bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7b70-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="e7b70-151">bir VM şifrelemek için hello işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e7b70-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="e7b70-152">Bir şifreleme anahtarının bir Azure anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7b70-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="e7b70-153">Merhaba şifreleme anahtar toobe diskleri şifrelemek için kullanılabilir yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e7b70-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="e7b70-154">tooread hello şifreleme anahtarını hello Azure anahtar kasası, Azure Active Directory'yi kullanarak hello uygun izinlere sahip bir uç nokta oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7b70-154">tooread hello cryptographic key from hello Azure Key Vault, create an endpoint using Azure Active Directory with hello appropriate permissions.</span></span>
4. <span data-ttu-id="e7b70-155">Merhaba komutu tooencrypt hello Azure Active Directory uç noktası ve uygun şifreleme anahtar toobe kullanılan belirtme, sanal diskler gönderin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory endpoint and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="e7b70-156">Hello Azure Active Directory uç nokta Azure anahtar Kasası'hello gereken şifreleme anahtarını ister.</span><span class="sxs-lookup"><span data-stu-id="e7b70-156">hello Azure Active Directory endpoint requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="e7b70-157">Merhaba sanal diskler sağlanan hello şifreleme anahtarı kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="e7b70-158">Destek Hizmetleri ve şifreleme işlemi</span><span class="sxs-lookup"><span data-stu-id="e7b70-158">Supporting services and encryption process</span></span>
<span data-ttu-id="e7b70-159">Disk şifrelemesi ek bileşenler aşağıdaki hello üzerinde dayanır:</span><span class="sxs-lookup"><span data-stu-id="e7b70-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="e7b70-160">**Azure anahtar kasası** -kullanılan toosafeguard şifreleme anahtarları ve gizli anahtarları hello disk şifreleme/şifre çözme işlemi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e7b70-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="e7b70-161">Varsa, mevcut bir Azure anahtar kasası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7b70-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="e7b70-162">Bir anahtar kasası tooencrypting disk toodedicate sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="e7b70-163">tooseparate yönetim sınırlarını ve anahtar görünürlük, ayrılmış bir anahtar kasası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7b70-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="e7b70-164">**Azure Active Directory** - tanıtıcıları hello gerekli şifreleme anahtarlarını güvenli değişimi ve kimlik doğrulaması için istenen eylemler.</span><span class="sxs-lookup"><span data-stu-id="e7b70-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="e7b70-165">Genellikle, uygulamanızı barındırmak için var olan bir Azure Active Directory örneğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7b70-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="e7b70-166">Merhaba uygulama uç noktası hello anahtar kasası için ve sanal makine Hizmetleri toorequest daha fazla bilgi ve hello uygun şifreleme anahtarları verilen.</span><span class="sxs-lookup"><span data-stu-id="e7b70-166">hello application is more of an endpoint for hello Key Vault and Virtual Machine services toorequest and get issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="e7b70-167">Azure Active Directory ile tümleşen gerçek uygulama geliştirme değil.</span><span class="sxs-lookup"><span data-stu-id="e7b70-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="e7b70-168">Gereksinimler ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="e7b70-168">Requirements and limitations</span></span>
<span data-ttu-id="e7b70-169">Desteklenen senaryolar ve disk şifrelemesi için gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="e7b70-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="e7b70-170">Linux sunucusu SKU'ları - Ubuntu ve CentOS, SUSE ve SUSE Linux Enterprise Server (SLES) ve Red Hat Enterprise Linux aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="e7b70-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="e7b70-171">Tüm kaynaklar (örneğin, anahtar kasası, depolama hesabı ve VM) hello olmalıdır aynı Azure bölgesinde ve abonelik.</span><span class="sxs-lookup"><span data-stu-id="e7b70-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="e7b70-172">Standart bir, D, DS, G ve GS serisi VM'ler.</span><span class="sxs-lookup"><span data-stu-id="e7b70-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="e7b70-173">Disk şifrelemesi senaryoları aşağıdaki hello şu anda desteklenmiyor:</span><span class="sxs-lookup"><span data-stu-id="e7b70-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="e7b70-174">Temel katman VM'ler.</span><span class="sxs-lookup"><span data-stu-id="e7b70-174">Basic tier VMs.</span></span>
* <span data-ttu-id="e7b70-175">Merhaba Klasik dağıtım modeli kullanılarak oluşturulan VM'ler.</span><span class="sxs-lookup"><span data-stu-id="e7b70-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="e7b70-176">İşletim sistemi disk şifrelemesi Linux sanal makineleri üzerinde devre dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="e7b70-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="e7b70-177">Şifreleme anahtarlarının zaten şifrelenmiş bir Linux VM Hello güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="e7b70-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-hello-azure-key-vault-and-keys"></a><span data-ttu-id="e7b70-178">Oluşturma Azure anahtar kasası ve anahtarları hello</span><span class="sxs-lookup"><span data-stu-id="e7b70-178">Create hello Azure Key Vault and keys</span></span>
<span data-ttu-id="e7b70-179">toocomplete hello geri kalanında bu kılavuz, gereksinim duyduğunuz hello [en son Azure CLI 1.0](../../xplat-cli-install.md) yüklü ve aşağıdaki gibi hello Resource Manager modunu kullanarak oturum:</span><span class="sxs-lookup"><span data-stu-id="e7b70-179">toocomplete hello remainder of this guide, you need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e7b70-180">Merhaba komut örnekleri tüm örnek parametreleri kendi adları, konum ve anahtar değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-180">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="e7b70-181">Merhaba aşağıdaki örnekleri kullanmak, bir kural `myResourceGroup`, `myKeyVault`, `myAADApp`vb..</span><span class="sxs-lookup"><span data-stu-id="e7b70-181">hello following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="e7b70-182">Merhaba ilk adımı şifreleme anahtarlarınızı toocreate Azure anahtar kasası toostore değil.</span><span class="sxs-lookup"><span data-stu-id="e7b70-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="e7b70-183">Azure anahtar kasası anahtarları, gizli depolayabilir veya toosecurely izin parolalar, uygulama ve hizmetlerinize uygulamadan.</span><span class="sxs-lookup"><span data-stu-id="e7b70-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="e7b70-184">Sanal disk şifrelemesi için anahtar kasası toostore kullanılan tooencrypt bir şifreleme anahtarı kullanın veya sanal diskleri şifresini.</span><span class="sxs-lookup"><span data-stu-id="e7b70-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="e7b70-185">Azure aboneliğinizde Hello Azure anahtar kasası sağlayıcısını etkinleştirin, ardından bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7b70-185">Enable hello Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="e7b70-186">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `WestUS` konumu:</span><span class="sxs-lookup"><span data-stu-id="e7b70-186">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="e7b70-187">depolama ve hello VM kendisini gibi kaynakları bulunmalıdır Hello Azure anahtar kasası içeren hello şifreleme anahtarlarını ve ilişkili işlem aynı bölgede hello.</span><span class="sxs-lookup"><span data-stu-id="e7b70-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="e7b70-188">Merhaba aşağıdaki örnekte oluşturur adlı bir Azure anahtar kasası `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="e7b70-188">hello following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="e7b70-189">Yazılım veya donanım güvenlik modeli (HSM) koruması kullanarak şifreleme anahtarlarını depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7b70-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="e7b70-190">HSM kullanmanın premium anahtar kasası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="e7b70-191">Premium yazılım korumalı anahtarlar depolar standart anahtar kasası yerine anahtar kasası ek maliyet toocreating yoktur.</span><span class="sxs-lookup"><span data-stu-id="e7b70-191">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="e7b70-192">bir ' % s'premium anahtar kasası, adım önceki hello içinde eklemek toocreate `--sku Premium` toohello komutu.</span><span class="sxs-lookup"><span data-stu-id="e7b70-192">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="e7b70-193">Standart bir anahtar kasası oluşturduğumuz beri hello aşağıdaki örnek yazılım korumalı anahtarlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="e7b70-193">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="e7b70-194">Her iki koruma modelleri için erişim toorequest hello şifreleme anahtarları hello VM toodecrypt hello sanal diskler önyüklendiğinde verilen toobe hello Azure platformu gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-194">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="e7b70-195">Bir şifreleme anahtarı, anahtar kasası içinde oluşturun, sonra sanal disk şifrelemesi ile kullanmak için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="e7b70-196">Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar `myKey` ve disk şifrelemesi için sağlar:</span><span class="sxs-lookup"><span data-stu-id="e7b70-196">hello following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a><span data-ttu-id="e7b70-197">Merhaba Azure Active Directory uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7b70-197">Create hello Azure Active Directory application</span></span>
<span data-ttu-id="e7b70-198">Sanal diskler şifrelenmiş veya şifresi, bir uç nokta toohandle hello kimlik doğrulama ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e7b70-198">When virtual disks are encrypted or decrypted, you use an endpoint toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="e7b70-199">Bu uç noktası, bir Azure Active Directory uygulaması hello Azure platformu toorequest hello uygun şifreleme anahtarları hello VM adına izin verir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-199">This endpoint, an Azure Active Directory application, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="e7b70-200">Birçok kuruluş Azure Active Directory dizinleri ayrılmış olsa, aboneliğinizde varsayılan Azure Active Directory örneği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="e7b70-201">Tam bir Azure Active Directory Uygulama oluşturmadığınızı gibi hello `--home-page` ve `--identifier-uris` aşağıdaki örneğine hello parametrelerinde toobe gerçek yönlendirilebilir adres gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="e7b70-201">As you are not creating a full Azure Active Directory application, hello `--home-page` and `--identifier-uris` parameters in hello following example do not need toobe actual routable address.</span></span> <span data-ttu-id="e7b70-202">Merhaba aşağıdaki örnek, ayrıca hello Azure portal oluşturma anahtarları yerine bir parola tabanlı gizlilik belirtir.</span><span class="sxs-lookup"><span data-stu-id="e7b70-202">hello following example also specifies a password-based secret rather than generating keys from within hello Azure portal.</span></span> <span data-ttu-id="e7b70-203">Bu sürede anahtarlar oluşturma hello Azure CLI ' yapılamaz.</span><span class="sxs-lookup"><span data-stu-id="e7b70-203">As this time, generating keys cannot be done from hello Azure CLI.</span></span>

<span data-ttu-id="e7b70-204">Azure Active Directory uygulamanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7b70-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="e7b70-205">Merhaba aşağıdaki örnek adlı bir uygulama oluşturur `myAADApp` ve bir parola kullanıyorsa `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="e7b70-205">hello following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="e7b70-206">Kendi parolanızı aşağıdaki gibi belirtin:</span><span class="sxs-lookup"><span data-stu-id="e7b70-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="e7b70-207">Merhaba Not `applicationId` döndürülen hello çıktısında komutu önceki hello.</span><span class="sxs-lookup"><span data-stu-id="e7b70-207">Make a note of hello `applicationId` that is returned in hello output from hello preceding command.</span></span> <span data-ttu-id="e7b70-208">Bu uygulama kimliği bazı adımları kalan hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e7b70-208">This application ID is used in some of hello remaining steps.</span></span> <span data-ttu-id="e7b70-209">Merhaba uygulaması ortamınızda erişilebilir olmasını sağlayın, ardından, bir hizmet asıl adı (SPN) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7b70-209">Next, create a service principal name (SPN) so that hello application is accessible within your environment.</span></span> <span data-ttu-id="e7b70-210">toosuccessfully şifrelemek veya şifresini sanal diskler, anahtar kasasında depolanan hello şifreleme anahtarı üzerindeki izinleri kümesi toopermit hello Azure Active Directory Uygulama tooread hello anahtarları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e7b70-210">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory application tooread hello keys.</span></span>

<span data-ttu-id="e7b70-211">Merhaba SPN oluşturmak ve hello uygun izinleri aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e7b70-211">Create hello SPN and set hello appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="e7b70-212">Sanal bir disk ekleyin ve şifreleme durumunu gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="e7b70-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="e7b70-213">tooactually bazı sanal diskler şifrelerseniz, VM var olan bir disk tooan eklemek olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7b70-213">tooactually encrypt some virtual disks, lets add a disk tooan existing VM.</span></span> <span data-ttu-id="e7b70-214">VM gibi varolan bir 5 Gb veri diski tooan ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e7b70-214">Add a 5Gb data disk tooan existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="e7b70-215">Merhaba sanal diskleri şu anda şifrelenmez.</span><span class="sxs-lookup"><span data-stu-id="e7b70-215">hello virtual disks are not currently encrypted.</span></span> <span data-ttu-id="e7b70-216">Merhaba, VM geçerli şifreleme durumu aşağıdaki gibi gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="e7b70-216">Review hello current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="e7b70-217">Sanal diskler şifrele</span><span class="sxs-lookup"><span data-stu-id="e7b70-217">Encrypt virtual disks</span></span>
<span data-ttu-id="e7b70-218">toonow şifrelemek hello sanal diskler, tüm hello önceki bileşenleri araya getirin:</span><span class="sxs-lookup"><span data-stu-id="e7b70-218">toonow encrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="e7b70-219">Merhaba Azure Active Directory uygulaması ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-219">Specify hello Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="e7b70-220">Şifrelenmiş disklerinizi Hello anahtar kasası toostore hello meta verileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-220">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="e7b70-221">Merhaba şifreleme anahtarları toouse hello gerçek şifreleme ve şifre çözme için belirtin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-221">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="e7b70-222">Tooencrypt hello işletim sistemi diski, hello veri diskleri veya tüm isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="e7b70-222">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="e7b70-223">Anahtar kasası kimliği URI hello ve ardından URL hello son adımda anahtar, oluşturulan Azure anahtar kasası ve hello anahtarınızı Hello ayrıntılarını gözden olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="e7b70-223">Lets review hello details for your Azure Key Vault and hello key you created, as you need hello Key Vault ID, URI, and then key URL in hello final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="e7b70-224">Merhaba Hello çıktısını kullanarak, sanal disklere şifrelemek `azure keyvault show` ve `azure keyvault key show` gibi komutlar:</span><span class="sxs-lookup"><span data-stu-id="e7b70-224">Encrypt your virtual disks using hello output from hello `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="e7b70-225">Hello yukarıdaki komut sahip birçok değişkenleri olarak hello aşağıdaki hello tam komut başvurusu için bir örnektir:</span><span class="sxs-lookup"><span data-stu-id="e7b70-225">As hello preceding command has many variables, hello following example is hello complete command for reference:</span></span>

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

<span data-ttu-id="e7b70-226">Hello Azure CLI ayrıntılı hataları hello şifreleme işlemi sırasında sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="e7b70-226">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="e7b70-227">Ek sorun giderme bilgileri için inceleyin `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` hello şifreleme VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e7b70-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on hello VM you are encrypting.</span></span>

<span data-ttu-id="e7b70-228">Son olarak, hello şifreleme durumunu gözden geçirmek sağlar yeniden sanal diskler şimdi şifrelendikten tooconfirm:</span><span class="sxs-lookup"><span data-stu-id="e7b70-228">Finally, lets review hello encryption status again tooconfirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="e7b70-229">Ek veri disklerinin ekleme</span><span class="sxs-lookup"><span data-stu-id="e7b70-229">Add additional data disks</span></span>
<span data-ttu-id="e7b70-230">Veri disklerinizi şifrelenmiş sonra daha sonra ek sanal diskler tooyour VM eklemek ve de şifreleme.</span><span class="sxs-lookup"><span data-stu-id="e7b70-230">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="e7b70-231">Merhaba çalıştırdığınızda `azure vm enable-disk-encryption` komutu, hello kullanarak artışı hello dizisi sürümü `--sequence-version` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e7b70-231">When you run hello `azure vm enable-disk-encryption` command, increment hello sequence version using hello `--sequence-version` parameter.</span></span> <span data-ttu-id="e7b70-232">Bu sıra sürüm parametresi tooperform verir üzerinde yinelenen işlemler hello aynı VM.</span><span class="sxs-lookup"><span data-stu-id="e7b70-232">This sequence version parameter allows you tooperform repeated operations on hello same VM.</span></span>

<span data-ttu-id="e7b70-233">Örneğin, ikinci bir sanal disk tooyour VM aşağıdaki şekilde ekleyin olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="e7b70-233">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="e7b70-234">Merhaba ekleyerek bu kez Hello komutu tooencrypt hello sanal diskler, yeniden `--sequence-version` parametre ve artan hello değerini bizim ilk aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e7b70-234">Rerun hello command tooencrypt hello virtual disks, this time adding hello `--sequence-version` parameter, and incrementing hello value from our first run as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="e7b70-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e7b70-235">Next steps</span></span>
* <span data-ttu-id="e7b70-236">Azure anahtar kasası, şifreleme anahtarlarını ve kasa, silme de dahil olmak üzere yönetme hakkında daha fazla bilgi için bkz: [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="e7b70-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="e7b70-237">Bir şifrelenmiş özel VM tooupload tooAzure, hazırlama gibi disk şifrelemesi hakkında daha fazla bilgi için bkz: [Azure Disk şifrelemesi](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="e7b70-237">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
