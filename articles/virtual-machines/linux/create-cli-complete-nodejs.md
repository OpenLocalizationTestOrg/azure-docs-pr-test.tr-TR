---
title: "Azure CLI 1.0 ile eksiksiz bir Linux ortamı oluşturma | Microsoft Docs"
description: "Depolama, bir Linux VM, bir sanal ağ ve alt ağ, bir yük dengeleyici, bir NIC, ortak bir IP ve tüm sıfırdan Azure CLI 1.0 kullanarak bir ağ güvenlik grubu oluşturun."
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
ms.openlocfilehash: 201ccd523e49d638ace50fbc0ffdceb705b35473
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-environment-with-the-azure-cli-10"></a><span data-ttu-id="08c1e-103">Azure CLI 1.0 ile eksiksiz bir Linux ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c1e-103">Create a complete Linux environment with the Azure CLI 1.0</span></span>
<span data-ttu-id="08c1e-104">Bu makalede, bir yük dengeleyici ve geliştirme ve basit bilgi işlem için yararlı olan VM'ler çifti ile basit bir ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="08c1e-105">İki çalışma, güvenli Linux, gelen herhangi bir yere Internet'te bağlanabileceği VM'ler kadar biz komut komut işleminde size kılavuzluk.</span><span class="sxs-lookup"><span data-stu-id="08c1e-105">We walk through the process command by command, until you have two working, secure Linux VMs to which you can connect from anywhere on the Internet.</span></span> <span data-ttu-id="08c1e-106">Ardından, daha karmaşık ağlar ve ortamlar geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c1e-106">Then you can move on to more complex networks and environments.</span></span>

<span data-ttu-id="08c1e-107">Yol boyunca bağımlılık hiyerarşi, Resource Manager dağıtım modeli sağlar ve bunu hakkında ne kadar güç sağlar öğrenin.</span><span class="sxs-lookup"><span data-stu-id="08c1e-107">Along the way, you learn about the dependency hierarchy that the Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="08c1e-108">Sistem nasıl yapılandırıldığını gördükten sonra bu çok daha hızlı bir şekilde kullanarak yeniden oluşturmak için kullanabileceğiniz [Azure Resource Manager şablonları](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08c1e-108">After you see how the system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="08c1e-109">Ortamınızı bölümlerini nasıl bir araya getireceğinizi öğrenin sonra da, bunları otomatikleştirmek için şablonlar oluşturma daha kolay olur.</span><span class="sxs-lookup"><span data-stu-id="08c1e-109">Also, after you learn how the parts of your environment fit together, creating templates to automate them becomes easier.</span></span>

<span data-ttu-id="08c1e-110">Ortam içerir:</span><span class="sxs-lookup"><span data-stu-id="08c1e-110">The environment contains:</span></span>

* <span data-ttu-id="08c1e-111">İki VM bir kullanılabilirlik kümesi içinde.</span><span class="sxs-lookup"><span data-stu-id="08c1e-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="08c1e-112">Yük Dengeleyici Yük Dengeleme kuralı bağlantı noktası 80 ile.</span><span class="sxs-lookup"><span data-stu-id="08c1e-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="08c1e-113">VM gelen istenmeyen trafiği korumak için ağ güvenlik grubu (NSG) kuralları.</span><span class="sxs-lookup"><span data-stu-id="08c1e-113">Network security group (NSG) rules to protect your VM from unwanted traffic.</span></span>

<span data-ttu-id="08c1e-114">Bu özel ortam oluşturmak için en son gerekir [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Kaynak Yöneticisi modunda (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="08c1e-114">To create this custom environment, you need the latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="08c1e-115">Ayrıca aracı ayrıştırma JSON gerekir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="08c1e-116">Bu örnekte [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="08c1e-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="08c1e-117">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="08c1e-117">CLI versions to complete the task</span></span>
<span data-ttu-id="08c1e-118">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="08c1e-118">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="08c1e-119">[Azure CLI 1.0](#quick-commands) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="08c1e-119">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="08c1e-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="08c1e-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="08c1e-121">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="08c1e-121">Quick commands</span></span>
<span data-ttu-id="08c1e-122">Bir VM için Azure karşıya yüklemek için hızlı bir şekilde, aşağıdaki bölümde ayrıntıları temel görevi gerekiyorsa komutları.</span><span class="sxs-lookup"><span data-stu-id="08c1e-122">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="08c1e-123">Her adım başlangıç belgenin geri kalanı bulunabilir bilgi ve içerik daha ayrıntılı [burada](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="08c1e-123">More detailed information and context for each step can be found in the rest of the document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="08c1e-124">Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="08c1e-124">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="08c1e-125">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="08c1e-125">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="08c1e-126">Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="08c1e-127">Kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-127">Create the resource group.</span></span> <span data-ttu-id="08c1e-128">Aşağıdaki örnek, bir kaynak grubu oluşturur `myResourceGroup` içinde `westeurope` konumu:</span><span class="sxs-lookup"><span data-stu-id="08c1e-128">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="08c1e-129">Kaynak Grup, JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="08c1e-129">Verify the resource group by using the JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="08c1e-130">Depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-130">Create the storage account.</span></span> <span data-ttu-id="08c1e-131">Aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-131">The following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="08c1e-132">(Depolama hesabı adı gerekir benzersiz olmalıdır, böylece kendi benzersiz bir ad sağlayın.)</span><span class="sxs-lookup"><span data-stu-id="08c1e-132">(The storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="08c1e-133">Depolama hesabı JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="08c1e-133">Verify the storage account by using the JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="08c1e-134">Sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-134">Create the virtual network.</span></span> <span data-ttu-id="08c1e-135">Aşağıdaki örnek adlı bir sanal ağ oluşturur `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-135">The following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="08c1e-136">Bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-136">Create a subnet.</span></span> <span data-ttu-id="08c1e-137">Aşağıdaki örnek adlı bir alt ağı oluşturur `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-137">The following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="08c1e-138">Sanal ağ ve alt JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="08c1e-138">Verify the virtual network and subnet by using the JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="08c1e-139">Genel IP oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-139">Create a public IP.</span></span> <span data-ttu-id="08c1e-140">Aşağıdaki örnek adlı ortak IP oluşturur `myPublicIP` DNS adı ile `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-140">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="08c1e-141">(DNS adı gerekir benzersiz olmalıdır, böylece kendi benzersiz bir ad sağlayın.)</span><span class="sxs-lookup"><span data-stu-id="08c1e-141">(The DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="08c1e-142">Yük Dengeleyici oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-142">Create the load balancer.</span></span> <span data-ttu-id="08c1e-143">Aşağıdaki örnek, adlandırılmış bir yük dengeleyici oluşturur `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-143">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="08c1e-144">Yük Dengeleyici için bir ön uç IP havuzu oluşturun ve genel IP ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c1e-144">Create a front-end IP pool for the load balancer, and associate the public IP.</span></span> <span data-ttu-id="08c1e-145">Aşağıdaki örnek adlı bir ön uç IP havuzu oluşturur `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-145">The following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="08c1e-146">Yük Dengeleyici için arka uç IP havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-146">Create the back-end IP pool for the load balancer.</span></span> <span data-ttu-id="08c1e-147">Aşağıdaki örnek adlı bir arka uç IP havuzu oluşturur `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-147">The following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="08c1e-148">SSH gelen ağ adresi çevirisi (NAT) kuralları yük dengeleyici için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-148">Create SSH inbound network address translation (NAT) rules for the load balancer.</span></span> <span data-ttu-id="08c1e-149">Aşağıdaki örnek, iki yük dengeleyici kuralı oluşturur `myLoadBalancerRuleSSH1` ve `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-149">The following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="08c1e-150">Web oluşturulamıyor gelen NAT kuralları yük dengeleyici için.</span><span class="sxs-lookup"><span data-stu-id="08c1e-150">Create the web inbound NAT rules for the load balancer.</span></span> <span data-ttu-id="08c1e-151">Aşağıdaki örnek adlı yük dengeleyici kuralı oluşturur `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-151">The following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="08c1e-152">Yük Dengeleyici durum araştırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-152">Create the load balancer health probe.</span></span> <span data-ttu-id="08c1e-153">Aşağıdaki örnek adlı bir TCP araştırması oluşturur `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-153">The following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="08c1e-154">Yük Dengeleyici, IP havuzları ve NAT kuralları JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="08c1e-154">Verify the load balancer, IP pools, and NAT rules by using the JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="08c1e-155">İlk ağ arabirim kartı (NIC) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-155">Create the first network interface card (NIC).</span></span> <span data-ttu-id="08c1e-156">Değiştir `#####-###-###` bölümleri, kendi Azure aboneliği ID'ye sahip</span><span class="sxs-lookup"><span data-stu-id="08c1e-156">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="08c1e-157">Aboneliğinizi çıktısında kimliği not ettiğiniz **jq** oluşturmakta kaynakları incelediğinizde.</span><span class="sxs-lookup"><span data-stu-id="08c1e-157">Your subscription ID is noted in the output of **jq** when you examine the resources you are creating.</span></span> <span data-ttu-id="08c1e-158">Abonelik Kimliğinizle de görüntüleyebilirsiniz `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="08c1e-159">Aşağıdaki örnek, adlandırılmış bir NIC oluşturur `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-159">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="08c1e-160">İkinci NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="08c1e-160">Create the second NIC.</span></span> <span data-ttu-id="08c1e-161">Aşağıdaki örnek, adlandırılmış bir NIC oluşturur `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-161">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="08c1e-162">İki NIC JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="08c1e-162">Verify the two NICs by using the JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="08c1e-163">Ağ güvenlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-163">Create the network security group.</span></span> <span data-ttu-id="08c1e-164">Aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-164">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="08c1e-165">Ağ güvenlik grubu için iki gelen kuralı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="08c1e-165">Add two inbound rules for the network security group.</span></span> <span data-ttu-id="08c1e-166">Aşağıdaki örnek, iki kural oluşturur `myNetworkSecurityGroupRuleSSH` ve `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-166">The following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="08c1e-167">Ağ güvenlik grubu ve gelen kuralları JSON ayrıştırıcısı kullanarak doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="08c1e-167">Verify the network security group and inbound rules by using the JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="08c1e-168">Ağ güvenlik grubu için iki NIC bağlayın:</span><span class="sxs-lookup"><span data-stu-id="08c1e-168">Bind the network security group to the two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="08c1e-169">Kullanılabilirlik kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-169">Create the availability set.</span></span> <span data-ttu-id="08c1e-170">Aşağıdaki örnek, kullanılabilirlik adlandırılmış kümesi oluşturur `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-170">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="08c1e-171">İlk Linux VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-171">Create the first Linux VM.</span></span> <span data-ttu-id="08c1e-172">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-172">The following example creates a VM named `myVM1`:</span></span>

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

<span data-ttu-id="08c1e-173">İkinci Linux VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-173">Create the second Linux VM.</span></span> <span data-ttu-id="08c1e-174">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-174">The following example creates a VM named `myVM2`:</span></span>

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

<span data-ttu-id="08c1e-175">JSON ayrıştırıcı doğrulamak için oluşturulmuş her şeyi kullanın:</span><span class="sxs-lookup"><span data-stu-id="08c1e-175">Use the JSON parser to verify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="08c1e-176">Ortamınızı hızla yeni örnekleri yeniden oluşturmak için bir şablonu dışarı aktarın:</span><span class="sxs-lookup"><span data-stu-id="08c1e-176">Export your new environment to a template to quickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="08c1e-177">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="08c1e-177">Detailed walkthrough</span></span>
<span data-ttu-id="08c1e-178">Ortamınızı yapı gibi her komutun ne yaptığını ayrıntılı adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="08c1e-178">The detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="08c1e-179">Bu kavramlar, kendi özel ortamınız için geliştirme veya üretim derlerken faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="08c1e-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="08c1e-180">Bilgisayarınızda yüklü olduğundan emin olun [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) oturum açmış ve Resource Manager modunu kullanma:</span><span class="sxs-lookup"><span data-stu-id="08c1e-180">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="08c1e-181">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="08c1e-181">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="08c1e-182">Örnek parametre adlarında `myResourceGroup`, `mystorageaccount`, ve `myVM`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="08c1e-183">Kaynak grupları oluşturun ve dağıtım konumları seçin</span><span class="sxs-lookup"><span data-stu-id="08c1e-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="08c1e-184">Azure kaynak gruplarını yapılandırma bilgilerini ve kaynak dağıtımları mantıksal yönetimini etkinleştirmek için meta veriler içeren mantıksal dağıtım varlıklardır.</span><span class="sxs-lookup"><span data-stu-id="08c1e-184">Azure resource groups are logical deployment entities that contain configuration information and metadata to enable the logical management of resource deployments.</span></span> <span data-ttu-id="08c1e-185">Aşağıdaki örnek, bir kaynak grubu oluşturur `myResourceGroup` içinde `westeurope` konumu:</span><span class="sxs-lookup"><span data-stu-id="08c1e-185">The following example creates a resource group named `myResourceGroup` in the `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="08c1e-186">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-186">Output:</span></span>

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

## <a name="create-a-storage-account"></a><span data-ttu-id="08c1e-187">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c1e-187">Create a storage account</span></span>
<span data-ttu-id="08c1e-188">Eklemek istediğiniz herhangi bir ek veri disklerinin ve VM diskleriniz için depolama hesapları gerekir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-188">You need storage accounts for your VM disks and for any additional data disks that you want to add.</span></span> <span data-ttu-id="08c1e-189">Kaynak grupları oluşturun sonra hemen hemen depolama hesapları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="08c1e-190">Burada kullandığımız `azure storage account create` komutu, hesap, kaynak grubu konumu geçirme denetler ve istediğiniz depolama destek türü.</span><span class="sxs-lookup"><span data-stu-id="08c1e-190">Here we use the `azure storage account create` command, passing the location of the account, the resource group that controls it, and the type of storage support you want.</span></span> <span data-ttu-id="08c1e-191">Aşağıdaki örnek adlı bir depolama hesabı oluşturur `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-191">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="08c1e-192">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="08c1e-193">Bizim kaynak grubu kullanarak incelemek için `azure group show` komutu, kullanalım [jq](https://stedolan.github.io/jq/) ile birlikte aracı `--json` Azure CLI seçeneği.</span><span class="sxs-lookup"><span data-stu-id="08c1e-193">To examine our resource group by using the `azure group show` command, let's use the [jq](https://stedolan.github.io/jq/) tool along with the `--json` Azure CLI option.</span></span> <span data-ttu-id="08c1e-194">(Kullanabileceğiniz **jsawk** veya JSON ayrıştırmak için tercih ettiğiniz herhangi bir dil kitaplığı.)</span><span class="sxs-lookup"><span data-stu-id="08c1e-194">(You can use **jsawk** or any language library you prefer to parse the JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="08c1e-195">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-195">Output:</span></span>

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

<span data-ttu-id="08c1e-196">CLI kullanarak depolama hesabına araştırmak için ilk hesap adlarını ve anahtarları ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-196">To investigate the storage account by using the CLI, you first need to set the account names and keys.</span></span> <span data-ttu-id="08c1e-197">Aşağıdaki örnekte depolama hesabı adı seçtiğiniz bir adla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="08c1e-197">Replace the name of the storage account in the following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="08c1e-198">Ardından, depolama bilgilerinizi kolayca görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="08c1e-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="08c1e-199">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="08c1e-200">Bir sanal ağ ve alt ağ oluşturun</span><span class="sxs-lookup"><span data-stu-id="08c1e-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="08c1e-201">Sonraki Azure ve Vm'lerinizi oluşturabileceğiniz bir alt ağ içinde çalışan bir sanal ağ oluşturmak ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="08c1e-201">Next you're going to need to create a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="08c1e-202">Aşağıdaki örnek adlı bir sanal ağ oluşturur `myVnet` ile `192.168.0.0/16` adres öneki:</span><span class="sxs-lookup"><span data-stu-id="08c1e-202">The following example creates a virtual network named `myVnet` with the `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="08c1e-203">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-203">Output:</span></span>

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

<span data-ttu-id="08c1e-204">Yeniden--json seçeneği kullanalım `azure group show` ve `jq` nasıl KAYNAKLARIMIZI oluşturmakta olduğumuz görmek için.</span><span class="sxs-lookup"><span data-stu-id="08c1e-204">Again, let's use the --json option of `azure group show` and `jq` to see how we're building our resources.</span></span> <span data-ttu-id="08c1e-205">Şimdi sahip olduğumuz bir `storageAccounts` kaynak ve `virtualNetworks` kaynak.</span><span class="sxs-lookup"><span data-stu-id="08c1e-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="08c1e-206">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-206">Output:</span></span>

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

<span data-ttu-id="08c1e-207">Şimdi bir alt ağda oluşturalım `myVnet` sanal ağ, sanal makineleri dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="08c1e-207">Now let's create a subnet in the `myVnet` virtual network into which the VMs are deployed.</span></span> <span data-ttu-id="08c1e-208">Kullanırız `azure network vnet subnet create` zaten oluşturduğumuz kaynakları birlikte komutu: `myResourceGroup` kaynak grubu ve `myVnet` sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="08c1e-208">We use the `azure network vnet subnet create` command, along with the resources we've already created: the `myResourceGroup` resource group and the `myVnet` virtual network.</span></span> <span data-ttu-id="08c1e-209">Aşağıdaki örnekte, eklediğimiz adlı alt ağın `mySubnet` alt ağ adresi öneki ile `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-209">In the following example, we add the subnet named `mySubnet` with the subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="08c1e-210">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up the subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up the subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="08c1e-211">Alt ağ içindeki sanal ağı mantıksal olarak olduğundan, biz biraz farklı bir komutla alt ağ bilgilerini arayın.</span><span class="sxs-lookup"><span data-stu-id="08c1e-211">Because the subnet is logically inside the virtual network, we look for the subnet information with a slightly different command.</span></span> <span data-ttu-id="08c1e-212">Kullanırız komut `azure network vnet show`, ancak kullanarak JSON çıktısını incelemek devam `jq`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-212">The command we use is `azure network vnet show`, but we continue to examine the JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="08c1e-213">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-213">Output:</span></span>

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

## <a name="create-a-public-ip-address"></a><span data-ttu-id="08c1e-214">Genel IP adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c1e-214">Create a public IP address</span></span>
<span data-ttu-id="08c1e-215">Şimdi biz yük dengeleyicinizin Ata genel IP adresi (PIP) oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="08c1e-215">Now let's create the public IP address (PIP) that we assign to your load balancer.</span></span> <span data-ttu-id="08c1e-216">Vm'leriniz için Internet'ten kullanarak bağlanmak sağlar `azure network public-ip create` komutu.</span><span class="sxs-lookup"><span data-stu-id="08c1e-216">It enables you to connect to your VMs from the Internet by using the `azure network public-ip create` command.</span></span> <span data-ttu-id="08c1e-217">Varsayılan Adres dinamik olduğundan, adlandırılmış bir DNS girişi oluşturuyoruz **cloudapp.azure.com** kullanarak etki alanı `--domain-name-label` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="08c1e-217">Because the default address is dynamic, we create a named DNS entry in the **cloudapp.azure.com** domain by using the `--domain-name-label` option.</span></span> <span data-ttu-id="08c1e-218">Aşağıdaki örnek adlı ortak IP oluşturur `myPublicIP` DNS adı ile `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-218">The following example creates a public IP named `myPublicIP` with the DNS name of `mypublicdns`.</span></span> <span data-ttu-id="08c1e-219">DNS adının benzersiz olması gerektiğinden, kendi benzersiz DNS adını belirtin:</span><span class="sxs-lookup"><span data-stu-id="08c1e-219">Because the DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="08c1e-220">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up the public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up the public ip "myPublicIP"
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

<span data-ttu-id="08c1e-221">Kendisiyle görebilmeniz için genel IP adresini de üst düzey bir kaynak değildir `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-221">The public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="08c1e-222">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-222">Output:</span></span>

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

<span data-ttu-id="08c1e-223">Tam kullanarak alt etki alanının tam etki alanı adı (FQDN) de dahil olmak üzere daha fazla kaynak ayrıntılarını araştırabilirsiniz `azure network public-ip show` komutu.</span><span class="sxs-lookup"><span data-stu-id="08c1e-223">You can investigate more resource details, including the fully qualified domain name (FQDN) of the subdomain, by using the complete `azure network public-ip show` command.</span></span> <span data-ttu-id="08c1e-224">Ortak IP adresi kaynağı mantıksal olarak ayrıldı, ancak belirli bir adresi yok henüz atanmamış.</span><span class="sxs-lookup"><span data-stu-id="08c1e-224">The public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="08c1e-225">Bir IP adresi elde etmek için değil henüz oluşturduk bir yük dengeleyici ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="08c1e-225">To obtain an IP address, you're going to need a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="08c1e-226">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-226">Output:</span></span>

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

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="08c1e-227">Bir yük dengeleyici ve IP havuzları oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c1e-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="08c1e-228">Bir yük dengeleyici oluşturduğunuzda, trafiği birden çok VM dağıtmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="08c1e-228">When you create a load balancer, it enables you to distribute traffic across multiple VMs.</span></span> <span data-ttu-id="08c1e-229">Ayrıca, Bakım veya ağır yük durumunda kullanıcı isteklerine yanıt birden çok VM çalıştırarak uygulamanız için artıklık da sağlar.</span><span class="sxs-lookup"><span data-stu-id="08c1e-229">It also provides redundancy to your application by running multiple VMs that respond to user requests in the event of maintenance or heavy loads.</span></span> <span data-ttu-id="08c1e-230">Aşağıdaki örnek, adlandırılmış bir yük dengeleyici oluşturur `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-230">The following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="08c1e-231">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up the load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="08c1e-232">Bizim yük dengeleyici sağlandığından bazı IP havuzları oluşturmak oldukça boş olur.</span><span class="sxs-lookup"><span data-stu-id="08c1e-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="08c1e-233">Bizim yük dengeleyicisi, ön uç için diğeri için arka uç için iki IP havuzları oluşturmak üzere istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="08c1e-233">We want to create two IP pools for our load balancer, one for the front end and one for the back end.</span></span> <span data-ttu-id="08c1e-234">Ön uç IP havuzu herkese görünür.</span><span class="sxs-lookup"><span data-stu-id="08c1e-234">The front-end IP pool is publicly visible.</span></span> <span data-ttu-id="08c1e-235">Ayrıca, daha önce oluşturduğumuz PIP atamak biz konum değil.</span><span class="sxs-lookup"><span data-stu-id="08c1e-235">It's also the location to which we assign the PIP that we created earlier.</span></span> <span data-ttu-id="08c1e-236">Ardından arka uç havuzu bizim VM'ler için bir konum olarak bağlanmak için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="08c1e-236">Then we use the back-end pool as a location for our VMs to connect to.</span></span> <span data-ttu-id="08c1e-237">Bu şekilde, sanal makineleri yük dengeleyiciye üzerinden trafik akabilir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-237">That way, the traffic can flow through the load balancer to the VMs.</span></span>

<span data-ttu-id="08c1e-238">İlk olarak, bizim ön uç IP havuzu oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="08c1e-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="08c1e-239">Aşağıdaki örnek adlı bir ön uç havuzu oluşturur `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-239">The following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="08c1e-240">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up the load balancer "myLoadBalancer"
+ Looking up the public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="08c1e-241">Nasıl kullandık Not `--public-ip-name` içinde geçirmek için geçiş `myPublicIP` daha önce oluşturduğumuz.</span><span class="sxs-lookup"><span data-stu-id="08c1e-241">Note how we used the `--public-ip-name` switch to pass in the `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="08c1e-242">Genel IP adresini yük dengeleyici ile atama Vm'leriniz Internet üzerinden erişmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="08c1e-242">Assigning the public IP address to the load balancer allows you to reach your VMs across the Internet.</span></span>

<span data-ttu-id="08c1e-243">Ardından, bizim ikinci IP havuzu bizim arka uç trafiği için bu süre oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="08c1e-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="08c1e-244">Aşağıdaki örnek adlı bir arka uç havuzu oluşturur `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-244">The following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="08c1e-245">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="08c1e-246">Bizim yük dengeleyici ile bakarak nasıl çalıştığını görebiliriz `azure network lb show` ve JSON çıktısını inceleyerek:</span><span class="sxs-lookup"><span data-stu-id="08c1e-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining the JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="08c1e-247">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-247">Output:</span></span>

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

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="08c1e-248">Yük dengeleyicisi NAT kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c1e-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="08c1e-249">Bizim yük dengeleyici üzerinden giden trafiği almak için biz ağ adresi gelen veya giden eylemleri belirtin çevirisi (NAT) kuralları oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-249">To get traffic flowing through our load balancer, we need to create network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="08c1e-250">Kullanılacak protokolü belirtin, sonra istediğiniz gibi dahili bağlantı noktaları için dış bağlantı noktası eşleme.</span><span class="sxs-lookup"><span data-stu-id="08c1e-250">You can specify the protocol to use, then map external ports to internal ports as desired.</span></span> <span data-ttu-id="08c1e-251">Bizim ortamı için SSH bizim VM'ler bizim yük dengeleyiciye üzerinden izin veren bazı kurallar oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="08c1e-251">For our environment, let's create some rules that allow SSH through our load balancer to our VMs.</span></span> <span data-ttu-id="08c1e-252">TCP bağlantı noktası 22 (hangi daha sonra oluşturuyoruz) bizim Vm'lerinde yönlendirmek için TCP bağlantı noktalarını 4222 ve 4223 ayarlarız.</span><span class="sxs-lookup"><span data-stu-id="08c1e-252">We set up TCP ports 4222 and 4223 to direct to TCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="08c1e-253">Aşağıdaki örnek, adında bir kural oluşturur `myLoadBalancerRuleSSH1` bağlantı noktası 22 TCP bağlantı noktası 4222 eşlemek için:</span><span class="sxs-lookup"><span data-stu-id="08c1e-253">The following example creates a rule named `myLoadBalancerRuleSSH1` to map TCP port 4222 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="08c1e-254">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up the load balancer "myLoadBalancer"
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

<span data-ttu-id="08c1e-255">Yordamı, ikinci NAT kuralı için SSH için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="08c1e-255">Repeat the procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="08c1e-256">Aşağıdaki örnek, adında bir kural oluşturur `myLoadBalancerRuleSSH2` TCP bağlantı noktası 4223 bağlantı noktası 22 eşlemek için:</span><span class="sxs-lookup"><span data-stu-id="08c1e-256">The following example creates a rule named `myLoadBalancerRuleSSH2` to map TCP port 4223 to port 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="08c1e-257">Şimdi de tane bizim IP havuzları kadar kural takma web trafiği için TCP bağlantı noktası 80 için NAT kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking the rule up to our IP pools.</span></span> <span data-ttu-id="08c1e-258">Biz kural bizim VM'ler için ayrı ayrı takma yerine bir IP havuzuna kural bağlanacağını varsa biz ekleyebilir veya VM'ler IP havuzundan kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c1e-258">If we hook up the rule to an IP pool, instead of hooking up the rule to our VMs individually, we can add or remove VMs from the IP pool.</span></span> <span data-ttu-id="08c1e-259">Yük Dengeleyici trafik akışını otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="08c1e-259">The load balancer automatically adjusts the flow of traffic.</span></span> <span data-ttu-id="08c1e-260">Aşağıdaki örnek, adında bir kural oluşturur `myLoadBalancerRuleWeb` TCP bağlantı noktası 80 80 numaralı bağlantı noktasına eşlemek için:</span><span class="sxs-lookup"><span data-stu-id="08c1e-260">The following example creates a rule named `myLoadBalancerRuleWeb` to map TCP port 80 to port 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="08c1e-261">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up the load balancer "myLoadBalancer"
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

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="08c1e-262">Bir yük dengeleyici durum araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="08c1e-262">Create a load balancer health probe</span></span>
<span data-ttu-id="08c1e-263">Bir sistem durumu araştırması düzenli aralıklarla işletim ve tanımlanan isteklerine yanıt emin olmak için yük dengeleyicinin ardındaysa VM'ler denetler.</span><span class="sxs-lookup"><span data-stu-id="08c1e-263">A health probe periodically checks on the VMs that are behind our load balancer to make sure they're operating and responding to requests as defined.</span></span> <span data-ttu-id="08c1e-264">Aksi durumda, kullanıcıların kendilerine yönlendirilmeye olmayan emin olmak için işlem kaldırılmış.</span><span class="sxs-lookup"><span data-stu-id="08c1e-264">If not, they're removed from operation to ensure that users aren't being directed to them.</span></span> <span data-ttu-id="08c1e-265">Aralıklarla ve zaman aşımı değerlerinin yanı sıra durumu araştırması için özel denetimleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c1e-265">You can define custom checks for the health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="08c1e-266">Sistem durumu araştırmalarının hakkında daha fazla bilgi için bkz: [yük dengeleyici yoklamaları](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08c1e-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="08c1e-267">Aşağıdaki örnek, bir TCP oluşturur sistem durumu araştırılan adlandırılmış `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-267">The following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="08c1e-268">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up the load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="08c1e-269">Burada, 15 saniye bizim durumu denetimleri için bir aralığı belirtildi.</span><span class="sxs-lookup"><span data-stu-id="08c1e-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="08c1e-270">Biz, en fazla dört araştırmalar (bir yük dengeleyici konak artık çalışmıyor varsaymadan önce dakika) eksik.</span><span class="sxs-lookup"><span data-stu-id="08c1e-270">We can miss a maximum of four probes (one minute) before the load balancer considers that the host is no longer functioning.</span></span>

## <a name="verify-the-load-balancer"></a><span data-ttu-id="08c1e-271">Yük Dengeleyici doğrulayın</span><span class="sxs-lookup"><span data-stu-id="08c1e-271">Verify the load balancer</span></span>
<span data-ttu-id="08c1e-272">Yük Dengeleyici yapılandırması şimdi yapılır.</span><span class="sxs-lookup"><span data-stu-id="08c1e-272">Now the load balancer configuration is done.</span></span> <span data-ttu-id="08c1e-273">Yaptığınız adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08c1e-273">Here are the steps you took:</span></span>

1. <span data-ttu-id="08c1e-274">Bir yük dengeleyici oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="08c1e-274">You created a load balancer.</span></span>
2. <span data-ttu-id="08c1e-275">Bir ön uç IP havuzu oluşturduğunuz ve bir genel IP atanmış.</span><span class="sxs-lookup"><span data-stu-id="08c1e-275">You created a front-end IP pool and assigned a public IP to it.</span></span>
3. <span data-ttu-id="08c1e-276">Sanal makineleri bağlanabileceği bir arka uç IP havuzu oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="08c1e-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="08c1e-277">Yönetim için web uygulamamız için TCP bağlantı noktası 80 sağlayan bir kural birlikte VM'ler için SSH izin veren NAT kuralları oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="08c1e-277">You created NAT rules that allow SSH to the VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="08c1e-278">Düzenli aralıklarla VM'ler denetlemek için bir sistem durumu araştırması eklendi.</span><span class="sxs-lookup"><span data-stu-id="08c1e-278">You added a health probe to periodically check the VMs.</span></span> <span data-ttu-id="08c1e-279">Bu sistem durumu araştırma, kullanıcılar artık çalışmıyor veya içerik hizmet veren bir VM erişmek denemeyin sağlar.</span><span class="sxs-lookup"><span data-stu-id="08c1e-279">This health probe ensures that users don't try to access a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="08c1e-280">Şimdi, yük dengeleyici şimdi gibi göründüğünü gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="08c1e-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="08c1e-281">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-281">Output:</span></span>

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

## <a name="create-an-nic-to-use-with-the-linux-vm"></a><span data-ttu-id="08c1e-282">Linux VM ile kullanmak için bir NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="08c1e-282">Create an NIC to use with the Linux VM</span></span>
<span data-ttu-id="08c1e-283">NIC program aracılığıyla kullanılabilir olduklarından kullanımları kuralları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c1e-283">NICs are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="08c1e-284">Birden fazla olabilir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-284">You can also have more than one.</span></span> <span data-ttu-id="08c1e-285">Aşağıdaki `azure network nic create` komutu, yük arka uç IP havuzu NIC'ye bağlanacağını ve SSH trafiğe izin vermek için NAT kuralı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="08c1e-285">In the following `azure network nic create` command, you hook up the NIC to the load back-end IP pool and associate it with the NAT rule to permit SSH traffic.</span></span>

<span data-ttu-id="08c1e-286">Değiştir `#####-###-###` bölümleri, kendi Azure aboneliği ID'ye sahip</span><span class="sxs-lookup"><span data-stu-id="08c1e-286">Replace the `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="08c1e-287">Aboneliğinizi çıktısında kimliği not ettiğiniz `jq` oluşturmakta kaynakları incelediğinizde.</span><span class="sxs-lookup"><span data-stu-id="08c1e-287">Your subscription ID is noted in the output of `jq` when you examine the resources you are creating.</span></span> <span data-ttu-id="08c1e-288">Abonelik Kimliğinizle de görüntüleyebilirsiniz `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="08c1e-289">Aşağıdaki örnek, adlandırılmış bir NIC oluşturur `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-289">The following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="08c1e-290">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up the subnet "mySubnet"
+ Looking up the network interface "myNic1"
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

<span data-ttu-id="08c1e-291">Kaynağı doğrudan inceleyerek ayrıntılarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c1e-291">You can see the details by examining the resource directly.</span></span> <span data-ttu-id="08c1e-292">Kullanarak kaynağın incelemeniz `azure network nic show` komutu:</span><span class="sxs-lookup"><span data-stu-id="08c1e-292">You examine the resource by using the `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="08c1e-293">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-293">Output:</span></span>

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

<span data-ttu-id="08c1e-294">Şimdi takma yeniden bizim arka uç IP havuzuna, ikinci bir NIC oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-294">Now we create the second NIC, hooking in to our back-end IP pool again.</span></span> <span data-ttu-id="08c1e-295">Bu zaman ikinci NAT kuralı SSH trafiğe izin verir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-295">This time the second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="08c1e-296">Aşağıdaki örnek, adlandırılmış bir NIC oluşturur `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-296">The following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="08c1e-297">Bir ağ güvenlik grubu ve kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c1e-297">Create a network security group and rules</span></span>
<span data-ttu-id="08c1e-298">Şimdi biz bir ağ güvenlik grubu ve NIC erişimi yöneten gelen kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c1e-298">Now we create a network security group and the inbound rules that govern access to the NIC.</span></span> <span data-ttu-id="08c1e-299">Bir ağ güvenlik grubu, bir NIC veya alt ağ için uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-299">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="08c1e-300">Vm'leriniz ve trafik akışını denetlemek için kurallar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="08c1e-300">You define rules to control the flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="08c1e-301">Aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-301">The following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="08c1e-302">NSG bağlantı noktası 22 (SSH desteklemek için) gelen bağlantılara izin vermek için gelen kuralı ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="08c1e-302">Let's add the inbound rule for the NSG to allow inbound connections on port 22 (to support SSH).</span></span> <span data-ttu-id="08c1e-303">Aşağıdaki örnek, adında bir kural oluşturur `myNetworkSecurityGroupRuleSSH` bağlantı noktası 22 üzerinde TCP'ye izin vermek için:</span><span class="sxs-lookup"><span data-stu-id="08c1e-303">The following example creates a rule named `myNetworkSecurityGroupRuleSSH` to allow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="08c1e-304">Şimdi NSG (web trafiği desteklemek için) 80 numaralı bağlantı noktasında gelen bağlantılara izin vermek için gelen kuralı ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="08c1e-304">Now let's add the inbound rule for the NSG to allow inbound connections on port 80 (to support web traffic).</span></span> <span data-ttu-id="08c1e-305">Aşağıdaki örnek, adında bir kural oluşturur `myNetworkSecurityGroupRuleHTTP` bağlantı noktası 80 üzerinde TCP'ye izin vermek için:</span><span class="sxs-lookup"><span data-stu-id="08c1e-305">The following example creates a rule named `myNetworkSecurityGroupRuleHTTP` to allow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="08c1e-306">Gelen kuralı, gelen ağ bağlantıları için bir filtredir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-306">The inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="08c1e-307">Bu örnekte, bağlantı noktası 22 için herhangi bir istek NIC'ye bizim VM geçirilir, anlamına gelir VM'ler sanal NIC için NSG bağlayın.</span><span class="sxs-lookup"><span data-stu-id="08c1e-307">In this example, we bind the NSG to the VMs virtual NIC, which means that any request to port 22 is passed through to the NIC on our VM.</span></span> <span data-ttu-id="08c1e-308">Bu gelen kuralı bir ağ bağlantısı hakkında ve bir uç nokta hakkında hangi hakkında Klasik dağıtımlarda olması.</span><span class="sxs-lookup"><span data-stu-id="08c1e-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="08c1e-309">Bir bağlantı noktasını açmak için bırakmalıdır `--source-port-range` kümesine '\*' (öğesinden gelen istekleri kabul etmek için varsayılan değer) **herhangi** bağlantı noktası isteme.</span><span class="sxs-lookup"><span data-stu-id="08c1e-309">To open a port, you must leave the `--source-port-range` set to '\*' (the default value) to accept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="08c1e-310">Bağlantı noktaları genellikle dinamik.</span><span class="sxs-lookup"><span data-stu-id="08c1e-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-to-the-nic"></a><span data-ttu-id="08c1e-311">NIC'ye bağlama</span><span class="sxs-lookup"><span data-stu-id="08c1e-311">Bind to the NIC</span></span>
<span data-ttu-id="08c1e-312">NSG NIC'ler bağlayın.</span><span class="sxs-lookup"><span data-stu-id="08c1e-312">Bind the NSG to the NICs.</span></span> <span data-ttu-id="08c1e-313">Bizim NIC'ler bizim ağ güvenlik grubuyla bağlanmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-313">We need to connect our NICs with our network security group.</span></span> <span data-ttu-id="08c1e-314">Hem bizim NIC'ler kanca için her iki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="08c1e-314">Run both commands, to hook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="08c1e-315">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c1e-315">Create an availability set</span></span>
<span data-ttu-id="08c1e-316">Kullanılabilirlik Yardım yayılan hata etki alanları ve yükseltme etki alanları arasında Vm'leriniz ayarlar.</span><span class="sxs-lookup"><span data-stu-id="08c1e-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="08c1e-317">Kullanılabilirlik kümesi Vm'leriniz için oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="08c1e-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="08c1e-318">Aşağıdaki örnek, kullanılabilirlik adlandırılmış kümesi oluşturur `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="08c1e-318">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="08c1e-319">Sanal makineler, ortak bir güç kaynağı ve ağ anahtarı paylaşmak gruplandırması hata etki alanlarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="08c1e-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="08c1e-320">Varsayılan olarak, en çok üç hata etki alanlarında kullanılabilirlik kümesi içinde yapılandırılmış olan sanal makinelere ayrılır.</span><span class="sxs-lookup"><span data-stu-id="08c1e-320">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="08c1e-321">Bu hata etki alanlarını birinde bir donanım sorunundan uygulamanızı çalıştıran her VM etkilemez olur.</span><span class="sxs-lookup"><span data-stu-id="08c1e-321">The idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="08c1e-322">Azure otomatik olarak VM'ler hata etki alanlarında bunları bir kullanılabilirlik kümesine yerleştirdiğinizde dağıtır.</span><span class="sxs-lookup"><span data-stu-id="08c1e-322">Azure automatically distributes VMs across the fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="08c1e-323">Yükseltme etki alanları, sanal makineler ve aynı anda yeniden temel alınan fiziksel donanım grupları belirtin.</span><span class="sxs-lookup"><span data-stu-id="08c1e-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="08c1e-324">Yükseltme etki alanları yeniden başlatılır sıra planlı bakım sırasında sıralı olmayabilir, ancak aynı anda yalnızca bir yükseltme yeniden başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="08c1e-324">The order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="08c1e-325">Yeniden Azure otomatik olarak Vm'leriniz yükseltme etki alanları arasında bir kullanılabilirlik sitede yerleştirme sırasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="08c1e-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="08c1e-326">Daha fazla bilgi edinin [VM'ler kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08c1e-326">Read more about [managing the availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-the-linux-vms"></a><span data-ttu-id="08c1e-327">Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="08c1e-327">Create the Linux VMs</span></span>
<span data-ttu-id="08c1e-328">Internet'ten erişilebilen sanal makineleri desteklemek için depolama ve ağ kaynaklarının oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="08c1e-328">You've created the storage and network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="08c1e-329">Şimdi şimdi bunları VM'ler oluşturun ve bir parola sahip olmayan bir SSH anahtarı ile güvenli.</span><span class="sxs-lookup"><span data-stu-id="08c1e-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="08c1e-330">Bu durumda, bir Ubuntu VM en son LTS göre oluşturmak için yapacağız.</span><span class="sxs-lookup"><span data-stu-id="08c1e-330">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="08c1e-331">Biz kullanarak bu görüntü bilgilerini bulun `azure vm image list`açıklandığı gibi [Azure VM görüntülerini bulma](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08c1e-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="08c1e-332">Komutunu kullanarak bir görüntü seçtik `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-332">We selected an image by using the command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="08c1e-333">Bu durumda, kullandığımız `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="08c1e-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="08c1e-334">Son alanı için biz geçirmek `latest` böylece gelecekte en son yapı'biz her zaman alın.</span><span class="sxs-lookup"><span data-stu-id="08c1e-334">For the last field, we pass `latest` so that in the future we always get the most recent build.</span></span> <span data-ttu-id="08c1e-335">(Kullanırız dizesi `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="08c1e-335">(The string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="08c1e-336">Bu sonraki adım zaten oluşturulmuş herkes alışkın olduğu bir ssh rsa ortak ve özel anahtarı eşleştirin Linux veya Mac kullanarak **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="08c1e-336">This next step is familiar to anyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="08c1e-337">Tüm sertifika anahtar çiftleri varsa değil, `~/.ssh` dizin oluşturabilirsiniz bunları:</span><span class="sxs-lookup"><span data-stu-id="08c1e-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="08c1e-338">Kullanarak otomatik olarak `azure vm create --generate-ssh-keys` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="08c1e-338">Automatically, by using the `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="08c1e-339">Kullanarak el ile [kendiniz oluşturmanız için yönergeler](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08c1e-339">Manually, by using [the instructions to create them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="08c1e-340">Alternatif olarak, kullanabileceğiniz `--admin-password` VM oluşturulduktan sonra SSH bağlantılarının kimliğini doğrulamak için yöntem.</span><span class="sxs-lookup"><span data-stu-id="08c1e-340">Alternatively, you can use the `--admin-password` method to authenticate your SSH connections after the VM is created.</span></span> <span data-ttu-id="08c1e-341">Bu yöntem genellikle daha az güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-341">This method is typically less secure.</span></span>

<span data-ttu-id="08c1e-342">Bizim tüm kaynakları ve bilgileri ile birlikte getirerek VM oluşturuyoruz `azure vm create` komutu:</span><span class="sxs-lookup"><span data-stu-id="08c1e-342">We create the VM by bringing all our resources and information together with the `azure vm create` command:</span></span>

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

<span data-ttu-id="08c1e-343">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up the VM "myVM1"
info:    Verifying the public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account mystorageaccount
+ Looking up the availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up the NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in the NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    The storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by the parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="08c1e-344">Varsayılan SSH anahtarları kullanılarak VM'nize hemen bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-344">You can connect to your VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="08c1e-345">Yük Dengeleyici üzerinden geçirme bu yana uygun bağlantı noktasını belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-345">Make sure that you specify the appropriate port since we're passing through the load balancer.</span></span> <span data-ttu-id="08c1e-346">(Bizim ilk VM için NAT kuralı bağlantı noktası 4222 bizim VM iletmek için ayarlarız.)</span><span class="sxs-lookup"><span data-stu-id="08c1e-346">(For our first VM, we set up the NAT rule to forward port 4222 to our VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="08c1e-347">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-347">Output:</span></span>

```bash
The authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="08c1e-348">Tane ikinci VM'nizi aynı şekilde oluşturun:</span><span class="sxs-lookup"><span data-stu-id="08c1e-348">Go ahead and create your second VM in the same manner:</span></span>

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

<span data-ttu-id="08c1e-349">Şimdi kullanabileceğiniz `azure vm show myResourceGroup myVM1` oluşturmuş olduğunuz incelemek için komutu.</span><span class="sxs-lookup"><span data-stu-id="08c1e-349">And you can now use the `azure vm show myResourceGroup myVM1` command to examine what you've created.</span></span> <span data-ttu-id="08c1e-350">Bu noktada, Ubuntu Vm'leriniz yük dengeleyici arkasında (parolalar devre dışı bırakıldığı için), yalnızca, SSH anahtar çifti ile içine imzalayabilirsiniz Azure'da kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="08c1e-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="08c1e-351">Nginx veya httpd yükleyin, bir web uygulaması dağıtma ve trafiği de görmenize yük dengeleyici sanal makineleri her ikisine de aktığı.</span><span class="sxs-lookup"><span data-stu-id="08c1e-351">You can install nginx or httpd, deploy a web app, and see the traffic flow through the load balancer to both of the VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="08c1e-352">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="08c1e-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "TestVM1"
+ Looking up the NIC "myNic1"
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


## <a name="export-the-environment-as-a-template"></a><span data-ttu-id="08c1e-353">Ortam şablon olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="08c1e-353">Export the environment as a template</span></span>
<span data-ttu-id="08c1e-354">Ne bu ortamını yerleşik, aynı parametreleri ya da eşleşecek bir üretim ortamında ek geliştirme ortamı oluşturmak istediğiniz?</span><span class="sxs-lookup"><span data-stu-id="08c1e-354">Now that you have built out this environment, what if you want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="08c1e-355">Resource Manager, ortamınız için tüm parametreleri tanımlayan JSON şablonlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="08c1e-355">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="08c1e-356">Bu JSON şablonunu başvurarak tüm ortamlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="08c1e-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="08c1e-357">Yapabilecekleriniz [JSON şablonları el ile oluşturabilir](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya sizin için JSON şablonunu oluşturmak için varolan bir ortama verme:</span><span class="sxs-lookup"><span data-stu-id="08c1e-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="08c1e-358">Bu komut oluşturur `myResourceGroup.json` geçerli çalışma dizini dosyasında.</span><span class="sxs-lookup"><span data-stu-id="08c1e-358">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="08c1e-359">Bu şablonu kullanarak bir ortam oluşturduğunuzda, yük dengeleyici, ağ arabirimlerine veya VM'ler için adlar dahil olmak üzere tüm kaynak adları, istenir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-359">When you create an environment from this template, you are prompted for all the resource names, including the names for the load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="08c1e-360">Ekleyerek bu adları şablon dosyanızın doldurabilirsiniz `-p` veya `--includeParameterDefaultValue` parametresi `azure group export` daha önce gösterilen komutu.</span><span class="sxs-lookup"><span data-stu-id="08c1e-360">You can populate these names in your template file by adding the `-p` or `--includeParameterDefaultValue` parameter to the `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="08c1e-361">Kaynak adları belirtmek için JSON şablonunuzu düzenleyin veya [parameters.json dosyası oluşturma](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) kaynak adları belirtir.</span><span class="sxs-lookup"><span data-stu-id="08c1e-361">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="08c1e-362">Bir ortamda, şablonu oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="08c1e-362">To create an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="08c1e-363">Okumak isteyebilirsiniz [şablonlardan dağıtma hakkında daha fazla](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08c1e-363">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="08c1e-364">Artımlı olarak update ortamlar, parametre dosyasını kullanın ve şablonları bir tek bir depolama konumdan erişim hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="08c1e-364">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08c1e-365">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08c1e-365">Next steps</span></span>
<span data-ttu-id="08c1e-366">Artık birden çok ağ bileşenleri ve VM'ler ile çalışmaya başlamak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="08c1e-366">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="08c1e-367">Burada sunulan çekirdek bileşenlerini kullanarak uygulamanızı oluşturmak için bu örnek ortamı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08c1e-367">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
