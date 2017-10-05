---
title: "Azure Güvenlik Merkezi'nde Endpoint protection durumu uyarıları gidermek | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi öneriyi uygulamayı gösterilmiştir ** çözmek Endpoint Protection durumu uyarıları **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 5e6b136d6bd3b11fb82126d104fd0cb149255118
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="d9915-103">Azure Güvenlik Merkezi'nde uç nokta koruma durumu uyarıları Çözümle</span><span class="sxs-lookup"><span data-stu-id="d9915-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="d9915-104">Azure Güvenlik Merkezi, algılanan endpoint protection durumu uyarıları gidermek önerir.</span><span class="sxs-lookup"><span data-stu-id="d9915-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="d9915-105">Güvenlik Merkezi, endpoint protection hatalarını ve kaç tane hataları hangi sanal makineleri (VM'ler) sahip görmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d9915-105">Security Center enables you to see which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="d9915-106">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="d9915-106">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="d9915-107">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="d9915-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="d9915-108">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="d9915-108">Implement the recommendation</span></span>
1. <span data-ttu-id="d9915-109">İçinde **öneriler dikey**seçin **gidermek Endpoint Protection durumu uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="d9915-109">In the **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="d9915-110">![Endpoint Protection sistem durumu uyarılarını çözümleme][1]</span><span class="sxs-lookup"><span data-stu-id="d9915-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="d9915-111">Bu dikey pencere açılır **Endpoint Protection hata** listelerinin VM'ler hataları ve hata sayısı için her bir VM.</span><span class="sxs-lookup"><span data-stu-id="d9915-111">This opens the blade **Endpoint Protection failure** which lists VMs with failures and the number of failures for each VM.</span></span> <span data-ttu-id="d9915-112">VM listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="d9915-112">Select a VM from the list.</span></span>
   <span data-ttu-id="d9915-113">![Uç nokta koruma hatası][2]</span><span class="sxs-lookup"><span data-stu-id="d9915-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="d9915-114">A **hataları listesi** hatalarının listesini görüntüleyen seçili VM için dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="d9915-114">A **Failures List** blade opens for the selected VM, displaying a list of failures.</span></span> <span data-ttu-id="d9915-115">Bir hata daha fazla bilgi için listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="d9915-115">Select a failure from the list to learn more.</span></span> <span data-ttu-id="d9915-116">Seçili hata hakkında bilgi içeren bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="d9915-116">This opens a blade with information about the selected failure.</span></span>
   <span data-ttu-id="d9915-117">![Hataları listesi][3]
   ![hatası olayı][4]</span><span class="sxs-lookup"><span data-stu-id="d9915-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="d9915-118">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d9915-118">See also</span></span>
<span data-ttu-id="d9915-119">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="d9915-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="d9915-120">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) - Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d9915-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d9915-121">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) - Önerilerin Azure kaynaklarınızı korumanıza nasıl yardım edeceği hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d9915-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d9915-122">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) - Azure kaynaklarınızın sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d9915-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="d9915-123">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) - Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d9915-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="d9915-124">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d9915-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="d9915-125">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) - Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9915-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="d9915-126">[Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - En son Azure güvenlik haberlerini ve bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="d9915-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
