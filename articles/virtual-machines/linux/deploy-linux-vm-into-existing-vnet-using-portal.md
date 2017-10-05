---
title: "Mevcut ağ Azure portal ile içine Linux VM'ler dağıtma | Microsoft Docs"
description: "Bir Linux VM mevcut bir Azure sanal Portalı'nı kullanarak ağa dağıtın."
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
ms.openlocfilehash: 964c0fc41773b50a9fbe476df47460484c2ada66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-portal"></a><span data-ttu-id="f5322-103">Mevcut Azure sanal ağda Azure portal ile Linux sanal makine dağıtma</span><span class="sxs-lookup"><span data-stu-id="f5322-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure portal</span></span>

<span data-ttu-id="f5322-104">Bu makalede, varolan bir sanal ağa (VNet) sanal makine (VM) dağıtma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f5322-104">This article shows you how to deploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="f5322-105">Sanal ağlar ve ağ güvenlik grupları gibi Azure varlıklar statik olmalıdır ve nadiren dağıtılan kaynakları uzun ömürlü.</span><span class="sxs-lookup"><span data-stu-id="f5322-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="f5322-106">Bir VNet dağıtıldıktan sonra hiçbir olumsuz etkiler altyapısı olmadan sabit redeployments tarafından yeniden.</span><span class="sxs-lookup"><span data-stu-id="f5322-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="f5322-107">Geleneksel olarak VNet hakkında düşünüyorum donanım ağ anahtarı - değil gerekir yepyeni bir donanım anahtar her dağıtımı ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f5322-107">Thinking about a VNet as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="f5322-108">Doğru yapılandırılmış bir VNet ile birlikte, yeni sunucuları bu Vnet'i tekrar tekrar VNet ömrü boyunca gereken birkaç varsa, değişikliklerle dağıtmak, devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5322-108">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="f5322-109">Kaynak grubunu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5322-109">Create the resource group</span></span>

<span data-ttu-id="f5322-110">İlk olarak, bu kılavuzda oluşturduğunuz her şeyi düzenlemek için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f5322-110">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="f5322-111">Azure kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f5322-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-the-vnet"></a><span data-ttu-id="f5322-113">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5322-113">Create the VNet</span></span>

<span data-ttu-id="f5322-114">Ardından, sanal makineleri içine başlatmak için bir VNet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f5322-114">Next, build a VNet to launch the VMs into.</span></span> <span data-ttu-id="f5322-115">VNet ve bir sonraki adımda bu alt ağ güvenlik grubuyla ilişkilendirilmiş bir alt ağ içerir.</span><span class="sxs-lookup"><span data-stu-id="f5322-115">The VNet contains one subnet and is associated with the network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="f5322-117">Alt ağ için bir Vnıc'teki Ekle</span><span class="sxs-lookup"><span data-stu-id="f5322-117">Add a VNic to the subnet</span></span>

<span data-ttu-id="f5322-118">Sanal ağ kartları (VNics) için farklı VM'ler bağlanabilir gibi önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f5322-118">Virtual network cards (VNics) are important as you can connect them to different VMs.</span></span> <span data-ttu-id="f5322-119">Bu yaklaşım VM'ler geçici olarak olabileceği Vnıc statik bir kaynak olarak tutar.</span><span class="sxs-lookup"><span data-stu-id="f5322-119">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="f5322-120">Bir Vnıc'teki oluşturun ve önceki adımda oluşturduğunuz alt ağ ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="f5322-120">Create a VNic and associate it with the subnet created in the previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-the-network-security-group"></a><span data-ttu-id="f5322-122">Ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="f5322-122">Create the network security group</span></span>

<span data-ttu-id="f5322-123">Azure ağ güvenlik grupları, bir Güvenlik Duvarı'nı ağ katmanında eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="f5322-123">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="f5322-124">Azure ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [bir ağ güvenlik grubu nedir](../../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f5322-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="f5322-126">Gelen bir SSH izin ver Kuralı Ekle</span><span class="sxs-lookup"><span data-stu-id="f5322-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="f5322-127">Gelen bağlantı noktası 22 trafiği ağ üzerinden bağlantı noktası 22 VM geçirilmesine izin veren bir kural oluşmasını VM Internet erişimi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f5322-127">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-the-nsg-with-the-subnet"></a><span data-ttu-id="f5322-129">NSG alt ağ ile ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="f5322-129">Associate the NSG with the subnet</span></span>

<span data-ttu-id="f5322-130">VNet ve oluşturulan alt ağ ile ağ güvenlik grubu alt ağı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="f5322-130">With the VNet and the subnet created, associate the network security group with the subnet.</span></span> <span data-ttu-id="f5322-131">Ağ güvenlik grupları, alt ağın tamamını veya bir tek tek Vnıc ile ilişkilendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="f5322-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="f5322-132">Alt ağ düzeyinde trafik filtreleme güvenlik duvarı ile tüm VNics ve alt ağ içindeki VM'ler ağ güvenlik grubu tarafından korunuyor.</span><span class="sxs-lookup"><span data-stu-id="f5322-132">With the firewall filtering traffic at the subnet level, all VNics and the VMs within the subnet are protected by the network security group.</span></span> <span data-ttu-id="f5322-133">Diğer ağ güvenlik grubu sadece tek bir Vnıc'teki ve koruma yalnızca bir VM ile ilişkilendirilen bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="f5322-133">The other approach is the network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="f5322-135">VNet ve NSG halinde VM dağıtma</span><span class="sxs-lookup"><span data-stu-id="f5322-135">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="f5322-136">Azure Portalı'nı kullanarak, var olan Azure kaynak grubu, sanal ağ, alt ağ ve Vnıc için Linux VM dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="f5322-136">Using the Azure portal, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="f5322-138">Var olan kaynakların seçmek için portalı kullanarak, varolan ağ içindeki VM dağıtmak için Azure isteyin.</span><span class="sxs-lookup"><span data-stu-id="f5322-138">By using the portal to choose existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="f5322-139">Bir VNet ve alt ağ dağıtıldıktan sonra Azure bölgesi içinde statik veya kalıcı kaynaklar olarak bırakılabilir.</span><span class="sxs-lookup"><span data-stu-id="f5322-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f5322-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f5322-140">Next steps</span></span>

* [<span data-ttu-id="f5322-141">Belirli bir dağıtımı oluşturmak için Azure Resource Manager şablonu kullanma</span><span class="sxs-lookup"><span data-stu-id="f5322-141">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="f5322-142">Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="f5322-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="f5322-143">Şablonları kullanarak Azure'da bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5322-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
