---
title: "aaaAzure CLI komut dosyası örneği - bir iç ve dış NSG ile iki VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - iç ve dış NSG ile iki VM oluşturma"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f04e62d09575bee34ac4aeee949736b34000c337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="8a1d9-103">Sanal makineler arasındaki ağ trafiğini güvenli</span><span class="sxs-lookup"><span data-stu-id="8a1d9-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="8a1d9-104">Bu komut dosyası iki sanal makine oluşturur ve gelen trafiği tooboth güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="8a1d9-105">Bir sanal makine üzerinde erişilebilir olduğundan hello Internet ve bir ağ güvenlik grubu (NSG) tooallow trafiği 3389 numaralı bağlantı noktası ve bağlantı noktası 80 üzerinde yapılandırdı.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 3389 and port 80.</span></span> <span data-ttu-id="8a1d9-106">Merhaba ikinci sanal makine üzerinde erişilebilir değil Internet hello ve sahip bir NSG yapılandırılmış tooonly izin hello ilk sanal makineye gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8a1d9-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8a1d9-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8a1d9-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="8a1d9-108">Clean up deployment</span></span> 

<span data-ttu-id="8a1d9-109">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="8a1d9-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="8a1d9-110">Script explanation</span></span>

<span data-ttu-id="8a1d9-111">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="8a1d9-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8a1d9-113">Komut</span><span class="sxs-lookup"><span data-stu-id="8a1d9-113">Command</span></span> | <span data-ttu-id="8a1d9-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="8a1d9-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8a1d9-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a1d9-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8a1d9-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8a1d9-117">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a1d9-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="8a1d9-118">Bir Azure sanal ağ ve alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="8a1d9-119">az ağ sanal alt oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a1d9-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="8a1d9-120">Bir alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="8a1d9-121">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="8a1d9-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="8a1d9-122">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="8a1d9-123">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="8a1d9-124">az ağ nsg kural güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="8a1d9-124">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="8a1d9-125">Bir NSG kuralını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-125">Updates an NSG rule.</span></span> <span data-ttu-id="8a1d9-126">Bu örnekte, trafiğin yalnızca hello ön uç alt ağından güncelleştirilmiş toopass hello arka uç kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-126">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="8a1d9-127">az ağ nsg kuralı listesi</span><span class="sxs-lookup"><span data-stu-id="8a1d9-127">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="8a1d9-128">Bir ağ güvenlik grubu kural hakkındaki bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-128">Returns information about a network security group rule.</span></span> <span data-ttu-id="8a1d9-129">Bu örnekte, hello kural adı, daha sonra hello betik kullanmak için bir değişkende depolanır.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-129">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="8a1d9-130">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="8a1d9-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="8a1d9-131">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="8a1d9-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8a1d9-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8a1d9-132">Next steps</span></span>

<span data-ttu-id="8a1d9-133">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a1d9-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8a1d9-134">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a1d9-134">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
