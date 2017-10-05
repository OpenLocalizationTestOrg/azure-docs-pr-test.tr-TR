---
title: "Azure Portalı'nı kullanarak bir VM için bağlantı noktalarını açmak | Microsoft Docs"
description: "Bir bağlantı noktasını açmak bir uç noktası, Windows Azure Portalı'nda resource manager dağıtım modelini kullanarak VM oluşturma hakkında bilgi edinin"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 33bc0be0aeae6d0276fd8999b9ac0a010e3067ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-to-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="c28bd-103">Azure portal ile bir sanal makineye bağlantı noktalarının nasıl</span><span class="sxs-lookup"><span data-stu-id="c28bd-103">How to open ports to a virtual machine with the Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="c28bd-104">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="c28bd-104">Quick commands</span></span>
<span data-ttu-id="c28bd-105">Ayrıca [Azure PowerShell kullanarak bu adımları uygulamadan](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c28bd-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="c28bd-106">İlk olarak, ağ güvenlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c28bd-106">First, create your Network Security Group.</span></span> <span data-ttu-id="c28bd-107">Portalda bir kaynak grubu seçin, **Ekle**, ardından aramak ve seçmek **ağ güvenlik grubu**:</span><span class="sxs-lookup"><span data-stu-id="c28bd-107">Select a resource group in the portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Ağ güvenlik grubu Ekle](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="c28bd-109">Ağ güvenlik grubu için bir ad girin, seçin veya bir kaynak grubu oluşturmak ve bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="c28bd-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="c28bd-110">Seçin **oluşturma** bitirdikten sonra:</span><span class="sxs-lookup"><span data-stu-id="c28bd-110">Select **Create** when finished:</span></span>

![Bir ağ güvenlik grubu oluşturun](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="c28bd-112">Yeni bir ağ güvenlik grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="c28bd-112">Select your new Network Security Group.</span></span> <span data-ttu-id="c28bd-113">'Gelen güvenlik kuralları' seçin ve ardından **Ekle** düğmesine bir kural oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="c28bd-113">Select 'Inbound security rules', then select the **Add** button to create a rule:</span></span>

![Bir gelen kuralı Ekle](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="c28bd-115">Bir ortak seçin **hizmet** açılır menüsünden gibi *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="c28bd-115">Choose a common **Service** from the drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="c28bd-116">Öğesini de seçebilirsiniz *özel* kullanmak için belirli bir bağlantı sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="c28bd-116">You can also select *Custom* to provide a specific port to use.</span></span> <span data-ttu-id="c28bd-117">İsterseniz, öncelik veya adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c28bd-117">If desired, change the priority or name.</span></span> <span data-ttu-id="c28bd-118">Öncelik, kuralları uygulanır - sırasını düşük sayısal değer etkiler, kural önce uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c28bd-118">The priority affects the order in which rules are applied - the lower the numerical value, the earlier the rule is applied.</span></span> <span data-ttu-id="c28bd-119">Öğesini de seçebilirsiniz **Gelişmiş** belirli bir kaynak IP Blok veya bağlantı noktası aralığı, örneğin girmek için bu ekranın üstünde.</span><span class="sxs-lookup"><span data-stu-id="c28bd-119">You can also select **Advanced** at the top of this screen to enter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="c28bd-120">Hazır olduğunuzda seçin **Tamam** kuralı oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="c28bd-120">When you are ready, select **OK** to create the rule:</span></span>

![Bir gelen kuralı oluşturun](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="c28bd-122">Ağ güvenlik grubunun bir alt ağ veya belirli ağ arabirimi ile ilişkilendirmek için son adımınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c28bd-122">Your final step is to associate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="c28bd-123">Şimdi ağ güvenlik grubu bir alt ağı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="c28bd-123">Let's associate the Network Security Group with a subnet.</span></span> <span data-ttu-id="c28bd-124">Seçin **alt ağlar**, ardından **ilişkilendirmek**:</span><span class="sxs-lookup"><span data-stu-id="c28bd-124">Select **Subnets**, then choose **Associate**:</span></span>

![Ağ güvenlik grubunun bir alt ağ ile ilişkilendirme](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="c28bd-126">Sanal ağınızı seçin ve ardından uygun alt ağ seçin:</span><span class="sxs-lookup"><span data-stu-id="c28bd-126">Select your virtual network, and then select the appropriate subnet:</span></span>

![Bir ağ güvenlik grubu sanal ağ ile ilişkilendirme](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="c28bd-128">Bağlantı noktası 80 üzerinde trafiğe izin verir ve bir alt ağ ile ilişkilendirilmiş bir gelen kuralı oluşturulan bir ağ güvenlik grubu oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="c28bd-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="c28bd-129">Bu alt ağa bağlanma herhangi bir VM bağlantı noktası 80 üzerinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="c28bd-129">Any VMs you connect to that subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="c28bd-130">Ağ güvenlik grupları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="c28bd-130">More information on Network Security Groups</span></span>
<span data-ttu-id="c28bd-131">Burada hızlı komutlar VM'nize akan trafikle başlamak ve çalıştırmak için olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c28bd-131">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="c28bd-132">Ağ güvenlik grupları birçok harika özellikler ve kaynaklarınıza erişimi denetlemek için ayrıntı düzeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c28bd-132">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="c28bd-133">Daha fazla bilgi edinebilirsiniz [bir ağ güvenlik grubu ve ACL oluşturma kuralları burada](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c28bd-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="c28bd-134">Yüksek oranda kullanılabilir web uygulamaları için Azure yük dengeleyici arkasında Vm'leriniz yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c28bd-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="c28bd-135">Yük Dengeleyici trafik filtreleme sağlar bir ağ güvenlik grubu olan VM'ler için trafiği dağıtır.</span><span class="sxs-lookup"><span data-stu-id="c28bd-135">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="c28bd-136">Daha fazla bilgi için bkz: [nasıl yükleneceğini Linux sanal makineleri yüksek oranda kullanılabilir bir uygulama oluşturmak için Azure Bakiye](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="c28bd-136">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c28bd-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c28bd-137">Next steps</span></span>
<span data-ttu-id="c28bd-138">Bu örnekte, HTTP trafiğine izin veren basit bir kural oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="c28bd-138">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="c28bd-139">Aşağıdaki makalelerde ayrıntılı ortamları oluşturma hakkında bilgi bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c28bd-139">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="c28bd-140">Azure Resource Manager'a genel bakış</span><span class="sxs-lookup"><span data-stu-id="c28bd-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="c28bd-141">Ağ Güvenlik Grubu (NSG) Nedir?</span><span class="sxs-lookup"><span data-stu-id="c28bd-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)