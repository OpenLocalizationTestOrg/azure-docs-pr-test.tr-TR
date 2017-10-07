---
title: "mevcut ağ Azure CLI 1.0 ile içine aaaDeploy Linux VM'ler | Microsoft Docs"
description: "Nasıl toodeploy kullanarak varolan bir sanal ağ içinde bir Linux VM hello Azure CLI 1.0"
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
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a><span data-ttu-id="19fc0-103">Nasıl toodeploy mevcut Azure sanal ağda hello Azure CLI 1.0 ile Linux sanal makine</span><span class="sxs-lookup"><span data-stu-id="19fc0-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI 1.0</span></span>

<span data-ttu-id="19fc0-104">Bu makale size nasıl gösterir toouse Azure CLI 1.0 toodeploy mevcut sanal ağda (VNet) sanal makine (VM).</span><span class="sxs-lookup"><span data-stu-id="19fc0-104">This article shows you how toouse Azure CLI 1.0 toodeploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="19fc0-105">Hello gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="19fc0-105">hello requirements are:</span></span>

- [<span data-ttu-id="19fc0-106">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="19fc0-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="19fc0-107">SSH ortak ve özel anahtar dosyaları</span><span class="sxs-lookup"><span data-stu-id="19fc0-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="19fc0-108">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="19fc0-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="19fc0-109">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="19fc0-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="19fc0-110">[Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="19fc0-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="19fc0-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="19fc0-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="19fc0-112">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="19fc0-112">Quick Commands</span></span>

<span data-ttu-id="19fc0-113">Tooquickly gerekiyorsa hello görevi, gerekli hello komutları bölümden hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="19fc0-113">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="19fc0-114">Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="19fc0-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="19fc0-115">Ön gereksinimlerini: SSH ile kaynak grubu, VNet, NSG gelen, alt ağ.</span><span class="sxs-lookup"><span data-stu-id="19fc0-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="19fc0-116">Tüm örnekleri kendi ayarlarınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="19fc0-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="19fc0-117">Merhaba VM hello sanal ağ altyapısıyla dağıtma</span><span class="sxs-lookup"><span data-stu-id="19fc0-117">Deploy hello VM into hello virtual network infrastructure</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="19fc0-118">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="19fc0-118">Detailed walkthrough</span></span>

<span data-ttu-id="19fc0-119">Azure varlıklar hello sanal ağlar gibi ve ağ güvenlik grupları nadiren dağıtılan kaynakları uzun ömürlü ve statik olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="19fc0-119">Azure assets like hello VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="19fc0-120">Bir VNet dağıtıldıktan sonra herhangi bir olumsuz etkiler toohello altyapı olmadan yeni dağıtımlar tarafından yeniden.</span><span class="sxs-lookup"><span data-stu-id="19fc0-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="19fc0-121">Geleneksel donanım ağ anahtarı olarak VNet düşünün.</span><span class="sxs-lookup"><span data-stu-id="19fc0-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="19fc0-122">Yeni donanım ile her bir dağıtım geçiş tooconfigure ihtiyaç duymaz.</span><span class="sxs-lookup"><span data-stu-id="19fc0-122">You would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="19fc0-123">Doğru yapılandırılmış bir VNet ile birlikte toodeploy yeni sunucuları bu sanal ağ içinde tekrar tekrar hello VNet hello ömrü boyunca gereken birkaç varsa, değişikliklerle devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19fc0-123">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="19fc0-124">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="19fc0-124">Create hello resource group</span></span>

<span data-ttu-id="19fc0-125">İlk olarak, bir kaynak grubu tooorganize bu kılavuzda oluşturduğunuz her şeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19fc0-125">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="19fc0-126">Kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="19fc0-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="19fc0-127">Merhaba VNet oluşturma</span><span class="sxs-lookup"><span data-stu-id="19fc0-127">Create hello VNet</span></span>

<span data-ttu-id="19fc0-128">Merhaba ilk VNet toolaunch hello VM'ler içine toobuild adımdır.</span><span class="sxs-lookup"><span data-stu-id="19fc0-128">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="19fc0-129">Merhaba VNet Bu izlenecek yol için bir alt ağ içerir.</span><span class="sxs-lookup"><span data-stu-id="19fc0-129">hello VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="19fc0-130">Azure sanal ağlar hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="19fc0-130">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="19fc0-131">Merhaba ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="19fc0-131">Create hello network security group</span></span>

<span data-ttu-id="19fc0-132">Merhaba alt varolan bir ağ güvenlik grubu yerleşik şekilde hello alt önce hello ağ güvenlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19fc0-132">hello subnet is built behind an existing network security group so build hello network security group before hello subnet.</span></span> <span data-ttu-id="19fc0-133">Azure ağ güvenlik grupları hello ağ katmanı eşdeğer tooa güvenlik duvarında değildir.</span><span class="sxs-lookup"><span data-stu-id="19fc0-133">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="19fc0-134">Azure ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [nasıl hello Azure CLI toocreate ağ güvenlik grupları](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="19fc0-134">For more information on Azure network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="19fc0-135">Gelen bir SSH izin ver Kuralı Ekle</span><span class="sxs-lookup"><span data-stu-id="19fc0-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="19fc0-136">Merhaba VM gelen bağlantı noktası 22 trafiği toobe veren bir kural hello ağ tooport 22 hello VM üzerinde geçirilen şekilde Internet gerekli hello erişimden gerekir.</span><span class="sxs-lookup"><span data-stu-id="19fc0-136">hello VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span>

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

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="19fc0-137">Bir alt ağ toohello VNet ekleme</span><span class="sxs-lookup"><span data-stu-id="19fc0-137">Add a subnet toohello VNet</span></span>

<span data-ttu-id="19fc0-138">VM'ler hello VNet içindeki bir alt ağda bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="19fc0-138">VMs within hello VNet must be located in a subnet.</span></span> <span data-ttu-id="19fc0-139">Her sanal ağ birden çok alt ağa sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="19fc0-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="19fc0-140">Merhaba alt ağı oluşturup hello ağ güvenlik grubuyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="19fc0-140">Create hello subnet and associate with hello network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="19fc0-141">Merhaba alt şimdi hello VNet eklenir ve hello ağ güvenlik grubu ve kuralı ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="19fc0-141">hello Subnet is now added inside hello VNet and associated with hello network security group and rule.</span></span>


## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="19fc0-142">Vnıc toohello alt ağ Ekle</span><span class="sxs-lookup"><span data-stu-id="19fc0-142">Add a VNic toohello subnet</span></span>

<span data-ttu-id="19fc0-143">Sanal ağ kartları (VNics), bunları toodifferent VM'ler bağlanarak yeniden gibi önemlidir.</span><span class="sxs-lookup"><span data-stu-id="19fc0-143">Virtual network cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="19fc0-144">Bu yaklaşım Hello VM'ler geçici olarak olabileceği hello Vnıc statik bir kaynak olarak tutar.</span><span class="sxs-lookup"><span data-stu-id="19fc0-144">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="19fc0-145">Bir Vnıc'teki oluşturup hello önceki adımda oluşturduğunuz hello alt ağı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="19fc0-145">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="19fc0-146">Merhaba VM hello VNet içine ve NSG dağıtma</span><span class="sxs-lookup"><span data-stu-id="19fc0-146">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="19fc0-147">Artık bir VNet ve alt ağ, sanal ağ ve SSH için bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek tooprotect hello alt davranan bir ağ güvenlik grubu içinde vardır.</span><span class="sxs-lookup"><span data-stu-id="19fc0-147">You now have a VNet and subnet inside that VNet, and a network security group acting tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="19fc0-148">Merhaba VM şimdi bu mevcut ağ altyapınızda içinde dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="19fc0-148">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="19fc0-149">Kullanarak Azure CLI hello ve hello `azure vm create` hello Linux VM olan Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc varolan dağıtılan toohello komutu.</span><span class="sxs-lookup"><span data-stu-id="19fc0-149">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="19fc0-150">Hello CLI toodeploy tam VM kullanma hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="19fc0-150">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md)</span></span>

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

<span data-ttu-id="19fc0-151">Hello kullanarak CLI toocall var olan kaynakların çıkışı hello mevcut ağ içinde Azure toodeploy hello VM toplamasını işaretler.</span><span class="sxs-lookup"><span data-stu-id="19fc0-151">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="19fc0-152">Bir VNet ve alt ağ dağıtıldıktan sonra Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="19fc0-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="19fc0-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19fc0-153">Next steps</span></span>

* [<span data-ttu-id="19fc0-154">Azure Resource Manager şablonu toocreate belirli bir dağıtım kullanın</span><span class="sxs-lookup"><span data-stu-id="19fc0-154">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="19fc0-155">Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="19fc0-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="19fc0-156">Şablonları kullanarak Azure'da bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="19fc0-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
