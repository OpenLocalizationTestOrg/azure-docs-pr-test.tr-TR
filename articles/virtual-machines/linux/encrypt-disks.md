---
title: "Azure'da bir Linux VM disklerde şifrelemek | Microsoft Docs"
description: "Bir Linux VM için Gelişmiş Güvenlik Azure CLI 2.0 kullanan sanal disklerde şifreleme"
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
ms.openlocfilehash: 172b4c8f5c098d776cb689543f5d8f163b8895b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="fe184-103">Bir Linux VM sanal disklerde şifreleme</span><span class="sxs-lookup"><span data-stu-id="fe184-103">How to encrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="fe184-104">Geliştirilmiş sanal makine (VM) güvenlik ve uyumluluk için Azure sanal diskleri şifrelenebilir.</span><span class="sxs-lookup"><span data-stu-id="fe184-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="fe184-105">Diskleri, bir Azure anahtar kasası güvenli şifreleme anahtarları kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="fe184-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="fe184-106">Bu şifreleme anahtarları denetlemek ve bunların kullanılması denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe184-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="fe184-107">Bu makalede Azure CLI 2.0 kullanarak bir Linux VM sanal disklerde şifrelemek nasıl ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="fe184-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 2.0.</span></span> <span data-ttu-id="fe184-108">Bu adımları [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ile de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe184-108">You can also perform these steps with the [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="fe184-109">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="fe184-109">Quick commands</span></span>
<span data-ttu-id="fe184-110">VM sanal disklerde şifrelemek için hızlı bir şekilde, aşağıdaki bölümde ayrıntıları temel görevi gerekiyorsa komutları.</span><span class="sxs-lookup"><span data-stu-id="fe184-110">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="fe184-111">Her adım, belgenin geri kalanında bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="fe184-111">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="fe184-112">En son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve bir Azure hesabı kullanarak oturum açmış [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fe184-112">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="fe184-113">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fe184-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="fe184-114">Örnek parametre adlarında *myResourceGroup*, *myKey*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="fe184-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="fe184-115">İlk olarak, Azure aboneliğinizle içinde Azure anahtar kasası sağlayıcısını etkinleştir [az sağlayıcı kaydı](/cli/azure/provider#register) ve sahip bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fe184-115">First, enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fe184-116">Aşağıdaki örnek, bir kaynak grubu adı oluşturur *myResourceGroup* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="fe184-116">The following example creates a resource group name *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="fe184-117">Bir Azure anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve anahtar kasası disk şifrelemesi ile kullanmak için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fe184-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="fe184-118">İçin benzersiz bir anahtar kasası adı belirtmeniz *keyvault_name* gibi:</span><span class="sxs-lookup"><span data-stu-id="fe184-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="fe184-119">Anahtar kasası ile bir şifreleme anahtarı oluşturmak [az keyvault anahtarı oluşturma](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="fe184-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="fe184-120">Aşağıdaki örnek adlı bir anahtar oluşturur *myKey*:</span><span class="sxs-lookup"><span data-stu-id="fe184-120">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="fe184-121">Azure Active Directory ile kullanarak bir hizmet sorumlusu oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="fe184-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="fe184-122">Hizmet sorumlusu kimlik doğrulama ve şifreleme anahtarlarının anahtar Kasası'ndan exchange işler.</span><span class="sxs-lookup"><span data-stu-id="fe184-122">The service principal handles the authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="fe184-123">Aşağıdaki örnek değerler kimliği ve parolası sonraki komutlarını kullanmak için hizmet sorumlusu için okur:</span><span class="sxs-lookup"><span data-stu-id="fe184-123">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="fe184-124">Hizmet sorumlusu oluşturduğunuzda parola yalnızca çıktı.</span><span class="sxs-lookup"><span data-stu-id="fe184-124">The password is only output when you create the service principal.</span></span> <span data-ttu-id="fe184-125">İsterseniz, görüntüleyin ve parola kaydı (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="fe184-125">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="fe184-126">Hizmet asıl adı ile listeleyebilirsiniz [az ad sp listesi](/cli/azure/ad/sp#list) ve belirli bir hizmet asıl ile ilgili ek bilgileri görüntülemek [az ad sp Göster](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="fe184-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="fe184-127">Anahtar kasası ile üzerindeki izinleri ayarla [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="fe184-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="fe184-128">Aşağıdaki örnekte, hizmet asıl kimliği önceki komuttan sağlanır:</span><span class="sxs-lookup"><span data-stu-id="fe184-128">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="fe184-129">Bir VM ile oluşturma [az vm oluşturma](/cli/azure/vm#create) ve 5 Gb veri diski ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fe184-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="fe184-130">Disk şifrelemesi yalnızca belirli Market görüntülerini destekler.</span><span class="sxs-lookup"><span data-stu-id="fe184-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="fe184-131">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur `myVM` kullanarak bir **CentOS 7.2n** görüntü:</span><span class="sxs-lookup"><span data-stu-id="fe184-131">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="fe184-132">VM kullanarak SSH `publicIpAddress` yukarıdaki komut çıktısında gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fe184-132">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="fe184-133">Bir bölüm ve dosya sistemi oluşturun, sonra veri diski bağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="fe184-133">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="fe184-134">Daha fazla bilgi için bkz: [yeni disk bağlamak için bir Linux VM Bağlan](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="fe184-134">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="fe184-135">SSH oturumunuzu kapatın.</span><span class="sxs-lookup"><span data-stu-id="fe184-135">Close your SSH session.</span></span>

<span data-ttu-id="fe184-136">VM ile şifrelemek [az vm şifrelemeyi etkinleştirmek](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="fe184-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="fe184-137">Aşağıdaki örnek kullanır `$sp_id` ve `$sp_password` önceki değişkenleri `ad sp create-for-rbac` komutu:</span><span class="sxs-lookup"><span data-stu-id="fe184-137">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="fe184-138">Disk şifrelemesi işlemin tamamlanması biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="fe184-138">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="fe184-139">İşlem durumunu izleme [az vm şifreleme Göster](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="fe184-139">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe184-140">Durum gösterir **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="fe184-140">The status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="fe184-141">Disk işletim sistemi durumu raporları bekleyin **VMRestartPending**, VM ile yeniden [az vm yeniden başlatma](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="fe184-141">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe184-142">Önyükleme işlemi sırasında disk şifreleme işlemi sonlandırılır, böylece yeniden şifreleme durumunu denetleyerek önce birkaç dakika bekleyin **az vm şifreleme Göster**:</span><span class="sxs-lookup"><span data-stu-id="fe184-142">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe184-143">Durum artık işletim sistemi diski ve veri diski olarak bildirmelisiniz **şifreli**.</span><span class="sxs-lookup"><span data-stu-id="fe184-143">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="fe184-144">Disk şifrelemesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="fe184-144">Overview of disk encryption</span></span>
<span data-ttu-id="fe184-145">Linux sanal makineleri sanal disklerde rest kullanarak şifrelenir [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="fe184-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="fe184-146">Azure sanal diskleri şifreleme ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="fe184-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="fe184-147">Şifreleme anahtarları yazılım koruması'nı kullanarak Azure anahtar kasası içinde depolanır veya içe aktarmak ya da anahtarlarınızı FIPS 140-2 Düzey 2 standartları sertifikalı donanım güvenlik modüllerinde (HSM'ler) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fe184-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="fe184-148">Bu şifreleme anahtarları denetimin korumak ve kullanımlarını denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe184-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="fe184-149">Bu şifreleme anahtarlarını şifrelemek ve şifresini çözmek, VM'ye bağlı sanal diskler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fe184-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="fe184-150">Bir Azure Active Directory Hizmet sorumlusu VM'ler açma ve kapatma gücü gibi bu şifreleme anahtarları verme için güvenli bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe184-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="fe184-151">Bir VM şifreleme işlemi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="fe184-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="fe184-152">Bir şifreleme anahtarının bir Azure anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fe184-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="fe184-153">Diskleri şifrelemek için kullanılabilmesi için şifreleme anahtarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fe184-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="fe184-154">Şifreleme anahtarı Azure anahtar Kasası'okumak için bir Azure Active Directory hizmet asıl uygun izinlerle birlikte oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fe184-154">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="fe184-155">Kullanılacak Azure Active Directory hizmet asıl ve uygun şifreleme anahtarını belirterek, sanal diskler şifrelemek için komutu yürütün.</span><span class="sxs-lookup"><span data-stu-id="fe184-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="fe184-156">Azure Active Directory hizmet asıl gereken şifreleme anahtarını Azure anahtar Kasası'ister.</span><span class="sxs-lookup"><span data-stu-id="fe184-156">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="fe184-157">Sanal diskler sağlanan şifreleme anahtarı kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="fe184-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="fe184-158">Şifreleme işlemi</span><span class="sxs-lookup"><span data-stu-id="fe184-158">Encryption process</span></span>
<span data-ttu-id="fe184-159">Disk şifrelemesi aşağıdaki ek bileşenlerini dayanır:</span><span class="sxs-lookup"><span data-stu-id="fe184-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="fe184-160">**Azure anahtar kasası** - şifreleme anahtarları ve gizli anahtarları disk şifreleme/şifre çözme işlemi için kullanılan korumak için kullanılan.</span><span class="sxs-lookup"><span data-stu-id="fe184-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="fe184-161">Varsa, mevcut bir Azure anahtar kasası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe184-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="fe184-162">Diskleri şifrelemek için bir anahtar kasası ayrılması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="fe184-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="fe184-163">Yönetim sınırlarını ve anahtar görünürlük ayırmak için ayrılmış bir anahtar kasası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe184-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="fe184-164">**Azure Active Directory** -güvenli değişimi gerekli şifreleme anahtarlarını ve kimlik doğrulaması istenen eylemler için işler.</span><span class="sxs-lookup"><span data-stu-id="fe184-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="fe184-165">Genellikle, uygulamanızı barındırmak için var olan bir Azure Active Directory örneğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe184-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="fe184-166">Hizmet sorumlusu istemek ve uygun şifreleme anahtarları verilmesi için güvenli bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe184-166">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="fe184-167">Azure Active Directory ile tümleşen gerçek uygulama geliştirme değil.</span><span class="sxs-lookup"><span data-stu-id="fe184-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="fe184-168">Gereksinimler ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="fe184-168">Requirements and limitations</span></span>
<span data-ttu-id="fe184-169">Desteklenen senaryolar ve disk şifrelemesi için gereksinimleri:</span><span class="sxs-lookup"><span data-stu-id="fe184-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="fe184-170">Aşağıdaki Linux sunucusu SKU'ları - Ubuntu ve CentOS, SUSE ve SUSE Linux Enterprise Server (SLES) ve Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="fe184-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="fe184-171">Tüm kaynaklar (örneğin, anahtar kasası, depolama hesabı ve VM) aynı Azure bölgesinde ve abonelik olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fe184-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="fe184-172">Standart bir, D, DS, G ve GS serisi VM'ler.</span><span class="sxs-lookup"><span data-stu-id="fe184-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="fe184-173">Disk şifrelemesi aşağıdaki senaryolarda şu anda desteklenmiyor:</span><span class="sxs-lookup"><span data-stu-id="fe184-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="fe184-174">Temel katman VM'ler.</span><span class="sxs-lookup"><span data-stu-id="fe184-174">Basic tier VMs.</span></span>
* <span data-ttu-id="fe184-175">Klasik dağıtım modeli kullanılarak oluşturulan VM'ler.</span><span class="sxs-lookup"><span data-stu-id="fe184-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="fe184-176">İşletim sistemi disk şifrelemesi Linux sanal makineleri üzerinde devre dışı bırakılıyor.</span><span class="sxs-lookup"><span data-stu-id="fe184-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="fe184-177">Zaten şifrelenmiş bir Linux VM üzerinde şifreleme anahtarlarını güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="fe184-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="fe184-178">Azure anahtar kasası ve anahtarları oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe184-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="fe184-179">En son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve bir Azure hesabı kullanarak oturum açmış [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fe184-179">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="fe184-180">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fe184-180">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="fe184-181">Örnek parametre adlarında *myResourceGroup*, *myKey*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="fe184-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="fe184-182">İlk adım, şifreleme anahtarlarını depolamak için bir Azure anahtar kasası oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="fe184-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="fe184-183">Azure anahtar kasası anahtarları, gizli ya da, uygulama ve hizmetlerinize güvenli bir şekilde uygulamak izin parolaları depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe184-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="fe184-184">Sanal disk şifreleme için şifreleme veya şifrelerini çözme, sanal diskler için kullanılan bir şifreleme anahtarı depolamak için anahtar kasası kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe184-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="fe184-185">Azure aboneliğinizle içinde Azure anahtar kasası sağlayıcısını etkinleştir [az sağlayıcı kaydı](/cli/azure/provider#register) ve sahip bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fe184-185">Enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fe184-186">Aşağıdaki örnek, bir kaynak grubu adı oluşturur *myResourceGroup* içinde `eastus` konumu:</span><span class="sxs-lookup"><span data-stu-id="fe184-186">The following example creates a resource group name *myResourceGroup* in the `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="fe184-187">Şifreleme anahtarlarını ve depolama ve VM gibi ilişkili işlem kaynakları içeren Azure anahtar kasası aynı bölgede bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fe184-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="fe184-188">Bir Azure anahtar kasası ile oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) ve anahtar kasası disk şifrelemesi ile kullanmak için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fe184-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="fe184-189">İçin benzersiz bir anahtar kasası adı belirtmeniz *keyvault_name* gibi:</span><span class="sxs-lookup"><span data-stu-id="fe184-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="fe184-190">Yazılım veya donanım güvenlik modeli (HSM) koruması kullanarak şifreleme anahtarlarını depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe184-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="fe184-191">HSM kullanmanın premium anahtar kasası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fe184-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="fe184-192">Premium yazılım korumalı anahtarlar depolar standart anahtar kasası yerine anahtar kasası oluşturmak için ek bir maliyet yoktur.</span><span class="sxs-lookup"><span data-stu-id="fe184-192">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="fe184-193">Premium anahtar kasası oluşturmak için önceki adımda ekleyin `--sku Premium` komutu.</span><span class="sxs-lookup"><span data-stu-id="fe184-193">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="fe184-194">Aşağıdaki örnek, standart bir anahtar kasası oluşturduğumuz bu yana yazılım korumalı anahtarlar kullanır.</span><span class="sxs-lookup"><span data-stu-id="fe184-194">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="fe184-195">Her iki koruma modeli için Azure platformu VM sanal diskleri şifresini çözmek için önyüklendiğinde şifreleme anahtarları istemek için erişim verilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe184-195">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="fe184-196">Anahtar kasası ile bir şifreleme anahtarı oluşturmak [az keyvault anahtarı oluşturma](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="fe184-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="fe184-197">Aşağıdaki örnek adlı bir anahtar oluşturur *myKey*:</span><span class="sxs-lookup"><span data-stu-id="fe184-197">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="fe184-198">Azure Active Directory Hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe184-198">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="fe184-199">Sanal diskler şifrelenmiş veya şifresi, kimlik doğrulama ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi işlemek için bir hesap belirtin.</span><span class="sxs-lookup"><span data-stu-id="fe184-199">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="fe184-200">Bu hesap, bir Azure Active Directory hizmet asıl adına VM uygun şifreleme anahtarları istemek Azure platformu sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe184-200">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="fe184-201">Birçok kuruluş Azure Active Directory dizinleri ayrılmış olsa, aboneliğinizde varsayılan Azure Active Directory örneği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fe184-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="fe184-202">Azure Active Directory ile kullanarak bir hizmet sorumlusu oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="fe184-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="fe184-203">Aşağıdaki örnek değerler kimliği ve parolası sonraki komutlarını kullanmak için hizmet sorumlusu için okur:</span><span class="sxs-lookup"><span data-stu-id="fe184-203">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="fe184-204">Parola yalnızca hizmet sorumlusu oluşturma görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fe184-204">The password is only displayed when you create the service principal.</span></span> <span data-ttu-id="fe184-205">İsterseniz, görüntüleyin ve parola kaydı (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="fe184-205">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="fe184-206">Hizmet asıl adı ile listeleyebilirsiniz [az ad sp listesi](/cli/azure/ad/sp#list) ve belirli bir hizmet asıl ile ilgili ek bilgileri görüntülemek [az ad sp Göster](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="fe184-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="fe184-207">Başarılı bir şekilde şifrelemek veya sanal diskleri şifresini çözmek için anahtar kasasında depolanan şifreleme anahtarı üzerindeki izinleri anahtarları okumak için Azure Active Directory Hizmet Asıl izin verecek şekilde ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe184-207">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="fe184-208">Anahtar kasası ile üzerindeki izinleri ayarla [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="fe184-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="fe184-209">Aşağıdaki örnekte, hizmet asıl kimliği önceki komuttan sağlanır:</span><span class="sxs-lookup"><span data-stu-id="fe184-209">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="fe184-210">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe184-210">Create virtual machine</span></span>
<span data-ttu-id="fe184-211">Bazı sanal diskler gerçekte şifrelemek için bir VM oluşturun ve bir veri diski Ekle olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="fe184-211">To actually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="fe184-212">İle şifrelemek için bir VM oluşturma [az vm oluşturma](/cli/azure/vm#create) ve 5 Gb veri diski ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fe184-212">Create a VM to encrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="fe184-213">Disk şifrelemesi yalnızca belirli Market görüntülerini destekler.</span><span class="sxs-lookup"><span data-stu-id="fe184-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="fe184-214">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur *myVM* kullanarak bir **CentOS 7.2n** görüntü:</span><span class="sxs-lookup"><span data-stu-id="fe184-214">The following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="fe184-215">VM kullanarak SSH `publicIpAddress` yukarıdaki komut çıktısında gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fe184-215">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="fe184-216">Bir bölüm ve dosya sistemi oluşturun, sonra veri diski bağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="fe184-216">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="fe184-217">Daha fazla bilgi için bkz: [yeni disk bağlamak için bir Linux VM Bağlan](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="fe184-217">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="fe184-218">SSH oturumunuzu kapatın.</span><span class="sxs-lookup"><span data-stu-id="fe184-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="fe184-219">Sanal makine şifrele</span><span class="sxs-lookup"><span data-stu-id="fe184-219">Encrypt virtual machine</span></span>
<span data-ttu-id="fe184-220">Sanal diskler şifrelemek için birlikte tüm önceki bileşenleri getirin:</span><span class="sxs-lookup"><span data-stu-id="fe184-220">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="fe184-221">Azure Active Directory hizmet asıl ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="fe184-221">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="fe184-222">Şifrelenmiş diskleriniz için meta verileri depolamak için anahtar kasası belirtin.</span><span class="sxs-lookup"><span data-stu-id="fe184-222">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="fe184-223">Gerçek şifreleme ve şifre çözme için kullanılacak şifreleme anahtarları belirtin.</span><span class="sxs-lookup"><span data-stu-id="fe184-223">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="fe184-224">İşletim sistemi diski, veri diskleri veya tüm şifrelemek isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="fe184-224">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="fe184-225">VM ile şifrelemek [az vm şifrelemeyi etkinleştirmek](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="fe184-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="fe184-226">Aşağıdaki örnek kullanır `$sp_id` ve `$sp_password` önceki değişkenleri `ad sp create-for-rbac` komutu:</span><span class="sxs-lookup"><span data-stu-id="fe184-226">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="fe184-227">Disk şifrelemesi işlemin tamamlanması biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="fe184-227">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="fe184-228">İşlem durumunu izleme [az vm şifreleme Göster](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="fe184-228">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe184-229">Çıktı aşağıdaki kesilmiş örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="fe184-229">The output is similar to the following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="fe184-230">Disk işletim sistemi durumu raporları bekleyin **VMRestartPending**, VM ile yeniden [az vm yeniden başlatma](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="fe184-230">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe184-231">Önyükleme işlemi sırasında disk şifreleme işlemi sonlandırılır, böylece yeniden şifreleme durumunu denetleyerek önce birkaç dakika bekleyin **az vm şifreleme Göster**:</span><span class="sxs-lookup"><span data-stu-id="fe184-231">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="fe184-232">Durum artık işletim sistemi diski ve veri diski olarak bildirmelisiniz **şifreli**.</span><span class="sxs-lookup"><span data-stu-id="fe184-232">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="fe184-233">Ek veri disklerinin ekleme</span><span class="sxs-lookup"><span data-stu-id="fe184-233">Add additional data disks</span></span>
<span data-ttu-id="fe184-234">Veri disklerinizi şifrelenmiş sonra daha sonra ek sanal diskleri VM'nize eklemek ve de şifreleme.</span><span class="sxs-lookup"><span data-stu-id="fe184-234">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="fe184-235">Örneğin, ikinci bir sanal disk VM'nize aşağıdaki şekilde ekleyin olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="fe184-235">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="fe184-236">Sanal diskler gibi şifrelemek için komutu yeniden çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fe184-236">Re-run the command to encrypt the virtual disks as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="fe184-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fe184-237">Next steps</span></span>
* <span data-ttu-id="fe184-238">Azure anahtar kasası, şifreleme anahtarlarını ve kasa, silme de dahil olmak üzere yönetme hakkında daha fazla bilgi için bkz: [anahtar kasası CLI kullanarak yönetme](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="fe184-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="fe184-239">Azure için karşıya yüklemek için şifrelenmiş bir özel VM hazırlama gibi disk şifrelemesi hakkında daha fazla bilgi için bkz: [Azure Disk şifrelemesi](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="fe184-239">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
