---
title: "Birden çok NIC ile azure'da bir Linux VM oluşturma | Microsoft Docs"
description: "Azure CLI ya da Resource Manager şablonları ile bağlı birden çok NIC içeren bir Linux VM oluşturmayı öğrenin."
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
ms.openlocfilehash: 814825cce61909167a1247a96c17a3ee9c5f2af4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="8c103-103">Azure CLI 1.0 kullanarak birden çok NIC ile Linux sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c103-103">Create a Linux virtual machine with multiple NICs using the Azure CLI 1.0</span></span>
<span data-ttu-id="8c103-104">Bir sanal makine (VM) bağlı birden çok sanal ağ arabirimlerine (NIC'ler) sahip Azure oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c103-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="8c103-105">Ön uç ve arka uç bağlantısı ya da izleme veya yedekleme çözümü için ayrılmış bir ağ için farklı alt ağlara sahip ortak bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="8c103-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="8c103-106">Bu makalede bağlı birden çok NIC içeren bir VM oluşturmak için hızlı komutları sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c103-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span></span> <span data-ttu-id="8c103-107">Ayrıntılı bilgi için kendi Bash betiklerini içinde birden çok NIC oluşturma dahil olmak üzere daha fazla okuyun hakkında [multi-NIC VM dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8c103-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="8c103-108">Farklı [VM boyutları](sizes.md) NIC'ler değişen çok sayıda desteği, bu nedenle, VM buna göre boyutu.</span><span class="sxs-lookup"><span data-stu-id="8c103-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="8c103-109">Birden çok NIC VM Oluştur - Azure CLI 1.0 ile mevcut bir VM'yi NIC'ler ekleyemezsiniz zaman eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="8c103-109">You must attach multiple NICs when you create a VM - you cannot add NICs to an existing VM with the Azure CLI 1.0.</span></span> <span data-ttu-id="8c103-110">Yapabilecekleriniz [Azure CLI 2.0 ile mevcut bir VM'yi NIC'ler eklemek](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="8c103-110">You can [add NICs to an existing VM with the Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="8c103-111">Ayrıca [özgün sanal diskler üzerinde dayalı bir VM oluşturma](copy-vm.md) ve VM dağıtmak gibi birden çok NIC oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c103-111">You can also [create a VM based on the original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy the VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8c103-112">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="8c103-112">CLI versions to complete the task</span></span>
<span data-ttu-id="8c103-113">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8c103-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="8c103-114">[Azure CLI 1.0](#create-supporting-resources) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="8c103-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8c103-115">[Azure CLI 2.0](multiple-nics.md): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="8c103-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="8c103-116">Destekleyici kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="8c103-116">Create supporting resources</span></span>
<span data-ttu-id="8c103-117">Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI](../../cli-install-nodejs.md) oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="8c103-117">Make sure that you have the [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="8c103-118">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8c103-118">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8c103-119">Örnek parametre adları dahil *myResourceGroup*, *mystorageaccount*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8c103-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="8c103-120">İlk olarak, bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c103-120">First, create a resource group.</span></span> <span data-ttu-id="8c103-121">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="8c103-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="8c103-122">Vm'leriniz tutmak için bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c103-122">Create a storage account to hold your VMs.</span></span> <span data-ttu-id="8c103-123">Aşağıdaki örnek adlı bir depolama hesabı oluşturur *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="8c103-123">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="8c103-124">Vm'leriniz için bağlanmak için bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c103-124">Create a virtual network to connect your VMs to.</span></span> <span data-ttu-id="8c103-125">Aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* bir adres öneki ile *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="8c103-125">The following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="8c103-126">İki sanal ağ alt - oluşturmak ön uç trafik, diğeri arka uç trafiği için.</span><span class="sxs-lookup"><span data-stu-id="8c103-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="8c103-127">Aşağıdaki örnek adlı iki alt ağı oluşturur *mySubnetFrontEnd* ve *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="8c103-127">The following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

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

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="8c103-128">Oluşturma ve birden çok NIC yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8c103-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="8c103-129">Hakkında daha fazla ayrıntı okuyabilirsiniz [Azure CLI kullanarak birden çok NIC dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), tüm NIC'ler oluşturmak için döngü işlemi komut dosyası gibi.</span><span class="sxs-lookup"><span data-stu-id="8c103-129">You can read more details about [deploying multiple NICs using the Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.</span></span>

<span data-ttu-id="8c103-130">Aşağıdaki örnek adlı iki NIC oluşturur *myNic1* ve *myNic2*, her alt ağa bağlanan bir NIC ile:</span><span class="sxs-lookup"><span data-stu-id="8c103-130">The following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting to each subnet:</span></span>

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

<span data-ttu-id="8c103-131">Genellikle, ayrıca oluşturduğunuz bir [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) veya [yük dengeleyici](../../load-balancer/load-balancer-overview.md) yönetmek ve trafik Vm'leriniz arasında dağıtmak amacıyla.</span><span class="sxs-lookup"><span data-stu-id="8c103-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="8c103-132">Aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8c103-132">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="8c103-133">Ağ güvenlik grubu kullanmaya, NIC bağlama `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="8c103-133">Bind your NICs to the Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="8c103-134">Aşağıdaki örnek bağlar *myNic1* ve *myNic2* ile *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8c103-134">The following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

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

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="8c103-135">Bir VM oluşturun ve NIC'ler ekleyin</span><span class="sxs-lookup"><span data-stu-id="8c103-135">Create a VM and attach the NICs</span></span>
<span data-ttu-id="8c103-136">VM oluştururken, artık birden çok NIC belirtin.</span><span class="sxs-lookup"><span data-stu-id="8c103-136">When creating the VM, you now specify multiple NICs.</span></span> <span data-ttu-id="8c103-137">Yerine `--nic-name` tek bir NIC sağlamak için bunun yerine kullandığınız `--nic-names` ve NIC virgülle ayrılmış bir listesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8c103-137">Rather using `--nic-name` to provide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="8c103-138">VM boyutu seçerken dikkatli gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c103-138">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="8c103-139">Bir VM'ye ekleyebilirsiniz NIC toplam sayısına yönelik sınırlar vardır.</span><span class="sxs-lookup"><span data-stu-id="8c103-139">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="8c103-140">Daha fazla bilgi edinin [Linux VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="8c103-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="8c103-141">Aşağıdaki örnek, birden çok NIC ve birden çok NIC kullanarak destekleyen bir VM boyutu belirtmek üzere gösterilmektedir (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="8c103-141">The following example shows how to specify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

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

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="8c103-142">Resource Manager şablonları kullanarak birden çok NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="8c103-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="8c103-143">Azure Resource Manager şablonları bildirim temelli JSON dosyaları ortamınızı tanımlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="8c103-143">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="8c103-144">Okuyabilirsiniz bir [genel bakış Azure Kaynak Yöneticisi'nin](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8c103-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="8c103-145">Resource Manager şablonları birden çok NIC oluşturma gibi dağıtımı sırasında bir kaynağın birden çok örneğini oluşturmak için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c103-145">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="8c103-146">Kullandığınız *kopyalama* oluşturmak için örnek sayısını belirtmek için:</span><span class="sxs-lookup"><span data-stu-id="8c103-146">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="8c103-147">Daha fazla bilgi edinin [kullanarak birden çok örneği oluşturma *kopya*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8c103-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="8c103-148">Aynı zamanda bir `copyIndex()` oluşturmanıza olanak tanıyan bir kaynak adı için bir sayı sonuna eklemek için `myNic1`, `myNic2`vb.. Dizin değeri ekleyerek bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="8c103-148">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="8c103-149">Tam örnek okuyabilirsiniz [Resource Manager şablonları kullanarak birden çok NIC oluşturma](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="8c103-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c103-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8c103-150">Next steps</span></span>
<span data-ttu-id="8c103-151">Gözden geçirdiğinizden emin olun [Linux VM boyutları](sizes.md) birden çok NIC ile VM oluşturmaya çalışırken.</span><span class="sxs-lookup"><span data-stu-id="8c103-151">Make sure to review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="8c103-152">Her VM boyutu destekliyorsa NIC sayısı dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8c103-152">Pay attention to the maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="8c103-153">Var olan bir VM için ek NIC'lerin eklenemiyor, VM dağıttığınızda tüm NIC'ler oluşturmalısınız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8c103-153">Remember that you cannot add additional NICs to an existing VM, you must create all the NICs when you deploy the VM.</span></span> <span data-ttu-id="8c103-154">Dağıtımlarınızı başından itibaren hedeflenen tüm gerekli ağ bağlantısı olduğundan emin olmak için planlama yaparken dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="8c103-154">Take care when planning your deployments to make sure that you have all the required network connectivity from the outset.</span></span>

