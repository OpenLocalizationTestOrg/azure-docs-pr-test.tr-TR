---
title: "aaaAdd yeni nesil güvenlik duvarı Azure Güvenlik Merkezi'nde | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi önerilerini gösterir. ** bir sonraki nesil güvenlik duvarı ** ekleyin ve ** yalnızca rota traffice NGFW aracılığıyla **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="a83a8-103">Azure Güvenlik Merkezi'nde yeni nesil güvenlik duvarı ekleme</span><span class="sxs-lookup"><span data-stu-id="a83a8-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="a83a8-104">Azure Güvenlik Merkezi, yeni nesil Güvenlik Duvarı (NGFW) bir Microsoft iş ortağı tooincrease güvenlik korumaları eklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="a83a8-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> <span data-ttu-id="a83a8-105">Bu belge, nasıl bir örnek üzerinden anlatan toodo bu.</span><span class="sxs-lookup"><span data-stu-id="a83a8-105">This document walks you through an example of how toodo this.</span></span>

> [!NOTE]
> <span data-ttu-id="a83a8-106">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="a83a8-106">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="a83a8-107">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="a83a8-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="a83a8-108">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="a83a8-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="a83a8-109">Merhaba, **önerileri** dikey penceresinde, select **yeni nesil güvenlik duvarı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="a83a8-109">In hello **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="a83a8-110">![Yeni Nesil Güvenlik Duvarı ekleme][1]</span><span class="sxs-lookup"><span data-stu-id="a83a8-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="a83a8-111">Merhaba, **yeni nesil güvenlik duvarı ekleme** dikey penceresinde, bir uç nokta seçin.</span><span class="sxs-lookup"><span data-stu-id="a83a8-111">In hello **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="a83a8-112">![Bir uç nokta seçin][2]</span><span class="sxs-lookup"><span data-stu-id="a83a8-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="a83a8-113">İkinci bir **yeni nesil güvenlik duvarı ekleme** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="a83a8-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="a83a8-114">Toouse varsa varolan bir çözümü seçebilir veya yeni bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a83a8-114">You can choose toouse an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="a83a8-115">Bu örnekte, yok varolan çözüm bir NGFW oluşturuyoruz şekilde.</span><span class="sxs-lookup"><span data-stu-id="a83a8-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="a83a8-116">![Yeni nesil güvenlik duvarı oluşturma][3]</span><span class="sxs-lookup"><span data-stu-id="a83a8-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="a83a8-117">toocreate bir NGFW hello tümleşik ortakları listesinden bir çözümü seçin.</span><span class="sxs-lookup"><span data-stu-id="a83a8-117">toocreate an NGFW, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="a83a8-118">Bu örnekte, biz seçin **Check Point**.</span><span class="sxs-lookup"><span data-stu-id="a83a8-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="a83a8-119">![Yeni nesil güvenlik duvarı çözümü seçin][4]</span><span class="sxs-lookup"><span data-stu-id="a83a8-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="a83a8-120">Merhaba **Check Point** dikey pencere açılır hello iş ortağı çözümü hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a83a8-120">hello **Check Point** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="a83a8-121">Seçin **oluşturma** hello bilgi dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="a83a8-121">Select **Create** in hello information blade.</span></span>
   <span data-ttu-id="a83a8-122">![Güvenlik Duvarı bilgileri dikey penceresi][5]</span><span class="sxs-lookup"><span data-stu-id="a83a8-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="a83a8-123">Merhaba **sanal makine oluşturma** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="a83a8-123">hello **Create virtual machine** blade opens.</span></span> <span data-ttu-id="a83a8-124">Buraya bir çalıştıran sanal makineyi (VM) ayarlama gerekli toospin hello NGFW bilgiler girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a83a8-124">Here you can enter information required toospin up a virtual machine (VM) that runs hello NGFW.</span></span> <span data-ttu-id="a83a8-125">Merhaba adımları ve gerekli hello NGFW bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a83a8-125">Follow hello steps and provide hello NGFW information required.</span></span> <span data-ttu-id="a83a8-126">Tamam tooapply seçin.</span><span class="sxs-lookup"><span data-stu-id="a83a8-126">Select OK tooapply.</span></span>
   <span data-ttu-id="a83a8-127">![Sanal makine toorun NGFW oluşturma][6]</span><span class="sxs-lookup"><span data-stu-id="a83a8-127">![Create virtual machine toorun NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="a83a8-128">Trafiği yalnızca NGFW aracılığıyla yönlendir</span><span class="sxs-lookup"><span data-stu-id="a83a8-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="a83a8-129">Toohello iade **önerileri** dikey.</span><span class="sxs-lookup"><span data-stu-id="a83a8-129">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="a83a8-130">Güvenlik Merkezi, adlı aracılığıyla bir NGFW eklendikten sonra yeni bir giriş oluşturulan **rota yalnızca trafiği NGFW aracılığıyla**.</span><span class="sxs-lookup"><span data-stu-id="a83a8-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="a83a8-131">Bu öneri, yalnızca Güvenlik Merkezi aracılığıyla, NGFW yüklediyseniz oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a83a8-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="a83a8-132">Internet'e yönelik uç noktaları varsa, Güvenlik Merkezi gelen trafiği tooyour, NGFW aracılığıyla VM zorla ağ güvenlik grubu kurallarını yapılandırmak önerir.</span><span class="sxs-lookup"><span data-stu-id="a83a8-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic tooyour VM through your NGFW.</span></span>

1. <span data-ttu-id="a83a8-133">Merhaba, **öneriler dikey**seçin **rota yalnızca trafiği NGFW aracılığıyla**.</span><span class="sxs-lookup"><span data-stu-id="a83a8-133">In hello **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="a83a8-134">![Trafiği yalnızca NGFW aracılığıyla yönlendirme][7]</span><span class="sxs-lookup"><span data-stu-id="a83a8-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="a83a8-135">Bu hello dikey pencere açılır **rota yalnızca trafiği NGFW aracılığıyla**, trafiği yönlendirebilir sanal makineleri listeler.</span><span class="sxs-lookup"><span data-stu-id="a83a8-135">This opens hello blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="a83a8-136">Bir VM hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="a83a8-136">Select a VM from hello list.</span></span>
   <span data-ttu-id="a83a8-137">![Bir VM seçin][8]</span><span class="sxs-lookup"><span data-stu-id="a83a8-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="a83a8-138">Hello için dikey penceresinde seçili VM açar, ilgili gelen kuralları görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="a83a8-138">A blade for hello selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="a83a8-139">Bir açıklama olası sonraki adımlar hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a83a8-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="a83a8-140">Seçin **gelen kuralları Düzenle** bir gelen kuralı düzenleme ile tooproceed.</span><span class="sxs-lookup"><span data-stu-id="a83a8-140">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span> <span data-ttu-id="a83a8-141">Merhaba beklenir, **kaynak** çok ayarlanmadı**herhangi** hello Internet'e yönelik uç noktalar ile bağlantılı için NGFW hello.</span><span class="sxs-lookup"><span data-stu-id="a83a8-141">hello expectation is that **Source** is not set too**Any** for hello Internet-facing endpoints linked with hello NGFW.</span></span> <span data-ttu-id="a83a8-142">toolearn hello gelen kuralı hello özellikleri hakkında daha fazla bilgi görmek [NSG kuralları](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="a83a8-142">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="a83a8-143">![Kuralları toolimit erişimi yapılandırma][9]
   ![düzenleme gelen kuralı][10]</span><span class="sxs-lookup"><span data-stu-id="a83a8-143">![Configure rules toolimit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="a83a8-144">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a83a8-144">See also</span></span>
<span data-ttu-id="a83a8-145">Bu belge size nasıl tooimplement hello Güvenlik Merkezi öneri "Ekleme yeni nesil güvenlik duvarı." gösterdi.</span><span class="sxs-lookup"><span data-stu-id="a83a8-145">This document showed you how tooimplement hello Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="a83a8-146">toolearn NGFWs ve hello denetim noktası iş ortağı çözümü hakkında daha fazla hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="a83a8-146">toolearn more about NGFWs and hello Check Point partner solution, see hello following:</span></span>

* [<span data-ttu-id="a83a8-147">Yeni nesil güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="a83a8-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="a83a8-148">Denetim noktası vSEC</span><span class="sxs-lookup"><span data-stu-id="a83a8-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="a83a8-149">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="a83a8-149">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="a83a8-150">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="a83a8-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="a83a8-151">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a83a8-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="a83a8-152">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a83a8-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="a83a8-153">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="a83a8-153">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="a83a8-154">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a83a8-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="a83a8-155">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a83a8-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="a83a8-156">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a83a8-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
