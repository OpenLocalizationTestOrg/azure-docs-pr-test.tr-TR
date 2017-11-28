---
title: "Azure Güvenlik Merkezi'nde güncelleştirme işletim sistemi sürümü | Microsoft Docs"
description: "Bu makalede Azure Güvenlik Merkezi öneriyi uygulamayı gösterilmiştir ** güncelleştirme işletim sistemi sürümü **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: aa372492-ecdb-4368-8fdd-d8ed31e216ee
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: ce0d178914907750e5da59f223a4b1e04b9bb6fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="6545c-103">Azure Güvenlik Merkezi'nde güncelleştirme işletim sistemi sürümü</span><span class="sxs-lookup"><span data-stu-id="6545c-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="6545c-104">İçindeki sanal makineler için (VM) bulut Hizmetleri, Azure Güvenlik Merkezi, daha yeni bir sürüm kullanılabilir işletim sistemi (OS) güncelleştirilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="6545c-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that the operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="6545c-105">Yalnızca bulut yuvaları izlenen üretimde çalışan web ve çalışan rolleri Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="6545c-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="6545c-106">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="6545c-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="6545c-107">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="6545c-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="6545c-108">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="6545c-108">Implement the recommendation</span></span>
1. <span data-ttu-id="6545c-109">İçinde **önerileri** dikey penceresinde, select **güncelleştirme işletim sistemi sürümü**.</span><span class="sxs-lookup"><span data-stu-id="6545c-109">In the **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="6545c-110">![İşletim sistemi sürümünü güncelleştirme][1]</span><span class="sxs-lookup"><span data-stu-id="6545c-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="6545c-111">Bu dikey pencere açılır **güncelleştirme işletim sistemi sürümü**.</span><span class="sxs-lookup"><span data-stu-id="6545c-111">This opens the blade **Update OS version**.</span></span> <span data-ttu-id="6545c-112">İşletim sistemi sürümü güncelleştirmek için bu dikey'ndaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6545c-112">Follow the steps in this blade to update the OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="6545c-113">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="6545c-113">See also</span></span>
<span data-ttu-id="6545c-114">Bu makalede "Güncelleştirme işletim sistemi sürümü." Güvenlik Merkezi öneriyi uygulamayı nasıl oluşturulacağını gösterir</span><span class="sxs-lookup"><span data-stu-id="6545c-114">This article showed you how to implement the Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="6545c-115">Bulut Hizmetleri ve bir bulut hizmeti için işletim sistemi sürümü güncelleştirme hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="6545c-115">To learn more about cloud services and updating the OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="6545c-116">Cloud Services’e genel bakış</span><span class="sxs-lookup"><span data-stu-id="6545c-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="6545c-117">Bir bulut hizmeti güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="6545c-117">How to update a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="6545c-118">Cloud Services’ı Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6545c-118">How to Configure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="6545c-119">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="6545c-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="6545c-120">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -- Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6545c-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="6545c-121">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6545c-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="6545c-122">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --Azure kaynaklarınızı sağlığını izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6545c-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="6545c-123">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) -- Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6545c-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="6545c-124">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6545c-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="6545c-125">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -- Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6545c-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="6545c-126">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --en son Azure güvenlik haberlerini ve bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="6545c-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-update-os-version/update-os-version.png
