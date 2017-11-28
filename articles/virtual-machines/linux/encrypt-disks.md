---
title: azure'da bir Linux VM aaaEncrypt disklerde | Microsoft Docs
description: "Nasıl tooencrypt sanal diskler için Artırılmış güvenliği kullanarak bir Linux VM üzerinde Azure CLI 2.0 hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="d605b-103">Nasıl bir Linux VM üzerindeki tooencrypt sanal diskler</span><span class="sxs-lookup"><span data-stu-id="d605b-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="d605b-104">Geliştirilmiş sanal makine (VM) güvenlik ve uyumluluk için Azure sanal diskleri şifrelenebilir.</span><span class="sxs-lookup"><span data-stu-id="d605b-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="d605b-105">Diskleri, bir Azure anahtar kasası güvenli şifreleme anahtarları kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="d605b-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="d605b-106">Bu şifreleme anahtarları denetlemek ve bunların kullanılması denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d605b-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="d605b-107">Bu makalede nasıl tooencrypt sanal diskler kullanarak bir Linux VM üzerinde Azure CLI 2.0 hello ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d605b-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="d605b-108">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d605b-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="d605b-109">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="d605b-109">Quick commands</span></span>
<span data-ttu-id="d605b-110">Tooquickly gerekiyorsa hello görevi, VM'yi sanal disklerde tooencrypt hello bölüm ayrıntıları hello temel aşağıdaki komutları.</span><span class="sxs-lookup"><span data-stu-id="d605b-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="d605b-111">Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="d605b-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="d605b-112">Merhaba son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d605b-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="d605b-113">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d605b-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d605b-114">Örnek parametre adlarında *myResourceGroup*, *myKey*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d605b-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="d605b-115">İlk olarak, Azure aboneliğinizle içinde hello Azure anahtar kasası sağlayıcısını etkinleştir [az sağlayıcı kaydı](/cli/azure/provider#register) ve sahip bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d605b-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d605b-116">Merhaba aşağıdaki örnekte oluşturur bir kaynak grubu adı *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="d605b-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="d605b-117">Bir Azure anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve hello anahtar kasası disk şifrelemesi ile kullanılmak üzere etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d605b-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="d605b-118">İçin benzersiz bir anahtar kasası adı belirtmeniz *keyvault_name* gibi:</span><span class="sxs-lookup"><span data-stu-id="d605b-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="d605b-119">Anahtar kasası ile bir şifreleme anahtarı oluşturmak [az keyvault anahtarı oluşturma](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="d605b-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="d605b-120">Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar *myKey*:</span><span class="sxs-lookup"><span data-stu-id="d605b-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="d605b-121">Azure Active Directory ile kullanarak bir hizmet sorumlusu oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="d605b-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="d605b-122">kimlik doğrulama ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi Hello hizmet asıl tanıtıcıları hello.</span><span class="sxs-lookup"><span data-stu-id="d605b-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="d605b-123">sonraki komutlarını kullanmak için kimliğini ve parolayı hello hizmet sorumlusu için hello değerler aşağıdaki örneğine hello okur:</span><span class="sxs-lookup"><span data-stu-id="d605b-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="d605b-124">Hizmet sorumlusu hello oluşturduğunuzda hello parola yalnızca çıktı.</span><span class="sxs-lookup"><span data-stu-id="d605b-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="d605b-125">İsterseniz, Görünüm ve kayıt parolanızı hello (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="d605b-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="d605b-126">Hizmet asıl adı ile listeleyebilirsiniz [az ad sp listesi](/cli/azure/ad/sp#list) ve belirli bir hizmet asıl ile ilgili ek bilgileri görüntülemek [az ad sp Göster](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="d605b-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="d605b-127">Anahtar kasası ile üzerindeki izinleri ayarla [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="d605b-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="d605b-128">Aşağıdaki örneğine hello hello hizmet asıl kimliği komutu önceki hello sağlanır:</span><span class="sxs-lookup"><span data-stu-id="d605b-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="d605b-129">Bir VM ile oluşturma [az vm oluşturma](/cli/azure/vm#create) ve 5 Gb veri diski ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d605b-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="d605b-130">Disk şifrelemesi yalnızca belirli Market görüntülerini destekler.</span><span class="sxs-lookup"><span data-stu-id="d605b-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="d605b-131">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` kullanarak bir **CentOS 7.2n** görüntü:</span><span class="sxs-lookup"><span data-stu-id="d605b-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="d605b-132">SSH VM tooyour kullanarak hello `publicIpAddress` komutu önceki hello hello çıktıda gösterilen.</span><span class="sxs-lookup"><span data-stu-id="d605b-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="d605b-133">Bir bölüm ve dosya sistemi oluşturun, sonra hello veri diski bağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="d605b-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="d605b-134">Daha fazla bilgi için bkz: [tooa Linux VM toomount hello yeni disk bağlanmak](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="d605b-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="d605b-135">SSH oturumunuzu kapatın.</span><span class="sxs-lookup"><span data-stu-id="d605b-135">Close your SSH session.</span></span>

<span data-ttu-id="d605b-136">VM ile şifrelemek [az vm şifrelemeyi etkinleştirmek](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="d605b-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="d605b-137">Merhaba aşağıdaki örnek kullanır hello `$sp_id` ve `$sp_password` hello önceki değişkenlerinden `ad sp create-for-rbac` komutu:</span><span class="sxs-lookup"><span data-stu-id="d605b-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="d605b-138">Merhaba disk şifreleme işlemi toocomplete için biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="d605b-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="d605b-139">Merhaba işlemine hello durumunu izlemek [az vm şifreleme Göster](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="d605b-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d605b-140">Merhaba durumu **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="d605b-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="d605b-141">Merhaba durum beklemeniz hello işletim sistemi disk raporlar için **VMRestartPending**, VM ile yeniden [az vm yeniden başlatma](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="d605b-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d605b-142">Merhaba disk şifreleme işlemi hello önyükleme işlemi sırasında sonlandırılır, böylece şifrelemeyle yeniden hello durumunu denetleyerek önce birkaç dakika bekleyin **az vm şifreleme Göster**:</span><span class="sxs-lookup"><span data-stu-id="d605b-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d605b-143">Merhaba durum şimdi raporu hello işletim sistemi diski ve veri diski olarak **şifreli**.</span><span class="sxs-lookup"><span data-stu-id="d605b-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="d605b-144">Disk şifrelemesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="d605b-144">Overview of disk encryption</span></span>
<span data-ttu-id="d605b-145">Linux sanal makineleri sanal disklerde rest kullanarak şifrelenir [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="d605b-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="d605b-146">Azure sanal diskleri şifreleme ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="d605b-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="d605b-147">Şifreleme anahtarları yazılım koruması'nı kullanarak Azure anahtar kasası içinde depolanır veya içe aktarmak ya da anahtarlarınızı tooFIPS sertifikalı donanım güvenlik modüllerinde (HSM'ler) 140-2 Düzey 2 standartları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d605b-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="d605b-148">Bu şifreleme anahtarları denetimin korumak ve kullanımlarını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d605b-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="d605b-149">Bu şifreleme anahtarlar kullanılan tooencrypt ve sanal diskleri ekli tooyour VM şifresini.</span><span class="sxs-lookup"><span data-stu-id="d605b-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="d605b-150">Bir Azure Active Directory Hizmet sorumlusu VM'ler açma ve kapatma gücü gibi bu şifreleme anahtarları verme için güvenli bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="d605b-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="d605b-151">bir VM şifrelemek için hello işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d605b-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="d605b-152">Bir şifreleme anahtarının bir Azure anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d605b-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="d605b-153">Merhaba şifreleme anahtar toobe diskleri şifrelemek için kullanılabilir yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="d605b-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="d605b-154">tooread hello şifreleme anahtarını hello Azure anahtar kasası oluşturma bir Azure Active Directory hizmet asıl hello uygun izinlere sahip.</span><span class="sxs-lookup"><span data-stu-id="d605b-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="d605b-155">Merhaba komutu tooencrypt hello Azure Active Directory hizmet asıl ve uygun şifreleme anahtar toobe kullanılan belirtme, sanal diskler gönderin.</span><span class="sxs-lookup"><span data-stu-id="d605b-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="d605b-156">Hello Azure Active Directory hizmet asıl istekleri Azure anahtar kasası gerekli şifreleme anahtarından hello.</span><span class="sxs-lookup"><span data-stu-id="d605b-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="d605b-157">Merhaba sanal diskler sağlanan hello şifreleme anahtarı kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="d605b-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="d605b-158">Şifreleme işlemi</span><span class="sxs-lookup"><span data-stu-id="d605b-158">Encryption process</span></span>
<span data-ttu-id="d605b-159">Disk şifrelemesi ek bileşenler aşağıdaki hello üzerinde dayanır:</span><span class="sxs-lookup"><span data-stu-id="d605b-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="d605b-160">**Azure anahtar kasası** -kullanılan toosafeguard şifreleme anahtarları ve gizli anahtarları hello disk şifreleme/şifre çözme işlemi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d605b-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="d605b-161">Varsa, mevcut bir Azure anahtar kasası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d605b-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="d605b-162">Bir anahtar kasası tooencrypting disk toodedicate sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="d605b-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="d605b-163">tooseparate yönetim sınırlarını ve anahtar görünürlük, ayrılmış bir anahtar kasası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d605b-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="d605b-164">**Azure Active Directory** - tanıtıcıları hello gerekli şifreleme anahtarlarını güvenli değişimi ve kimlik doğrulaması için istenen eylemler.</span><span class="sxs-lookup"><span data-stu-id="d605b-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="d605b-165">Genellikle, uygulamanızı barındırmak için var olan bir Azure Active Directory örneğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d605b-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="d605b-166">Merhaba hizmet sorumlusu hello uygun şifreleme anahtarları verilmesi ve güvenli mekanizması toorequest sağlar.</span><span class="sxs-lookup"><span data-stu-id="d605b-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="d605b-167">Azure Active Directory ile tümleşen gerçek uygulama geliştirme değil.</span><span class="sxs-lookup"><span data-stu-id="d605b-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="d605b-168">Gereksinimler ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="d605b-168">Requirements and limitations</span></span>
<span data-ttu-id="d605b-169">Desteklenen senaryolar ve disk şifrelemesi için gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="d605b-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="d605b-170">Linux sunucusu SKU'ları - Ubuntu ve CentOS, SUSE ve SUSE Linux Enterprise Server (SLES) ve Red Hat Enterprise Linux aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="d605b-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="d605b-171">Tüm kaynaklar (örneğin, anahtar kasası, depolama hesabı ve VM) hello olmalıdır aynı Azure bölgesinde ve abonelik.</span><span class="sxs-lookup"><span data-stu-id="d605b-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="d605b-172">Standart bir, D, DS, G ve GS serisi VM'ler.</span><span class="sxs-lookup"><span data-stu-id="d605b-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="d605b-173">Disk şifrelemesi senaryoları aşağıdaki hello şu anda desteklenmiyor:</span><span class="sxs-lookup"><span data-stu-id="d605b-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="d605b-174">Temel katman VM'ler.</span><span class="sxs-lookup"><span data-stu-id="d605b-174">Basic tier VMs.</span></span>
* <span data-ttu-id="d605b-175">Merhaba Klasik dağıtım modeli kullanılarak oluşturulan VM'ler.</span><span class="sxs-lookup"><span data-stu-id="d605b-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="d605b-176">İşletim sistemi disk şifrelemesi Linux sanal makineleri üzerinde devre dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="d605b-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="d605b-177">Şifreleme anahtarlarının zaten şifrelenmiş bir Linux VM Hello güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="d605b-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="d605b-178">Azure anahtar kasası ve anahtarları oluşturma</span><span class="sxs-lookup"><span data-stu-id="d605b-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="d605b-179">Merhaba son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d605b-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="d605b-180">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d605b-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d605b-181">Örnek parametre adlarında *myResourceGroup*, *myKey*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d605b-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="d605b-182">Merhaba ilk adımı şifreleme anahtarlarınızı toocreate Azure anahtar kasası toostore değil.</span><span class="sxs-lookup"><span data-stu-id="d605b-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="d605b-183">Azure anahtar kasası anahtarları, gizli depolayabilir veya toosecurely izin parolalar, uygulama ve hizmetlerinize uygulamadan.</span><span class="sxs-lookup"><span data-stu-id="d605b-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="d605b-184">Sanal disk şifrelemesi için anahtar kasası toostore kullanılan tooencrypt bir şifreleme anahtarı kullanın veya sanal diskleri şifresini.</span><span class="sxs-lookup"><span data-stu-id="d605b-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="d605b-185">Azure aboneliğinizle içinde Hello Azure anahtar kasası sağlayıcısını etkinleştir [az sağlayıcı kaydı](/cli/azure/provider#register) ve sahip bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d605b-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d605b-186">Merhaba aşağıdaki örnekte oluşturur bir kaynak grubu adı *myResourceGroup* hello içinde `eastus` konumu:</span><span class="sxs-lookup"><span data-stu-id="d605b-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="d605b-187">depolama ve hello VM kendisini gibi kaynakları bulunmalıdır Hello Azure anahtar kasası içeren hello şifreleme anahtarlarını ve ilişkili işlem aynı bölgede hello.</span><span class="sxs-lookup"><span data-stu-id="d605b-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="d605b-188">Bir Azure anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve hello anahtar kasası disk şifrelemesi ile kullanılmak üzere etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d605b-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="d605b-189">İçin benzersiz bir anahtar kasası adı belirtmeniz *keyvault_name* gibi:</span><span class="sxs-lookup"><span data-stu-id="d605b-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="d605b-190">Yazılım veya donanım güvenlik modeli (HSM) koruması kullanarak şifreleme anahtarlarını depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d605b-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="d605b-191">HSM kullanmanın premium anahtar kasası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d605b-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="d605b-192">Premium yazılım korumalı anahtarlar depolar standart anahtar kasası yerine anahtar kasası ek maliyet toocreating yoktur.</span><span class="sxs-lookup"><span data-stu-id="d605b-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="d605b-193">bir ' % s'premium anahtar kasası, adım önceki hello içinde eklemek toocreate `--sku Premium` toohello komutu.</span><span class="sxs-lookup"><span data-stu-id="d605b-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="d605b-194">Standart bir anahtar kasası oluşturduğumuz beri hello aşağıdaki örnek yazılım korumalı anahtarlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="d605b-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="d605b-195">Her iki koruma modelleri için erişim toorequest hello şifreleme anahtarları hello VM toodecrypt hello sanal diskler önyüklendiğinde verilen toobe hello Azure platformu gerekir.</span><span class="sxs-lookup"><span data-stu-id="d605b-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="d605b-196">Anahtar kasası ile bir şifreleme anahtarı oluşturmak [az keyvault anahtarı oluşturma](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="d605b-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="d605b-197">Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar *myKey*:</span><span class="sxs-lookup"><span data-stu-id="d605b-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="d605b-198">Azure Active Directory hizmet asıl Hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="d605b-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="d605b-199">Sanal diskler şifrelenmiş veya şifresi olduğunda bir hesabı toohandle hello kimlik doğrulaması ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi belirtin.</span><span class="sxs-lookup"><span data-stu-id="d605b-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="d605b-200">Bu hesabı, bir Azure Active Directory hizmet asıl hello Azure platformu toorequest hello uygun şifreleme anahtarları hello VM adına izin verir.</span><span class="sxs-lookup"><span data-stu-id="d605b-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="d605b-201">Birçok kuruluş Azure Active Directory dizinleri ayrılmış olsa, aboneliğinizde varsayılan Azure Active Directory örneği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d605b-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="d605b-202">Azure Active Directory ile kullanarak bir hizmet sorumlusu oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="d605b-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="d605b-203">sonraki komutlarını kullanmak için kimliğini ve parolayı hello hizmet sorumlusu için hello değerler aşağıdaki örneğine hello okur:</span><span class="sxs-lookup"><span data-stu-id="d605b-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="d605b-204">Merhaba parola yalnızca hello hizmet sorumlusu oluşturma görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d605b-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="d605b-205">İsterseniz, Görünüm ve kayıt parolanızı hello (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="d605b-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="d605b-206">Hizmet asıl adı ile listeleyebilirsiniz [az ad sp listesi](/cli/azure/ad/sp#list) ve belirli bir hizmet asıl ile ilgili ek bilgileri görüntülemek [az ad sp Göster](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="d605b-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="d605b-207">toosuccessfully şifrelemek veya şifresini sanal diskler, anahtar kasasında depolanan hello şifreleme anahtarı üzerindeki izinleri kümesi toopermit hello Azure Active Directory hizmet asıl tooread hello anahtarları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d605b-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="d605b-208">Anahtar kasası ile üzerindeki izinleri ayarla [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="d605b-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="d605b-209">Aşağıdaki örneğine hello hello hizmet asıl kimliği komutu önceki hello sağlanır:</span><span class="sxs-lookup"><span data-stu-id="d605b-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="d605b-210">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="d605b-210">Create virtual machine</span></span>
<span data-ttu-id="d605b-211">tooactually bazı sanal diskler şifrelerseniz, bir VM oluşturun ve bir veri diski Ekle olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d605b-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="d605b-212">VM tooencrypt ile oluşturma [az vm oluşturma](/cli/azure/vm#create) ve 5 Gb veri diski ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d605b-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="d605b-213">Disk şifrelemesi yalnızca belirli Market görüntülerini destekler.</span><span class="sxs-lookup"><span data-stu-id="d605b-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="d605b-214">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* kullanarak bir **CentOS 7.2n** görüntü:</span><span class="sxs-lookup"><span data-stu-id="d605b-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="d605b-215">SSH VM tooyour kullanarak hello `publicIpAddress` komutu önceki hello hello çıktıda gösterilen.</span><span class="sxs-lookup"><span data-stu-id="d605b-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="d605b-216">Bir bölüm ve dosya sistemi oluşturun, sonra hello veri diski bağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="d605b-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="d605b-217">Daha fazla bilgi için bkz: [tooa Linux VM toomount hello yeni disk bağlanmak](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="d605b-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="d605b-218">SSH oturumunuzu kapatın.</span><span class="sxs-lookup"><span data-stu-id="d605b-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="d605b-219">Sanal makine şifrele</span><span class="sxs-lookup"><span data-stu-id="d605b-219">Encrypt virtual machine</span></span>
<span data-ttu-id="d605b-220">tooencrypt hello sanal diskler, tüm hello önceki bileşenleri birlikte getirin:</span><span class="sxs-lookup"><span data-stu-id="d605b-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="d605b-221">Hello Azure Active Directory hizmet asıl ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="d605b-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="d605b-222">Şifrelenmiş disklerinizi Hello anahtar kasası toostore hello meta verileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="d605b-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="d605b-223">Merhaba şifreleme anahtarları toouse hello gerçek şifreleme ve şifre çözme için belirtin.</span><span class="sxs-lookup"><span data-stu-id="d605b-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="d605b-224">Tooencrypt hello işletim sistemi diski, hello veri diskleri veya tüm isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="d605b-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="d605b-225">VM ile şifrelemek [az vm şifrelemeyi etkinleştirmek](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="d605b-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="d605b-226">Merhaba aşağıdaki örnek kullanır hello `$sp_id` ve `$sp_password` hello önceki değişkenlerinden `ad sp create-for-rbac` komutu:</span><span class="sxs-lookup"><span data-stu-id="d605b-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="d605b-227">Merhaba disk şifreleme işlemi toocomplete için biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="d605b-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="d605b-228">Merhaba işlemine hello durumunu izlemek [az vm şifreleme Göster](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="d605b-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d605b-229">Merhaba, benzer toohello aşağıdaki kesilmiş örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="d605b-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="d605b-230">Merhaba durum beklemeniz hello işletim sistemi disk raporlar için **VMRestartPending**, VM ile yeniden [az vm yeniden başlatma](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="d605b-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d605b-231">Merhaba disk şifreleme işlemi hello önyükleme işlemi sırasında sonlandırılır, böylece şifrelemeyle yeniden hello durumunu denetleyerek önce birkaç dakika bekleyin **az vm şifreleme Göster**:</span><span class="sxs-lookup"><span data-stu-id="d605b-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d605b-232">Merhaba durum şimdi raporu hello işletim sistemi diski ve veri diski olarak **şifreli**.</span><span class="sxs-lookup"><span data-stu-id="d605b-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="d605b-233">Ek veri disklerinin ekleme</span><span class="sxs-lookup"><span data-stu-id="d605b-233">Add additional data disks</span></span>
<span data-ttu-id="d605b-234">Veri disklerinizi şifrelenmiş sonra daha sonra ek sanal diskler tooyour VM eklemek ve de şifreleme.</span><span class="sxs-lookup"><span data-stu-id="d605b-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="d605b-235">Örneğin, ikinci bir sanal disk tooyour VM aşağıdaki şekilde ekleyin olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="d605b-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="d605b-236">Merhaba komutu tooencrypt hello sanal diskler gibi yeniden çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d605b-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a><span data-ttu-id="d605b-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d605b-237">Next steps</span></span>
* <span data-ttu-id="d605b-238">Azure anahtar kasası, şifreleme anahtarlarını ve kasa, silme de dahil olmak üzere yönetme hakkında daha fazla bilgi için bkz: [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="d605b-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="d605b-239">Bir şifrelenmiş özel VM tooupload tooAzure, hazırlama gibi disk şifrelemesi hakkında daha fazla bilgi için bkz: [Azure Disk şifrelemesi](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="d605b-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
