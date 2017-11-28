---
title: "Azure Güvenlik Merkezi'nde VM Aracısı etkinleştirme | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi öneriyi uygulamayı gösterilmiştir ** etkinleştirmek VM Aracısı **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 337a7adfd93c76882a749685702bea6d1524c96a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="0faa7-103">Azure Güvenlik Merkezi'nde VM aracısını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="0faa7-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="0faa7-104">Aşağıdakileri yapmak için sanal makineleri (VM'ler) üzerinde VM Aracısı yüklenmelidir [veri toplamayı etkinleştirmek](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="0faa7-104">The VM Agent must be installed on virtual machines (VMs) in order to [enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="0faa7-105">Azure Güvenlik Merkezi, hangi VM'ler VM Aracısı gerektirir ve bu vm'lerde VM Aracısı etkinleştirmenizi öneririz görmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="0faa7-105">Azure Security Center enables you to see which VMs require the VM Agent and will recommend that you enable the VM Agent on those VMs.</span></span>

<span data-ttu-id="0faa7-106">VM Aracısı, Azure Marketi’nden dağıtılan VM’ler için varsayılan olarak yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="0faa7-106">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="0faa7-107">[VM Aracısı ve Uzantılar – 2. Kısım](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) makalesinde VM Aracısının nasıl yüklendiğine ilişkin bilgiler verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0faa7-107">The article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="0faa7-108">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="0faa7-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="0faa7-109">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="0faa7-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="0faa7-110">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="0faa7-110">Implement the recommendation</span></span>
1. <span data-ttu-id="0faa7-111">İçinde **öneriler dikey**seçin **etkinleştirmek VM Aracısı**.</span><span class="sxs-lookup"><span data-stu-id="0faa7-111">In the **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="0faa7-112">![VM Aracısını etkinleştirin][1]</span><span class="sxs-lookup"><span data-stu-id="0faa7-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="0faa7-113">Bu dikey pencere açılır **VM Aracısı eksik veya yanıt vermiyor**.</span><span class="sxs-lookup"><span data-stu-id="0faa7-113">This opens the blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="0faa7-114">Bu dikey VM Aracısı gerektiren sanal makineleri listeler.</span><span class="sxs-lookup"><span data-stu-id="0faa7-114">This blade lists the VMs that require the VM Agent.</span></span> <span data-ttu-id="0faa7-115">Dikey VM Aracısı'nı yüklemek için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="0faa7-115">Follow the instructions on the blade to install the VM agent.</span></span>
   <span data-ttu-id="0faa7-116">![VM Aracısı eksik.][2]</span><span class="sxs-lookup"><span data-stu-id="0faa7-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="0faa7-117">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0faa7-117">See also</span></span>
<span data-ttu-id="0faa7-118">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="0faa7-118">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="0faa7-119">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) - Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0faa7-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="0faa7-120">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) - Önerilerin Azure kaynaklarınızı korumanıza nasıl yardım edeceği hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0faa7-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="0faa7-121">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) - Azure kaynaklarınızın sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0faa7-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="0faa7-122">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) - Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0faa7-122">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="0faa7-123">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0faa7-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="0faa7-124">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) - Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0faa7-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="0faa7-125">[Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - En son Azure güvenlik haberlerini ve bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="0faa7-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
