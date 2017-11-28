---
title: "Azure Güvenlik Merkezi'nde Internet'e yönelik uç noktalar aracılığıyla erişimi kısıtlama | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi öneriyi uygulamayı gösterilmiştir ** Internet'e yönelik uç nokta ** aracılığıyla erişimi kısıtlayın."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: f7309c617f1705205e2c9f1b1b48d141391d45da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="1114e-103">Azure Güvenlik Merkezi'nde Internet'e yönelik uç noktalar aracılığıyla erişimi kısıtlama</span><span class="sxs-lookup"><span data-stu-id="1114e-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="1114e-104">Azure Güvenlik Merkezi, herhangi bir ağ güvenlik grupları (Nsg'ler) varsa, "tüm" kaynak IP adresleri erişime izin verecek bir veya daha fazla gelen kuralları Internet'e yönelik uç noktalar aracılığıyla erişimi kısıtlamak önerir.</span><span class="sxs-lookup"><span data-stu-id="1114e-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="1114e-105">"Herhangi bir" erişim açma kaynaklarınıza erişmek saldırganlar sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1114e-105">Opening access to “any” may enable attackers to access your resources.</span></span> <span data-ttu-id="1114e-106">Güvenlik Merkezi, aslında erişmesi gereken kaynak IP adresleri için erişimi kısıtlamak için bu gelen kuralları Düzenle önerir.</span><span class="sxs-lookup"><span data-stu-id="1114e-106">Security Center will recommend that you edit these inbound rules to restrict access to source IP addresses that actually need access.</span></span>

<span data-ttu-id="1114e-107">Bu öneri, "" kaynağı olarak içeren herhangi bir web dışı bağlantı için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1114e-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="1114e-108">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="1114e-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="1114e-109">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="1114e-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="1114e-110">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="1114e-110">Implement the recommendation</span></span>
1. <span data-ttu-id="1114e-111">İçinde **öneriler dikey**seçin **Internet'e yönelik uç noktası aracılığıyla erişimi kısıtlamak**.</span><span class="sxs-lookup"><span data-stu-id="1114e-111">In the **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![İnternet'e yönelik uç nokta ile erişimi kısıtlama][1]
2. <span data-ttu-id="1114e-113">Bu dikey pencere açılır **Internet'e yönelik uç noktası aracılığıyla erişimi kısıtlamak**.</span><span class="sxs-lookup"><span data-stu-id="1114e-113">This opens the blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="1114e-114">Bu dikey potansiyel bir güvenlik sorunu oluşturmak gelen kuralları ile sanal makineleri (VM'ler) listeler.</span><span class="sxs-lookup"><span data-stu-id="1114e-114">This blade lists the virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="1114e-115">Bir VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="1114e-115">Select a VM.</span></span>

   ![Bir VM seçin][2]
3. <span data-ttu-id="1114e-117">**NSG** ağ güvenlik grubu bilgileri, ilgili gelen kuralları ve ilişkili VM dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1114e-117">The **NSG** blade displays Network Security Group information, related inbound rules, and the associated VM.</span></span> <span data-ttu-id="1114e-118">Seçin **gelen kuralları Düzenle** bir gelen kuralı düzenleme ile devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="1114e-118">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span>

   ![Ağ güvenlik grubu dikey penceresi][3]
4. <span data-ttu-id="1114e-120">Üzerinde **gelen güvenlik kuralları** dikey penceresinde düzenlemek için gelen kuralı seçin.</span><span class="sxs-lookup"><span data-stu-id="1114e-120">On the **Inbound security rules** blade select the inbound rule to edit.</span></span> <span data-ttu-id="1114e-121">Bu örnekte, şimdi seçin **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="1114e-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Gelen güvenlik kuralları][4]

   <span data-ttu-id="1114e-123">Not, ayrıca seçebilirsiniz **varsayılan kuralları** tüm Nsg'ler tarafından bulunan varsayılan kurallar kümesini görmek için.</span><span class="sxs-lookup"><span data-stu-id="1114e-123">Note, you can also select **Default rules** to see the set of default rules contained by all NSGs.</span></span> <span data-ttu-id="1114e-124">Varsayılan kurallar silinemez ancak daha düşük bir öncelik atandığı için oluşturduğunuz kurallar tarafından kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="1114e-124">The default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by the rules that you create.</span></span> <span data-ttu-id="1114e-125">Daha fazla bilgi edinmek [varsayılan kuralları](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="1114e-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Varsayılan kurallar][5]
5. <span data-ttu-id="1114e-127">Üzerinde **AllowWeb** dikey penceresinde, gelen kuralı özelliklerini düzenlemek için **kaynak** bir IP adresi veya IP adresleri bloğu.</span><span class="sxs-lookup"><span data-stu-id="1114e-127">On the **AllowWeb** blade, edit the properties of the inbound rule so that the **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="1114e-128">Gelen kuralı özellikleri hakkında daha fazla bilgi için bkz: [NSG kuralları](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="1114e-128">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Gelen kuralını Düzenle][6]

## <a name="see-also"></a><span data-ttu-id="1114e-130">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="1114e-130">See also</span></span>
<span data-ttu-id="1114e-131">Bu makalede "Internet'e yönelik uç nokta aracılığıyla erişimi kısıtlama". Güvenlik Merkezi öneriyi uygulamayı nasıl oluşturulacağını gösterir</span><span class="sxs-lookup"><span data-stu-id="1114e-131">This article showed you how to implement the Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="1114e-132">Nsg'ler ve kurallarını etkinleştirme hakkında daha fazla bilgi edinmek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="1114e-132">To learn more about enabling NSGs and rules, see the following:</span></span>

* [<span data-ttu-id="1114e-133">Ağ Güvenlik Grubu (NSG) Nedir?</span><span class="sxs-lookup"><span data-stu-id="1114e-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="1114e-134">Azure portalını kullanarak Nsg'ler yönetme</span><span class="sxs-lookup"><span data-stu-id="1114e-134">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="1114e-135">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="1114e-135">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="1114e-136">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) - Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1114e-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="1114e-137">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) - Önerilerin Azure kaynaklarınızı korumanıza nasıl yardım edeceği hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1114e-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="1114e-138">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) - Azure kaynaklarınızın sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1114e-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="1114e-139">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) - Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1114e-139">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="1114e-140">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1114e-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="1114e-141">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) - Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1114e-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="1114e-142">[Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - En son Azure güvenlik haberlerini ve bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="1114e-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
