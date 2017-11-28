---
title: "birden çok NIC ile azure'da bir Linux VM aaaCreate | Microsoft Docs"
description: "Toocreate birden çok NIC içeren bir Linux VM hello Azure CLI 2.0 veya Resource Manager şablonları kullanarak tooit nasıl bağlı öğrenin."
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
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="2c34e-103">Nasıl toocreate Linux sahip bir sanal makine azure'da birden çok ağ arabirim kartları</span><span class="sxs-lookup"><span data-stu-id="2c34e-103">How toocreate a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="2c34e-104">Birden çok sanal ağ arabirimlerine (NIC'ler) bağlı tooit sahip Azure'da bir sanal makine (VM) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c34e-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="2c34e-105">Yaygın bir senaryo toohave farklı alt ağlar için ön uç ve arka uç bağlantısı olan veya ayrılmış bir ağ tooa izleme veya yedekleme çözümü.</span><span class="sxs-lookup"><span data-stu-id="2c34e-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="2c34e-106">Bu makalede tooit toocreate birden çok NIC içeren bir VM ekli nasıl ve ne ayrıntıları tooadd veya kaldırma NIC var olan bir VM'den.</span><span class="sxs-lookup"><span data-stu-id="2c34e-106">This article details how toocreate a VM with multiple NICs attached tooit and how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="2c34e-107">Ayrıntılı bilgi için kendi içinde birden çok NIC nasıl toocreate Bash de dahil olmak üzere komut dosyaları, daha fazla okuyun hakkında [multi-NIC VM dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2c34e-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="2c34e-108">Farklı [VM boyutları](sizes.md) NIC'ler değişen çok sayıda desteği, bu nedenle, VM buna göre boyutu.</span><span class="sxs-lookup"><span data-stu-id="2c34e-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="2c34e-109">Bu makalede nasıl toocreate VM ile birden çok NIC içeren bir hello Azure CLI 2.0 ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2c34e-109">This article details how toocreate a VM with multiple NICs with hello Azure CLI 2.0.</span></span> <span data-ttu-id="2c34e-110">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2c34e-110">You can also perform these steps with hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="2c34e-111">Destekleyici kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="2c34e-111">Create supporting resources</span></span>
<span data-ttu-id="2c34e-112">Son yükleme hello [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="2c34e-112">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="2c34e-113">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2c34e-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2c34e-114">Örnek parametre adları dahil *myResourceGroup*, *mystorageaccount*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="2c34e-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="2c34e-115">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="2c34e-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2c34e-116">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="2c34e-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="2c34e-117">Merhaba sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="2c34e-117">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="2c34e-118">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ve adlı alt ağ *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="2c34e-118">hello following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="2c34e-119">Merhaba arka uç trafiği için bir alt ağ oluşturmak [az ağ sanal alt oluşturma](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="2c34e-119">Create a subnet for hello back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="2c34e-120">Merhaba aşağıdaki örnek adlı bir alt ağı oluşturur *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="2c34e-120">hello following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="2c34e-121">Bir ağ güvenlik grubu oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="2c34e-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="2c34e-122">Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="2c34e-122">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="2c34e-123">Oluşturma ve birden çok NIC yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2c34e-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="2c34e-124">İki NIC ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="2c34e-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="2c34e-125">Merhaba aşağıdaki örnekte oluşturur adlı iki NIC *myNic1* ve *myNic2*, bağlı tooeach alt ağı bağlayan bir NIC ile Merhaba ağ güvenlik grubu:</span><span class="sxs-lookup"><span data-stu-id="2c34e-125">hello following example creates two NICs, named *myNic1* and *myNic2*, connected hello network security group, with one NIC connecting tooeach subnet:</span></span>

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

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="2c34e-126">Bir VM oluşturun ve hello NIC ekleme</span><span class="sxs-lookup"><span data-stu-id="2c34e-126">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="2c34e-127">Merhaba NIC'ler belirtin hello VM oluşturduğunuzda ile oluşturulan `--nics`.</span><span class="sxs-lookup"><span data-stu-id="2c34e-127">When you create hello VM, specify hello NICs you created with `--nics`.</span></span> <span data-ttu-id="2c34e-128">Merhaba VM boyutu seçtiğinizde tootake dikkatli da gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c34e-128">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="2c34e-129">Merhaba tooa VM ekleyebilirsiniz NIC toplam sayısına yönelik sınırlar vardır.</span><span class="sxs-lookup"><span data-stu-id="2c34e-129">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="2c34e-130">Daha fazla bilgi edinin [Linux VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="2c34e-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="2c34e-131">[az vm create](/cli/azure/vm#create) ile bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c34e-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2c34e-132">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM*:</span><span class="sxs-lookup"><span data-stu-id="2c34e-132">hello following example creates a VM named *myVM*:</span></span>

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

## <a name="add-a-nic-tooa-vm"></a><span data-ttu-id="2c34e-133">NIC tooa VM ekleme</span><span class="sxs-lookup"><span data-stu-id="2c34e-133">Add a NIC tooa VM</span></span>
<span data-ttu-id="2c34e-134">Merhaba önceki adımları bir VM ile birden çok NIC oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2c34e-134">hello previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="2c34e-135">Azure CLI 2.0 hello ile VM varolan NIC'ler tooan de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c34e-135">You can also add NICs tooan existing VM with hello Azure CLI 2.0.</span></span> 

<span data-ttu-id="2c34e-136">Başka bir NIC ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="2c34e-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="2c34e-137">Merhaba aşağıdaki örnekte oluşturur adlı bir NIC *myNic3* bağlı toohello arka uç alt ağı ve hello önceki adımlarda oluşturduğunuz ağ güvenlik grubu:</span><span class="sxs-lookup"><span data-stu-id="2c34e-137">hello following example creates a NIC named *myNic3* connected toohello back-end subnet and network security group created in hello previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="2c34e-138">tooadd NIC tooan var olan VM ilk ayırması VM ile Merhaba [az vm serbest bırakma](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="2c34e-138">tooadd a NIC tooan existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="2c34e-139">Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="2c34e-139">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="2c34e-140">Ekleme NIC ile Merhaba [az vm NIC eklemeniz](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="2c34e-140">Add hello NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="2c34e-141">Merhaba aşağıdaki örnek, *myNic3* çok*myVM*:</span><span class="sxs-lookup"><span data-stu-id="2c34e-141">hello following example adds *myNic3* too*myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="2c34e-142">Başlangıç VM ile Merhaba [az vm başlangıç](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="2c34e-142">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="2c34e-143">Bir NIC bir sanal makineden kaldırın</span><span class="sxs-lookup"><span data-stu-id="2c34e-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="2c34e-144">Mevcut bir VM'yi NIC'den tooremove ilk hello VM serbest bırakma ile [az vm serbest bırakma](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="2c34e-144">tooremove a NIC from an existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="2c34e-145">Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="2c34e-145">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="2c34e-146">Kaldırma NIC ile Merhaba [az vm NIC kaldırmak](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="2c34e-146">Remove hello NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="2c34e-147">Merhaba aşağıdaki örnek kaldırır *myNic3* gelen *myVM*:</span><span class="sxs-lookup"><span data-stu-id="2c34e-147">hello following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="2c34e-148">Başlangıç VM ile Merhaba [az vm başlangıç](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="2c34e-148">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="2c34e-149">Resource Manager şablonları kullanarak birden çok NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="2c34e-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="2c34e-150">Azure Resource Manager şablonları bildirim temelli JSON dosyaları toodefine ortamınız kullanın.</span><span class="sxs-lookup"><span data-stu-id="2c34e-150">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="2c34e-151">Okuyabilirsiniz bir [genel bakış Azure Kaynak Yöneticisi'nin](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c34e-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="2c34e-152">Resource Manager şablonları bir şekilde toocreate birden çok NIC oluşturma gibi dağıtım işlemi sırasında birden fazla örneğini bir kaynak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2c34e-152">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="2c34e-153">Kullandığınız *kopya* toospecify hello örnekleri toocreate sayısı:</span><span class="sxs-lookup"><span data-stu-id="2c34e-153">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="2c34e-154">Daha fazla bilgi edinin [kullanarak birden çok örneği oluşturma *kopya*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2c34e-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="2c34e-155">De kullanabilirsiniz bir `copyIndex()` toothen sona toocreate sağlayan bir numara tooa kaynak adı `myNic1`, `myNic2`, vb. hello aşağıdaki hello dizin değeri ekleyerek bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="2c34e-155">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="2c34e-156">Tam örnek okuyabilirsiniz [Resource Manager şablonları kullanarak birden çok NIC oluşturma](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="2c34e-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c34e-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c34e-157">Next steps</span></span>
<span data-ttu-id="2c34e-158">Gözden geçirme [Linux VM boyutları](sizes.md) toocreating birden çok NIC içeren bir VM çalışırken.</span><span class="sxs-lookup"><span data-stu-id="2c34e-158">Review [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="2c34e-159">Dikkat toohello en fazla sayıda her VM boyutu destekliyorsa NIC ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="2c34e-159">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 
