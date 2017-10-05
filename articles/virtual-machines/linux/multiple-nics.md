---
title: "Birden çok NIC ile azure'da bir Linux VM oluşturma | Microsoft Docs"
description: "Azure CLI 2.0 veya Resource Manager şablonları ile bağlı birden çok NIC içeren bir Linux VM oluşturmayı öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8a2931e462079c101c91497d459d7d3126234244
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="46d59-103">Linux sanal makine Azure'da ile birden fazla ağ arabirimi kartları oluşturma</span><span class="sxs-lookup"><span data-stu-id="46d59-103">How to create a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="46d59-104">Bir sanal makine (VM) bağlı birden çok sanal ağ arabirimlerine (NIC'ler) sahip Azure oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46d59-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="46d59-105">Ön uç ve arka uç bağlantısı ya da izleme veya yedekleme çözümü için ayrılmış bir ağ için farklı alt ağlara sahip ortak bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="46d59-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="46d59-106">Bu makalede, bağlı birden çok NIC içeren bir VM oluşturma ve ekleme veya NIC var olan bir sanal makineden kaldırın ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="46d59-106">This article details how to create a VM with multiple NICs attached to it and how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="46d59-107">Ayrıntılı bilgi için kendi Bash betiklerini içinde birden çok NIC oluşturma dahil olmak üzere daha fazla okuyun hakkında [multi-NIC VM dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="46d59-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="46d59-108">Farklı [VM boyutları](sizes.md) NIC'ler değişen çok sayıda desteği, bu nedenle, VM buna göre boyutu.</span><span class="sxs-lookup"><span data-stu-id="46d59-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="46d59-109">Bu makalede Azure CLI 2.0 ile birden çok NIC içeren bir VM oluşturmak nasıl ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="46d59-109">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span></span> <span data-ttu-id="46d59-110">Bu adımları [Azure CLI 1.0](multiple-nics-nodejs.md) ile de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46d59-110">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="46d59-111">Destekleyici kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="46d59-111">Create supporting resources</span></span>
<span data-ttu-id="46d59-112">En son yükleme [Azure CLI 2.0](/cli/azure/install-az-cli2) ve bir Azure hesabı kullanarak oturum açma [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="46d59-112">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="46d59-113">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="46d59-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="46d59-114">Örnek parametre adları dahil *myResourceGroup*, *mystorageaccount*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="46d59-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="46d59-115">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="46d59-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="46d59-116">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="46d59-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="46d59-117">İle sanal ağ oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="46d59-117">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="46d59-118">Aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ve adlı alt ağ *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="46d59-118">The following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="46d59-119">Arka uç trafiği için bir alt ağ oluşturmak [az ağ sanal alt oluşturma](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="46d59-119">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="46d59-120">Aşağıdaki örnek adlı bir alt ağı oluşturur *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="46d59-120">The following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="46d59-121">Bir ağ güvenlik grubu oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="46d59-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="46d59-122">Aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="46d59-122">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="46d59-123">Oluşturma ve birden çok NIC yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46d59-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="46d59-124">İki NIC ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="46d59-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="46d59-125">Aşağıdaki örnek adlı iki NIC oluşturur *myNic1* ve *myNic2*, her alt ağa bağlanan bir NIC ile ağ güvenlik grubu bağlı:</span><span class="sxs-lookup"><span data-stu-id="46d59-125">The following example creates two NICs, named *myNic1* and *myNic2*, connected the network security group, with one NIC connecting to each subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="46d59-126">Bir VM oluşturun ve NIC'ler ekleyin</span><span class="sxs-lookup"><span data-stu-id="46d59-126">Create a VM and attach the NICs</span></span>
<span data-ttu-id="46d59-127">İle oluşturulan NIC'ler belirtin VM oluşturduğunuzda `--nics`.</span><span class="sxs-lookup"><span data-stu-id="46d59-127">When you create the VM, specify the NICs you created with `--nics`.</span></span> <span data-ttu-id="46d59-128">VM boyutu seçerken dikkatli gerekir.</span><span class="sxs-lookup"><span data-stu-id="46d59-128">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="46d59-129">Bir VM'ye ekleyebilirsiniz NIC toplam sayısına yönelik sınırlar vardır.</span><span class="sxs-lookup"><span data-stu-id="46d59-129">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="46d59-130">Daha fazla bilgi edinin [Linux VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="46d59-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="46d59-131">[az vm create](/cli/azure/vm#create) ile bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="46d59-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="46d59-132">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur *myVM*:</span><span class="sxs-lookup"><span data-stu-id="46d59-132">The following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-to-a-vm"></a><span data-ttu-id="46d59-133">Bir VM için bir NIC eklemeniz</span><span class="sxs-lookup"><span data-stu-id="46d59-133">Add a NIC to a VM</span></span>
<span data-ttu-id="46d59-134">Önceki adımları bir VM ile birden çok NIC oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="46d59-134">The previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="46d59-135">Azure CLI 2.0 ile mevcut bir VM'yi NIC'ler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46d59-135">You can also add NICs to an existing VM with the Azure CLI 2.0.</span></span> 

<span data-ttu-id="46d59-136">Başka bir NIC ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="46d59-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="46d59-137">Aşağıdaki örnek, adlandırılmış bir NIC oluşturur *myNic3* önceki adımlarda oluşturduğunuz arka uç alt ağı ve ağ güvenlik grubuna bağlı:</span><span class="sxs-lookup"><span data-stu-id="46d59-137">The following example creates a NIC named *myNic3* connected to the back-end subnet and network security group created in the previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="46d59-138">Mevcut bir VM'yi bir NIC eklemek için önce VM ile serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="46d59-138">To add a NIC to an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="46d59-139">Aşağıdaki örnek adlı VM kaldırır *myVM*:</span><span class="sxs-lookup"><span data-stu-id="46d59-139">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="46d59-140">NIC ekleme [az vm NIC eklemeniz](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="46d59-140">Add the NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="46d59-141">Aşağıdaki örnek, *myNic3* için *myVM*:</span><span class="sxs-lookup"><span data-stu-id="46d59-141">The following example adds *myNic3* to *myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="46d59-142">VM Başlat [az vm başlangıç](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="46d59-142">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="46d59-143">Bir NIC bir sanal makineden kaldırın</span><span class="sxs-lookup"><span data-stu-id="46d59-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="46d59-144">Bir NIC var olan bir sanal makineden kaldırmak için ilk VM ile serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="46d59-144">To remove a NIC from an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="46d59-145">Aşağıdaki örnek adlı VM kaldırır *myVM*:</span><span class="sxs-lookup"><span data-stu-id="46d59-145">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="46d59-146">NIC ile Kaldır [az vm NIC kaldırmak](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="46d59-146">Remove the NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="46d59-147">Aşağıdaki örnek kaldırır *myNic3* gelen *myVM*:</span><span class="sxs-lookup"><span data-stu-id="46d59-147">The following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="46d59-148">VM Başlat [az vm başlangıç](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="46d59-148">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="46d59-149">Resource Manager şablonları kullanarak birden çok NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="46d59-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="46d59-150">Azure Resource Manager şablonları bildirim temelli JSON dosyaları ortamınızı tanımlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="46d59-150">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="46d59-151">Okuyabilirsiniz bir [genel bakış Azure Kaynak Yöneticisi'nin](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46d59-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="46d59-152">Resource Manager şablonları birden çok NIC oluşturma gibi dağıtımı sırasında bir kaynağın birden çok örneğini oluşturmak için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="46d59-152">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="46d59-153">Kullandığınız *kopyalama* oluşturmak için örnek sayısını belirtmek için:</span><span class="sxs-lookup"><span data-stu-id="46d59-153">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="46d59-154">Daha fazla bilgi edinin [kullanarak birden çok örneği oluşturma *kopya*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="46d59-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="46d59-155">Aynı zamanda bir `copyIndex()` oluşturmanıza olanak tanıyan bir kaynak adı için bir sayı sonuna eklemek için `myNic1`, `myNic2`vb.. Dizin değeri ekleyerek bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="46d59-155">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="46d59-156">Tam örnek okuyabilirsiniz [Resource Manager şablonları kullanarak birden çok NIC oluşturma](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="46d59-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46d59-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46d59-157">Next steps</span></span>
<span data-ttu-id="46d59-158">Gözden geçirme [Linux VM boyutları](sizes.md) birden çok NIC ile VM oluşturmaya çalışırken.</span><span class="sxs-lookup"><span data-stu-id="46d59-158">Review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="46d59-159">Her VM boyutu destekliyorsa NIC sayısı dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="46d59-159">Pay attention to the maximum number of NICs each VM size supports.</span></span> 