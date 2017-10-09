---
title: "Ağ güvenlik grupları Azure Güvenlik Merkezi'nde aaaEnable | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** etkinleştirmek ağ güvenlik grupları **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="9fd4a-103">Ağ güvenlik grupları Azure Güvenlik Merkezi'nde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="9fd4a-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="9fd4a-104">Azure Güvenlik Merkezi bir zaten etkin değilse, bir ağ güvenlik grubu (NSG) etkinleştirmenizi önerir.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="9fd4a-105">Nsg'ler izin veren veya bir sanal ağ tooyour VM örnekleri ağ trafiği reddeden erişim denetimi listesi (ACL) kurallarının bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="9fd4a-106">NSG'ler alt ağlarla veya bu alt ağların içindeki tekil VM örnekleriyle ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="9fd4a-107">Bir NSG'yi bir alt ağ ile ilişkili olduğunda hello ACL kuralları bu alt ağdaki tooall hello VM örnekleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-107">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="9fd4a-108">Buna ek olarak, trafiği tooan tek tek VM kısıtlanabilir başka bir NSG ilişkilendirerek doğrudan toothat VM.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-108">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span> <span data-ttu-id="9fd4a-109">toolearn daha fazla [bir ağ güvenlik grubu (NSG) nedir?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="9fd4a-109">toolearn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="9fd4a-110">Nsg'ler etkin yoksa Güvenlik Merkezi iki önerileri tooyou sunar: alt ağları ve ağ güvenlik grupları sanal makinelerde etkinleştir üzerinde ağ güvenlik grupları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-110">If you do not have NSGs enabled, Security Center presents two recommendations tooyou: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="9fd4a-111">Hangi düzeyinde, alt ağ veya VM, tooapply Nsg'ler seçin.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-111">You choose which level, subnet or VM, tooapply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="9fd4a-112">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-112">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="9fd4a-113">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="9fd4a-114">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="9fd4a-114">Implement hello recommendation</span></span>
1. <span data-ttu-id="9fd4a-115">Merhaba, **önerileri** dikey penceresinde, select **etkinleştirmek ağ güvenlik grupları** alt ağlarda veya sanal makinelerde.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-115">In hello **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="9fd4a-116">![Ağ Güvenlik Gruplarını Etkinleştirme][1]</span><span class="sxs-lookup"><span data-stu-id="9fd4a-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="9fd4a-117">Bu hello dikey pencere açılır **eksik ağ güvenlik gruplarını yapılandırma** alt ağlar için veya seçtiğiniz hello öneri bağlı olarak sanal makineler için.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-117">This opens hello blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on hello recommendation that you selected.</span></span> <span data-ttu-id="9fd4a-118">Bir alt ağ veya sanal makine tooconfigure bir NSG seçin.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-118">Select a subnet or a virtual machine tooconfigure an NSG on.</span></span>

   ![Alt ağı için NSG yapılandırma][2]

   ![VM için NSG yapılandırma][3]
3. <span data-ttu-id="9fd4a-121">Merhaba üzerinde **ağ güvenlik grubunu seçme** dikey penceresinde, varolan bir NSG veya seçin **Yeni Oluştur** toocreate bir NSG.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-121">On hello **Choose network security group** blade, select an existing NSG or select **Create new** toocreate an NSG.</span></span>

   ![Ağ güvenlik grubu seç][4]

<span data-ttu-id="9fd4a-123">Bir NSG oluşturursanız, hello adımları [nasıl Azure portal kullanarak toomanage Nsg'ler hello](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate bir NSG ve güvenlik kuralları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-123">If you create an NSG, follow hello steps in [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="9fd4a-124">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-124">See also</span></span>
<span data-ttu-id="9fd4a-125">Bu makalede nasıl tooimplement hello Güvenlik Merkezi öneri "etkinleştirmek ağ güvenlik grupları" alt ağ veya sanal makineleri için gösterdi.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-125">This article showed you how tooimplement hello Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="9fd4a-126">Nsg'ler, etkinleştirme hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="9fd4a-126">toolearn more about enabling NSGs, see hello following:</span></span>

* [<span data-ttu-id="9fd4a-127">Ağ Güvenlik Grubu (NSG) Nedir?</span><span class="sxs-lookup"><span data-stu-id="9fd4a-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="9fd4a-128">Azure portal kullanarak toomanage Nsg'ler nasıl hello</span><span class="sxs-lookup"><span data-stu-id="9fd4a-128">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="9fd4a-129">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="9fd4a-129">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="9fd4a-130">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9fd4a-131">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9fd4a-132">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="9fd4a-133">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="9fd4a-134">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="9fd4a-135">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="9fd4a-136">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --hello en son Azure güvenlik haberlerini ve bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="9fd4a-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
