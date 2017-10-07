---
title: "aaaAzure CLI komut dosyası örneği - bir Linux VM oluşturma | Microsoft Docs"
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
ms.openlocfilehash: c9855204a85cc0f6cd758a1d20121fbeea070943
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="2c705-103">Tam olarak yapılandırılmış bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="2c705-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="2c705-104">Bu komut dosyasını bir Ubuntu işletim sistemine sahip bir Azure sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2c705-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="2c705-105">Hello komut dosyasını çalıştırdıktan sonra hello sanal makineye SSH üzerinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c705-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2c705-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="2c705-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2c705-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="2c705-107">Clean up deployment</span></span> 

<span data-ttu-id="2c705-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="2c705-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2c705-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="2c705-109">Script explanation</span></span>

<span data-ttu-id="2c705-110">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="2c705-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2c705-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="2c705-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2c705-112">Komut</span><span class="sxs-lookup"><span data-stu-id="2c705-112">Command</span></span> | <span data-ttu-id="2c705-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="2c705-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2c705-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c705-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2c705-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2c705-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2c705-116">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c705-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="2c705-117">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2c705-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="2c705-118">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="2c705-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="2c705-119">Bir ortak IP adresi statik bir IP adresi ve ilişkili bir DNS adı ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2c705-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="2c705-120">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c705-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="2c705-121">Merhaba Internet ve hello sanal makine arasında bir güvenlik sınırı olan bir ağ güvenlik grubu (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2c705-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="2c705-122">az ağ nsg kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c705-122">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="2c705-123">Bir NSG kural tooallow oluşturur gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="2c705-123">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="2c705-124">Bu örnekte, bağlantı noktası 22 SSH trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="2c705-124">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="2c705-125">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="2c705-125">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="2c705-126">Bir sanal ağ kartı oluşturur ve toohello sanal ağ, alt ağ ve NSG ekler.</span><span class="sxs-lookup"><span data-stu-id="2c705-126">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="2c705-127">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c705-127">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2c705-128">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="2c705-128">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="2c705-129">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="2c705-129">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="2c705-130">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="2c705-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2c705-131">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="2c705-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2c705-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c705-132">Next steps</span></span>

<span data-ttu-id="2c705-133">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2c705-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2c705-134">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c705-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
