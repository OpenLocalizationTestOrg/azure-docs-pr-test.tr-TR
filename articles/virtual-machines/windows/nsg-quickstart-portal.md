---
title: "aaaOpen bağlantı noktalarını tooa VM kullanarak hello Azure portalı | Microsoft Docs"
description: "Bilgi nasıl tooopen bir bağlantı noktası / bir uç nokta tooyour Windows VM oluşturma hello resource manager dağıtım modeline hello Azure Portal kullanarak"
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
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="7d1e2-103">Tooopen hello Azure portalı ile yeni bir sanal makine tooa nasıl bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="7d1e2-103">How tooopen ports tooa virtual machine with hello Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="7d1e2-104">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="7d1e2-104">Quick commands</span></span>
<span data-ttu-id="7d1e2-105">Ayrıca [Azure PowerShell kullanarak bu adımları uygulamadan](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7d1e2-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="7d1e2-106">İlk olarak, ağ güvenlik grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-106">First, create your Network Security Group.</span></span> <span data-ttu-id="7d1e2-107">Merhaba Portalı'nda bir kaynak grubu seçin, **Ekle**, ardından aramak ve seçmek **ağ güvenlik grubu**:</span><span class="sxs-lookup"><span data-stu-id="7d1e2-107">Select a resource group in hello portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Ağ güvenlik grubu Ekle](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="7d1e2-109">Ağ güvenlik grubu için bir ad girin, seçin veya bir kaynak grubu oluşturmak ve bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="7d1e2-110">Seçin **oluşturma** bitirdikten sonra:</span><span class="sxs-lookup"><span data-stu-id="7d1e2-110">Select **Create** when finished:</span></span>

![Bir ağ güvenlik grubu oluşturun](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="7d1e2-112">Yeni bir ağ güvenlik grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-112">Select your new Network Security Group.</span></span> <span data-ttu-id="7d1e2-113">'Gelen güvenlik kuralları' seçin ve ardından hello **Ekle** düğmesini toocreate bir kural:</span><span class="sxs-lookup"><span data-stu-id="7d1e2-113">Select 'Inbound security rules', then select hello **Add** button toocreate a rule:</span></span>

![Bir gelen kuralı Ekle](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="7d1e2-115">Bir ortak seçin **hizmet** hello açılan menüsünden gibi *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-115">Choose a common **Service** from hello drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="7d1e2-116">Öğesini de seçebilirsiniz *özel* tooprovide belirli bir bağlantı noktası toouse.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-116">You can also select *Custom* tooprovide a specific port toouse.</span></span> <span data-ttu-id="7d1e2-117">İsterseniz, hello öncelik veya adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-117">If desired, change hello priority or name.</span></span> <span data-ttu-id="7d1e2-118">Merhaba öncelik içinde kuralları uygulanır - hello sırasını hello alt hello sayısal değer etkiler, hello önceki hello kuralı uygulanır.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-118">hello priority affects hello order in which rules are applied - hello lower hello numerical value, hello earlier hello rule is applied.</span></span> <span data-ttu-id="7d1e2-119">Öğesini de seçebilirsiniz **Gelişmiş** hello bu ekran tooenter üstündeki belirli bir kaynak IP Blok veya bağlantı noktası aralığı, örneğin.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-119">You can also select **Advanced** at hello top of this screen tooenter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="7d1e2-120">Hazır olduğunuzda seçin **Tamam** toocreate hello kural:</span><span class="sxs-lookup"><span data-stu-id="7d1e2-120">When you are ready, select **OK** toocreate hello rule:</span></span>

![Bir gelen kuralı oluşturun](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="7d1e2-122">Ağınızda güvenlik grubunun bir alt ağ veya belirli bir ağ arabiriminde tooassociate, son adımdır.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-122">Your final step is tooassociate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="7d1e2-123">Şimdi hello ağ güvenlik grubunun bir alt ağı ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-123">Let's associate hello Network Security Group with a subnet.</span></span> <span data-ttu-id="7d1e2-124">Seçin **alt ağlar**, ardından **ilişkilendirmek**:</span><span class="sxs-lookup"><span data-stu-id="7d1e2-124">Select **Subnets**, then choose **Associate**:</span></span>

![Ağ güvenlik grubunun bir alt ağ ile ilişkilendirme](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="7d1e2-126">Sanal ağınızı seçin ve ardından hello uygun alt ağ seçin:</span><span class="sxs-lookup"><span data-stu-id="7d1e2-126">Select your virtual network, and then select hello appropriate subnet:</span></span>

![Bir ağ güvenlik grubu sanal ağ ile ilişkilendirme](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="7d1e2-128">Bağlantı noktası 80 üzerinde trafiğe izin verir ve bir alt ağ ile ilişkilendirilmiş bir gelen kuralı oluşturulan bir ağ güvenlik grubu oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="7d1e2-129">Toothat alt bağlanmak herhangi bir VM bağlantı noktası 80 üzerinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-129">Any VMs you connect toothat subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="7d1e2-130">Ağ güvenlik grupları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="7d1e2-130">More information on Network Security Groups</span></span>
<span data-ttu-id="7d1e2-131">Burada hızlı komutları Hello tooget yukarı ve trafik boyunca tooyour VM ile çalışmaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-131">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="7d1e2-132">Ağ güvenlik grupları, birçok harika özellikler ve denetleme tooyour kaynaklara erişmek için ayrıntı düzeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-132">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="7d1e2-133">Daha fazla bilgi edinebilirsiniz [bir ağ güvenlik grubu ve ACL oluşturma kuralları burada](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7d1e2-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="7d1e2-134">Yüksek oranda kullanılabilir web uygulamaları için Azure yük dengeleyici arkasında Vm'leriniz yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="7d1e2-135">Merhaba yük dengeleyici trafik filtreleme sağlar bir ağ güvenlik grubuyla trafiği tooVMs dağıtır.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-135">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="7d1e2-136">Daha fazla bilgi için bkz: [nasıl tooload Bakiye Linux sanal yüksek oranda kullanılabilir bir uygulama içinde Azure toocreate makineleri](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="7d1e2-136">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d1e2-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7d1e2-137">Next steps</span></span>
<span data-ttu-id="7d1e2-138">Bu örnekte, bir basit kural tooallow HTTP trafiği oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7d1e2-138">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="7d1e2-139">Aşağıdaki makaleleri hello ayrıntılı ortamları oluşturma hakkında bilgi bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7d1e2-139">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="7d1e2-140">Azure Resource Manager'a genel bakış</span><span class="sxs-lookup"><span data-stu-id="7d1e2-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="7d1e2-141">Ağ Güvenlik Grubu (NSG) Nedir?</span><span class="sxs-lookup"><span data-stu-id="7d1e2-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)