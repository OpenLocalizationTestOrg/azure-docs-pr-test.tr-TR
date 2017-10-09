---
title: aaaHow tooload dengelemek Linux sanal makineleri azure'da | Microsoft Docs
description: "Nasıl toouse hello Azure yük dengeleyici toocreate yüksek oranda kullanılabilir ve güvenli bir uygulama üç Linux VM'ler arasında bilgi edinin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="c2448-103">Nasıl tooload Bakiye Azure toocreate Linux sanal makineleri yüksek oranda kullanılabilir bir uygulama</span><span class="sxs-lookup"><span data-stu-id="c2448-103">How tooload balance Linux virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="c2448-104">Yük Dengeleme, birden çok sanal makine genelinde gelen istekleri yayarak daha yüksek düzeyde kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="c2448-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="c2448-105">Bu öğreticide, trafiği dağıtmak ve yüksek kullanılabilirlik sağlamak hello farklı bileşenler hello Azure yük dengeleyici hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="c2448-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="c2448-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c2448-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c2448-107">Bir Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="c2448-108">Bir yük dengeleyici durum araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="c2448-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="c2448-109">Yük Dengeleyici trafiği kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="c2448-110">Bulut init toocreate temel bir Node.js uygulama kullanın</span><span class="sxs-lookup"><span data-stu-id="c2448-110">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="c2448-111">Sanal makineler oluşturmak ve tooa yük dengeleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="c2448-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="c2448-112">Bir yük dengeleyici eylemde görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="c2448-112">View a load balancer in action</span></span>
> * <span data-ttu-id="c2448-113">Ekleme ve sanal makineleri yük dengeleyiciden kaldırın</span><span class="sxs-lookup"><span data-stu-id="c2448-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c2448-114">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="c2448-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c2448-115">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="c2448-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c2448-116">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c2448-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="c2448-117">Azure yük dengeleyici genel bakış</span><span class="sxs-lookup"><span data-stu-id="c2448-117">Azure load balancer overview</span></span>
<span data-ttu-id="c2448-118">Bir Azure yük dengeleyici gelen trafiği sağlıklı VM'ler arasında dağıtarak yüksek kullanılabilirlik sağlayan bir katman 4 (TCP, UDP) yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="c2448-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="c2448-119">Bir yük dengeleyici durum araştırması her VM üzerinde belirli bir bağlantı noktasını izler ve yalnızca trafik tooan dağıtır işletimsel VM.</span><span class="sxs-lookup"><span data-stu-id="c2448-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="c2448-120">Bir veya daha fazla ortak IP adreslerini içeren bir ön uç IP yapılandırmasını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c2448-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="c2448-121">Bu ön uç IP yapılandırmasını yük dengeleyici ve uygulamaları toobe hello Internet erişilebilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="c2448-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="c2448-122">Sanal makineler tooa yük dengeleyici, sanal ağ arabirim kartı (NIC) kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="c2448-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="c2448-123">toodistribute trafiği toohello VM'ler, bir arka uç adres havuzu hello sanal (NIC) bağlı toohello yük dengeleyici hello IP adreslerini içerir.</span><span class="sxs-lookup"><span data-stu-id="c2448-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="c2448-124">toocontrol hello akış trafiği belirli bağlantı noktalarını ve tooyour VM'ler eşleme protokolleri için yük dengeleyici kuralları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c2448-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>

<span data-ttu-id="c2448-125">Merhaba önceki öğretici çok izlediyseniz[bir sanal makine ölçek kümesi oluşturma](tutorial-create-vmss.md), bir yük dengeleyici sizin için oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="c2448-125">If you followed hello previous tutorial too[create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="c2448-126">Tüm bu bileşenlerin, hello ölçek kümesinin bir parçası olarak yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="c2448-126">All these components were configured for you as part of hello scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="c2448-127">Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-127">Create Azure load balancer</span></span>
<span data-ttu-id="c2448-128">Bu bölümde, nasıl oluşturma ve her bileşenin hello yük dengeleyicinin yapılandırma ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="c2448-128">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="c2448-129">Yük Dengeleyici oluşturmadan önce bir kaynak grubuyla oluşturmanız [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c2448-130">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupLoadBalancer* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="c2448-130">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="c2448-131">Genel IP adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-131">Create a public IP address</span></span>
<span data-ttu-id="c2448-132">tooaccess uygulamanıza Internet Merhaba, hello yük dengeleyici için bir ortak IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2448-132">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="c2448-133">Bir ortak IP adresiyle oluşturma [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="c2448-134">Merhaba aşağıdaki örnekte oluşturur adlı ortak IP adresi *myPublicIP* hello içinde *myResourceGroupLoadBalancer* kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="c2448-134">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="c2448-135">Yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-135">Create a load balancer</span></span>
<span data-ttu-id="c2448-136">Bir yük dengeleyici ile oluşturma [az ağ lb oluşturma](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="c2448-137">Merhaba aşağıdaki örnek adlı bir yük dengeleyici oluşturur *myLoadBalancer* ve atar hello *myPublicIP* adresi toohello ön uç IP yapılandırması:</span><span class="sxs-lookup"><span data-stu-id="c2448-137">hello following example creates a load balancer named *myLoadBalancer* and assigns hello *myPublicIP* address toohello front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="c2448-138">Bir sistem durumu araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="c2448-138">Create a health probe</span></span>
<span data-ttu-id="c2448-139">tooallow hello yük dengeleyici toomonitor hello durumu, uygulamanızın bir sistem durumu araştırması kullanın.</span><span class="sxs-lookup"><span data-stu-id="c2448-139">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="c2448-140">Merhaba durumu araştırması dinamik olarak ekler veya kendi yanıt toohealth denetimleri temel hello yük dengeleyici döndürme VM'ler kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c2448-140">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="c2448-141">Varsayılan olarak, bir VM hello yük dengeleyici dağıtımı 15 saniyelik aralıklarda iki ardışık hatadan sonra kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="c2448-141">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="c2448-142">Bir protokol veya belirli bir sistem onay sayfasında uygulamanız için temel bir sistem durumu araştırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c2448-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="c2448-143">Aşağıdaki örnek hello bir TCP araştırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c2448-143">hello following example creates a TCP probe.</span></span> <span data-ttu-id="c2448-144">Daha fazla hassas sistem durumu denetimlerinin özel HTTP araştırmalara de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2448-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="c2448-145">Özel bir HTTP araştırma kullanırken, hello sistem durumu onay sayfasında, aşağıdaki gibi oluşturmalısınız *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="c2448-145">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="c2448-146">Merhaba araştırma döndürmelidir bir **HTTP 200 Tamam** hello yük dengeleyici tookeep hello ana döndürme yanıtı.</span><span class="sxs-lookup"><span data-stu-id="c2448-146">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="c2448-147">toocreate TCP durumu araştırması, kullandığınız [az ağ lb araştırma oluşturmak](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-147">toocreate a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="c2448-148">Merhaba aşağıdaki örnek adlı bir sistem durumu araştırması oluşturur *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="c2448-148">hello following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="c2448-149">Yük Dengeleyici kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-149">Create a load balancer rule</span></span>
<span data-ttu-id="c2448-150">Yük Dengeleyici kuralı kullanılan toodefine olduğu dağıtılmış toohello VM'ler nasıl trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="c2448-150">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="c2448-151">Merhaba ön uç IP yapılandırmasını hello gelen trafiği ve hello arka uç IP havuzu tooreceive hello trafiği için hello gerekli kaynak ve hedef bağlantı noktası ile birlikte tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c2448-151">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="c2448-152">toomake trafiği yalnızca sağlıklı VM'ler aldığınızdan emin, aynı zamanda hello sistem durumu araştırma toouse tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c2448-152">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="c2448-153">Yük Dengeleyici kuralı ile oluşturma [az ağ lb kuralını](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="c2448-154">Merhaba aşağıdaki örnek adlı bir kural oluşturur *myLoadBalancerRule*, kullandığı hello *myHealthProbe* durum araştırması ve bağlantı noktası bakiyelerini trafiğine *80*:</span><span class="sxs-lookup"><span data-stu-id="c2448-154">hello following example creates a rule named *myLoadBalancerRule*, uses hello *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a><span data-ttu-id="c2448-155">Sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c2448-155">Configure virtual network</span></span>
<span data-ttu-id="c2448-156">Bazı sanal makineleri dağıtmak ve, dengeleyici sınayabilirsiniz önce sanal ağ kaynaklarına destekleme hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c2448-156">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="c2448-157">Sanal ağlar hakkında daha fazla bilgi için bkz: Merhaba [Azure Sanal Ağları Yönet](tutorial-virtual-network.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="c2448-157">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="c2448-158">Ağ kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="c2448-158">Create network resources</span></span>
<span data-ttu-id="c2448-159">Bir sanal ağ ile oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="c2448-160">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* adlı bir alt ağ ile *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="c2448-160">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="c2448-161">tooadd bir ağ güvenlik grubu, kullandığınız [az ağ nsg oluşturma](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-161">tooadd a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="c2448-162">Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="c2448-162">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="c2448-163">Ağ güvenlik grubu kural oluştururken [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="c2448-164">Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu kural *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="c2448-164">hello following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="c2448-165">Sanal NIC ile oluşturulan [az ağ NIC oluşturma](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="c2448-166">Merhaba aşağıdaki örnek üç sanal NIC oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c2448-166">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="c2448-167">(Bir sanal NIC aşağıdaki hello uygulamanızda adımları için oluşturduğunuz her VM için).</span><span class="sxs-lookup"><span data-stu-id="c2448-167">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="c2448-168">Ek sanal NIC ve sanal makineleri herhangi bir zamanda oluşturmak ve bunları toohello yük dengeleyici Ekle:</span><span class="sxs-lookup"><span data-stu-id="c2448-168">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a><span data-ttu-id="c2448-169">Sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="c2448-170">Bulut init yapılandırma oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-170">Create cloud-init config</span></span>
<span data-ttu-id="c2448-171">Önceki bir öğretici içinde [nasıl toocustomize Linux sanal bir makinede ilk önyükleme](tutorial-automate-vm-deployment.md), size nasıl öğrenilen tooautomate VM özelleştirme bulut init ile.</span><span class="sxs-lookup"><span data-stu-id="c2448-171">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="c2448-172">Kullanabileceğiniz aynı bulut init yapılandırma dosyası tooinstall NGINX hello ve basit bir 'Hello World' Node.js uygulaması çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c2448-172">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="c2448-173">Geçerli kabuğunuzu adlı bir dosya oluşturun *bulut init.txt* Yapıştır hello izleyerek yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c2448-173">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="c2448-174">Örneğin, yerel makinenizde değil hello bulut Kabuk hello dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c2448-174">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="c2448-175">Girin `sensible-editor cloud-init.txt` toocreate hello dosya ve kullanılabilir düzenleyicileri listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2448-175">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="c2448-176">Merhaba tüm bulut init dosyanın doğru şekilde kopyalandığından emin olun, özellikle ilk satırı hello:</span><span class="sxs-lookup"><span data-stu-id="c2448-176">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a><span data-ttu-id="c2448-177">Sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-177">Create virtual machines</span></span>
<span data-ttu-id="c2448-178">tooimprove hello yüksek kullanılabilirlik, uygulamanızın bir kullanılabilirlik kümesine Vm'leriniz yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="c2448-178">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="c2448-179">Kullanılabilirlik kümeleri hakkında daha fazla bilgi için bkz: hello önceki [nasıl toocreate yüksek oranda kullanılabilir sanal makineleri](tutorial-availability-sets.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="c2448-179">For more information about availability sets, see hello previous [How toocreate highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="c2448-180">Kullanılabilirlik kümesi oluştur [az vm kullanılabilirlik kümesi oluşturma](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="c2448-181">Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="c2448-181">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="c2448-182">Merhaba VM'ler ile oluşturduğunuz artık [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c2448-182">Now you can create hello VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="c2448-183">Merhaba aşağıdaki örnek üç VM'ler oluşturur ve zaten mevcut değilse SSH anahtarları üretir:</span><span class="sxs-lookup"><span data-stu-id="c2448-183">hello following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="c2448-184">Hello Azure CLI toohello istemi döndükten sonra toorun devam arka plan görevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c2448-184">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="c2448-185">Merhaba `--no-wait` parametre değil tüm görevleri toocomplete hello için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="c2448-185">hello `--no-wait` parameter does not wait for all hello tasks toocomplete.</span></span> <span data-ttu-id="c2448-186">Başka bir birkaç hello uygulamaya erişmek için dakika olabilir.</span><span class="sxs-lookup"><span data-stu-id="c2448-186">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="c2448-187">Merhaba uygulamayı her VM çalıştıran hello yük dengeleyici durum araştırması otomatik olarak algılar.</span><span class="sxs-lookup"><span data-stu-id="c2448-187">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="c2448-188">Merhaba uygulama çalışmaya başladıktan sonra hello yük dengeleyici kuralı toodistribute trafiği başlatır.</span><span class="sxs-lookup"><span data-stu-id="c2448-188">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="c2448-189">Test yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="c2448-189">Test load balancer</span></span>
<span data-ttu-id="c2448-190">Merhaba, yük dengeleyici ile genel IP adresi elde [az ağ ortak IP Göster](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="c2448-190">Obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="c2448-191">Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIP* daha önce oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="c2448-191">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="c2448-192">Ardından tooa web tarayıcısında hello genel IP adresi girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2448-192">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="c2448-193">Unutmayın - hello yük dengeleyici toodistribute trafiği toothem başlamadan önce birkaç dakika hello hello VM'ler toobe hazır alır.</span><span class="sxs-lookup"><span data-stu-id="c2448-193">Remember - it takes a few minutes hello hello VMs toobe ready before hello load balancer starts toodistribute traffic toothem.</span></span> <span data-ttu-id="c2448-194">Merhaba uygulama gösterilir, hello VM hello hostname dahil olmak üzere bu hello yük dengeleyici trafiği tooas aşağıdaki örneğine hello içinde dağıtılmış:</span><span class="sxs-lookup"><span data-stu-id="c2448-194">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Çalışan Node.js uygulaması](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="c2448-196">toosee hello yük dengeleyici, uygulamanızı çalıştıran tüm üç VM'ler arasında trafiği dağıtmak, zorla web tarayıcınızı yenileme.</span><span class="sxs-lookup"><span data-stu-id="c2448-196">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="c2448-197">Sanal makineleri ekleyip</span><span class="sxs-lookup"><span data-stu-id="c2448-197">Add and remove VMs</span></span>
<span data-ttu-id="c2448-198">Merhaba işletim sistemi güncelleştirmelerini yükleme gibi uygulamanızı çalıştıran VM'ler tooperform bakım gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c2448-198">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="c2448-199">toodeal trafiğinin artmasına tooyour uygulamayla ihtiyacınız olabilecek tooadd ilave VM'ler.</span><span class="sxs-lookup"><span data-stu-id="c2448-199">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="c2448-200">Bu bölümde, nasıl gösterilir tooremove veya VM hello yük dengeleyiciden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c2448-200">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="c2448-201">Bir VM hello yük dengeleyiciden kaldırın</span><span class="sxs-lookup"><span data-stu-id="c2448-201">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="c2448-202">Merhaba arka uç adres havuzu ile bir VM kaldırabilirsiniz [az ağ NIC IP-config adres havuzu kaldırmak](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="c2448-202">You can remove a VM from hello backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="c2448-203">Aşağıdaki örnek kaldırır hello hello sanal bir NIC'ye **myVM2** gelen *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="c2448-203">hello following example removes hello virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="c2448-204">toosee hello yük dengeleyici iki kalan hello arasında trafiği dağıtmak uygulamanızı çalıştıran VM'ler, zorla web tarayıcınızı yenileme.</span><span class="sxs-lookup"><span data-stu-id="c2448-204">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="c2448-205">Merhaba işletim sistemi güncelleştirmeleri yükleme veya VM yeniden başlatma gerçekleştirme gibi VM üzerinde bakım artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2448-205">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="c2448-206">Bir VM toohello yük dengeleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="c2448-206">Add a VM toohello load balancer</span></span>
<span data-ttu-id="c2448-207">VM bakım gerçekleştirdikten sonra veya tooexpand kapasitesine ihtiyacınız varsa, bir VM toohello arka uç adres havuzuyla ekleyebilirsiniz [az ağ NIC IP-config adres havuzu ekleme](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="c2448-207">After performing VM maintenance, or if you need tooexpand capacity, you can add a VM toohello backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="c2448-208">Merhaba aşağıdaki örnek, hello sanal bir NIC'ye **myVM2** çok*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="c2448-208">hello following example adds hello virtual NIC for **myVM2** too*myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="c2448-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c2448-209">Next steps</span></span>
<span data-ttu-id="c2448-210">Bu öğreticide, bir yük dengeleyici oluşturulur ve sanal makineleri tooit bağlı.</span><span class="sxs-lookup"><span data-stu-id="c2448-210">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="c2448-211">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="c2448-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c2448-212">Bir Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="c2448-213">Bir yük dengeleyici durum araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="c2448-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="c2448-214">Yük Dengeleyici trafiği kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2448-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="c2448-215">Bulut init toocreate temel bir Node.js uygulama kullanın</span><span class="sxs-lookup"><span data-stu-id="c2448-215">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="c2448-216">Sanal makineler oluşturmak ve tooa yük dengeleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="c2448-216">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="c2448-217">Bir yük dengeleyici eylemde görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="c2448-217">View a load balancer in action</span></span>
> * <span data-ttu-id="c2448-218">Ekleme ve sanal makineleri yük dengeleyiciden kaldırın</span><span class="sxs-lookup"><span data-stu-id="c2448-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="c2448-219">Toohello sonraki öğretici toolearn Azure sanal ağı bileşenleri hakkında daha fazla ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="c2448-219">Advance toohello next tutorial toolearn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2448-220">VM’leri ve sanal ağları yönetme</span><span class="sxs-lookup"><span data-stu-id="c2448-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
