---
title: "Azure CLI örnek komut dosyası - bir Linux VM şifrelemek | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - bir Linux VM şifrele"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9388bce04e37d049301521f808cd8494c327e335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="369a8-103">Azure'da bir Linux sanal makine şifrele</span><span class="sxs-lookup"><span data-stu-id="369a8-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="369a8-104">Bu komut dosyasını güvenli bir Azure anahtar kasası, şifreleme anahtarları, Azure Active Directory hizmet asıl ve Linux sanal makine (VM) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="369a8-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="369a8-105">VM şifreleme anahtarı anahtar kasası ve hizmet asıl kimlik bilgileri kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="369a8-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="369a8-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="369a8-106">Sample script</span></span>

<span data-ttu-id="369a8-107">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "şifrelemek VM diskleri")]</span><span class="sxs-lookup"><span data-stu-id="369a8-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="369a8-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="369a8-108">Clean up deployment</span></span> 

<span data-ttu-id="369a8-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="369a8-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="369a8-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="369a8-110">Script explanation</span></span>

<span data-ttu-id="369a8-111">Bu komut, bir kaynak grubu, Azure anahtar kasası, hizmet sorumlusu, sanal makine ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="369a8-111">This script uses the following commands to create a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="369a8-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="369a8-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="369a8-113">Komut</span><span class="sxs-lookup"><span data-stu-id="369a8-113">Command</span></span> | <span data-ttu-id="369a8-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="369a8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="369a8-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="369a8-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="369a8-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="369a8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="369a8-117">az keyvault oluşturma</span><span class="sxs-lookup"><span data-stu-id="369a8-117">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="369a8-118">Şifreleme anahtarları gibi güvenli veri depolamak için bir Azure anahtar kasası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="369a8-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="369a8-119">az keyvault anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="369a8-119">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="369a8-120">Bir şifreleme anahtarı anahtar kasası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="369a8-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="369a8-121">az ad sp oluşturma-için-rbac</span><span class="sxs-lookup"><span data-stu-id="369a8-121">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="369a8-122">Bir Azure Active Directory güvenli bir şekilde kimlik doğrulaması ve şifreleme anahtarlarının erişimi denetlemek için hizmet sorumlusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="369a8-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="369a8-123">az keyvault-ilkesini ayarlama</span><span class="sxs-lookup"><span data-stu-id="369a8-123">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="369a8-124">Şifreleme anahtarları için hizmet asıl erişim vermek için bu anahtar kasası üzerinde izinlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="369a8-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="369a8-125">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="369a8-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="369a8-126">Sanal makine oluşturur ve ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="369a8-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="369a8-127">Bu komut ayrıca kullanılacak sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="369a8-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="369a8-128">az vm şifrelemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="369a8-128">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="369a8-129">Hizmet asıl kimlik bilgilerini ve şifreleme anahtarı kullanarak bir VM üzerinde şifrelemeyi etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="369a8-129">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="369a8-130">az vm şifreleme Göster</span><span class="sxs-lookup"><span data-stu-id="369a8-130">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="369a8-131">VM şifreleme işleminin durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="369a8-131">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="369a8-132">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="369a8-132">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="369a8-133">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="369a8-133">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="369a8-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="369a8-134">Next steps</span></span>

<span data-ttu-id="369a8-135">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="369a8-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="369a8-136">Ek sanal makine CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="369a8-136">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
