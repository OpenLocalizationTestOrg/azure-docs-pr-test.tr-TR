---
title: "aaaOpen tooa Linux VM Azure CLI 1.0 ile bağlantı noktaları | Microsoft Docs"
description: "Bilgi nasıl tooopen bir bağlantı noktası / bir uç nokta tooyour Linux VM oluşturma hello Azure resource manager dağıtım kullanarak modeli ve Azure CLI 1.0 hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="a1410-103">Azure kullanarak açma bağlantı noktaları ve uç noktaları tooa Linux VM hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a1410-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="a1410-104">Bir bağlantı noktasını açın ya da bir uç nokta oluşturma tooa bir alt ağ veya VM ağ arabirimine bir ağ filtre oluşturarak azure'da sanal makine (VM).</span><span class="sxs-lookup"><span data-stu-id="a1410-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="a1410-105">Gelen ve giden trafiği denetleyen bu filtreler hello trafiği alan bir bağlı ağ güvenlik grubu toohello kaynakta yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="a1410-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="a1410-106">Bağlantı noktası 80 üzerinde web trafiği yaygın bir örneği kullanalım.</span><span class="sxs-lookup"><span data-stu-id="a1410-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="a1410-107">Bu makalede, nasıl bir bağlantı noktası tooa VM kullanarak tooopen hello Azure CLI 1.0 gösterir.</span><span class="sxs-lookup"><span data-stu-id="a1410-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a1410-108">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="a1410-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="a1410-109">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="a1410-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="a1410-110">[Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="a1410-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a1410-111">[Azure CLI 2.0](nsg-quickstart.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="a1410-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="a1410-112">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="a1410-112">Quick commands</span></span>
<span data-ttu-id="a1410-113">toocreate bir ağ güvenlik grubu ve gereksinim kurallarını [Azure CLI 1.0 hello](../../cli-install-nodejs.md) yüklü ve kullanarak Resource Manager moduna:</span><span class="sxs-lookup"><span data-stu-id="a1410-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="a1410-114">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a1410-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a1410-115">Örnek parametre adları dahil *myResourceGroup*, *myNetworkSecurityGroup*, ve *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="a1410-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="a1410-116">Kendi ad ve konum uygun şekilde girme, ağ güvenlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a1410-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="a1410-117">Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu *myNetworkSecurityGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="a1410-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="a1410-118">Bir kural tooallow HTTP trafiği tooyour Web ekleme (veya SSH erişim ya da veritabanı bağlantısı gibi kendi senaryosu için ayarlama).</span><span class="sxs-lookup"><span data-stu-id="a1410-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="a1410-119">Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRule* tooallow TCP bağlantı noktası 80 üzerinde trafiği:</span><span class="sxs-lookup"><span data-stu-id="a1410-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="a1410-120">Ağ güvenlik grubu Hello VM ağ arabirimi (NIC) ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="a1410-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="a1410-121">Merhaba aşağıdaki örnek ilişkilendirir adlı mevcut NIC'in *myNic* hello adlı ağ güvenlik grubu ile *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="a1410-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="a1410-122">Alternatif olarak, ağ güvenlik grubu sadece tek bir VM'de ağ arabirimi toohello yerine bir sanal ağ alt ağ ile ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1410-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="a1410-123">Merhaba aşağıdaki örnek ilişkilendirir adlı mevcut bir alt *mySubnet* hello içinde *myVnet* hello adlı ağ güvenlik grubu ile sanal ağ *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="a1410-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="a1410-124">Ağ güvenlik grupları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="a1410-124">More information on Network Security Groups</span></span>
<span data-ttu-id="a1410-125">Burada hızlı komutları Hello tooget yukarı ve trafik boyunca tooyour VM ile çalışmaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="a1410-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="a1410-126">Ağ güvenlik grupları, birçok harika özellikler ve denetleme tooyour kaynaklara erişmek için ayrıntı düzeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1410-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="a1410-127">Daha fazla bilgi edinebilirsiniz [bir ağ güvenlik grubu ve ACL oluşturma kuralları burada](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a1410-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="a1410-128">Azure Resource Manager şablonları bir parçası olarak ağ güvenlik grupları ve ACL kuralları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1410-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="a1410-129">Daha fazla bilgi edinin [şablonları ile ağ güvenlik grupları oluşturma](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="a1410-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="a1410-130">VM üzerinde toouse bağlantı noktası iletme toomap benzersiz dış bağlantı noktası tooan iç bağlantı noktası gerekiyorsa, bir yük dengeleyici ve ağ adresi çevirisi (NAT) kuralları kullanır.</span><span class="sxs-lookup"><span data-stu-id="a1410-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="a1410-131">Örneğin, tooexpose TCP bağlantı noktası 8080 dışarıdan istediğiniz ve bir VM üzerinde yönlendirilen trafiği tooTCP bağlantı noktası 80 sahip.</span><span class="sxs-lookup"><span data-stu-id="a1410-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="a1410-132">Hakkında bilgi alabilirsiniz [bir Internet'e yönelik Yük Dengeleyici oluşturma](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a1410-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1410-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1410-133">Next steps</span></span>
<span data-ttu-id="a1410-134">Bu örnekte, bir basit kural tooallow HTTP trafiği oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="a1410-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="a1410-135">Aşağıdaki makaleleri hello ayrıntılı ortamları oluşturma hakkında bilgi bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a1410-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="a1410-136">Azure Resource Manager'a genel bakış</span><span class="sxs-lookup"><span data-stu-id="a1410-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="a1410-137">Ağ Güvenlik Grubu (NSG) Nedir?</span><span class="sxs-lookup"><span data-stu-id="a1410-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="a1410-138">Yük Dengeleyiciler için Azure Resource Manager'a genel bakış</span><span class="sxs-lookup"><span data-stu-id="a1410-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

