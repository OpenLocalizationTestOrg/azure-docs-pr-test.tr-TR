---
title: "Azure Güvenlik Merkezi'nde aaaResolve endpoint protection durumu uyarıları | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** çözmek Endpoint Protection durumu uyarıları **."
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
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="fdc2c-103">Azure Güvenlik Merkezi'nde uç nokta koruma durumu uyarıları Çözümle</span><span class="sxs-lookup"><span data-stu-id="fdc2c-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="fdc2c-104">Azure Güvenlik Merkezi, algılanan endpoint protection durumu uyarıları gidermek önerir.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="fdc2c-105">Güvenlik Merkezi, endpoint protection hatalarını ve kaç tane hataları hangi sanal makineleri (VM'ler) sahip toosee sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-105">Security Center enables you toosee which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="fdc2c-106">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-106">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="fdc2c-107">Bu, adım adım ilerleyen bir kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="fdc2c-108">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="fdc2c-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="fdc2c-109">Merhaba, **öneriler dikey**seçin **gidermek Endpoint Protection durumu uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-109">In hello **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="fdc2c-110">![Endpoint Protection sistem durumu uyarılarını çözümleme][1]</span><span class="sxs-lookup"><span data-stu-id="fdc2c-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="fdc2c-111">Bu hello dikey pencere açılır **Endpoint Protection hata** listelerinin VM'ler hataları ve hello sayısı için her bir VM.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-111">This opens hello blade **Endpoint Protection failure** which lists VMs with failures and hello number of failures for each VM.</span></span> <span data-ttu-id="fdc2c-112">Bir VM hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-112">Select a VM from hello list.</span></span>
   <span data-ttu-id="fdc2c-113">![Uç nokta koruma hatası][2]</span><span class="sxs-lookup"><span data-stu-id="fdc2c-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="fdc2c-114">A **hataları listesi** hello hatalarının listesini görüntüleyen VM, seçilen için dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-114">A **Failures List** blade opens for hello selected VM, displaying a list of failures.</span></span> <span data-ttu-id="fdc2c-115">Bir hata hello listesi toolearn daha fazla seçin.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-115">Select a failure from hello list toolearn more.</span></span> <span data-ttu-id="fdc2c-116">Bu, seçilen hello hata hakkında bilgi içeren bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-116">This opens a blade with information about hello selected failure.</span></span>
   <span data-ttu-id="fdc2c-117">![Hataları listesi][3]
   ![hatası olayı][4]</span><span class="sxs-lookup"><span data-stu-id="fdc2c-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="fdc2c-118">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-118">See also</span></span>
<span data-ttu-id="fdc2c-119">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="fdc2c-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="fdc2c-120">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md)--öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="fdc2c-121">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) - Önerilerin Azure kaynaklarınızı korumanıza nasıl yardım edeceği hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="fdc2c-122">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md)--nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="fdc2c-123">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md)--öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="fdc2c-124">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="fdc2c-125">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md)--hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="fdc2c-126">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/)--hello en son Azure güvenlik haberlerini ve bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="fdc2c-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
