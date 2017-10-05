---
title: "Azure CLI betik örnek - çok katmanlı uygulamalar için bir ağ oluşturun. | Microsoft Docs"
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
ms.openlocfilehash: de65d820f2d9eea49b58185c81d815675fd76740
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="988f0-103">Çok katmanlı uygulamalar için bir ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="988f0-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="988f0-104">Bu komut dosyası örneği ön uç ve arka uç alt ağları ile bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="988f0-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="988f0-105">Arka uç alt ağ trafiği MySQL, bağlantı noktası 3306 sınırlı olsa ön uç alt ağ trafiği HTTP ve SSH, ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="988f0-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="988f0-106">Betiği çalıştırdıktan sonra bir web sunucusu ve MySQL yazılım dağıtabilirsiniz her alt ağda iki sanal makineye sahip.</span><span class="sxs-lookup"><span data-stu-id="988f0-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="988f0-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="988f0-107">Sample script</span></span>


<span data-ttu-id="988f0-108">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "çok katmanlı uygulama için sanal ağ")]</span><span class="sxs-lookup"><span data-stu-id="988f0-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="988f0-109">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="988f0-109">Clean up deployment</span></span> 

<span data-ttu-id="988f0-110">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="988f0-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="988f0-111">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="988f0-111">Script explanation</span></span>

<span data-ttu-id="988f0-112">Bu komut, bir kaynak grubu, sanal ağ ve ağ güvenlik grupları oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="988f0-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="988f0-113">Komut özgü belgelere Tablo bağlantıları her komut.</span><span class="sxs-lookup"><span data-stu-id="988f0-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="988f0-114">Komut</span><span class="sxs-lookup"><span data-stu-id="988f0-114">Command</span></span> | <span data-ttu-id="988f0-115">Notlar</span><span class="sxs-lookup"><span data-stu-id="988f0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="988f0-116">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="988f0-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="988f0-117">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="988f0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="988f0-118">az ağ vnet oluşturma</span><span class="sxs-lookup"><span data-stu-id="988f0-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="988f0-119">Bir Azure sanal ağı ve ön uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="988f0-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="988f0-120">az ağ alt ağı oluşturun</span><span class="sxs-lookup"><span data-stu-id="988f0-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="988f0-121">Bir arka uç alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="988f0-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="988f0-122">az ağ genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="988f0-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="988f0-123">VM Internet'ten erişmek için genel bir IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="988f0-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="988f0-124">az ağ NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="988f0-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="988f0-125">Sanal ağ arabirimi oluşturur ve bunları sanal ağın ön uç ve arka uç alt ağlara ekler.</span><span class="sxs-lookup"><span data-stu-id="988f0-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="988f0-126">az ağ nsg oluşturma</span><span class="sxs-lookup"><span data-stu-id="988f0-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="988f0-127">Ağ ön uç ve arka uç alt ağlar için ilişkili güvenlik grupları (NSG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="988f0-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="988f0-128">az ağ nsg kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="988f0-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="988f0-129">İzin veren veya özel alt ağları için belirli bağlantı noktalarını engellemek NSG kuralları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="988f0-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="988f0-130">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="988f0-130">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="988f0-131">Sanal makineler oluşturur ve her bir VM için bir NIC ekler.</span><span class="sxs-lookup"><span data-stu-id="988f0-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="988f0-132">Bu komut ayrıca kullanmak için sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="988f0-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="988f0-133">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="988f0-133">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="988f0-134">Bir kaynak grubu ve içerdiği tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="988f0-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="988f0-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="988f0-135">Next steps</span></span>

<span data-ttu-id="988f0-136">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="988f0-136">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="988f0-137">Ek ağ CLI kod örnekleri bulunabilir [Azure ağ genel görünümü belgeleri](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="988f0-137">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>