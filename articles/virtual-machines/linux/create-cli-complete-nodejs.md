---
title: "aaaCreate hello Azure CLI 1.0 ile eksiksiz bir Linux ortamı | Microsoft Docs"
description: "Tüm hello Azure CLI 1.0 kullanarak plan hello depolama, bir Linux VM, bir sanal ağ ve alt ağ, bir yük dengeleyici, bir NIC, ortak bir IP ve bir ağ güvenlik grubu oluşturun."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a><span data-ttu-id="cd3c2-103">Azure CLI 1.0 hello ile eksiksiz bir Linux ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd3c2-103">Create a complete Linux environment with hello Azure CLI 1.0</span></span>
<span data-ttu-id="cd3c2-104">Bu makalede, bir yük dengeleyici ve geliştirme ve basit bilgi işlem için yararlı olan VM'ler çifti ile basit bir ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="cd3c2-105">Biz komutu tarafından komut hello işleminde size kılavuzluk, iki çalışma kadar gelen herhangi bir yere hello Internet üzerinde bağlayabilirsiniz Linux VM'ler toowhich güvenli.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-105">We walk through hello process command by command, until you have two working, secure Linux VMs toowhich you can connect from anywhere on hello Internet.</span></span> <span data-ttu-id="cd3c2-106">Ardından, toomore karmaşık ağlar ve ortamları taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-106">Then you can move on toomore complex networks and environments.</span></span>

<span data-ttu-id="cd3c2-107">Merhaba yol boyunca hello Resource Manager dağıtım modeli sağlar ve hakkında ne kadar güç sağlar hello bağımlılık hiyerarşi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-107">Along hello way, you learn about hello dependency hierarchy that hello Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="cd3c2-108">Merhaba sistem nasıl yapılandırıldığını gördükten sonra bu çok daha hızlı bir şekilde kullanarak yeniden oluşturmak için kullanabileceğiniz [Azure Resource Manager şablonları](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd3c2-108">After you see how hello system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="cd3c2-109">Ayrıca, hello bölümleri ortamınızın nasıl bir araya getireceğinizi öğrenin sonra şablonları tooautomate oluşturarak bunları olur daha kolay.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-109">Also, after you learn how hello parts of your environment fit together, creating templates tooautomate them becomes easier.</span></span>

<span data-ttu-id="cd3c2-110">Merhaba ortamı içerir:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-110">hello environment contains:</span></span>

* <span data-ttu-id="cd3c2-111">İki VM bir kullanılabilirlik kümesi içinde.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="cd3c2-112">Yük Dengeleyici Yük Dengeleme kuralı bağlantı noktası 80 ile.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="cd3c2-113">Ağ güvenlik grubu (NSG), VM istenmeyen trafiğinden tooprotect kuralları.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-113">Network security group (NSG) rules tooprotect your VM from unwanted traffic.</span></span>

<span data-ttu-id="cd3c2-114">toocreate bu özel ortam hello son gereksinim [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Kaynak Yöneticisi modunda (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="cd3c2-114">toocreate this custom environment, you need hello latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="cd3c2-115">Ayrıca aracı ayrıştırma JSON gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="cd3c2-116">Bu örnekte [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="cd3c2-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="cd3c2-117">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="cd3c2-117">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="cd3c2-118">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-118">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="cd3c2-119">[Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="cd3c2-119">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="cd3c2-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="cd3c2-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="cd3c2-121">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="cd3c2-121">Quick commands</span></span>
<span data-ttu-id="cd3c2-122">Tooquickly gerekiyorsa hello görevi, hello bölüm ayrıntıları hello aşağıdaki komutları tooupload VM tooAzure temel.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-122">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="cd3c2-123">Her adım başlangıç hello belgenin hello kalan bulunabilir bilgi ve içerik daha ayrıntılı [burada](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="cd3c2-123">More detailed information and context for each step can be found in hello rest of hello document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="cd3c2-124">Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0 hello](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-124">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="cd3c2-125">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-125">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="cd3c2-126">Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="cd3c2-127">Merhaba kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-127">Create hello resource group.</span></span> <span data-ttu-id="cd3c2-128">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westeurope` konumu:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-128">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="cd3c2-129">Merhaba kaynak grubu hello JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-129">Verify hello resource group by using hello JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="cd3c2-130">Merhaba depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-130">Create hello storage account.</span></span> <span data-ttu-id="cd3c2-131">Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-131">hello following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="cd3c2-132">(Merhaba depolama hesabı adı gerekir benzersiz olması, bu nedenle, kendi benzersiz bir ad sağlayın.)</span><span class="sxs-lookup"><span data-stu-id="cd3c2-132">(hello storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="cd3c2-133">Merhaba depolama hesabı hello JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-133">Verify hello storage account by using hello JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="cd3c2-134">Merhaba sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-134">Create hello virtual network.</span></span> <span data-ttu-id="cd3c2-135">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-135">hello following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="cd3c2-136">Bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-136">Create a subnet.</span></span> <span data-ttu-id="cd3c2-137">Merhaba aşağıdaki örnek adlı bir alt ağı oluşturur `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-137">hello following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="cd3c2-138">Merhaba sanal ağ ve alt hello JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-138">Verify hello virtual network and subnet by using hello JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="cd3c2-139">Genel IP oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-139">Create a public IP.</span></span> <span data-ttu-id="cd3c2-140">Merhaba aşağıdaki örnekte oluşturur adlı ortak IP `myPublicIP` hello DNS adı ile `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-140">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="cd3c2-141">(Merhaba DNS adı gerekir benzersiz olması, bu nedenle, kendi benzersiz bir ad sağlayın.)</span><span class="sxs-lookup"><span data-stu-id="cd3c2-141">(hello DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="cd3c2-142">Merhaba yük dengeleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-142">Create hello load balancer.</span></span> <span data-ttu-id="cd3c2-143">Merhaba aşağıdaki örnek adlı bir yük dengeleyici oluşturur `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-143">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="cd3c2-144">Merhaba yük dengeleyici için bir ön uç IP havuzu oluşturun ve hello genel IP ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-144">Create a front-end IP pool for hello load balancer, and associate hello public IP.</span></span> <span data-ttu-id="cd3c2-145">Merhaba aşağıdaki örnek adlı bir ön uç IP havuzu oluşturur `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-145">hello following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="cd3c2-146">Merhaba yük dengeleyici için Hello arka uç IP havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-146">Create hello back-end IP pool for hello load balancer.</span></span> <span data-ttu-id="cd3c2-147">Merhaba aşağıdaki örnekte oluşturur adlı bir arka uç IP havuzu `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-147">hello following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="cd3c2-148">SSH gelen ağ adresi çevirisi (NAT) kuralları hello yük dengeleyici için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-148">Create SSH inbound network address translation (NAT) rules for hello load balancer.</span></span> <span data-ttu-id="cd3c2-149">Merhaba aşağıdaki örnekte oluşturur iki yük dengeleyici kuralları, `myLoadBalancerRuleSSH1` ve `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-149">hello following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="cd3c2-150">Merhaba web oluşturmak yük dengeleyici gelen NAT kuralları hello için.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-150">Create hello web inbound NAT rules for hello load balancer.</span></span> <span data-ttu-id="cd3c2-151">Merhaba aşağıdaki örnek adlı bir yük dengeleyici kuralı oluşturur `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-151">hello following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="cd3c2-152">Merhaba yük dengeleyici durum araştırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-152">Create hello load balancer health probe.</span></span> <span data-ttu-id="cd3c2-153">Merhaba aşağıdaki örnek adlı bir TCP araştırması oluşturur `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-153">hello following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="cd3c2-154">Merhaba yük dengeleyici, IP havuzları ve NAT kuralları hello JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-154">Verify hello load balancer, IP pools, and NAT rules by using hello JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="cd3c2-155">Merhaba ilk ağ arabirim kartı (NIC) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-155">Create hello first network interface card (NIC).</span></span> <span data-ttu-id="cd3c2-156">Hello yerine `#####-###-###` bölümleri, kendi Azure aboneliği ID'ye sahip</span><span class="sxs-lookup"><span data-stu-id="cd3c2-156">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="cd3c2-157">Aboneliğinizi hello çıktısında kimliği not ettiğiniz **jq** oluşturmakta hello kaynakları incelediğinizde.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-157">Your subscription ID is noted in hello output of **jq** when you examine hello resources you are creating.</span></span> <span data-ttu-id="cd3c2-158">Abonelik Kimliğinizle de görüntüleyebilirsiniz `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="cd3c2-159">Merhaba aşağıdaki örnekte oluşturur adlı bir NIC `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-159">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="cd3c2-160">Merhaba ikinci NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="cd3c2-160">Create hello second NIC.</span></span> <span data-ttu-id="cd3c2-161">Merhaba aşağıdaki örnekte oluşturur adlı bir NIC `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-161">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="cd3c2-162">Merhaba iki NIC hello JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-162">Verify hello two NICs by using hello JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="cd3c2-163">Merhaba ağ güvenlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-163">Create hello network security group.</span></span> <span data-ttu-id="cd3c2-164">Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-164">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="cd3c2-165">Merhaba ağ güvenlik grubu için iki gelen kuralı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-165">Add two inbound rules for hello network security group.</span></span> <span data-ttu-id="cd3c2-166">Merhaba aşağıdaki örnekte oluşturur iki kural `myNetworkSecurityGroupRuleSSH` ve `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-166">hello following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="cd3c2-167">Merhaba ağ güvenlik grubu ve gelen kuralları hello JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-167">Verify hello network security group and inbound rules by using hello JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="cd3c2-168">Merhaba ağ güvenliği bağlama toohello iki NIC grubu:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-168">Bind hello network security group toohello two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="cd3c2-169">Merhaba kullanılabilirlik kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-169">Create hello availability set.</span></span> <span data-ttu-id="cd3c2-170">Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-170">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="cd3c2-171">Oluşturma ilk Linux VM hello.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-171">Create hello first Linux VM.</span></span> <span data-ttu-id="cd3c2-172">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-172">hello following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="cd3c2-173">Merhaba oluşturma Linux VM ikinci.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-173">Create hello second Linux VM.</span></span> <span data-ttu-id="cd3c2-174">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-174">hello following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="cd3c2-175">Merhaba JSON ayrıştırıcı tooverify bu her şeyi, oluşturulmuş kullanın:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-175">Use hello JSON parser tooverify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="cd3c2-176">Yeni ortam tooa şablonu tooquickly yeniden oluşturmanız yeni örneklerinizi dışarı aktarın:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-176">Export your new environment tooa template tooquickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="cd3c2-177">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="cd3c2-177">Detailed walkthrough</span></span>
<span data-ttu-id="cd3c2-178">Merhaba izleyin ayrıntılı adımlar ortamınızı yapı gibi her komutun ne yaptığını açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-178">hello detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="cd3c2-179">Bu kavramlar, kendi özel ortamınız için geliştirme veya üretim derlerken faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="cd3c2-180">Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0 hello](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-180">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="cd3c2-181">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-181">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="cd3c2-182">Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="cd3c2-183">Kaynak grupları oluşturun ve dağıtım konumları seçin</span><span class="sxs-lookup"><span data-stu-id="cd3c2-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="cd3c2-184">Azure kaynak gruplarını yapılandırma bilgilerini ve meta veri tooenable hello mantıksal Yönetimi kaynak dağıtımlarını içeren mantıksal dağıtım varlıklardır.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-184">Azure resource groups are logical deployment entities that contain configuration information and metadata tooenable hello logical management of resource deployments.</span></span> <span data-ttu-id="cd3c2-185">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westeurope` konumu:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-185">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="cd3c2-186">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-186">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="cd3c2-187">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd3c2-187">Create a storage account</span></span>
<span data-ttu-id="cd3c2-188">Tooadd istediğiniz depolama hesapları olan ek veri disklerinin ve VM diskleri için gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-188">You need storage accounts for your VM disks and for any additional data disks that you want tooadd.</span></span> <span data-ttu-id="cd3c2-189">Kaynak grupları oluşturun sonra hemen hemen depolama hesapları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="cd3c2-190">Merhaba burada kullandığımız `azure storage account create` komutunu hello hello hesabı, hello kaynak grubu konumunu geçirme denetler ve istediğiniz depolama destek hello türü.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-190">Here we use hello `azure storage account create` command, passing hello location of hello account, hello resource group that controls it, and hello type of storage support you want.</span></span> <span data-ttu-id="cd3c2-191">Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-191">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="cd3c2-192">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="cd3c2-193">Bizim kaynak grubunda hello kullanarak tooexamine `azure group show` komutu, hello kullanalım [jq](https://stedolan.github.io/jq/) aracı ile birlikte hello `--json` Azure CLI seçeneği.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-193">tooexamine our resource group by using hello `azure group show` command, let's use hello [jq](https://stedolan.github.io/jq/) tool along with hello `--json` Azure CLI option.</span></span> <span data-ttu-id="cd3c2-194">(Kullanabileceğiniz **jsawk** veya tooparse tercih ettiğiniz herhangi bir dil kitaplığı hello JSON.)</span><span class="sxs-lookup"><span data-stu-id="cd3c2-194">(You can use **jsawk** or any language library you prefer tooparse hello JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="cd3c2-195">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-195">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="cd3c2-196">Merhaba CLI kullanarak tooinvestigate hello depolama hesabı, önce tooset hello hesap adlarını ve anahtarları gerekir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-196">tooinvestigate hello storage account by using hello CLI, you first need tooset hello account names and keys.</span></span> <span data-ttu-id="cd3c2-197">Aşağıdaki seçtiğiniz bir adla örneğine hello hello depolama hesabında Hello adını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-197">Replace hello name of hello storage account in hello following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="cd3c2-198">Ardından, depolama bilgilerinizi kolayca görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="cd3c2-199">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="cd3c2-200">Bir sanal ağ ve alt ağ oluşturun</span><span class="sxs-lookup"><span data-stu-id="cd3c2-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="cd3c2-201">Sonraki tooneed toocreate Azure ve Vm'lerinizi oluşturabileceğiniz bir alt ağ içinde çalışan bir sanal ağ oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-201">Next you're going tooneed toocreate a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="cd3c2-202">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur `myVnet` hello ile `192.168.0.0/16` adres öneki:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-202">hello following example creates a virtual network named `myVnet` with hello `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="cd3c2-203">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-203">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="cd3c2-204">Yeniden hello--json seçeneği kullanalım `azure group show` ve `jq` toosee nasıl KAYNAKLARIMIZI oluşturmakta olduğumuz.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-204">Again, let's use hello --json option of `azure group show` and `jq` toosee how we're building our resources.</span></span> <span data-ttu-id="cd3c2-205">Şimdi sahip olduğumuz bir `storageAccounts` kaynak ve `virtualNetworks` kaynak.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="cd3c2-206">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-206">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="cd3c2-207">Şimdi bir alt ağ hello oluşturalım `myVnet` sanal ağ içinde hangi hello VM'ler dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-207">Now let's create a subnet in hello `myVnet` virtual network into which hello VMs are deployed.</span></span> <span data-ttu-id="cd3c2-208">Merhaba kullanırız `azure network vnet subnet create` zaten oluşturduğumuz hello kaynakları birlikte komutu: Merhaba `myResourceGroup` kaynak grubu ve hello `myVnet` sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-208">We use hello `azure network vnet subnet create` command, along with hello resources we've already created: hello `myResourceGroup` resource group and hello `myVnet` virtual network.</span></span> <span data-ttu-id="cd3c2-209">Aşağıdaki örneğine hello adlı hello alt eklediğimiz `mySubnet` hello alt ağ adresi öneki ile `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-209">In hello following example, we add hello subnet named `mySubnet` with hello subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="cd3c2-210">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="cd3c2-211">Merhaba alt mantıksal olarak hello sanal ağ içinde olduğundan, biz biraz farklı bir komutla hello alt ağ bilgilerini arayın.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-211">Because hello subnet is logically inside hello virtual network, we look for hello subnet information with a slightly different command.</span></span> <span data-ttu-id="cd3c2-212">Merhaba komutu kullanırız `azure network vnet show`, ancak kullanarak tooexamine hello JSON çıktısını devam `jq`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-212">hello command we use is `azure network vnet show`, but we continue tooexamine hello JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="cd3c2-213">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-213">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="cd3c2-214">Genel IP adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd3c2-214">Create a public IP address</span></span>
<span data-ttu-id="cd3c2-215">Şimdi biz tooyour yük dengeleyici atamak hello genel IP adresi (PIP) oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-215">Now let's create hello public IP address (PIP) that we assign tooyour load balancer.</span></span> <span data-ttu-id="cd3c2-216">Merhaba Internet gelen tooconnect tooyour VM'ler hello kullanarak sağlar `azure network public-ip create` komutu.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-216">It enables you tooconnect tooyour VMs from hello Internet by using hello `azure network public-ip create` command.</span></span> <span data-ttu-id="cd3c2-217">Merhaba varsayılan adres dinamik olduğundan, adlandırılmış bir DNS girişi hello oluşturuyoruz **cloudapp.azure.com** hello kullanarak etki alanı `--domain-name-label` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-217">Because hello default address is dynamic, we create a named DNS entry in hello **cloudapp.azure.com** domain by using hello `--domain-name-label` option.</span></span> <span data-ttu-id="cd3c2-218">Merhaba aşağıdaki örnekte oluşturur adlı ortak IP `myPublicIP` hello DNS adı ile `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-218">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="cd3c2-219">Merhaba DNS adının benzersiz olması gerektiğinden, kendi benzersiz DNS adını belirtin:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-219">Because hello DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="cd3c2-220">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="cd3c2-221">ile görebilirsiniz hello ortak IP adresini de üst düzey bir kaynak olduğundan `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-221">hello public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="cd3c2-222">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-222">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="cd3c2-223">Merhaba tam kullanarak hello hello alt etki alanının tam etki alanı adı (FQDN) de dahil olmak üzere daha fazla kaynak ayrıntılarını araştırabilirsiniz `azure network public-ip show` komutu.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-223">You can investigate more resource details, including hello fully qualified domain name (FQDN) of hello subdomain, by using hello complete `azure network public-ip show` command.</span></span> <span data-ttu-id="cd3c2-224">Merhaba ortak IP adresi kaynağı mantıksal olarak ayrıldı, ancak belirli bir adresi yok henüz atanmamış.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-224">hello public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="cd3c2-225">bir IP adresi tooobtain, tooneed değil henüz oluşturduk bir yük dengeleyici oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-225">tooobtain an IP address, you're going tooneed a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="cd3c2-226">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-226">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="cd3c2-227">Bir yük dengeleyici ve IP havuzları oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd3c2-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="cd3c2-228">Bir yük dengeleyici oluşturduğunuzda, toodistribute trafiği arasında birden çok VM sağlar.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-228">When you create a load balancer, it enables you toodistribute traffic across multiple VMs.</span></span> <span data-ttu-id="cd3c2-229">Ayrıca, Bakım veya ağır yükten hello olayı içinde toouser isteklerine yanıt birden çok VM çalıştırarak artıklık tooyour uygulama da sağlar.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-229">It also provides redundancy tooyour application by running multiple VMs that respond toouser requests in hello event of maintenance or heavy loads.</span></span> <span data-ttu-id="cd3c2-230">Merhaba aşağıdaki örnek adlı bir yük dengeleyici oluşturur `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-230">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="cd3c2-231">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="cd3c2-232">Bizim yük dengeleyici sağlandığından bazı IP havuzları oluşturmak oldukça boş olur.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="cd3c2-233">Toocreate iki IP havuzları istiyoruz bizim yük dengeleyici, biri hello ön uç için diğeri hello arka uç için.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-233">We want toocreate two IP pools for our load balancer, one for hello front end and one for hello back end.</span></span> <span data-ttu-id="cd3c2-234">Merhaba ön uç IP havuzu herkese görünür.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-234">hello front-end IP pool is publicly visible.</span></span> <span data-ttu-id="cd3c2-235">Ayrıca, biz hello daha önce oluşturduğumuz PIP atamak hello konumu toowhich unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-235">It's also hello location toowhich we assign hello PIP that we created earlier.</span></span> <span data-ttu-id="cd3c2-236">Ardından hello arka uç havuzu gibi bir konuma bizim VM'ler tooconnect için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-236">Then we use hello back-end pool as a location for our VMs tooconnect to.</span></span> <span data-ttu-id="cd3c2-237">Bu şekilde hello trafiği hello yük dengeleyici toohello VM'ler akabilir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-237">That way, hello traffic can flow through hello load balancer toohello VMs.</span></span>

<span data-ttu-id="cd3c2-238">İlk olarak, bizim ön uç IP havuzu oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="cd3c2-239">Merhaba aşağıdaki örnekte oluşturur adlı bir ön uç havuzu `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-239">hello following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="cd3c2-240">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="cd3c2-241">Merhaba nasıl kullandık Not `--public-ip-name` toopass hello geçiş `myPublicIP` daha önce oluşturduğumuz.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-241">Note how we used hello `--public-ip-name` switch toopass in hello `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="cd3c2-242">Merhaba ortak IP adresi toohello yük dengeleyici tooreach sağlar, VM'ler hello Internet üzerindeki.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-242">Assigning hello public IP address toohello load balancer allows you tooreach your VMs across hello Internet.</span></span>

<span data-ttu-id="cd3c2-243">Ardından, bizim ikinci IP havuzu bizim arka uç trafiği için bu süre oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="cd3c2-244">Merhaba aşağıdaki örnekte oluşturur adlı bir arka uç havuzu `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-244">hello following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="cd3c2-245">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="cd3c2-246">Bizim yük dengeleyici ile bakarak nasıl çalıştığını görebiliriz `azure network lb show` hello JSON çıktısını inceleyerek:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining hello JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="cd3c2-247">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-247">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="cd3c2-248">Yük dengeleyicisi NAT kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd3c2-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="cd3c2-249">Bizim yük dengeleyici üzerinden akan tooget trafiği gelen veya giden eylemleri belirtin toocreate ağ adresi çevirisi (NAT) kuralları ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-249">tooget traffic flowing through our load balancer, we need toocreate network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="cd3c2-250">Merhaba Protokolü toouse belirtin, sonra istediğiniz gibi dış bağlantı noktaları toointernal bağlantı noktalarını eşleyin.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-250">You can specify hello protocol toouse, then map external ports toointernal ports as desired.</span></span> <span data-ttu-id="cd3c2-251">Bizim ortamı için SSH bizim yük dengeleyici tooour VM'ler izin veren bazı kurallar oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-251">For our environment, let's create some rules that allow SSH through our load balancer tooour VMs.</span></span> <span data-ttu-id="cd3c2-252">(Bu, daha sonra oluşturuyoruz) bizim Vm'lerinde TCP bağlantı noktaları 4222 ve 4223 toodirect tooTCP bağlantı 22 ayarlarız.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-252">We set up TCP ports 4222 and 4223 toodirect tooTCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="cd3c2-253">Merhaba aşağıdaki örnek adlı bir kural oluşturur `myLoadBalancerRuleSSH1` toomap TCP bağlantı noktası 4222 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-253">hello following example creates a rule named `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="cd3c2-254">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="cd3c2-255">Merhaba yordamı, ikinci NAT kuralı için SSH için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-255">Repeat hello procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="cd3c2-256">Merhaba aşağıdaki örnek adlı bir kural oluşturur `myLoadBalancerRuleSSH2` toomap TCP bağlantı noktası 4223 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-256">hello following example creates a rule named `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="cd3c2-257">Şimdi de tane hello kural tooour IP havuzları takma web trafiği için TCP bağlantı noktası 80 için NAT kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking hello rule up tooour IP pools.</span></span> <span data-ttu-id="cd3c2-258">Biz hello kural tooan hello kural tooour VM'ler ayrı ayrı takma yerine IP havuzu kanca varsa biz ekleyebilir veya VM'ler hello IP havuzundan kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-258">If we hook up hello rule tooan IP pool, instead of hooking up hello rule tooour VMs individually, we can add or remove VMs from hello IP pool.</span></span> <span data-ttu-id="cd3c2-259">Merhaba yük dengeleyici trafik akışını hello otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-259">hello load balancer automatically adjusts hello flow of traffic.</span></span> <span data-ttu-id="cd3c2-260">Merhaba aşağıdaki örnek adlı bir kural oluşturur `myLoadBalancerRuleWeb` toomap TCP bağlantı noktası 80 tooport 80:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-260">hello following example creates a rule named `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="cd3c2-261">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="cd3c2-262">Bir yük dengeleyici durum araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="cd3c2-262">Create a load balancer health probe</span></span>
<span data-ttu-id="cd3c2-263">Bir sistem durumu araştırması düzenli aralıklarla hello bizim yük dengeleyici toomake işletim ve toorequests tanımlanan yanıt emin olan VM'ler üzerinde denetimleri.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-263">A health probe periodically checks on hello VMs that are behind our load balancer toomake sure they're operating and responding toorequests as defined.</span></span> <span data-ttu-id="cd3c2-264">Bunlar gelen kaldırdıysanız değil, kullanıcılar olan olmayan işlemi tooensure toothem yönlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-264">If not, they're removed from operation tooensure that users aren't being directed toothem.</span></span> <span data-ttu-id="cd3c2-265">Aralıklarla ve zaman aşımı değerlerinin yanı sıra hello durumu araştırması için özel denetimleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-265">You can define custom checks for hello health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="cd3c2-266">Sistem durumu araştırmalarının hakkında daha fazla bilgi için bkz: [yük dengeleyici yoklamaları](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd3c2-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="cd3c2-267">Merhaba aşağıdaki örnekte oluşturur bir TCP durumu araştırılan adlandırılmış `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-267">hello following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="cd3c2-268">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="cd3c2-269">Burada, 15 saniye bizim durumu denetimleri için bir aralığı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="cd3c2-270">Biz, en fazla dört araştırmalar (Merhaba barındıran artık çalışmıyor hello yük dengeleyici varsaymadan önce bir dakika) eksik.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-270">We can miss a maximum of four probes (one minute) before hello load balancer considers that hello host is no longer functioning.</span></span>

## <a name="verify-hello-load-balancer"></a><span data-ttu-id="cd3c2-271">Merhaba yük dengeleyici doğrulayın</span><span class="sxs-lookup"><span data-stu-id="cd3c2-271">Verify hello load balancer</span></span>
<span data-ttu-id="cd3c2-272">Şimdi hello yük dengeleyici yapılandırması yapılır.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-272">Now hello load balancer configuration is done.</span></span> <span data-ttu-id="cd3c2-273">Yaptığınız hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-273">Here are hello steps you took:</span></span>

1. <span data-ttu-id="cd3c2-274">Bir yük dengeleyici oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-274">You created a load balancer.</span></span>
2. <span data-ttu-id="cd3c2-275">Bir ön uç IP havuzu oluşturduğunuz ve bir ortak IP tooit atanmış.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-275">You created a front-end IP pool and assigned a public IP tooit.</span></span>
3. <span data-ttu-id="cd3c2-276">Sanal makineleri bağlanabileceği bir arka uç IP havuzu oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="cd3c2-277">SSH toohello VM'ler Yönetim için web uygulamamız için TCP bağlantı noktası 80 sağlayan bir kural ile birlikte izin veren NAT kuralları oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-277">You created NAT rules that allow SSH toohello VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="cd3c2-278">Sistem durumu araştırma tooperiodically onay hello VM'ler eklendi.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-278">You added a health probe tooperiodically check hello VMs.</span></span> <span data-ttu-id="cd3c2-279">Bu sistem durumu araştırma kullanıcılar tooaccess artık çalışmıyor veya içerik hizmet veren bir VM denemeyin sağlar.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-279">This health probe ensures that users don't try tooaccess a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="cd3c2-280">Şimdi, yük dengeleyici şimdi gibi göründüğünü gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="cd3c2-281">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-281">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a><span data-ttu-id="cd3c2-282">Bir NIC toouse hello ile Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd3c2-282">Create an NIC toouse with hello Linux VM</span></span>
<span data-ttu-id="cd3c2-283">NIC program aracılığıyla kullanılabilir olduklarından kuralları tootheir kullanım uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-283">NICs are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="cd3c2-284">Birden fazla olabilir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-284">You can also have more than one.</span></span> <span data-ttu-id="cd3c2-285">Merhaba aşağıdaki `azure network nic create` komutu, hello NIC toohello yük arka uç IP Havuzu'nu bağlanmasını ve NAT kuralı toopermit SSH trafiği hello ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-285">In hello following `azure network nic create` command, you hook up hello NIC toohello load back-end IP pool and associate it with hello NAT rule toopermit SSH traffic.</span></span>

<span data-ttu-id="cd3c2-286">Hello yerine `#####-###-###` bölümleri, kendi Azure aboneliği ID'ye sahip</span><span class="sxs-lookup"><span data-stu-id="cd3c2-286">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="cd3c2-287">Aboneliğinizi hello çıktısında kimliği not ettiğiniz `jq` oluşturmakta hello kaynakları incelediğinizde.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-287">Your subscription ID is noted in hello output of `jq` when you examine hello resources you are creating.</span></span> <span data-ttu-id="cd3c2-288">Abonelik Kimliğinizle de görüntüleyebilirsiniz `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="cd3c2-289">Merhaba aşağıdaki örnekte oluşturur adlı bir NIC `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-289">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="cd3c2-290">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="cd3c2-291">Merhaba kaynak doğrudan inceleyerek hello ayrıntılarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-291">You can see hello details by examining hello resource directly.</span></span> <span data-ttu-id="cd3c2-292">Hello kullanarak hello kaynağın incelemeniz `azure network nic show` komutu:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-292">You examine hello resource by using hello `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="cd3c2-293">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-293">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="cd3c2-294">Oluşturuyoruz artık tooour arka uç IP havuzundaki yeniden takma, ikinci bir NIC hello.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-294">Now we create hello second NIC, hooking in tooour back-end IP pool again.</span></span> <span data-ttu-id="cd3c2-295">Bu zaman hello ikinci NAT kuralı SSH trafiğe izin verir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-295">This time hello second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="cd3c2-296">Merhaba aşağıdaki örnekte oluşturur adlı bir NIC `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-296">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="cd3c2-297">Bir ağ güvenlik grubu ve kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd3c2-297">Create a network security group and rules</span></span>
<span data-ttu-id="cd3c2-298">Bir ağ güvenlik grubu oluşturun ve yöneten gelen kuralları hello artık toohello NIC erişim</span><span class="sxs-lookup"><span data-stu-id="cd3c2-298">Now we create a network security group and hello inbound rules that govern access toohello NIC.</span></span> <span data-ttu-id="cd3c2-299">Bir ağ güvenlik grubu uygulanan tooa NIC veya alt ağ olabilir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-299">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="cd3c2-300">Vm'leriniz ve bu moddan kuralları toocontrol hello trafik akışını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-300">You define rules toocontrol hello flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="cd3c2-301">Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-301">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="cd3c2-302">Merhaba NSG tooallow için gelen kuralı hello ekleyelim gelen bağlantı noktası 22 (toosupport SSH) bağlantı.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-302">Let's add hello inbound rule for hello NSG tooallow inbound connections on port 22 (toosupport SSH).</span></span> <span data-ttu-id="cd3c2-303">Merhaba aşağıdaki örnek adlı bir kural oluşturur `myNetworkSecurityGroupRuleSSH` tooallow TCP bağlantı noktası 22:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-303">hello following example creates a rule named `myNetworkSecurityGroupRuleSSH` tooallow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="cd3c2-304">Şimdi hello NSG tooallow için gelen kuralı hello ekleyelim gelen bağlantı noktası 80 (toosupport web trafiği) bağlantı.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-304">Now let's add hello inbound rule for hello NSG tooallow inbound connections on port 80 (toosupport web traffic).</span></span> <span data-ttu-id="cd3c2-305">Merhaba aşağıdaki örnek adlı bir kural oluşturur `myNetworkSecurityGroupRuleHTTP` tooallow TCP bağlantı noktası 80 üzerinde:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-305">hello following example creates a rule named `myNetworkSecurityGroupRuleHTTP` tooallow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="cd3c2-306">Merhaba gelen kuralı, gelen ağ bağlantıları için bir filtredir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-306">hello inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="cd3c2-307">Bu örnekte, hello NSG toohello tüm istek tooport 22 bizim VM NIC toohello geçirilen anlamına gelir VM'ler sanal NIC bağlayın.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-307">In this example, we bind hello NSG toohello VMs virtual NIC, which means that any request tooport 22 is passed through toohello NIC on our VM.</span></span> <span data-ttu-id="cd3c2-308">Bu gelen kuralı bir ağ bağlantısı hakkında ve bir uç nokta hakkında hangi hakkında Klasik dağıtımlarda olması.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="cd3c2-309">tooopen bir bağlantı noktası, hello bırakın gerekir `--source-port-range` çok Ayarla '\*' (Merhaba varsayılan değer) tooaccept gelen istekleri **herhangi** bağlantı noktası isteme.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-309">tooopen a port, you must leave hello `--source-port-range` set too'\*' (hello default value) tooaccept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="cd3c2-310">Bağlantı noktaları genellikle dinamik.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-toohello-nic"></a><span data-ttu-id="cd3c2-311">Toohello NIC bağlama</span><span class="sxs-lookup"><span data-stu-id="cd3c2-311">Bind toohello NIC</span></span>
<span data-ttu-id="cd3c2-312">Merhaba NSG toohello NIC'ler bağlayın.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-312">Bind hello NSG toohello NICs.</span></span> <span data-ttu-id="cd3c2-313">Tooconnect bizim NIC'ler bizim ağ güvenlik grubuyla ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-313">We need tooconnect our NICs with our network security group.</span></span> <span data-ttu-id="cd3c2-314">Bizim NIC'ler her ikisi de yukarı toohook hem komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-314">Run both commands, toohook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="cd3c2-315">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd3c2-315">Create an availability set</span></span>
<span data-ttu-id="cd3c2-316">Kullanılabilirlik Yardım yayılan hata etki alanları ve yükseltme etki alanları arasında Vm'leriniz ayarlar.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="cd3c2-317">Kullanılabilirlik kümesi Vm'leriniz için oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="cd3c2-318">Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-318">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="cd3c2-319">Sanal makineler, ortak bir güç kaynağı ve ağ anahtarı paylaşmak gruplandırması hata etki alanlarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="cd3c2-320">Varsayılan olarak, kullanılabilirlik kümesi içinde yapılandırılmış hello sanal makineleri toothree hata etki alanları arasında ayrılır.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-320">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="cd3c2-321">Merhaba bir donanım sorunundan birinde bu hata etki alanları, uygulamanızı çalıştıran her VM etkilemez olur.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-321">hello idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="cd3c2-322">Azure otomatik olarak VM'ler hello hata etki alanlarında bunları bir kullanılabilirlik kümesine yerleştirdiğinizde dağıtır.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-322">Azure automatically distributes VMs across hello fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="cd3c2-323">Yükseltme etki alanları belirtmek sanal makineler ve hello yeniden temel alınan fiziksel donanım grupları aynı anda.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="cd3c2-324">Yükseltme etki alanları yeniden başlatılır hello sıra planlı bakım sırasında sıralı olmayabilir, ancak aynı anda yalnızca bir yükseltme yeniden başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-324">hello order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="cd3c2-325">Yeniden Azure otomatik olarak Vm'leriniz yükseltme etki alanları arasında bir kullanılabilirlik sitede yerleştirme sırasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="cd3c2-326">Daha fazla bilgi edinin [VM'ler hello kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd3c2-326">Read more about [managing hello availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-hello-linux-vms"></a><span data-ttu-id="cd3c2-327">Merhaba Linux VM'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd3c2-327">Create hello Linux VMs</span></span>
<span data-ttu-id="cd3c2-328">Internet'ten erişilebilen toosupport VM'ler hello depolama ve ağ kaynaklarını oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-328">You've created hello storage and network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="cd3c2-329">Şimdi şimdi bunları VM'ler oluşturun ve bir parola sahip olmayan bir SSH anahtarı ile güvenli.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="cd3c2-330">Bu durumda, bir Ubuntu VM tabanlı hello üzerinde toocreate yapacağız en son LTS.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-330">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="cd3c2-331">Biz kullanarak bu görüntü bilgilerini bulun `azure vm image list`açıklandığı gibi [Azure VM görüntülerini bulma](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd3c2-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="cd3c2-332">Merhaba komutunu kullanarak bir görüntü seçtik `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-332">We selected an image by using hello command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="cd3c2-333">Bu durumda, kullandığımız `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="cd3c2-334">Merhaba son alanı için biz geçirmek `latest` böylece hello gelecekte biz her zaman en son yapı hello alın.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-334">For hello last field, we pass `latest` so that in hello future we always get hello most recent build.</span></span> <span data-ttu-id="cd3c2-335">(kullanırız hello dizesi `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="cd3c2-335">(hello string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="cd3c2-336">Bu zaten oluşturdu tanıdık tooanyone sonraki adımdır bir ssh rsa ortak ve özel anahtarı eşleştirin Linux veya Mac kullanarak **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-336">This next step is familiar tooanyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="cd3c2-337">Tüm sertifika anahtar çiftleri varsa değil, `~/.ssh` dizin oluşturabilirsiniz bunları:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="cd3c2-338">Hello kullanarak otomatik olarak `azure vm create --generate-ssh-keys` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-338">Automatically, by using hello `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="cd3c2-339">Kullanarak el ile [hello yönergeleri toocreate bunları kendiniz](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd3c2-339">Manually, by using [hello instructions toocreate them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="cd3c2-340">Alternatif olarak, hello kullanabilirsiniz `--admin-password` yöntemi tooauthenticate SSH bağlantılarınızı hello VM sonra oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-340">Alternatively, you can use hello `--admin-password` method tooauthenticate your SSH connections after hello VM is created.</span></span> <span data-ttu-id="cd3c2-341">Bu yöntem genellikle daha az güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-341">This method is typically less secure.</span></span>

<span data-ttu-id="cd3c2-342">Bizim tüm kaynaklara ve bilgi ile birlikte hello getirerek hello VM oluşturuyoruz `azure vm create` komutu:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-342">We create hello VM by bringing all our resources and information together with hello `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="cd3c2-343">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="cd3c2-344">Varsayılan SSH anahtarları kullanılarak tooyour VM hemen bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-344">You can connect tooyour VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="cd3c2-345">Merhaba yük dengeleyici üzerinden geçirme bu yana hello uygun bağlantı noktasını belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-345">Make sure that you specify hello appropriate port since we're passing through hello load balancer.</span></span> <span data-ttu-id="cd3c2-346">(Bizim ilk VM için hello NAT kuralı tooforward bağlantı noktası 4222 tooour VM ayarlarız.)</span><span class="sxs-lookup"><span data-stu-id="cd3c2-346">(For our first VM, we set up hello NAT rule tooforward port 4222 tooour VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="cd3c2-347">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-347">Output:</span></span>

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="cd3c2-348">Tane hello ikinci VM oluşturun aynı şekilde:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-348">Go ahead and create your second VM in hello same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="cd3c2-349">Merhaba şimdi kullanabileceğiniz `azure vm show myResourceGroup myVM1` oluşturmuş olduğunuz tooexamine komutu.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-349">And you can now use hello `azure vm show myResourceGroup myVM1` command tooexamine what you've created.</span></span> <span data-ttu-id="cd3c2-350">Bu noktada, Ubuntu Vm'leriniz yük dengeleyici arkasında (parolalar devre dışı bırakıldığı için), yalnızca, SSH anahtar çifti ile içine imzalayabilirsiniz Azure'da kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="cd3c2-351">Nginx veya httpd yükleyin, bir web uygulaması dağıtma ve hello trafiğini hello yük dengeleyici tooboth hello VM'lerin aktığı.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-351">You can install nginx or httpd, deploy a web app, and see hello traffic flow through hello load balancer tooboth of hello VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="cd3c2-352">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a><span data-ttu-id="cd3c2-353">Merhaba ortamı şablon olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="cd3c2-353">Export hello environment as a template</span></span>
<span data-ttu-id="cd3c2-354">Bir ek geliştirme ortamı hello toocreate ne istediğiniz bu ortam yerleşik göre aynı parametreleri veya eşleşecek bir üretim ortamında?</span><span class="sxs-lookup"><span data-stu-id="cd3c2-354">Now that you have built out this environment, what if you want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="cd3c2-355">Resource Manager, ortamınız için tüm hello parametreleri tanımlayan JSON şablonlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-355">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="cd3c2-356">Bu JSON şablonunu başvurarak tüm ortamlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="cd3c2-357">Yapabilecekleriniz [JSON şablonları el ile oluşturabilir](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya var olan bir ortam toocreate hello JSON şablonunu verdiğiniz:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="cd3c2-358">Bu komut hello oluşturur `myResourceGroup.json` geçerli çalışma dizini dosyasında.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-358">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="cd3c2-359">Bu şablonu kullanarak bir ortam oluşturduğunuzda, hello yük dengeleyici, ağ arabirimleri ya da VM'ler için hello adları dahil olmak üzere tüm hello kaynak adları istenir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-359">When you create an environment from this template, you are prompted for all hello resource names, including hello names for hello load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="cd3c2-360">Merhaba ekleyerek bu adları şablon dosyanızın doldurabilirsiniz `-p` veya `--includeParameterDefaultValue` parametresi toohello `azure group export` daha önce gösterilen komutu.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-360">You can populate these names in your template file by adding hello `-p` or `--includeParameterDefaultValue` parameter toohello `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="cd3c2-361">JSON şablonunu toospecify hello kaynak adları, düzenlemek veya [parameters.json dosyası oluşturma](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello kaynak adları belirtir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-361">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="cd3c2-362">şablonunuzu bir ortamdan toocreate:</span><span class="sxs-lookup"><span data-stu-id="cd3c2-362">toocreate an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="cd3c2-363">Tooread isteyebilirsiniz [nasıl hakkında daha fazla şablonlardan toodeploy](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd3c2-363">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="cd3c2-364">Nasıl tooincrementally güncelleştirme ortamlarda, hello parametreleri dosyasını kullanın ve şablonları bir tek bir depolama konumundan erişim hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-364">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd3c2-365">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cd3c2-365">Next steps</span></span>
<span data-ttu-id="cd3c2-366">Artık birden çok ağ bileşenleri ve VM'ler ile çalışmaya hazır toobegin demektir.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-366">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="cd3c2-367">Burada sunulan hello çekirdek bileşenlerini kullanarak, bu örnek ortamı toobuild uygulamanızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd3c2-367">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
