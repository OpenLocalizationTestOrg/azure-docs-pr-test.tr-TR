---
title: "Ağ güvenlik grupları Azure Güvenlik Merkezi'nde etkinleştirme | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi öneriyi uygulamayı gösterilmiştir ** etkinleştirmek ağ güvenlik grupları **."
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
ms.openlocfilehash: 1e034d59d8847f237fa0d4c772344d45cd618576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="36d8d-103">Ağ güvenlik grupları Azure Güvenlik Merkezi'nde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="36d8d-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="36d8d-104">Azure Güvenlik Merkezi bir zaten etkin değilse, bir ağ güvenlik grubu (NSG) etkinleştirmenizi önerir.</span><span class="sxs-lookup"><span data-stu-id="36d8d-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="36d8d-105">Nsg'ler izin veren veya bir sanal ağ üzerindeki VM örneklerinize ağ trafiğinin reddeden erişim denetimi listesi (ACL) kurallarının bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="36d8d-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="36d8d-106">NSG'ler alt ağlarla veya bu alt ağların içindeki tekil VM örnekleriyle ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="36d8d-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="36d8d-107">NSG bir alt ağ ile ilişkili olduğunda ACL kuralları bu alt ağdaki tüm VM örnekleri için geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="36d8d-107">When an NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span> <span data-ttu-id="36d8d-108">Ayrıca, tekil bir VM trafik kısıtlanabilir başka bir NSG doğrudan bu VM ilişkilendirerek.</span><span class="sxs-lookup"><span data-stu-id="36d8d-108">In addition, traffic to an individual VM can be restricted further by associating an NSG directly to that VM.</span></span> <span data-ttu-id="36d8d-109">Daha fazla bilgi edinmek için [bir ağ güvenlik grubu (NSG) nedir?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="36d8d-109">To learn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="36d8d-110">Nsg'ler etkin yoksa Güvenlik Merkezi iki önerileri size gösterir: alt ağları ve ağ güvenlik grupları sanal makinelerde etkinleştir üzerinde ağ güvenlik grupları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="36d8d-110">If you do not have NSGs enabled, Security Center presents two recommendations to you: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="36d8d-111">Hangi düzeyinde, alt ağ veya Nsg'ler uygulamak için VM seçin.</span><span class="sxs-lookup"><span data-stu-id="36d8d-111">You choose which level, subnet or VM, to apply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="36d8d-112">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="36d8d-112">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="36d8d-113">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="36d8d-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="36d8d-114">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="36d8d-114">Implement the recommendation</span></span>
1. <span data-ttu-id="36d8d-115">İçinde **önerileri** dikey penceresinde, select **etkinleştirmek ağ güvenlik grupları** alt ağlarda veya sanal makinelerde.</span><span class="sxs-lookup"><span data-stu-id="36d8d-115">In the **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="36d8d-116">![Ağ Güvenlik Gruplarını Etkinleştirme][1]</span><span class="sxs-lookup"><span data-stu-id="36d8d-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="36d8d-117">Bu dikey pencere açılır **eksik ağ güvenlik gruplarını yapılandırma** alt ağlar için veya seçtiğiniz öneri bağlı olarak sanal makineler için.</span><span class="sxs-lookup"><span data-stu-id="36d8d-117">This opens the blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on the recommendation that you selected.</span></span> <span data-ttu-id="36d8d-118">Bir alt ağ ya da bir NSG yapılandırmak için bir sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="36d8d-118">Select a subnet or a virtual machine to configure an NSG on.</span></span>

   ![Alt ağı için NSG yapılandırma][2]

   ![VM için NSG yapılandırma][3]
3. <span data-ttu-id="36d8d-121">Üzerinde **ağ güvenlik grubunu seçme** dikey penceresinde, varolan bir NSG veya seçin **Yeni Oluştur** bir NSG oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="36d8d-121">On the **Choose network security group** blade, select an existing NSG or select **Create new** to create an NSG.</span></span>

   ![Ağ güvenlik grubu seç][4]

<span data-ttu-id="36d8d-123">Bir NSG'yi oluşturursanız, adımları [Azure portalını kullanarak Nsg'ler yönetme](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) bir NSG oluşturmak ve güvenlik kuralları ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="36d8d-123">If you create an NSG, follow the steps in [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) to create an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="36d8d-124">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="36d8d-124">See also</span></span>
<span data-ttu-id="36d8d-125">Bu makalenin alt ağlar ya da sanal makineleri için Güvenlik Merkezi öneri "Ağ güvenlik grupları'ı etkinleştir" uygulamak nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="36d8d-125">This article showed you how to implement the Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="36d8d-126">Nsg'ler etkinleştirme hakkında daha fazla bilgi edinmek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="36d8d-126">To learn more about enabling NSGs, see the following:</span></span>

* [<span data-ttu-id="36d8d-127">Ağ Güvenlik Grubu (NSG) Nedir?</span><span class="sxs-lookup"><span data-stu-id="36d8d-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="36d8d-128">Azure portalını kullanarak Nsg'ler yönetme</span><span class="sxs-lookup"><span data-stu-id="36d8d-128">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="36d8d-129">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="36d8d-129">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="36d8d-130">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -- Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="36d8d-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="36d8d-131">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="36d8d-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="36d8d-132">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --Azure kaynaklarınızı sağlığını izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="36d8d-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="36d8d-133">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) -- Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="36d8d-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="36d8d-134">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="36d8d-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="36d8d-135">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -- Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36d8d-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="36d8d-136">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --en son Azure güvenlik haberlerini ve bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="36d8d-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
