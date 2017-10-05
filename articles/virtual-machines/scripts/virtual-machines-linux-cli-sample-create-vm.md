---
title: "Azure CLI örnek komut dosyası - bir Linux VM oluşturma | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - bir Linux VM oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: dc7e7276bcea32c59c67a42dedaffcedfd0cf907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="27c4f-103">Tam olarak yapılandırılmış bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="27c4f-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="27c4f-104">Bu komut dosyasını bir Ubuntu işletim sistemine sahip bir Azure sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="27c4f-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="27c4f-105">Betiği çalıştırdıktan sonra sanal makinenin SSH üzerinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27c4f-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="27c4f-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="27c4f-106">Sample script</span></span>

<span data-ttu-id="27c4f-107">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "hızlı VM oluştur")]</span><span class="sxs-lookup"><span data-stu-id="27c4f-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="27c4f-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="27c4f-108">Clean up deployment</span></span> 

<span data-ttu-id="27c4f-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="27c4f-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="27c4f-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="27c4f-110">Script explanation</span></span>

<span data-ttu-id="27c4f-111">Bu komut, bir kaynak grubu, sanal makine ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="27c4f-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="27c4f-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="27c4f-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="27c4f-113">Komut</span><span class="sxs-lookup"><span data-stu-id="27c4f-113">Command</span></span> | <span data-ttu-id="27c4f-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="27c4f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="27c4f-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="27c4f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="27c4f-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="27c4f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="27c4f-117">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="27c4f-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="27c4f-118">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="27c4f-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="27c4f-119">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="27c4f-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="27c4f-120">Bir ortak IP adresi statik bir IP adresi ve ilişkili bir DNS adı ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="27c4f-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="27c4f-121">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="27c4f-121">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="27c4f-122">Internet ve sanal makine arasında bir güvenlik sınırı olan bir ağ güvenlik grubu (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="27c4f-122">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="27c4f-123">az ağ nsg kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="27c4f-123">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="27c4f-124">Gelen trafiğe izin veren bir NSG kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="27c4f-124">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="27c4f-125">Bu örnekte, bağlantı noktası 22 SSH trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="27c4f-125">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="27c4f-126">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="27c4f-126">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="27c4f-127">Bir sanal ağ kartı oluşturur ve sanal ağ, alt ağ ve NSG ekler.</span><span class="sxs-lookup"><span data-stu-id="27c4f-127">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="27c4f-128">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="27c4f-128">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="27c4f-129">Sanal makine oluşturur ve ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="27c4f-129">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="27c4f-130">Bu komut ayrıca kullanılacak sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="27c4f-130">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="27c4f-131">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="27c4f-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="27c4f-132">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="27c4f-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="27c4f-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27c4f-133">Next steps</span></span>

<span data-ttu-id="27c4f-134">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="27c4f-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="27c4f-135">Ek sanal makine CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27c4f-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
