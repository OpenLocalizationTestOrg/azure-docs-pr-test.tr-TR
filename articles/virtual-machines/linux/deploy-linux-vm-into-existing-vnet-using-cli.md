---
title: "mevcut ağ Azure CLI 2.0 ile içine aaaDeploy Linux VM'ler | Microsoft Docs"
description: "Nasıl toodeploy kullanarak varolan bir sanal ağ içinde Linux sanal makine hello Azure CLI 2.0 öğrenin"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a><span data-ttu-id="54dae-103">Nasıl toodeploy mevcut Azure sanal ağda hello Azure CLI ile Linux sanal makine</span><span class="sxs-lookup"><span data-stu-id="54dae-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI</span></span>

<span data-ttu-id="54dae-104">Bu makale size nasıl toouse hello Azure CLI 2.0 toodeploy bir sanal makine (VM) var olan bir sanal ağı gösterir.</span><span class="sxs-lookup"><span data-stu-id="54dae-104">This article shows you how toouse hello Azure CLI 2.0 toodeploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="54dae-105">Hello gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="54dae-105">hello requirements are:</span></span>

- [<span data-ttu-id="54dae-106">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="54dae-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="54dae-107">SSH ortak ve özel anahtar dosyaları</span><span class="sxs-lookup"><span data-stu-id="54dae-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="54dae-108">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="54dae-108">You can also perform these steps with hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="54dae-109">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="54dae-109">Quick Commands</span></span>
<span data-ttu-id="54dae-110">Tooquickly gerekiyorsa hello görevi, gerekli hello komutları bölümden hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="54dae-110">If you need tooquickly accomplish hello task, hello following section details hello  commands needed.</span></span> <span data-ttu-id="54dae-111">Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="54dae-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="54dae-112">toocreate bu özel ortam hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="54dae-112">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="54dae-113">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="54dae-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="54dae-114">Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="54dae-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="54dae-115">**Ön gereksinimlerini:** Azure kaynak grubu, sanal ağ ve alt ağ, ağ güvenlik grubu SSH ile gelen ve bir sanal ağ arabirim kartı.</span><span class="sxs-lookup"><span data-stu-id="54dae-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="54dae-116">Merhaba VM hello sanal ağ altyapısıyla dağıtma</span><span class="sxs-lookup"><span data-stu-id="54dae-116">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="54dae-117">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="54dae-117">Detailed walkthrough</span></span>

<span data-ttu-id="54dae-118">Sanal ağlar ve ağ güvenlik grupları gibi Azure varlıklar statik olmalıdır ve nadiren dağıtılan kaynakları uzun ömürlü.</span><span class="sxs-lookup"><span data-stu-id="54dae-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="54dae-119">Bir sanal ağ dağıtıldıktan sonra herhangi bir olumsuz etkiler toohello altyapı olmadan yeni dağıtımlar tarafından yeniden.</span><span class="sxs-lookup"><span data-stu-id="54dae-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="54dae-120">Geleneksel donanım ağ anahtarı olarak bir sanal ağ yapılandırmanızda -, yepyeni bir donanım her dağıtımı ile geçiş tooconfigure ihtiyaç duymaz.</span><span class="sxs-lookup"><span data-stu-id="54dae-120">Think about a virtual network as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="54dae-121">Doğru şekilde yapılandırılmış bir sanal ağ ile toodeploy devam edebilmeniz için yeni VM'ler bu sanal ağla defalarca az içine, varsa, değişiklikleri gerekli hello sanal ağ hello ömrü boyunca.</span><span class="sxs-lookup"><span data-stu-id="54dae-121">With a correctly configured virtual network, you can continue toodeploy new VMs into that virtual network over and over with few, if any, changes required over hello life of hello virtual network.</span></span>

<span data-ttu-id="54dae-122">toocreate bu özel ortam hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="54dae-122">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="54dae-123">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="54dae-123">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="54dae-124">Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="54dae-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="54dae-125">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="54dae-125">Create hello resource group</span></span>

<span data-ttu-id="54dae-126">İlk olarak, bir Azure kaynak grubu tooorganize bu kılavuzda oluşturduğunuz her şeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54dae-126">First, create an Azure resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="54dae-127">Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54dae-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="54dae-128">Merhaba kaynak grubuyla oluşturma [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="54dae-128">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="54dae-129">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="54dae-129">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="54dae-130">Merhaba sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="54dae-130">Create hello virtual network</span></span>

<span data-ttu-id="54dae-131">Bir Azure sanal ağı toolaunch hello içine VM'ler yapı sağlar.</span><span class="sxs-lookup"><span data-stu-id="54dae-131">Lets build an Azure virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="54dae-132">Sanal ağlar hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="54dae-132">For more information on virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="54dae-133">Merhaba sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="54dae-133">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="54dae-134">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ve adlı alt ağ *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="54dae-134">hello following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="54dae-135">Merhaba ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="54dae-135">Create hello network security group</span></span>

<span data-ttu-id="54dae-136">Azure ağ güvenlik grupları hello ağ katmanı eşdeğer tooa güvenlik duvarında değildir.</span><span class="sxs-lookup"><span data-stu-id="54dae-136">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="54dae-137">Ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [nasıl hello Azure CLI toocreate ağ güvenlik gruplarını](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="54dae-137">For more information on network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="54dae-138">Merhaba ağ güvenlik grubu oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="54dae-138">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="54dae-139">Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="54dae-139">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="54dae-140">Gelen bir SSH izin ver Kuralı Ekle</span><span class="sxs-lookup"><span data-stu-id="54dae-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="54dae-141">Merhaba VM gelen bağlantı noktası 22 trafiği toobe veren bir kural hello ağ tooport 22 hello VM üzerinde geçirilen şekilde Internet gerekli hello erişimden gerekir.</span><span class="sxs-lookup"><span data-stu-id="54dae-141">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span> <span data-ttu-id="54dae-142">Merhaba ağ güvenlik grubu için bir gelen kuralı Ekle [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="54dae-142">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="54dae-143">Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="54dae-143">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a><span data-ttu-id="54dae-144">Merhaba alt toohello ağ güvenlik grubu Ekle</span><span class="sxs-lookup"><span data-stu-id="54dae-144">Attach hello subnet toohello network security group</span></span>

<span data-ttu-id="54dae-145">Merhaba ağ güvenlik grubu kural uygulanan tooa alt ağ veya belirli bir sanal ağ arabirimi olabilir.</span><span class="sxs-lookup"><span data-stu-id="54dae-145">hello network security group rules can be applied tooa subnet or a specific virtual network interface.</span></span> <span data-ttu-id="54dae-146">Merhaba ağ güvenlik grubu tooour alt ekleme olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="54dae-146">Lets attach hello network security group tooour subnet.</span></span> <span data-ttu-id="54dae-147">Alt ağ toohello ağ güvenlik grubuyla attach [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="54dae-147">Attach your subnet toohello network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a><span data-ttu-id="54dae-148">Bir sanal ağ arabirim kartı toohello alt ağ Ekle</span><span class="sxs-lookup"><span data-stu-id="54dae-148">Add a virtual network interface card toohello subnet</span></span>

<span data-ttu-id="54dae-149">Sanal ağ arabirimi kartları (VNics), bunları toodifferent VM'ler bağlanarak yeniden gibi önemlidir.</span><span class="sxs-lookup"><span data-stu-id="54dae-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="54dae-150">Merhaba VM'ler geçici olarak olabileceği bu yeniden tookeep hello Vnıc statik bir kaynak olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="54dae-150">This reuse allows you tookeep hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="54dae-151">Bir Vnıc'teki oluşturun ve hello alt ağ ile ilişkilendirmek [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="54dae-151">Create a VNic and associate it with hello subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="54dae-152">Merhaba aşağıdaki örnekte oluşturur adlı bir Vnıc'teki *myNic*:</span><span class="sxs-lookup"><span data-stu-id="54dae-152">hello following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="54dae-153">Merhaba VM hello sanal ağ altyapısıyla dağıtma</span><span class="sxs-lookup"><span data-stu-id="54dae-153">Deploy hello VM into hello virtual network infrastructure</span></span>

<span data-ttu-id="54dae-154">Artık bir sanal ağ ve alt ağ ve bir ağ güvenlik grubu tooprotect hello alt SSH için bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="54dae-154">You now have a virtual network and subnet, and a network security group tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="54dae-155">Merhaba VM şimdi bu mevcut ağ altyapınızda içinde dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="54dae-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="54dae-156">İle VM oluşturma [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="54dae-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="54dae-157">Merhaba hakkında daha fazla bilgi toouse hello Azure CLI 2.0 toodeploy ile tam bir VM bayrakları için bkz: [hello Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="54dae-157">For more information on hello flags toouse with hello Azure CLI 2.0 toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="54dae-158">Aşağıdaki örnek hello Azure yönetilen diskleri kullanan bir VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="54dae-158">hello following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="54dae-159">Bu diskleri hello Azure platformu tarafından işlenir ve hazırlık veya konumu toostore gerektirmez bunları.</span><span class="sxs-lookup"><span data-stu-id="54dae-159">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="54dae-160">Yönetilen diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Disklere genel bakış](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54dae-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="54dae-161">Yönetilmeyen toouse diskleri istiyorsanız hello ek nota bakın.</span><span class="sxs-lookup"><span data-stu-id="54dae-161">If you wish toouse unmanaged disks, see hello additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="54dae-162">Yönetilen diskleri kullanırsanız, bu adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="54dae-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="54dae-163">Yönetilmeyen toouse diskleri istiyorsanız, ek parametreler toohello devam etmeden komutu yönetilmeyen toocreate diskleri adlı hello depolama hesabındaki aşağıdaki tooadd hello gereksinim `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="54dae-163">If you wish toouse unmanaged disks, you need tooadd hello following additional parameters toohello proceeding command toocreate unmanaged disks in hello storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="54dae-164">Hello kullanarak CLI toocall var olan kaynakların çıkışı hello mevcut ağ içinde Azure toodeploy hello VM toplamasını işaretler.</span><span class="sxs-lookup"><span data-stu-id="54dae-164">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="54dae-165">Bir sanal ağ ve alt ağ dağıtıldıktan sonra Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="54dae-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="54dae-166">Bu örnekte, değil oluşturun ve bu VM hello Internet genel olarak erişilebilir olmamasını sağlayacak şekilde genel bir IP adresi toohello Vnıc, atayın.</span><span class="sxs-lookup"><span data-stu-id="54dae-166">In this example, you did not create and assign a public IP address toohello VNic, so this VM is not publicly accessible over hello Internet.</span></span> <span data-ttu-id="54dae-167">Daha fazla bilgi için bkz: [hello Azure CLI kullanarak bir statik genel IP ile bir VM oluşturma](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="54dae-167">For more information, see [Create a VM with a static public IP using hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54dae-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54dae-168">Next steps</span></span>
<span data-ttu-id="54dae-169">Azure'da yollar toocreate sanal makineler hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="54dae-169">For more information about ways toocreate virtual machines in Azure, see hello following resources:</span></span>

* [<span data-ttu-id="54dae-170">Azure Resource Manager şablonu toocreate belirli bir dağıtım kullanın</span><span class="sxs-lookup"><span data-stu-id="54dae-170">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="54dae-171">Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="54dae-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="54dae-172">Şablonları kullanarak Azure'da bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="54dae-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
