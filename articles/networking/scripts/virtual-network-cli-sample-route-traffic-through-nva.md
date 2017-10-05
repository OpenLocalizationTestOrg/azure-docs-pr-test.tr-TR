---
title: "Azure CLI komut dosyası örneği - rota trafiği ağ sanal gereç aracılığıyla | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - güvenlik duvarı ağ sanal gereç yoluyla trafiği yönlendirme."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 78091b515c00591a4af8d807945475b6be50188a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="982ea-103">Bir ağ sanal gereç yoluyla trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="982ea-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="982ea-104">Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="982ea-105">Ayrıca IP iletme iki alt ağlar arasında trafiği yönlendirmek için etkin olan bir VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="982ea-106">Komut dosyasını çalıştırdıktan sonra VM için bir güvenlik duvarı uygulaması gibi ağ yazılım dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="982ea-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="982ea-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="982ea-107">Sample script</span></span>


<span data-ttu-id="982ea-108">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "trafiği ağ sanal gereç aracılığıyla yönlendirmek")]</span><span class="sxs-lookup"><span data-stu-id="982ea-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="982ea-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="982ea-109">Clean up deployment</span></span> 

<span data-ttu-id="982ea-110">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="982ea-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="982ea-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="982ea-111">Script explanation</span></span>

<span data-ttu-id="982ea-112">Bu komut, bir kaynak grubu, sanal ağ ve ağ güvenlik grupları oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="982ea-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="982ea-113">Komut özgü belgelere Tablo bağlantıları her komut.</span><span class="sxs-lookup"><span data-stu-id="982ea-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="982ea-114">Komut</span><span class="sxs-lookup"><span data-stu-id="982ea-114">Command</span></span> | <span data-ttu-id="982ea-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="982ea-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="982ea-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="982ea-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="982ea-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="982ea-118">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="982ea-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="982ea-119">Bir Azure sanal ağı ve ön uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="982ea-120">az ağ alt ağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="982ea-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="982ea-121">Arka uç ve DMZ alt ağlar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="982ea-122">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="982ea-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="982ea-123">VM Internet'ten erişmek için genel bir IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="982ea-124">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="982ea-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="982ea-125">Bir sanal ağ arabirimi ve onu için IP iletimini etkinleştirme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="982ea-126">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="982ea-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="982ea-127">Bir ağ güvenlik grubu (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="982ea-128">az ağ nsg kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="982ea-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="982ea-129">HTTP ve HTTPS bağlantı noktalarını VM'ye gelen izin NSG kuralları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="982ea-130">az ağ sanal ağ alt ağı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="982ea-130">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="982ea-131">Nsg'ler ve alt ağlara yol tablolarını ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="982ea-131">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="982ea-132">az ağ rota tablosu oluştur</span><span class="sxs-lookup"><span data-stu-id="982ea-132">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="982ea-133">Tüm yollar için yol tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="982ea-134">az ağ yol tablosu yol oluşturma</span><span class="sxs-lookup"><span data-stu-id="982ea-134">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="982ea-135">Alt ağlar ve VM ile Internet arasında trafiği yönlendirmek için yollar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="982ea-135">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="982ea-136">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="982ea-136">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="982ea-137">Bir sanal makine oluşturur ve NIC ekler.</span><span class="sxs-lookup"><span data-stu-id="982ea-137">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="982ea-138">Bu komut ayrıca kullanmak için sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="982ea-138">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="982ea-139">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="982ea-139">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="982ea-140">Bir kaynak grubu ve içerdiği tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="982ea-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="982ea-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="982ea-141">Next steps</span></span>

<span data-ttu-id="982ea-142">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="982ea-142">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="982ea-143">Ek ağ CLI kod örnekleri bulunabilir [Azure ağ genel görünümü belgeleri](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="982ea-143">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>