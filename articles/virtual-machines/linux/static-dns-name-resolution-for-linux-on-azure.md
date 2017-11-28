---
title: "aaaUse VM için iç DNS ad çözümlemesi hello Azure CLI 2.0 ile | Microsoft Docs"
description: "Nasıl toocreate sanal ağ arabirim kartları ve iç DNS hello Azure CLI 2.0 ile Azure VM ad çözümlemesi için kullanın"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="989f1-103">Sanal ağ arabirim kartları oluşturma ve Azure VM ad çözümlemesi için iç DNS kullanma</span><span class="sxs-lookup"><span data-stu-id="989f1-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="989f1-104">Bu makalede nasıl ağ arabirimi kartları (vNics) ve DNS etiket adları'hello Azure CLI 2.0 ile tooset statik iç DNS adlarını Linux sanal kullanarak VM'ler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="989f1-104">This article shows you how tooset static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with hello Azure CLI 2.0.</span></span> <span data-ttu-id="989f1-105">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="989f1-105">You can also perform these steps with hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="989f1-106">Statik DNS adları, bu belge için kullanılan bir Jenkins yapı sunucusu veya Git sunucusu gibi kalıcı altyapı hizmetleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="989f1-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="989f1-107">Hello gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="989f1-107">hello requirements are:</span></span>

* [<span data-ttu-id="989f1-108">Bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="989f1-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="989f1-109">SSH ortak ve özel anahtar dosyaları</span><span class="sxs-lookup"><span data-stu-id="989f1-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="989f1-110">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="989f1-110">Quick commands</span></span>
<span data-ttu-id="989f1-111">Tooquickly gerekiyorsa hello görevi, gerekli hello komutları bölümden hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="989f1-111">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="989f1-112">Her adım hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada başlangıç](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="989f1-112">More detailed information and context for each step can be found in hello rest of hello document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="989f1-113">Aşağıdaki adımları tooperform ihtiyacınız hello son [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="989f1-113">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="989f1-114">Ön gereksinimlerini: Kaynak grubu, sanal ağ ve alt ağ, ağ güvenlik grubu SSH ile gelen.</span><span class="sxs-lookup"><span data-stu-id="989f1-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="989f1-115">Bir sanal ağ arabirim kartı statik iç DNS adı ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="989f1-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="989f1-116">Merhaba Vnıc ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="989f1-116">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="989f1-117">Merhaba `--internal-dns-name` hello sanal ağ arabirim kartı (Vnıc) hello statik DNS ad sağlar ayarı hello DNS etiketi CLI bayrağı içindir.</span><span class="sxs-lookup"><span data-stu-id="989f1-117">hello `--internal-dns-name` CLI flag is for setting hello DNS label, which provides hello static DNS name for hello virtual network interface card (vNic).</span></span> <span data-ttu-id="989f1-118">Merhaba aşağıdaki örnekte oluşturur adlı bir Vnıc'teki `myNic`, toohello bağlayan `myVnet` sanal ağ ve olarak adlandırılan bir iç DNS ad kayıt oluşturur `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="989f1-118">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a><span data-ttu-id="989f1-119">Bir VM'yi dağıtmak ve hello Vnıc bağlanın</span><span class="sxs-lookup"><span data-stu-id="989f1-119">Deploy a VM and connect hello vNic</span></span>
<span data-ttu-id="989f1-120">[az vm create](/cli/azure/vm#create) ile bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="989f1-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="989f1-121">Merhaba `--nics` bayrağı hello dağıtım tooAzure sırasında hello Vnıc toohello VM bağlanır.</span><span class="sxs-lookup"><span data-stu-id="989f1-121">hello `--nics` flag connects hello vNic toohello VM during hello deployment tooAzure.</span></span> <span data-ttu-id="989f1-122">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` Azure yönetilen disklerle ve adlı ekler hello Vnıc `myNic` adım önceki hello gelen:</span><span class="sxs-lookup"><span data-stu-id="989f1-122">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="989f1-123">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="989f1-123">Detailed walkthrough</span></span>

<span data-ttu-id="989f1-124">Bir tam sürekli tümleştirme ve sürekli dağıtımı (CiCd) altyapısı Azure ile ilgili belirli sunucuları toobe statik veya uzun süreli sunucuları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="989f1-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span> <span data-ttu-id="989f1-125">Sanal ağlar ve ağ güvenlik grupları hello gibi Azure varlıklar statik ve nadiren dağıtılan kaynakları uzun ömürlü önerilir.</span><span class="sxs-lookup"><span data-stu-id="989f1-125">It is recommended that Azure assets like hello virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="989f1-126">Bir sanal ağ dağıtıldıktan sonra herhangi bir olumsuz etkiler toohello altyapı olmadan yeni dağıtımlar tarafından yeniden.</span><span class="sxs-lookup"><span data-stu-id="989f1-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="989f1-127">Daha sonra bir Git deposu sunucusu ekleyebilir veya Jenkins Otomasyon sunucusu CiCd toothis geliştirme veya test ortamları için sanal ağ sunar.</span><span class="sxs-lookup"><span data-stu-id="989f1-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd toothis virtual network for your development or test environments.</span></span>  

<span data-ttu-id="989f1-128">İç DNS adları, yalnızca bir Azure sanal ağı içinde çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="989f1-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="989f1-129">Merhaba DNS adlarını iç olduğundan, bunlar dışında ek güvenlik toohello altyapısı sağlayan Internet çözümlenebilir toohello değildir.</span><span class="sxs-lookup"><span data-stu-id="989f1-129">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="989f1-130">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="989f1-130">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="989f1-131">Örnek parametre adlarında `myResourceGroup`, `myNic`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="989f1-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="989f1-132">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="989f1-132">Create hello resource group</span></span>
<span data-ttu-id="989f1-133">İlk olarak, hello kaynak grubuyla oluşturun [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="989f1-133">First, create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="989f1-134">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westus` konumu:</span><span class="sxs-lookup"><span data-stu-id="989f1-134">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="989f1-135">Merhaba sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="989f1-135">Create hello virtual network</span></span>

<span data-ttu-id="989f1-136">Merhaba sonraki adım, bir sanal ağ toolaunch hello VM'ler içine toobuild olacaktır.</span><span class="sxs-lookup"><span data-stu-id="989f1-136">hello next step is toobuild a virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="989f1-137">Merhaba sanal ağ Bu izlenecek yol için bir alt ağ içerir.</span><span class="sxs-lookup"><span data-stu-id="989f1-137">hello virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="989f1-138">Azure sanal ağlar hakkında daha fazla bilgi için bkz: [hello Azure CLI kullanarak bir sanal ağ oluşturma](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="989f1-138">For more information on Azure virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="989f1-139">Merhaba sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="989f1-139">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="989f1-140">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur `myVnet` ve adlı alt ağ `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="989f1-140">hello following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="989f1-141">Merhaba ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="989f1-141">Create hello Network Security Group</span></span>
<span data-ttu-id="989f1-142">Azure ağ güvenlik grupları hello ağ katmanı eşdeğer tooa güvenlik duvarında değildir.</span><span class="sxs-lookup"><span data-stu-id="989f1-142">Azure Network Security Groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="989f1-143">Ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [nasıl toocreate Nsg'ler Azure CLI hello](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="989f1-143">For more information about Network Security Groups, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="989f1-144">Merhaba ağ güvenlik grubu oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="989f1-144">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="989f1-145">Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="989f1-145">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a><span data-ttu-id="989f1-146">Bir gelen kuralı tooallow SSH ekleme</span><span class="sxs-lookup"><span data-stu-id="989f1-146">Add an inbound rule tooallow SSH</span></span>
<span data-ttu-id="989f1-147">Merhaba ağ güvenlik grubu için bir gelen kuralı Ekle [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="989f1-147">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="989f1-148">Merhaba aşağıdaki örnek adlı bir kural oluşturur `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="989f1-148">hello following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a><span data-ttu-id="989f1-149">Ağ güvenlik grubu hello ile Merhaba alt ağını ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="989f1-149">Associate hello subnet with hello Network Security Group</span></span>
<span data-ttu-id="989f1-150">Merhaba ağ güvenlik grubu ile tooassociate hello alt ağını [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="989f1-150">tooassociate hello subnet with hello Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="989f1-151">Merhaba aşağıdaki örnek ilişkilendirir hello alt ağ adı `mySubnet` hello adlı ağ güvenlik grubu ile `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="989f1-151">hello following example associates hello subnet name `mySubnet` with hello Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="989f1-152">Merhaba sanal ağ arabirim kartı ve statik DNS adları oluşturun</span><span class="sxs-lookup"><span data-stu-id="989f1-152">Create hello virtual network interface card and static DNS names</span></span>
<span data-ttu-id="989f1-153">Azure çok esnektir, ancak toouse DNS adlarını VM ad çözümlemesi için bir DNS etiketi içeren toocreate sanal ağ arabirimi kartları (vNics) gerekir.</span><span class="sxs-lookup"><span data-stu-id="989f1-153">Azure is very flexible, but toouse DNS names for VM name resolution, you need toocreate virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="989f1-154">bunları bağlantı kurarak toodifferent VM'ler hello altyapı yaşam döngüsü yeniden kullanabileceğiniz gibi vNics önemlidir.</span><span class="sxs-lookup"><span data-stu-id="989f1-154">vNics are important as you can reuse them by connecting them toodifferent VMs over hello infrastructure lifecycle.</span></span> <span data-ttu-id="989f1-155">Bu yaklaşım Hello VM'ler geçici olarak olabileceği hello Vnıc statik bir kaynak olarak tutar.</span><span class="sxs-lookup"><span data-stu-id="989f1-155">This approach keeps hello vNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="989f1-156">Merhaba vNic üzerinde etiketleme DNS kullanarak, mümkün tooenable basit ad çözümlemesi hello VNet içindeki diğer vm'lerden duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="989f1-156">By using DNS labeling on hello vNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span> <span data-ttu-id="989f1-157">Hello DNS adı tarafından sağlayan diğer VM'ler tooaccess hello Otomasyon sunucusu çözümlenebilir adları kullanarak `Jenkins` veya hello Git sunucusu olarak `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="989f1-157">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  

<span data-ttu-id="989f1-158">Merhaba Vnıc ile oluşturma [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="989f1-158">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="989f1-159">Merhaba aşağıdaki örnekte oluşturur adlı bir Vnıc'teki `myNic`, toohello bağlayan `myVnet` adlı sanal ağ `myVnet`ve olarak adlandırılan bir iç DNS ad kayıt oluşturur `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="989f1-159">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="989f1-160">Merhaba VM hello sanal ağ altyapısıyla dağıtma</span><span class="sxs-lookup"><span data-stu-id="989f1-160">Deploy hello VM into hello virtual network infrastructure</span></span>
<span data-ttu-id="989f1-161">Şimdi bir sanal ağ ve alt ağ, SSH ve bir Vnıc için bağlantı noktası 22 dışındaki tüm gelen trafiği engelleyerek bizim alt ağ güvenlik duvarı tooprotect davranan bir ağ güvenlik grubu sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="989f1-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="989f1-162">Artık bu mevcut ağ altyapınızda içinde bir VM dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="989f1-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="989f1-163">[az vm create](/cli/azure/vm#create) ile bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="989f1-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="989f1-164">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM` Azure yönetilen disklerle ve adlı ekler hello Vnıc `myNic` adım önceki hello gelen:</span><span class="sxs-lookup"><span data-stu-id="989f1-164">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="989f1-165">Hello kullanarak CLI toocall var olan kaynakların çıkışı biz hello mevcut ağ içinde Azure toodeploy hello VM istemeniz işaretler.</span><span class="sxs-lookup"><span data-stu-id="989f1-165">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="989f1-166">bir VNet ve alt ağ dağıtıldıktan sonra tooreiterate, bunlar Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="989f1-166">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="989f1-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="989f1-167">Next steps</span></span>
* [<span data-ttu-id="989f1-168">Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="989f1-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="989f1-169">Şablonları kullanarak Azure'da bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="989f1-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
