---
title: "aaaAzure CLI komut dosyası örneği - bir iç ve dış NSG ile iki VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - iç ve dış NSG ile iki VM oluşturma"
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
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="6da2d-103">Sanal makineler arasındaki ağ trafiğini güvenli</span><span class="sxs-lookup"><span data-stu-id="6da2d-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="6da2d-104">Bu komut dosyası iki sanal makine oluşturur ve gelen trafiği tooboth güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="6da2d-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="6da2d-105">Bir sanal makine üzerinde erişilebilir olduğundan hello internet ve ağ güvenlik grubu (NSG) bağlantı noktası 22 ve bağlantı noktası 80 üzerinde tooallow trafiği yapılandırdı.</span><span class="sxs-lookup"><span data-stu-id="6da2d-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 22 and port 80.</span></span> <span data-ttu-id="6da2d-106">Merhaba ikinci sanal makine üzerinde erişilebilir değil Internet hello ve sahip bir NSG yapılandırılmış tooonly izin hello ilk sanal makineye gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="6da2d-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6da2d-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="6da2d-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6da2d-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="6da2d-108">Clean up deployment</span></span> 

<span data-ttu-id="6da2d-109">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="6da2d-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6da2d-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="6da2d-110">Script explanation</span></span>

<span data-ttu-id="6da2d-111">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="6da2d-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6da2d-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="6da2d-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6da2d-113">Komut</span><span class="sxs-lookup"><span data-stu-id="6da2d-113">Command</span></span> | <span data-ttu-id="6da2d-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="6da2d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6da2d-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6da2d-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6da2d-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6da2d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6da2d-117">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="6da2d-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="6da2d-118">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6da2d-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="6da2d-119">az ağ sanal alt oluşturma</span><span class="sxs-lookup"><span data-stu-id="6da2d-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="6da2d-120">Bir alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6da2d-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="6da2d-121">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="6da2d-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6da2d-122">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="6da2d-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="6da2d-123">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6da2d-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="6da2d-124">az ağ nsg kuralı listesi</span><span class="sxs-lookup"><span data-stu-id="6da2d-124">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="6da2d-125">Bir ağ güvenlik grubu kural hakkındaki bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="6da2d-125">Returns information about a network security group rule.</span></span> <span data-ttu-id="6da2d-126">Bu örnekte, hello kural adı, daha sonra hello betik kullanmak için bir değişkende depolanır.</span><span class="sxs-lookup"><span data-stu-id="6da2d-126">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="6da2d-127">az ağ nsg kural güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="6da2d-127">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="6da2d-128">Bir NSG kuralını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="6da2d-128">Updates an NSG rule.</span></span> <span data-ttu-id="6da2d-129">Bu örnekte, trafiğin yalnızca hello ön uç alt ağından güncelleştirilmiş toopass hello arka uç kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="6da2d-129">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="6da2d-130">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="6da2d-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6da2d-131">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="6da2d-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6da2d-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6da2d-132">Next steps</span></span>

<span data-ttu-id="6da2d-133">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6da2d-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6da2d-134">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6da2d-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
