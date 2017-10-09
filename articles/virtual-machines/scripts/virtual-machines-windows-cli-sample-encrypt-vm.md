---
title: "aaaAzure CLI betik örnek - Windows VM şifrelemek | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - VM Windows şifrele"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 7a9928467f818cd5358d3d19bff5129d8fa21313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="dbd64-103">Azure'da Windows sanal makine şifrele</span><span class="sxs-lookup"><span data-stu-id="dbd64-103">Encrypt a Windows virtual machine in Azure</span></span>

<span data-ttu-id="dbd64-104">Bu komut dosyasını güvenli bir Azure anahtar kasası, şifreleme anahtarları, Azure Active Directory Hizmet sorumlusu ve bir Windows sanal makine (VM) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dbd64-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="dbd64-105">Merhaba VM hello şifreleme anahtarı anahtar kasası ve hizmet asıl kimlik bilgileri kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="dbd64-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dbd64-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="dbd64-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dbd64-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="dbd64-107">Clean up deployment</span></span> 

<span data-ttu-id="dbd64-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="dbd64-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="dbd64-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="dbd64-109">Script explanation</span></span>

<span data-ttu-id="dbd64-110">Bu komut dosyasını bir kaynak grubu, Azure anahtar kasası, hizmet asıl, sanal makine, komutları toocreate aşağıdaki hello kullanır ve tüm kaynakları ilgili.</span><span class="sxs-lookup"><span data-stu-id="dbd64-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="dbd64-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="dbd64-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dbd64-112">Komut</span><span class="sxs-lookup"><span data-stu-id="dbd64-112">Command</span></span> | <span data-ttu-id="dbd64-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="dbd64-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dbd64-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd64-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dbd64-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dbd64-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dbd64-116">az keyvault oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd64-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="dbd64-117">Azure anahtar kasası bir toostore güvenli veri şifreleme anahtarları gibi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dbd64-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="dbd64-118">az keyvault anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd64-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="dbd64-119">Bir şifreleme anahtarı anahtar kasası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dbd64-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="dbd64-120">az ad sp oluşturma-için-rbac</span><span class="sxs-lookup"><span data-stu-id="dbd64-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="dbd64-121">Bir Azure Active Directory hizmet asıl toosecurely kimlik doğrulaması ve Denetim erişim tooencryption tuşları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dbd64-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="dbd64-122">az keyvault-ilkesini ayarlama</span><span class="sxs-lookup"><span data-stu-id="dbd64-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="dbd64-123">İzinleri hello anahtar kasası toogrant üzerinde hello hizmet asıl erişim tooencryption anahtarları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="dbd64-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="dbd64-124">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd64-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="dbd64-125">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="dbd64-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="dbd64-126">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="dbd64-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="dbd64-127">az vm şifrelemeyi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="dbd64-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="dbd64-128">Merhaba hizmet asıl kimlik bilgilerini ve şifreleme anahtarı kullanarak bir VM üzerinde şifrelemeyi etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="dbd64-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="dbd64-129">az vm şifreleme Göster</span><span class="sxs-lookup"><span data-stu-id="dbd64-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="dbd64-130">Merhaba VM şifreleme işlemi Hello durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="dbd64-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="dbd64-131">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="dbd64-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="dbd64-132">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="dbd64-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dbd64-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dbd64-133">Next steps</span></span>

<span data-ttu-id="dbd64-134">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dbd64-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dbd64-135">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dbd64-135">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span></span>
