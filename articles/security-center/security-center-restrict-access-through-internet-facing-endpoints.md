---
title: "Azure Güvenlik Merkezi'nde Internet'e yönelik uç noktalar aracılığıyla aaaRestrict erişimi | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** Internet'e yönelik uç nokta ** aracılığıyla erişimi kısıtlayın."
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
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="52b33-103">Azure Güvenlik Merkezi'nde Internet'e yönelik uç noktalar aracılığıyla erişimi kısıtlama</span><span class="sxs-lookup"><span data-stu-id="52b33-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="52b33-104">Azure Güvenlik Merkezi, herhangi bir ağ güvenlik grupları (Nsg'ler) varsa, "tüm" kaynak IP adresleri erişime izin verecek bir veya daha fazla gelen kuralları Internet'e yönelik uç noktalar aracılığıyla erişimi kısıtlamak önerir.</span><span class="sxs-lookup"><span data-stu-id="52b33-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="52b33-105">Erişim çok "herhangi" açma saldırganlar tooaccess kaynaklarınızı sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="52b33-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="52b33-106">Güvenlik Merkezi, erişim gerektiren bu gelen kuralları toorestrict erişim toosource IP adreslerini Düzenle önerir.</span><span class="sxs-lookup"><span data-stu-id="52b33-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="52b33-107">Bu öneri, "" kaynağı olarak içeren herhangi bir web dışı bağlantı için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="52b33-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="52b33-108">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="52b33-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="52b33-109">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="52b33-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="52b33-110">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="52b33-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="52b33-111">Merhaba, **öneriler dikey**seçin **Internet'e yönelik uç noktası aracılığıyla erişimi kısıtlamak**.</span><span class="sxs-lookup"><span data-stu-id="52b33-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![İnternet'e yönelik uç nokta ile erişimi kısıtlama][1]
2. <span data-ttu-id="52b33-113">Bu hello dikey pencere açılır **Internet'e yönelik uç noktası aracılığıyla erişimi kısıtlamak**.</span><span class="sxs-lookup"><span data-stu-id="52b33-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="52b33-114">Bu dikey potansiyel bir güvenlik sorunu oluşturmak gelen kuralları ile Merhaba sanal makineleri (VM'ler) listeler.</span><span class="sxs-lookup"><span data-stu-id="52b33-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="52b33-115">Bir VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="52b33-115">Select a VM.</span></span>

   ![Bir VM seçin][2]
3. <span data-ttu-id="52b33-117">Merhaba **NSG** dikey ağ güvenlik grubu bilgileri, ilgili gelen kuralları, görüntüler ve hello ilişkili VM.</span><span class="sxs-lookup"><span data-stu-id="52b33-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="52b33-118">Seçin **gelen kuralları Düzenle** bir gelen kuralı düzenleme ile tooproceed.</span><span class="sxs-lookup"><span data-stu-id="52b33-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![Ağ güvenlik grubu dikey penceresi][3]
4. <span data-ttu-id="52b33-120">Merhaba üzerinde **gelen güvenlik kuralları** hello gelen kuralı tooedit dikey seçin.</span><span class="sxs-lookup"><span data-stu-id="52b33-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="52b33-121">Bu örnekte, şimdi seçin **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="52b33-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Gelen güvenlik kuralları][4]

   <span data-ttu-id="52b33-123">Not, ayrıca seçebilirsiniz **varsayılan kuralları** toosee hello tüm Nsg'ler tarafından bulunan varsayılan kuralları kümesi.</span><span class="sxs-lookup"><span data-stu-id="52b33-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="52b33-124">Merhaba varsayılan kurallar silinemez ancak daha düşük bir öncelik atandığı için oluşturduğunuz hello kurallarıyla kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="52b33-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="52b33-125">Daha fazla bilgi edinmek [varsayılan kuralları](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="52b33-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Varsayılan kurallar][5]
5. <span data-ttu-id="52b33-127">Merhaba üzerinde **AllowWeb** dikey penceresinde, hello şekilde hello gelen kuralı düzenleme hello özelliklerini **kaynak** bir IP adresi veya IP adresleri bloğu.</span><span class="sxs-lookup"><span data-stu-id="52b33-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="52b33-128">toolearn hello gelen kuralı hello özellikleri hakkında daha fazla bilgi görmek [NSG kuralları](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="52b33-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Gelen kuralını Düzenle][6]

## <a name="see-also"></a><span data-ttu-id="52b33-130">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="52b33-130">See also</span></span>
<span data-ttu-id="52b33-131">Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "erişimi kısıtlama Internet'e yönelik uç noktası aracılığıyla." gösterdi.</span><span class="sxs-lookup"><span data-stu-id="52b33-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="52b33-132">Nsg'ler ve kurallarını etkinleştirme hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="52b33-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="52b33-133">Ağ Güvenlik Grubu (NSG) Nedir?</span><span class="sxs-lookup"><span data-stu-id="52b33-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="52b33-134">Azure portal kullanarak toomanage Nsg'ler nasıl hello</span><span class="sxs-lookup"><span data-stu-id="52b33-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="52b33-135">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="52b33-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="52b33-136">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md)--öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="52b33-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="52b33-137">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) - Önerilerin Azure kaynaklarınızı korumanıza nasıl yardım edeceği hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="52b33-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="52b33-138">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md)--nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="52b33-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="52b33-139">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md)--öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="52b33-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="52b33-140">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="52b33-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="52b33-141">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md)--hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52b33-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="52b33-142">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/)--hello en son Azure güvenlik haberlerini ve bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="52b33-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
