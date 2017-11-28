---
title: "aaaAzure CLI betik örnek - çok katmanlı uygulamalar için bir ağ oluşturun. | Microsoft Docs"
description: "Azure CLI betik örnek - çok katmanlı uygulamalar için bir sanal ağ oluşturun."
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="cd144-103">Çok katmanlı uygulamalar için bir ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd144-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="cd144-104">Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd144-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="cd144-105">Trafik toohello ön uç alt sınırlı tooHTTP ve SSH, trafik toohello sırasında arka uç alt sınırlı tooMySQL, bağlantı noktası 3306.</span><span class="sxs-lookup"><span data-stu-id="cd144-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="cd144-106">Çalışan hello betik sonra iki sanal makine, bir web sunucusu ve MySQL yazılım dağıtabilirsiniz her alt ağda gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd144-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="cd144-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="cd144-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="cd144-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="cd144-108">Clean up deployment</span></span> 

<span data-ttu-id="cd144-109">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="cd144-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="cd144-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="cd144-110">Script explanation</span></span>

<span data-ttu-id="cd144-111">Bu komut dosyası komutları toocreate aşağıdaki hello bir kaynak grubu, sanal ağ ve ağ güvenlik grupları kullanır.</span><span class="sxs-lookup"><span data-stu-id="cd144-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="cd144-112">Her komut hello tablosundaki toocommand özgü belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="cd144-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="cd144-113">Komut</span><span class="sxs-lookup"><span data-stu-id="cd144-113">Command</span></span> | <span data-ttu-id="cd144-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="cd144-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cd144-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd144-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="cd144-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd144-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cd144-117">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd144-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="cd144-118">Bir Azure sanal ağı ve ön uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd144-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="cd144-119">az ağ alt ağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="cd144-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="cd144-120">Bir arka uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd144-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="cd144-121">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="cd144-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="cd144-122">Ortak IP adresi tooaccess hello VM Internet hello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd144-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="cd144-123">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="cd144-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="cd144-124">Sanal ağ arabirimi oluşturur ve bunları toohello sanal ağın ön uç ve arka uç alt ekler.</span><span class="sxs-lookup"><span data-stu-id="cd144-124">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="cd144-125">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd144-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="cd144-126">İlişkili toohello ön uç ve arka uç alt ağlar, ağ güvenlik gruplarını (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd144-126">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="cd144-127">az ağ nsg kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd144-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="cd144-128">İzin verme veya engelleme belirli bağlantı noktalarını toospecific alt NSG kuralları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cd144-128">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="cd144-129">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd144-129">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="cd144-130">Sanal makineler oluşturur ve NIC tooeach VM ekler.</span><span class="sxs-lookup"><span data-stu-id="cd144-130">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="cd144-131">Bu komut ayrıca hello sanal makine görüntü toouse ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="cd144-131">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="cd144-132">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="cd144-132">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="cd144-133">Bir kaynak grubu ve içerdiği tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="cd144-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cd144-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cd144-134">Next steps</span></span>

<span data-ttu-id="cd144-135">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cd144-135">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="cd144-136">Ek ağ CLI kod örnekleri hello bulunabilir [Azure ağ genel görünümü belgeleri](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="cd144-136">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
