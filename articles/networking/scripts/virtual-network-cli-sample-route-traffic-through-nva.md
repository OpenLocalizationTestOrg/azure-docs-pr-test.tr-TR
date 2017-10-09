---
title: "aaaAzure CLI komut dosyası örneği - rota trafiği ağ sanal gereç aracılığıyla | Microsoft Docs"
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="aacda-103">Bir ağ sanal gereç yoluyla trafiği yönlendirme</span><span class="sxs-lookup"><span data-stu-id="aacda-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="aacda-104">Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="aacda-105">Ayrıca hello iki alt ağlar arasında etkin tooroute trafiğinin iletme IP ile VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="aacda-106">Merhaba komut dosyasını çalıştırdıktan sonra bir güvenlik duvarı uygulaması toohello VM gibi ağ yazılım dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aacda-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="aacda-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="aacda-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="aacda-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="aacda-108">Clean up deployment</span></span> 

<span data-ttu-id="aacda-109">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="aacda-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="aacda-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="aacda-110">Script explanation</span></span>

<span data-ttu-id="aacda-111">Bu komut dosyası komutları toocreate aşağıdaki hello bir kaynak grubu, sanal ağ ve ağ güvenlik grupları kullanır.</span><span class="sxs-lookup"><span data-stu-id="aacda-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="aacda-112">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="aacda-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="aacda-113">Komut</span><span class="sxs-lookup"><span data-stu-id="aacda-113">Command</span></span> | <span data-ttu-id="aacda-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="aacda-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="aacda-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="aacda-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="aacda-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="aacda-117">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="aacda-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="aacda-118">Bir Azure sanal ağı ve ön uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="aacda-119">az ağ alt ağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="aacda-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="aacda-120">Arka uç ve DMZ alt ağlar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-120">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="aacda-121">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="aacda-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="aacda-122">Ortak IP adresi tooaccess hello VM Internet hello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="aacda-123">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="aacda-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="aacda-124">Bir sanal ağ arabirimi ve onu için IP iletimini etkinleştirme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-124">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="aacda-125">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="aacda-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="aacda-126">Bir ağ güvenlik grubu (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-126">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="aacda-127">az ağ nsg kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="aacda-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="aacda-128">HTTP ve HTTPS bağlantı noktalarını toohello VM gelene izin ver NSG kuralları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-128">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="aacda-129">az ağ sanal ağ alt ağı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="aacda-129">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="aacda-130">Nsg'ler ilişkilendirilmiş bir hello ve rota toosubnets tabloları.</span><span class="sxs-lookup"><span data-stu-id="aacda-130">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="aacda-131">az ağ rota tablosu oluştur</span><span class="sxs-lookup"><span data-stu-id="aacda-131">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="aacda-132">Tüm yollar için yol tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-132">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="aacda-133">az ağ yol tablosu yol oluşturma</span><span class="sxs-lookup"><span data-stu-id="aacda-133">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="aacda-134">Yollar tooroute trafiği alt ağlar arasında ve hello Internet üzerinden hello VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aacda-134">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="aacda-135">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="aacda-135">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="aacda-136">Bir sanal makine oluşturur ve hello NIC tooit ekler.</span><span class="sxs-lookup"><span data-stu-id="aacda-136">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="aacda-137">Bu komut ayrıca hello sanal makine görüntü toouse ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="aacda-137">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="aacda-138">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="aacda-138">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="aacda-139">Bir kaynak grubu ve içerdiği tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="aacda-139">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aacda-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aacda-140">Next steps</span></span>

<span data-ttu-id="aacda-141">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aacda-141">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="aacda-142">Ek ağ CLI kod örnekleri hello bulunabilir [Azure ağ genel görünümü belgeleri](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="aacda-142">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
