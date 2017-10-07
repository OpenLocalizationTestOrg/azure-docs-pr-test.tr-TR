---
title: "Azure Güvenlik Merkezi'nde güvenlik uyarılarını aaaHandling | Microsoft Docs"
description: "Bu belge toouse Azure Güvenlik Merkezi özellikleri toohandle güvenlik olaylarına yardımcı olur."
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
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="018ac-103">Azure Güvenlik Merkezi’nde Güvenlik Olaylarını İşleme</span><span class="sxs-lookup"><span data-stu-id="018ac-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="018ac-104">Önceliklendirme ve güvenlik uyarıları İnceleme olabilir zaman bile hello en becerikli güvenlik analistleri için alıcı ve çoğu için sabit tooeven bilmeniz nerede olduğu toobegin.</span><span class="sxs-lookup"><span data-stu-id="018ac-104">Triaging and investigating security alerts can be time consuming for even hello most skilled security analysts, and for many it is hard tooeven know where toobegin.</span></span> <span data-ttu-id="018ac-105">Kullanarak [analytics](security-center-detection-capabilities.md) ayrı arasında tooconnect hello bilgi [güvenlik uyarıları](security-center-managing-and-responding-alerts.md), Güvenlik Merkezi, bir saldırı kampanya tek bir görünümünü sağlayabilir ve ilişkili tüm hello uyarılar – yapabilecekleriniz hızlı bir şekilde hangi eylemleri hello saldırgan sürdü ve hangi kaynaklara etkilendiğini anlayın.</span><span class="sxs-lookup"><span data-stu-id="018ac-105">By using [analytics](security-center-detection-capabilities.md) tooconnect hello information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of hello related alerts – you can quickly understand what actions hello attacker took and what resources were impacted.</span></span>

<span data-ttu-id="018ac-106">Bu belge nasıl toouse güvenlik uyarısı Güvenlik Merkezi tooassist özelliği, güvenlik olaylarını işleme açıklanır.</span><span class="sxs-lookup"><span data-stu-id="018ac-106">This document discusses how toouse security alert capability in Security Center tooassist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="018ac-107">Güvenlik olayı nedir?</span><span class="sxs-lookup"><span data-stu-id="018ac-107">What is a security incident?</span></span>
<span data-ttu-id="018ac-108">Güvenlik Merkezi'nde bir güvenlik olayı, bir kaynağın [sonlandırma zinciri](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) desenleri ile hizalanan tüm uyarılarının toplamıdır.</span><span class="sxs-lookup"><span data-stu-id="018ac-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="018ac-109">Olaylar görünür hello [güvenlik uyarıları](security-center-managing-and-responding-alerts.md) döşeme ve dikey.</span><span class="sxs-lookup"><span data-stu-id="018ac-109">Incidents appear in hello [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="018ac-110">Bir olay, tooobtain sağlayan hello ilgili uyarıların listesi, her oluşumu hakkında daha fazla bilgi görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="018ac-110">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="018ac-111">Güvenlik olaylarını yönetme</span><span class="sxs-lookup"><span data-stu-id="018ac-111">Managing security incidents</span></span>
<span data-ttu-id="018ac-112">Hello güvenlik uyarıları kutucuğuna bakarak geçerli güvenlik olayları gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="018ac-112">You can review your current security incidents by looking at hello security alerts tile.</span></span> <span data-ttu-id="018ac-113">Hello Azure portalına erişmek ve her güvenlik olay hakkında daha fazla ayrıntı toosee hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="018ac-113">Access hello Azure Portal and follow hello steps below toosee more details about each security incident:</span></span>

1. <span data-ttu-id="018ac-114">Merhaba Güvenlik Merkezi panosunda hello görürsünüz **güvenlik uyarıları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="018ac-114">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Güvenlik Merkezi'nde güvenlik uyarıları kutucuğu](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="018ac-116">Bu kutucuğu tooexpand ve bir güvenlik olayı algılandığında varsa, aşağıda gösterildiği gibi hello güvenlik uyarıları grafik altında görünür tıklatın:</span><span class="sxs-lookup"><span data-stu-id="018ac-116">Click on this tile tooexpand it and if a security incident is detected, it will appear under hello security alerts graph as shown  below:</span></span>

    ![Güvenlik olayı](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="018ac-118">Karşılaştırıldığında, tooother uyarıları Hello güvenlik olay açıklaması farklı bir simge sahip olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="018ac-118">Notice that hello security incident description has a different icon compared tooother alerts.</span></span> <span data-ttu-id="018ac-119">' I tıklatın, üzerinde tooview bu olay hakkında daha ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="018ac-119">Click on it tooview more details about this incident.</span></span>

    ![Güvenlik olayı](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="018ac-121">Merhaba üzerinde **olay** daha görürsünüz dikey geçerli durumunu (, bu durumda yüksek olan), önem derecesi, tam açıklamasını içerir, bu güvenlik olay hakkında ayrıntıları (Bu durumda hala olduğunu *etkin*, hangi hello kullanıcı anlamına gelir, bir eylem tooit gerçekleştirilecek kurmadı - bu hello olay hello içinde sağ tıklayarak yapılabilir **güvenlik uyarıları** dikey), hello saldırıya kaynak (Bu durumda *VM1*) hello olay için düzeltme adımları hello ve hello alt bölmede bu olayın dahil edilen hello uyarıların vardır.</span><span class="sxs-lookup"><span data-stu-id="018ac-121">On hello **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies hello user hasn't taken an action tooit - this can be done by right clicking on hello incident in hello **Security alerts** blade), hello attacked resource (in this case *VM1*), hello remediation steps for hello incident, and in hello bottom pane you have hello alerts that were included in this incident.</span></span> <span data-ttu-id="018ac-122">Her uyarı hakkında daha fazla bilgi tooobtain istiyorsanız, onu ve başka bir dikey pencere yalnızca'ı tıklatın, aşağıda gösterildiği gibi açılır:</span><span class="sxs-lookup"><span data-stu-id="018ac-122">If you want tooobtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![Güvenlik olayı](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="018ac-124">Bu dikey penceresinde Hello bilgi according toohello uyarı değişir.</span><span class="sxs-lookup"><span data-stu-id="018ac-124">hello information on this blade will vary according toohello alert.</span></span> <span data-ttu-id="018ac-125">Okuma [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları](security-center-managing-and-responding-alerts.md) hakkında daha fazla bilgi için toomanage Bu uyarılar.</span><span class="sxs-lookup"><span data-stu-id="018ac-125">Read [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how toomanage these alerts.</span></span> <span data-ttu-id="018ac-126">Bu özellik ile ilgili bazı önemli noktalar:</span><span class="sxs-lookup"><span data-stu-id="018ac-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="018ac-127">Yeni bir filtre görünüm tooIncident uyarıları yalnızca, yalnızca toocustomize ya da her ikisini de sağlar.</span><span class="sxs-lookup"><span data-stu-id="018ac-127">A new filter enables you toocustomize your view tooIncident only, Alerts only, or both.</span></span>
* <span data-ttu-id="018ac-128">Merhaba aynı uyarının bir olay (varsa) yanı sıra toobe tek başına uyarı olarak görünür bir parçası olarak bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="018ac-128">hello same alert can exist as part of an Incident (if applicable), as well as toobe visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="018ac-129">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="018ac-129">See also</span></span>
<span data-ttu-id="018ac-130">Bu belgede, Güvenlik Merkezi'nde güvenlik olay özelliği toouse hello nasıl öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="018ac-130">In this document, you learned how toouse hello security incident capability in Security Center.</span></span> <span data-ttu-id="018ac-131">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="018ac-131">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="018ac-132">Yönetme ve Azure Güvenlik Merkezi'nde toosecurity uyarılarını yanıt</span><span class="sxs-lookup"><span data-stu-id="018ac-132">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="018ac-133">Azure Güvenlik Merkezi Algılama Özellikleri</span><span class="sxs-lookup"><span data-stu-id="018ac-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="018ac-134">Azure Güvenlik Merkezi Planlama ve İşlemler Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="018ac-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="018ac-135">Yönetme ve Azure Güvenlik Merkezi'nde toosecurity uyarılarını yanıt</span><span class="sxs-lookup"><span data-stu-id="018ac-135">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="018ac-136">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md)--hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="018ac-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="018ac-137">[Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="018ac-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
