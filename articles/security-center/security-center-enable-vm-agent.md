---
title: "Azure Güvenlik Merkezi'nde VM Aracısı aaaEnable | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** etkinleştirmek VM Aracısı **."
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
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="24752-103">Azure Güvenlik Merkezi'nde VM aracısını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="24752-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="24752-104">Merhaba VM Aracısı sanal makineleri (VM'ler) sırayla çok yüklenmelidir[veri toplamayı etkinleştirmek](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="24752-104">hello VM Agent must be installed on virtual machines (VMs) in order too[enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="24752-105">Sanal makineleri gerektiren, toosee VM Aracısı hello ve işlem etkinleştirmenizi öneririz azure Güvenlik Merkezi sağlar, bu vm'lerde VM Aracısı hello.</span><span class="sxs-lookup"><span data-stu-id="24752-105">Azure Security Center enables you toosee which VMs require hello VM Agent and will recommend that you enable hello VM Agent on those VMs.</span></span>

<span data-ttu-id="24752-106">Merhaba VM Aracısı, Azure Marketi hello dağıtılan VM'ler için varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="24752-106">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="24752-107">Merhaba makale [VM aracısı ve uzantılar – Kısım 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) nasıl tooinstall hello üzerinde VM aracısı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="24752-107">hello article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="24752-108">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="24752-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="24752-109">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="24752-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="24752-110">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="24752-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="24752-111">Merhaba, **öneriler dikey**seçin **etkinleştirmek VM Aracısı**.</span><span class="sxs-lookup"><span data-stu-id="24752-111">In hello **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="24752-112">![VM Aracısını etkinleştirin][1]</span><span class="sxs-lookup"><span data-stu-id="24752-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="24752-113">Bu hello dikey pencere açılır **VM Aracısı eksik veya yanıt vermiyor**.</span><span class="sxs-lookup"><span data-stu-id="24752-113">This opens hello blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="24752-114">Bu dikey penceresinde hello VM Aracısı gerektiren hello sanal makineleri listeler.</span><span class="sxs-lookup"><span data-stu-id="24752-114">This blade lists hello VMs that require hello VM Agent.</span></span> <span data-ttu-id="24752-115">Merhaba dikey tooinstall hello VM Aracısı'nı Hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="24752-115">Follow hello instructions on hello blade tooinstall hello VM agent.</span></span>
   <span data-ttu-id="24752-116">![VM Aracısı eksik.][2]</span><span class="sxs-lookup"><span data-stu-id="24752-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="24752-117">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="24752-117">See also</span></span>
<span data-ttu-id="24752-118">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="24752-118">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="24752-119">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md)--öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="24752-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="24752-120">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) - Önerilerin Azure kaynaklarınızı korumanıza nasıl yardım edeceği hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="24752-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="24752-121">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md)--nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="24752-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="24752-122">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md)--öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="24752-122">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="24752-123">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="24752-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="24752-124">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md)--hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24752-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="24752-125">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/)--hello en son Azure güvenlik haberlerini ve bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="24752-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
