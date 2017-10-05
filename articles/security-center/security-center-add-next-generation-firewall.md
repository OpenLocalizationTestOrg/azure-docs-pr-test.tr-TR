---
title: "Azure Güvenlik Merkezi'nde yeni nesil güvenlik duvarı ekleme | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi önerileri uygulamak gösterilmiştir ** bir sonraki nesil güvenlik duvarı ** ekleyin ve ** yalnızca rota traffice NGFW aracılığıyla **."
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
ms.openlocfilehash: 30589d0a943517c03394a3aae7c03c8094e78c1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="f8a1e-103">Azure Güvenlik Merkezi'nde yeni nesil güvenlik duvarı ekleme</span><span class="sxs-lookup"><span data-stu-id="f8a1e-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="f8a1e-104">Azure Güvenlik Merkezi bir Microsoft iş ortağı güvenlik korumaları artırmak için yeni nesil Güvenlik Duvarı (NGFW) eklediğiniz önerebilir.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> <span data-ttu-id="f8a1e-105">Bu belge, bunun nasıl yapılacağı örneği aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-105">This document walks you through an example of how to do this.</span></span>

> [!NOTE]
> <span data-ttu-id="f8a1e-106">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="f8a1e-107">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="f8a1e-108">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="f8a1e-108">Implement the recommendation</span></span>
1. <span data-ttu-id="f8a1e-109">İçinde **önerileri** dikey penceresinde, select **yeni nesil güvenlik duvarı ekleme**.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-109">In the **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="f8a1e-110">![Yeni Nesil Güvenlik Duvarı ekleme][1]</span><span class="sxs-lookup"><span data-stu-id="f8a1e-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="f8a1e-111">İçinde **yeni nesil güvenlik duvarı ekleme** dikey penceresinde, bir uç nokta seçin.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-111">In the **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="f8a1e-112">![Bir uç nokta seçin][2]</span><span class="sxs-lookup"><span data-stu-id="f8a1e-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="f8a1e-113">İkinci bir **yeni nesil güvenlik duvarı ekleme** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="f8a1e-114">Varsa varolan bir çözümü kullanmayı seçebilirsiniz veya yeni bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-114">You can choose to use an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="f8a1e-115">Bu örnekte, yok varolan çözüm bir NGFW oluşturuyoruz şekilde.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="f8a1e-116">![Yeni nesil güvenlik duvarı oluşturma][3]</span><span class="sxs-lookup"><span data-stu-id="f8a1e-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="f8a1e-117">Bir NGFW oluşturmak için bir çözüm tümleşik ortakları listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-117">To create an NGFW, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="f8a1e-118">Bu örnekte, biz seçin **Check Point**.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="f8a1e-119">![Yeni nesil güvenlik duvarı çözümü seçin][4]</span><span class="sxs-lookup"><span data-stu-id="f8a1e-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="f8a1e-120">**Check Point** dikey pencere açılır iş ortağı çözümü hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-120">The **Check Point** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="f8a1e-121">Seçin **oluşturma** bilgi dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-121">Select **Create** in the information blade.</span></span>
   <span data-ttu-id="f8a1e-122">![Güvenlik Duvarı bilgileri dikey penceresi][5]</span><span class="sxs-lookup"><span data-stu-id="f8a1e-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="f8a1e-123">**Sanal makine oluşturma** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-123">The **Create virtual machine** blade opens.</span></span> <span data-ttu-id="f8a1e-124">Buraya bir NGFW'nun çalıştıran sanal makineyi (VM) dönmesi için gerekli bilgileri girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-124">Here you can enter information required to spin up a virtual machine (VM) that runs the NGFW.</span></span> <span data-ttu-id="f8a1e-125">Aşağıdaki adımları uygulayın ve gerekli NGFW bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-125">Follow the steps and provide the NGFW information required.</span></span> <span data-ttu-id="f8a1e-126">Uygulamak için Tamam'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-126">Select OK to apply.</span></span>
   <span data-ttu-id="f8a1e-127">![NGFW çalıştırmak için sanal makine oluşturma][6]</span><span class="sxs-lookup"><span data-stu-id="f8a1e-127">![Create virtual machine to run NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="f8a1e-128">Trafiği yalnızca NGFW aracılığıyla yönlendir</span><span class="sxs-lookup"><span data-stu-id="f8a1e-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="f8a1e-129">Geri dönüp **önerileri** dikey.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-129">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="f8a1e-130">Güvenlik Merkezi, adlı aracılığıyla bir NGFW eklendikten sonra yeni bir giriş oluşturulan **rota yalnızca trafiği NGFW aracılığıyla**.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="f8a1e-131">Bu öneri, yalnızca Güvenlik Merkezi aracılığıyla, NGFW yüklediyseniz oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="f8a1e-132">Internet'e yönelik uç noktaları varsa, Güvenlik Merkezi, NGFW aracılığıyla, VM'ye gelen trafiği zorla ağ güvenlik grubu kurallarını yapılandırmak önerir.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic to your VM through your NGFW.</span></span>

1. <span data-ttu-id="f8a1e-133">İçinde **öneriler dikey**seçin **rota yalnızca trafiği NGFW aracılığıyla**.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-133">In the **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="f8a1e-134">![Trafiği yalnızca NGFW aracılığıyla yönlendirme][7]</span><span class="sxs-lookup"><span data-stu-id="f8a1e-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="f8a1e-135">Bu dikey pencere açılır **rota yalnızca trafiği NGFW aracılığıyla**, trafiği yönlendirebilir sanal makineleri listeler.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-135">This opens the blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="f8a1e-136">VM listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-136">Select a VM from the list.</span></span>
   <span data-ttu-id="f8a1e-137">![Bir VM seçin][8]</span><span class="sxs-lookup"><span data-stu-id="f8a1e-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="f8a1e-138">İlgili gelen kuralları görüntüleme seçili VM için bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-138">A blade for the selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="f8a1e-139">Bir açıklama olası sonraki adımlar hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="f8a1e-140">Seçin **gelen kuralları Düzenle** bir gelen kuralı düzenleme ile devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-140">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span> <span data-ttu-id="f8a1e-141">Beklentisi **kaynak** ayarlanmazsa **herhangi** NGFW'nun ile bağlantılı Internet'e yönelik uç noktalar için.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-141">The expectation is that **Source** is not set to **Any** for the Internet-facing endpoints linked with the NGFW.</span></span> <span data-ttu-id="f8a1e-142">Gelen kuralı özellikleri hakkında daha fazla bilgi için bkz: [NSG kuralları](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="f8a1e-142">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="f8a1e-143">![Erişimi sınırlamak için kurallar Yapılandır][9]
   ![düzenleme gelen kuralı][10]</span><span class="sxs-lookup"><span data-stu-id="f8a1e-143">![Configure rules to limit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="f8a1e-144">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-144">See also</span></span>
<span data-ttu-id="f8a1e-145">Bu belgede Güvenlik Merkezi öneri "Ekleme yeni nesil güvenlik duvarı." uygulamak nasıl oluşturulacağını gösterir</span><span class="sxs-lookup"><span data-stu-id="f8a1e-145">This document showed you how to implement the Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="f8a1e-146">NGFWs ve denetim noktası iş ortağı çözümü hakkında daha fazla bilgi için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-146">To learn more about NGFWs and the Check Point partner solution, see the following:</span></span>

* [<span data-ttu-id="f8a1e-147">Yeni nesil güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="f8a1e-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="f8a1e-148">Denetim noktası vSEC</span><span class="sxs-lookup"><span data-stu-id="f8a1e-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="f8a1e-149">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="f8a1e-149">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="f8a1e-150">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --güvenlik ilkeleri yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="f8a1e-151">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f8a1e-152">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --Azure kaynaklarınızı sağlığını izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="f8a1e-153">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) -- Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-153">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="f8a1e-154">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="f8a1e-155">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -- Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="f8a1e-156">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8a1e-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

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
