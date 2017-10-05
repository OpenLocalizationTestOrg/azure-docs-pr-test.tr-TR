---
title: "Mevcut ağ Azure CLI 1.0 ile içine Linux VM'ler dağıtma | Microsoft Docs"
description: "Bir varolan sanal Azure CLI 1.0 kullanarak ağınıza bir Linux VM dağıtma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a><span data-ttu-id="44bc0-103">Mevcut Azure sanal ağda Azure CLI 1.0 ile Linux sanal makine dağıtma</span><span class="sxs-lookup"><span data-stu-id="44bc0-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI 1.0</span></span>

<span data-ttu-id="44bc0-104">Bu makalede Azure CLI 1.0 var olan bir sanal ağa (VNet) sanal makine (VM) dağıtmak için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="44bc0-104">This article shows you how to use Azure CLI 1.0 to deploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="44bc0-105">Gereksinimler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="44bc0-105">The requirements are:</span></span>

- [<span data-ttu-id="44bc0-106">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="44bc0-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="44bc0-107">SSH ortak ve özel anahtar dosyaları</span><span class="sxs-lookup"><span data-stu-id="44bc0-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="44bc0-108">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="44bc0-108">CLI versions to complete the task</span></span>
<span data-ttu-id="44bc0-109">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="44bc0-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="44bc0-110">[Azure CLI 1.0](#quick-commands) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="44bc0-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="44bc0-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="44bc0-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="44bc0-112">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="44bc0-112">Quick Commands</span></span>

<span data-ttu-id="44bc0-113">Hızlı bir şekilde görevi gerçekleştirmek gerekiyorsa, aşağıdaki bölümde gerekli komutları ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="44bc0-113">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="44bc0-114">Her adım, belgenin geri kalanında bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="44bc0-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="44bc0-115">Ön gereksinimlerini: SSH ile kaynak grubu, VNet, NSG gelen, alt ağ.</span><span class="sxs-lookup"><span data-stu-id="44bc0-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="44bc0-116">Tüm örnekleri kendi ayarlarınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="44bc0-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="44bc0-117">VM sanal ağ altyapısını dağıtma</span><span class="sxs-lookup"><span data-stu-id="44bc0-117">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="44bc0-118">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="44bc0-118">Detailed walkthrough</span></span>

<span data-ttu-id="44bc0-119">Sanal ağlar Azure varlıklar gibi ve ağ güvenlik grupları nadiren dağıtılan kaynakları uzun ömürlü ve statik olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44bc0-119">Azure assets like the VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="44bc0-120">Bir VNet dağıtıldıktan sonra hiçbir olumsuz etkiler altyapısı olmadan yeni dağıtımlar tarafından yeniden.</span><span class="sxs-lookup"><span data-stu-id="44bc0-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="44bc0-121">Geleneksel donanım ağ anahtarı olarak VNet düşünün.</span><span class="sxs-lookup"><span data-stu-id="44bc0-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="44bc0-122">Yepyeni bir donanım anahtarı ile her bir dağıtım yapılandırmak ihtiyaç duymaz.</span><span class="sxs-lookup"><span data-stu-id="44bc0-122">You would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="44bc0-123">Doğru yapılandırılmış bir VNet ile birlikte, yeni sunucuları bu Vnet'i tekrar tekrar VNet ömrü boyunca gereken birkaç varsa, değişikliklerle dağıtmak, devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44bc0-123">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="44bc0-124">Kaynak grubunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="44bc0-124">Create the resource group</span></span>

<span data-ttu-id="44bc0-125">İlk olarak, bu kılavuzda oluşturduğunuz her şeyi düzenlemek için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44bc0-125">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="44bc0-126">Kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="44bc0-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a><span data-ttu-id="44bc0-127">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="44bc0-127">Create the VNet</span></span>

<span data-ttu-id="44bc0-128">İlk adım, içine sanal makineleri başlatmak için bir VNet oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="44bc0-128">The first step is to build a VNet to launch the VMs into.</span></span> <span data-ttu-id="44bc0-129">Sanal ağ Bu izlenecek yol için bir alt ağ içerir.</span><span class="sxs-lookup"><span data-stu-id="44bc0-129">The VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="44bc0-130">Azure sanal ağlar hakkında daha fazla bilgi için bkz: [Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="44bc0-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="44bc0-131">Ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="44bc0-131">Create the network security group</span></span>

<span data-ttu-id="44bc0-132">Alt ardındaki var olan bir ağda yerleşik güvenlik grubu böylece alt önce ağ güvenlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44bc0-132">The subnet is built behind an existing network security group so build the network security group before the subnet.</span></span> <span data-ttu-id="44bc0-133">Azure ağ güvenlik grupları, bir Güvenlik Duvarı'nı ağ katmanında eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="44bc0-133">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="44bc0-134">Azure ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [ağ güvenlik grupları Azure CLI oluşturma](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="44bc0-134">For more information on Azure network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="44bc0-135">Gelen bir SSH izin ver Kuralı Ekle</span><span class="sxs-lookup"><span data-stu-id="44bc0-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="44bc0-136">Gelen bağlantı noktası 22 trafiği ağ üzerinden bağlantı noktası 22 VM geçirilmesine izin veren bir kural gerektiği şekilde VM internet erişimi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="44bc0-136">The VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="44bc0-137">Sanal ağ için bir alt ağ Ekle</span><span class="sxs-lookup"><span data-stu-id="44bc0-137">Add a subnet to the VNet</span></span>

<span data-ttu-id="44bc0-138">Sanal ağ içindeki VM'ler bir alt ağda bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44bc0-138">VMs within the VNet must be located in a subnet.</span></span> <span data-ttu-id="44bc0-139">Her sanal ağ birden çok alt ağa sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="44bc0-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="44bc0-140">Alt ağ oluşturmak ve ağ güvenlik grubuyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="44bc0-140">Create the subnet and associate with the network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="44bc0-141">Alt ağ şimdi VNet eklenir ve ağ güvenlik grubu ve kuralı ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="44bc0-141">The Subnet is now added inside the VNet and associated with the network security group and rule.</span></span>


## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="44bc0-142">Alt ağ için bir Vnıc'teki Ekle</span><span class="sxs-lookup"><span data-stu-id="44bc0-142">Add a VNic to the subnet</span></span>

<span data-ttu-id="44bc0-143">Sanal ağ kartları (VNics), bunları farklı VM'ler bağlanarak yeniden gibi önemlidir.</span><span class="sxs-lookup"><span data-stu-id="44bc0-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="44bc0-144">Bu yaklaşım VM'ler geçici olarak olabileceği Vnıc statik bir kaynak olarak tutar.</span><span class="sxs-lookup"><span data-stu-id="44bc0-144">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="44bc0-145">Bir Vnıc'teki oluşturun ve önceki adımda oluşturduğunuz alt ağ ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="44bc0-145">Create a VNic and associate it with the subnet created in the previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="44bc0-146">VNet ve NSG halinde VM dağıtma</span><span class="sxs-lookup"><span data-stu-id="44bc0-146">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="44bc0-147">Artık bir VNet ve alt ağ, VNet ve alt ağ için SSH bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek korumak için davranan bir ağ güvenlik grubu içinde vardır.</span><span class="sxs-lookup"><span data-stu-id="44bc0-147">You now have a VNet and subnet inside that VNet, and a network security group acting to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="44bc0-148">VM şimdi bu mevcut ağ altyapınızda içinde dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="44bc0-148">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="44bc0-149">Azure CLI kullanarak ve `azure vm create` komutu, var olan Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc için Linux VM dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="44bc0-149">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="44bc0-150">Tam bir VM'yi dağıtmak için CLI kullanma ile ilgili daha fazla bilgi için bkz: [Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="44bc0-150">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="44bc0-151">Var olan kaynakları çağırmak için CLI bayrakları kullanarak, varolan ağ içindeki VM dağıtmak için Azure isteyin.</span><span class="sxs-lookup"><span data-stu-id="44bc0-151">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="44bc0-152">Bir VNet ve alt ağ dağıtıldıktan sonra Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="44bc0-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="44bc0-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44bc0-153">Next steps</span></span>

* [<span data-ttu-id="44bc0-154">Belirli bir dağıtımı oluşturmak için Azure Resource Manager şablonu kullanma</span><span class="sxs-lookup"><span data-stu-id="44bc0-154">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="44bc0-155">Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="44bc0-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="44bc0-156">Şablonları kullanarak Azure'da bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="44bc0-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
