---
title: "aaaAzure CLI betik örnek - Windows Server VM oluşturma | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - Windows Server VM oluşturma"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="673ff-103">Hello Azure CLI ile bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="673ff-103">Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="673ff-104">Bu komut dosyasını Windows Server 2016 çalıştıran bir Azure sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="673ff-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="673ff-105">Merhaba komut dosyasını çalıştırdıktan sonra hello sanal makine bir Uzak Masaüstü bağlantısı üzerinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="673ff-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="673ff-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="673ff-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="673ff-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="673ff-107">Clean up deployment</span></span> 

<span data-ttu-id="673ff-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="673ff-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="673ff-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="673ff-109">Script explanation</span></span>

<span data-ttu-id="673ff-110">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="673ff-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="673ff-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="673ff-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="673ff-112">Komut</span><span class="sxs-lookup"><span data-stu-id="673ff-112">Command</span></span> | <span data-ttu-id="673ff-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="673ff-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="673ff-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="673ff-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="673ff-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="673ff-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="673ff-116">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="673ff-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="673ff-117">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="673ff-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="673ff-118">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="673ff-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="673ff-119">Bir ortak IP adresi statik bir IP adresi ve ilişkili bir DNS adı ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="673ff-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="673ff-120">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="673ff-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="673ff-121">Merhaba Internet ve hello sanal makine arasında bir güvenlik sınırı olan bir ağ güvenlik grubu (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="673ff-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="673ff-122">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="673ff-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="673ff-123">Bir sanal ağ kartı oluşturur ve toohello sanal ağ, alt ağ ve NSG ekler.</span><span class="sxs-lookup"><span data-stu-id="673ff-123">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="673ff-124">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="673ff-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="673ff-125">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="673ff-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="673ff-126">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="673ff-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="673ff-127">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="673ff-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="673ff-128">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="673ff-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="673ff-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="673ff-129">Next steps</span></span>

<span data-ttu-id="673ff-130">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="673ff-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="673ff-131">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="673ff-131">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
