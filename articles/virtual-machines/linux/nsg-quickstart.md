---
title: "aaaOpen tooa Linux VM Azure CLI 2.0 ile bağlantı noktaları | Microsoft Docs"
description: "Bilgi nasıl tooopen bir bağlantı noktası / bir uç nokta tooyour Linux VM oluşturma hello Azure resource manager dağıtım kullanarak modeli ve Azure CLI 2.0 hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="d7d95-103">Bağlantı noktaları ve uç noktaları tooa Linux VM hello Azure CLI ile Aç</span><span class="sxs-lookup"><span data-stu-id="d7d95-103">Open ports and endpoints tooa Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="d7d95-104">Bir bağlantı noktasını açın ya da bir uç nokta oluşturma tooa bir alt ağ veya VM ağ arabirimine bir ağ filtre oluşturarak azure'da sanal makine (VM).</span><span class="sxs-lookup"><span data-stu-id="d7d95-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="d7d95-105">Gelen ve giden trafiği denetleyen bu filtreler hello trafiği alan bir bağlı ağ güvenlik grubu toohello kaynakta yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d7d95-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="d7d95-106">Bağlantı noktası 80 üzerinde web trafiği yaygın bir örneği kullanalım.</span><span class="sxs-lookup"><span data-stu-id="d7d95-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="d7d95-107">Bu makale size nasıl gösterir tooopen hello Azure CLI 2.0 ile bir bağlantı noktası tooa VM.</span><span class="sxs-lookup"><span data-stu-id="d7d95-107">This article shows you how tooopen a port tooa VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="d7d95-108">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d7d95-108">You can also perform these steps with hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="d7d95-109">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="d7d95-109">Quick commands</span></span>
<span data-ttu-id="d7d95-110">toocreate bir ağ güvenlik grubu ve ihtiyacınız olan kuralların hello son [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d7d95-110">toocreate a Network Security Group and rules you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d7d95-111">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d7d95-111">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d7d95-112">Örnek parametre adlarında *myResourceGroup*, *myNetworkSecurityGroup*, ve *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="d7d95-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="d7d95-113">Merhaba ağ güvenlik grubu oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="d7d95-113">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="d7d95-114">Merhaba aşağıdaki örnek adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="d7d95-114">hello following example creates a network security group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="d7d95-115">Olan bir kural eklemek [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) tooallow HTTP trafiği tooyour Web sunucusu (veya SSH erişim ya da veritabanı bağlantısı gibi kendi senaryosu için ayarlayın).</span><span class="sxs-lookup"><span data-stu-id="d7d95-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="d7d95-116">Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRule* tooallow TCP bağlantı noktası 80 üzerinde trafiği:</span><span class="sxs-lookup"><span data-stu-id="d7d95-116">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="d7d95-117">VM ağ arabirimi (NIC) ilişkilendirmek Hello ağ güvenlik grubu [az ağ NIC güncelleştirmesi](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="d7d95-117">Associate hello Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="d7d95-118">Merhaba aşağıdaki örnek ilişkilendirir adlı mevcut NIC'in *myNic* hello adlı ağ güvenlik grubu ile *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="d7d95-118">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="d7d95-119">Alternatif olarak, bir sanal ağ alt ağı ile ağ güvenlik grubu ilişkilendirebilirsiniz [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update) yalnızca tek bir VM'de ağ arabirimi toohello yerine.</span><span class="sxs-lookup"><span data-stu-id="d7d95-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="d7d95-120">Merhaba aşağıdaki örnek ilişkilendirir adlı mevcut bir alt *mySubnet* hello içinde *myVnet* hello adlı ağ güvenlik grubu ile sanal ağ *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="d7d95-120">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="d7d95-121">Ağ güvenlik grupları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="d7d95-121">More information on Network Security Groups</span></span>
<span data-ttu-id="d7d95-122">Burada hızlı komutları Hello tooget yukarı ve trafik boyunca tooyour VM ile çalışmaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="d7d95-122">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="d7d95-123">Ağ güvenlik grupları, birçok harika özellikler ve denetleme tooyour kaynaklara erişmek için ayrıntı düzeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7d95-123">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="d7d95-124">Daha fazla bilgi edinebilirsiniz [bir ağ güvenlik grubu ve ACL oluşturma kuralları burada](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="d7d95-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="d7d95-125">Yüksek oranda kullanılabilir web uygulamaları için Azure yük dengeleyici arkasında Vm'leriniz yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7d95-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="d7d95-126">Merhaba yük dengeleyici trafik filtreleme sağlar bir ağ güvenlik grubuyla trafiği tooVMs dağıtır.</span><span class="sxs-lookup"><span data-stu-id="d7d95-126">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="d7d95-127">Daha fazla bilgi için bkz: [nasıl tooload Bakiye Linux sanal yüksek oranda kullanılabilir bir uygulama içinde Azure toocreate makineleri](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="d7d95-127">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7d95-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7d95-128">Next steps</span></span>
<span data-ttu-id="d7d95-129">Bu örnekte, bir basit kural tooallow HTTP trafiği oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d7d95-129">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="d7d95-130">Aşağıdaki makaleleri hello ayrıntılı ortamları oluşturma hakkında bilgi bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d7d95-130">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="d7d95-131">Azure Resource Manager'a genel bakış</span><span class="sxs-lookup"><span data-stu-id="d7d95-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="d7d95-132">Ağ Güvenlik Grubu (NSG) Nedir?</span><span class="sxs-lookup"><span data-stu-id="d7d95-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
