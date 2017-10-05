---
title: "Azure Güvenlik Merkezi'nde güvenlik uyarılarını işleme | Microsoft Belgeleri"
description: "Bu belge, güvenlik olaylarını işlemek için Azure Güvenlik Merkezi özelliklerini kullanmanıza yardımcı olur."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: a302f8cb2555eef469a24da2523fdd9b97cc5730
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="0f2be-103">Azure Güvenlik Merkezi’nde Güvenlik Olaylarını İşleme</span><span class="sxs-lookup"><span data-stu-id="0f2be-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="0f2be-104">Güvenlik uyarılarının önceliklendirilmesi ve araştırılması en nitelikli güvenlik analiz uzmanları için bile vakit harcayıcı olabilir ve birçoğu için nereden başlanacağını bilmek bile zordur.</span><span class="sxs-lookup"><span data-stu-id="0f2be-104">Triaging and investigating security alerts can be time consuming for even the most skilled security analysts, and for many it is hard to even know where to begin.</span></span> <span data-ttu-id="0f2be-105">Farklı [güvenlik uyarıları](security-center-managing-and-responding-alerts.md) arasındaki bilgileri bağlamak için [Analiz](security-center-detection-capabilities.md) özelliğini kullanan Güvenlik Merkezi, bir saldırı kampanyasını ve tüm ilgili uyarıları tek bir yerde görmenizi sağlayabilir; saldırganın hangi işlemleri yaptığını ve hangi kaynakların etkilendiğini hızlıca görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f2be-105">By using [analytics](security-center-detection-capabilities.md) to connect the information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of the related alerts – you can quickly understand what actions the attacker took and what resources were impacted.</span></span>

<span data-ttu-id="0f2be-106">Bu belge Güvenlik Merkezi’ndeki güvenlik uyarısı özelliğinin güvenlik olaylarını işlemenize nasıl yardımcı olduğunu ele almaktadır.</span><span class="sxs-lookup"><span data-stu-id="0f2be-106">This document discusses how to use security alert capability in Security Center to assist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="0f2be-107">Güvenlik olayı nedir?</span><span class="sxs-lookup"><span data-stu-id="0f2be-107">What is a security incident?</span></span>
<span data-ttu-id="0f2be-108">Güvenlik Merkezi'nde bir güvenlik olayı, bir kaynağın [sonlandırma zinciri](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) desenleri ile hizalanan tüm uyarılarının toplamıdır.</span><span class="sxs-lookup"><span data-stu-id="0f2be-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="0f2be-109">Olaylar [Güvenlik Uyarıları](security-center-managing-and-responding-alerts.md) kutucuğunda ve dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0f2be-109">Incidents appear in the [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="0f2be-110">Bir Olay, her olay hakkında daha fazla bilgi almanızı sağlayan ilgili uyarıların listesini ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="0f2be-110">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="0f2be-111">Güvenlik olaylarını yönetme</span><span class="sxs-lookup"><span data-stu-id="0f2be-111">Managing security incidents</span></span>
<span data-ttu-id="0f2be-112">Geçerli güvenlik olaylarınızı güvenlik uyarıları kutucuğuna bakarak gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f2be-112">You can review your current security incidents by looking at the security alerts tile.</span></span> <span data-ttu-id="0f2be-113">Azure Portal’a erişin ve aşağıdaki adımları izleyerek her bir güvenlik olayına ilişkin daha fazla ayrıntı görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="0f2be-113">Access the Azure Portal and follow the steps below to see more details about each security incident:</span></span>

1. <span data-ttu-id="0f2be-114">Güvenlik Merkezi panosunda **Güvenlik uyarıları** kutucuğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0f2be-114">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Güvenlik Merkezi'nde güvenlik uyarıları kutucuğu](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="0f2be-116">Bu kutucuğa tıklayarak kutucuğu genişletin; bir güvenlik olayı algılanırsa aşağıda gösterildiği gibi güvenlik uyarıları grafiğinin altında görünür:</span><span class="sxs-lookup"><span data-stu-id="0f2be-116">Click on this tile to expand it and if a security incident is detected, it will appear under the security alerts graph as shown  below:</span></span>

    ![Güvenlik olayı](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="0f2be-118">Güvenlik olayı açıklamasının diğer uyarılardan farklı bir simgeye sahip olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="0f2be-118">Notice that the security incident description has a different icon compared to other alerts.</span></span> <span data-ttu-id="0f2be-119">Bu olay hakkında daha fazla ayrıntı görüntülemek için üzerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0f2be-119">Click on it to view more details about this incident.</span></span>

    ![Güvenlik olayı](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="0f2be-121">**Olay** dikey penceresinde, bu güvenlik olayının tam açıklaması, önem düzeyi (bu durumda yüksektir), olayın geçerli durumu (bu durumda hala *etkindir* ve kullanıcının uyarı için henüz bir eylem gerçekleştirmediğini gösterir; bu işlem, **Güvenlik uyarıları** dikey penceresinde olaya tıklanarak gerçekleştirilebilir), saldırılan kaynak (bu durumda *VM1*), ve düzeltme adımları dahil olmak üzere olayla ilgili daha fazla ayrıntıyı görürsünüz ve alt bölmede bu olaya dahil edilen uyarılar yer alır.</span><span class="sxs-lookup"><span data-stu-id="0f2be-121">On the **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies the user hasn't taken an action to it - this can be done by right clicking on the incident in the **Security alerts** blade), the attacked resource (in this case *VM1*), the remediation steps for the incident, and in the bottom pane you have the alerts that were included in this incident.</span></span> <span data-ttu-id="0f2be-122">Her uyarı hakkında daha fazla bilgi edinmek istiyorsanız, uyarıya tıklayarak aşağıda gösterildiği gibi başka bir dikey pencere açılmasını sağlayın:</span><span class="sxs-lookup"><span data-stu-id="0f2be-122">If you want to obtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![Güvenlik olayı](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="0f2be-124">Bu dikey penceredeki bilgiler uyarıya göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f2be-124">The information on this blade will vary according to the alert.</span></span> <span data-ttu-id="0f2be-125">Bu uyarıların nasıl yönetileceği hakkında daha fazla bilgi için [Azure Güvenlik Merkezi’nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="0f2be-125">Read [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how to manage these alerts.</span></span> <span data-ttu-id="0f2be-126">Bu özellik ile ilgili bazı önemli noktalar:</span><span class="sxs-lookup"><span data-stu-id="0f2be-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="0f2be-127">Yeni bir filtre, görünümünüzü Yalnızca olay, Yalnızca uyarılar veya her ikisi için özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0f2be-127">A new filter enables you to customize your view to Incident only, Alerts only, or both.</span></span>
* <span data-ttu-id="0f2be-128">Aynı uyarı bir Olayın (varsa) parçası olabilir ve aynı zamanda tek başına uyarı olarak görünebilir.</span><span class="sxs-lookup"><span data-stu-id="0f2be-128">The same alert can exist as part of an Incident (if applicable), as well as to be visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="0f2be-129">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0f2be-129">See also</span></span>
<span data-ttu-id="0f2be-130">Bu belgede, Güvenlik Merkezi'nde güvenlik olayı özelliğini nasıl kullanacağınız hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="0f2be-130">In this document, you learned how to use the security incident capability in Security Center.</span></span> <span data-ttu-id="0f2be-131">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="0f2be-131">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="0f2be-132">Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama</span><span class="sxs-lookup"><span data-stu-id="0f2be-132">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="0f2be-133">Azure Güvenlik Merkezi Algılama Özellikleri</span><span class="sxs-lookup"><span data-stu-id="0f2be-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="0f2be-134">Azure Güvenlik Merkezi Planlama ve İşlemler Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="0f2be-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="0f2be-135">Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama</span><span class="sxs-lookup"><span data-stu-id="0f2be-135">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="0f2be-136">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) - Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f2be-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="0f2be-137">[Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="0f2be-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
