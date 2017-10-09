---
title: "mevcut ağ Azure portal ile içine aaaDeploy Linux VM'ler | Microsoft Docs"
description: "Bir Linux VM mevcut bir Azure sanal hello portal kullanarak ağa dağıtın."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a><span data-ttu-id="b1579-103">Nasıl toodeploy mevcut Azure sanal ağda hello Azure portal ile Linux sanal makine</span><span class="sxs-lookup"><span data-stu-id="b1579-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure portal</span></span>

<span data-ttu-id="b1579-104">Bu makale size nasıl gösterir toodeploy mevcut sanal ağda (VNet) sanal makine (VM).</span><span class="sxs-lookup"><span data-stu-id="b1579-104">This article shows you how toodeploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="b1579-105">Sanal ağlar ve ağ güvenlik grupları gibi Azure varlıklar statik olmalıdır ve nadiren dağıtılan kaynakları uzun ömürlü.</span><span class="sxs-lookup"><span data-stu-id="b1579-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="b1579-106">Bir VNet dağıtıldıktan sonra herhangi bir olumsuz etkiler toohello altyapı olmadan sabit redeployments tarafından yeniden.</span><span class="sxs-lookup"><span data-stu-id="b1579-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="b1579-107">Geleneksel olarak VNet hakkında düşünüyorum donanım ağ anahtarı - ihtiyacınız olmayan yepyeni bir donanım her dağıtımı ile geçiş tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="b1579-107">Thinking about a VNet as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="b1579-108">Doğru yapılandırılmış bir VNet ile birlikte toodeploy yeni sunucuları bu sanal ağ içinde tekrar tekrar hello VNet hello ömrü boyunca gereken birkaç varsa, değişikliklerle devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1579-108">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="b1579-109">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="b1579-109">Create hello resource group</span></span>

<span data-ttu-id="b1579-110">İlk olarak, bir kaynak grubu tooorganize bu kılavuzda oluşturduğunuz her şeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1579-110">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="b1579-111">Azure kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b1579-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a><span data-ttu-id="b1579-113">Merhaba VNet oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1579-113">Create hello VNet</span></span>

<span data-ttu-id="b1579-114">Ardından, bir VNet toolaunch hello içine VM'ler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1579-114">Next, build a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="b1579-115">Merhaba VNet ve hello ağ güvenlik grubu sonraki adımda bu alt ağ ile ilişkilendirilmiş bir alt ağ içerir.</span><span class="sxs-lookup"><span data-stu-id="b1579-115">hello VNet contains one subnet and is associated with hello network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="b1579-117">Vnıc toohello alt ağ Ekle</span><span class="sxs-lookup"><span data-stu-id="b1579-117">Add a VNic toohello subnet</span></span>

<span data-ttu-id="b1579-118">Sanal ağ kartları (VNics) toodifferent VM'ler bağlanabilir gibi önemlidir.</span><span class="sxs-lookup"><span data-stu-id="b1579-118">Virtual network cards (VNics) are important as you can connect them toodifferent VMs.</span></span> <span data-ttu-id="b1579-119">Bu yaklaşım Hello VM'ler geçici olarak olabileceği hello Vnıc statik bir kaynak olarak tutar.</span><span class="sxs-lookup"><span data-stu-id="b1579-119">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="b1579-120">Bir Vnıc'teki oluşturup hello önceki adımda oluşturduğunuz hello alt ağı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="b1579-120">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a><span data-ttu-id="b1579-122">Merhaba ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="b1579-122">Create hello network security group</span></span>

<span data-ttu-id="b1579-123">Azure ağ güvenlik grupları hello ağ katmanı eşdeğer tooa güvenlik duvarında değildir.</span><span class="sxs-lookup"><span data-stu-id="b1579-123">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="b1579-124">Azure ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [bir ağ güvenlik grubu nedir](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="b1579-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="b1579-126">Gelen bir SSH izin ver Kuralı Ekle</span><span class="sxs-lookup"><span data-stu-id="b1579-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="b1579-127">Merhaba VM hello erişimden gereken gelen bağlantı noktası 22 trafiği toobe veren bir kural, VM oluşturulduğunda hello üzerinde hello ağ tooport 22 geçirilen şekilde Internet.</span><span class="sxs-lookup"><span data-stu-id="b1579-127">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a><span data-ttu-id="b1579-129">Merhaba NSG hello alt ağı ile ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="b1579-129">Associate hello NSG with hello subnet</span></span>

<span data-ttu-id="b1579-130">Merhaba VNet ve oluşturulan hello alt ağ ile Merhaba ağ güvenlik grubu hello alt ağı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="b1579-130">With hello VNet and hello subnet created, associate hello network security group with hello subnet.</span></span> <span data-ttu-id="b1579-131">Ağ güvenlik grupları, alt ağın tamamını veya bir tek tek Vnıc ile ilişkilendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b1579-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="b1579-132">Merhaba alt ağ düzeyindeki trafiği filtreleme hello güvenlik duvarı ile tüm VNics ve hello alt ağ içindeki VM'ler hello hello ağ güvenlik grubu tarafından korunuyor.</span><span class="sxs-lookup"><span data-stu-id="b1579-132">With hello firewall filtering traffic at hello subnet level, all VNics and hello VMs within hello subnet are protected by hello network security group.</span></span> <span data-ttu-id="b1579-133">Merhaba diğer yaklaşım olduğu hello ağ güvenlik grubu olması yalnızca tek bir Vnıc'teki ile ilişkili olan ve tek bir VM koruma.</span><span class="sxs-lookup"><span data-stu-id="b1579-133">hello other approach is hello network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="b1579-135">Merhaba VM hello VNet içine ve NSG dağıtma</span><span class="sxs-lookup"><span data-stu-id="b1579-135">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="b1579-136">Hello Azure portal kullanarak hello Linux VM dağıtılan toohello Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc mevcut değildir.</span><span class="sxs-lookup"><span data-stu-id="b1579-136">Using hello Azure portal, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="b1579-138">Merhaba portal toochoose var olan kaynakları kullanarak hello mevcut ağ içinde Azure toodeploy hello VM isteyin.</span><span class="sxs-lookup"><span data-stu-id="b1579-138">By using hello portal toochoose existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="b1579-139">Bir VNet ve alt ağ dağıtıldıktan sonra Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="b1579-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b1579-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b1579-140">Next steps</span></span>

* [<span data-ttu-id="b1579-141">Azure Resource Manager şablonu toocreate belirli bir dağıtım kullanın</span><span class="sxs-lookup"><span data-stu-id="b1579-141">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="b1579-142">Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="b1579-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="b1579-143">Şablonları kullanarak Azure'da bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1579-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
