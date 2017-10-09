---
title: "birden çok NIC ile azure'da bir Linux VM aaaCreate | Microsoft Docs"
description: "Toocreate birden çok NIC içeren bir Linux VM hello Azure CLI ya da Resource Manager şablonları kullanarak tooit nasıl bağlı öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="1ffa9-103">İle birden çok NIC hello Azure CLI 1.0 kullanarak bir Linux sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="1ffa9-103">Create a Linux virtual machine with multiple NICs using hello Azure CLI 1.0</span></span>
<span data-ttu-id="1ffa9-104">Birden çok sanal ağ arabirimlerine (NIC'ler) bağlı tooit sahip Azure'da bir sanal makine (VM) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="1ffa9-105">Yaygın bir senaryo toohave farklı alt ağlar için ön uç ve arka uç bağlantısı olan veya ayrılmış bir ağ tooa izleme veya yedekleme çözümü.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="1ffa9-106">Bu makalede Hızlı komutları toocreate birden çok NIC bağlı tooit'yle bir VM'yi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-106">This article provides quick commands toocreate a VM with multiple NICs attached tooit.</span></span> <span data-ttu-id="1ffa9-107">Ayrıntılı bilgi için kendi içinde birden çok NIC nasıl toocreate Bash de dahil olmak üzere komut dosyaları, daha fazla okuyun hakkında [multi-NIC VM dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1ffa9-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="1ffa9-108">Farklı [VM boyutları](sizes.md) NIC'ler değişen çok sayıda desteği, bu nedenle, VM buna göre boyutu.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="1ffa9-109">Birden çok NIC VM oluşturma - VM hello Azure CLI 1.0 ile varolan NIC'ler tooan ekleyemezsiniz zaman eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-109">You must attach multiple NICs when you create a VM - you cannot add NICs tooan existing VM with hello Azure CLI 1.0.</span></span> <span data-ttu-id="1ffa9-110">Yapabilecekleriniz [VM hello Azure CLI 2.0 ile varolan NIC'ler tooan eklemek](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="1ffa9-110">You can [add NICs tooan existing VM with hello Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="1ffa9-111">Ayrıca [hello özgün sanal diskler üzerinde dayalı bir VM oluşturma](copy-vm.md) ve hello VM dağıtmak gibi birden çok NIC oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-111">You can also [create a VM based on hello original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy hello VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1ffa9-112">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="1ffa9-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="1ffa9-113">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1ffa9-114">[Azure CLI 1.0](#create-supporting-resources) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="1ffa9-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1ffa9-115">[Azure CLI 2.0](multiple-nics.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="1ffa9-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="1ffa9-116">Destekleyici kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="1ffa9-116">Create supporting resources</span></span>
<span data-ttu-id="1ffa9-117">Merhaba sahip olduğunuzdan emin olun [Azure CLI](../../cli-install-nodejs.md) oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-117">Make sure that you have hello [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1ffa9-118">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-118">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1ffa9-119">Örnek parametre adları dahil *myResourceGroup*, *mystorageaccount*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="1ffa9-120">İlk olarak, bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-120">First, create a resource group.</span></span> <span data-ttu-id="1ffa9-121">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="1ffa9-122">Bir depolama hesabı toohold Vm'leriniz oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-122">Create a storage account toohold your VMs.</span></span> <span data-ttu-id="1ffa9-123">Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-123">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="1ffa9-124">Bir sanal ağ tooconnect Vm'leriniz için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-124">Create a virtual network tooconnect your VMs to.</span></span> <span data-ttu-id="1ffa9-125">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* bir adres öneki ile *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-125">hello following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="1ffa9-126">İki sanal ağ alt - oluşturmak ön uç trafik, diğeri arka uç trafiği için.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="1ffa9-127">Merhaba aşağıdaki örnekte oluşturur adlı iki alt *mySubnetFrontEnd* ve *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-127">hello following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="1ffa9-128">Oluşturma ve birden çok NIC yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1ffa9-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="1ffa9-129">Hakkında daha fazla ayrıntı okuyabilirsiniz [hello Azure CLI kullanarak birden çok NIC dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), tüm hello NIC'ler toocreate döngü hello işlemi komut dosyası gibi.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-129">You can read more details about [deploying multiple NICs using hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting hello process of looping through toocreate all hello NICs.</span></span>

<span data-ttu-id="1ffa9-130">Merhaba aşağıdaki örnekte oluşturur adlı iki NIC *myNic1* ve *myNic2*, tooeach alt ağı bağlayan bir NIC ile:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-130">hello following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting tooeach subnet:</span></span>

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

<span data-ttu-id="1ffa9-131">Genellikle ayrıca oluşturduğunuz bir [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) veya [yük dengeleyici](../../load-balancer/load-balancer-overview.md) toohelp yönetmek ve Vm'leriniz arasında trafiği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="1ffa9-132">Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-132">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="1ffa9-133">NIC toohello ağ güvenlik grubu kullanarak bağlama `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-133">Bind your NICs toohello Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="1ffa9-134">Merhaba aşağıdaki örnek bağlar *myNic1* ve *myNic2* ile *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-134">hello following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="1ffa9-135">Bir VM oluşturun ve hello NIC ekleme</span><span class="sxs-lookup"><span data-stu-id="1ffa9-135">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="1ffa9-136">Merhaba VM oluştururken, artık birden çok NIC belirtin.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-136">When creating hello VM, you now specify multiple NICs.</span></span> <span data-ttu-id="1ffa9-137">Yerine `--nic-name` tooprovide tek bir NIC, bunun yerine kullandığınız `--nic-names` ve NIC virgülle ayrılmış bir listesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-137">Rather using `--nic-name` tooprovide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="1ffa9-138">Merhaba VM boyutu seçtiğinizde tootake dikkatli da gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-138">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="1ffa9-139">Merhaba tooa VM ekleyebilirsiniz NIC toplam sayısına yönelik sınırlar vardır.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-139">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="1ffa9-140">Daha fazla bilgi edinin [Linux VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="1ffa9-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="1ffa9-141">Merhaba aşağıdaki nasıl toospecify kullanarak destekleyen birden çok NIC ve ardından bir VM boyutu birden çok örnekte NIC'ler (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="1ffa9-141">hello following example shows how toospecify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="1ffa9-142">Resource Manager şablonları kullanarak birden çok NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="1ffa9-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="1ffa9-143">Azure Resource Manager şablonları bildirim temelli JSON dosyaları toodefine ortamınız kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-143">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="1ffa9-144">Okuyabilirsiniz bir [genel bakış Azure Kaynak Yöneticisi'nin](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ffa9-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1ffa9-145">Resource Manager şablonları bir şekilde toocreate birden çok NIC oluşturma gibi dağıtım işlemi sırasında birden fazla örneğini bir kaynak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-145">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="1ffa9-146">Kullandığınız *kopya* toospecify hello örnekleri toocreate sayısı:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-146">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="1ffa9-147">Daha fazla bilgi edinin [kullanarak birden çok örneği oluşturma *kopya*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="1ffa9-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="1ffa9-148">De kullanabilirsiniz bir `copyIndex()` toothen sona toocreate sağlayan bir numara tooa kaynak adı `myNic1`, `myNic2`, vb. hello aşağıdaki hello dizin değeri ekleyerek bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1ffa9-148">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="1ffa9-149">Tam örnek okuyabilirsiniz [Resource Manager şablonları kullanarak birden çok NIC oluşturma](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="1ffa9-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ffa9-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ffa9-150">Next steps</span></span>
<span data-ttu-id="1ffa9-151">Emin tooreview olun [Linux VM boyutları](sizes.md) toocreating birden çok NIC içeren bir VM çalışırken.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-151">Make sure tooreview [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="1ffa9-152">Dikkat toohello en fazla sayıda her VM boyutu destekliyorsa NIC ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-152">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="1ffa9-153">VM varolan Ek NIC tooan eklenemiyor, hello VM dağıttığınızda tüm hello NIC'ler oluşturmalısınız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-153">Remember that you cannot add additional NICs tooan existing VM, you must create all hello NICs when you deploy hello VM.</span></span> <span data-ttu-id="1ffa9-154">Merhaba outset tüm gerekli hello ağ bağlantısı olduğundan emin, dağıtımları toomake planlaması yaparken dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="1ffa9-154">Take care when planning your deployments toomake sure that you have all hello required network connectivity from hello outset.</span></span>

