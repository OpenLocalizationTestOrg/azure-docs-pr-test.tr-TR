---
title: "aaaAzure CLI komut dosyası örneği - filtre VM ağ trafiğini | Microsoft Docs"
description: "Azure CLI betik örnek - gelen ve giden VM ağ trafiğini filtre."
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="d297a-103">Gelen ve giden VM ağ trafiği filtreleme</span><span class="sxs-lookup"><span data-stu-id="d297a-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="d297a-104">Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d297a-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d297a-105">Gelen ağ trafiğini toohello ön uç alt sınırlı tooHTTP, HTTPS ve SSH, giden sırada trafiği toohello hello arka uç alt ağından Internet izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="d297a-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="d297a-106">Merhaba komut dosyasını çalıştırdıktan sonra iki NIC içeren bir sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="d297a-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="d297a-107">Her NIC'nin bağlı tooa farklı alt değil.</span><span class="sxs-lookup"><span data-stu-id="d297a-107">Each NIC is connected tooa different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d297a-108">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="d297a-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d297a-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="d297a-109">Clean up deployment</span></span> 

<span data-ttu-id="d297a-110">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="d297a-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d297a-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="d297a-111">Script explanation</span></span>

<span data-ttu-id="d297a-112">Bu komut dosyası komutları toocreate aşağıdaki hello bir kaynak grubu, sanal ağ ve ağ güvenlik grupları kullanır.</span><span class="sxs-lookup"><span data-stu-id="d297a-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="d297a-113">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="d297a-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="d297a-114">Komut</span><span class="sxs-lookup"><span data-stu-id="d297a-114">Command</span></span> | <span data-ttu-id="d297a-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="d297a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d297a-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d297a-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d297a-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d297a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d297a-118">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="d297a-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="d297a-119">Bir Azure sanal ağı ve ön uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d297a-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="d297a-120">az ağ alt ağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="d297a-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="d297a-121">Bir arka uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d297a-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="d297a-122">az ağ sanal ağ alt ağı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d297a-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="d297a-123">Nsg'ler toosubnets ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="d297a-123">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="d297a-124">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="d297a-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="d297a-125">Ortak IP adresi tooaccess hello VM Internet hello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d297a-125">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="d297a-126">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="d297a-126">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="d297a-127">Sanal ağ arabirimi oluşturur ve bunları toohello sanal ağın ön uç ve arka uç alt ekler.</span><span class="sxs-lookup"><span data-stu-id="d297a-127">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="d297a-128">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="d297a-128">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="d297a-129">İlişkili toohello ön uç ve arka uç alt ağlar, ağ güvenlik gruplarını (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d297a-129">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="d297a-130">az ağ nsg kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d297a-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="d297a-131">İzin verme veya engelleme belirli bağlantı noktalarını toospecific alt NSG kuralları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d297a-131">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="d297a-132">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="d297a-132">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="d297a-133">Sanal makineler oluşturur ve NIC tooeach VM ekler.</span><span class="sxs-lookup"><span data-stu-id="d297a-133">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="d297a-134">Bu komut ayrıca hello sanal makine görüntü toouse ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d297a-134">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="d297a-135">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="d297a-135">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="d297a-136">Bir kaynak grubu ve içerdiği tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="d297a-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d297a-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d297a-137">Next steps</span></span>

<span data-ttu-id="d297a-138">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d297a-138">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="d297a-139">Ek ağ CLI kod örnekleri hello bulunabilir [Azure ağ genel görünümü belgeleri](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="d297a-139">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
