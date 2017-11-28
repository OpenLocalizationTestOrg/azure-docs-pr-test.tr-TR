---
title: "Azure Güvenlik Merkezi tehdit zekası raporu | Microsoft Docs"
description: "Bu belge, bir araştırma sırasında güvenlik uyarıları hakkında daha fazla bilgiye ulaşmak için Azure Güvenlik Merkezi Tehdit Zekası Raporlarını kullanmanıza yardımcı olur."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: b4310cf4e6849c67031b3ec8b1fd5957e35f7ea6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a><span data-ttu-id="13350-103">Azure Güvenlik Merkezi Tehdit Zekası Raporu</span><span class="sxs-lookup"><span data-stu-id="13350-103">Azure Security Center Threat Intelligence Report</span></span>
<span data-ttu-id="13350-104">Bu belge, Azure Güvenlik Merkezi Tehdit Zekası Raporlarının, güvenlik uyarılarını oluşturan tehditler hakkında daha fazla bilgi edinmenize nasıl yardımcı olabileceğini açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="13350-104">This document explains how Azure Security Center Threat Intelligent Reports can help you learn more about a threat that generated a security alert.</span></span>

## <a name="what-is-a-threat-intelligence-report"></a><span data-ttu-id="13350-105">Tehdit zekası rapor nedir?</span><span class="sxs-lookup"><span data-stu-id="13350-105">What is a threat intelligence report?</span></span>
<span data-ttu-id="13350-106">Güvenlik Merkezi tehdit algılaması Azure kaynaklarınızdan, ağınızdan ve bağlı iş ortağı çözümlerinden güvenlik verilerini izleyerek çalışır.</span><span class="sxs-lookup"><span data-stu-id="13350-106">Security Center threat detection works by monitoring security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="13350-107">Tehditleri belirlemek amacıyla bu bilgileri genellikle birden fazla kaynaktan bilgileri ilişkilendirerek analiz eder.</span><span class="sxs-lookup"><span data-stu-id="13350-107">It analyzes this information, often correlating information from multiple sources, to identify threats.</span></span> <span data-ttu-id="13350-108">Bu işlem, Güvenlik Merkezi [tanılama özelliklerinin](security-center-detection-capabilities.md) bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="13350-108">This process is part of the Security Center [detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="13350-109">Güvenlik Merkezi tarafından bir tehdit algılandığında, belirli bir olay için düzeltme önerileri de dahil olmak üzere ayrıntılı bilgiler içeren bir [güvenlik uyarısı](security-center-managing-and-responding-alerts.md) tetikler.</span><span class="sxs-lookup"><span data-stu-id="13350-109">When Security Center identifies a threat, it will trigger a [security alert](security-center-managing-and-responding-alerts.md), which contains detailed information regarding a particular event, including suggestions for remediation.</span></span> <span data-ttu-id="13350-110">Güvenlik Merkezi, olay yanıt ekiplerine tehdit araştırma ve düzeltme süreçlerinde yardımcı olmak üzere aşağıdaki bilgiler de dahil olmak üzere algılanan tehdit hakkında bilgiler içeren bir tehdit zekası raporu sunar:</span><span class="sxs-lookup"><span data-stu-id="13350-110">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected, including information such as the:</span></span>

* <span data-ttu-id="13350-111">Saldırganların kimliği veya bağlantıları (bu konuda bilgi varsa)</span><span class="sxs-lookup"><span data-stu-id="13350-111">Attacker’s identity or associations (if this information is available)</span></span>
* <span data-ttu-id="13350-112">Saldırganların hedefleri</span><span class="sxs-lookup"><span data-stu-id="13350-112">Attackers’ objectives</span></span>
* <span data-ttu-id="13350-113">Güncel ve geçmiş saldırı kampanyaları (bu konuda bilgi varsa)</span><span class="sxs-lookup"><span data-stu-id="13350-113">Current and historical attack campaigns (if this information is available)</span></span>
* <span data-ttu-id="13350-114">Saldırganların taktikleri, araçları ve yordamları</span><span class="sxs-lookup"><span data-stu-id="13350-114">Attackers’ tactics, tools and procedures</span></span>
* <span data-ttu-id="13350-115">URL’ler ve dosya karmaları gibi ilgili tehlike göstergeleri (IoC)</span><span class="sxs-lookup"><span data-stu-id="13350-115">Associated indicators of compromise (IoC) such as URLs and file hashes</span></span>
* <span data-ttu-id="13350-116">Azure kaynaklarınızın risk altında olup olmadığını belirlemenize yardımcı olmak için sektörel ve coğrafi yaygınlık bilgisi olan mağdur bilimi</span><span class="sxs-lookup"><span data-stu-id="13350-116">Victimology, which is the industry and geographic prevalence to assist you in determining if your Azure resources are at risk</span></span>
* <span data-ttu-id="13350-117">Azaltma ve düzeltme bilgileri</span><span class="sxs-lookup"><span data-stu-id="13350-117">Mitigation and remediation information</span></span>

> [!NOTE]
> <span data-ttu-id="13350-118">Raporlardaki bilgi düzeyi değişiklik gösterir. Ayrıntı düzeyi kötü amaçlı yazılımın etkinliğine ve yaygınlığına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="13350-118">The amount of information in any particular report will vary; the level of detail is based on the malware’s activity and prevalence.</span></span>
>
>

<span data-ttu-id="13350-119">Güvenlik Merkezi’nde, saldırıya göre değişiklik gösteren üç tehdit raporu türü vardır.</span><span class="sxs-lookup"><span data-stu-id="13350-119">Security Center has three types of threat reports, which can vary according to the attack.</span></span> <span data-ttu-id="13350-120">Raporlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="13350-120">The reports available are:</span></span>

* <span data-ttu-id="13350-121">**Etkinlik Grubu Raporu**: Saldırganlar, amaçları ve taktikleri hakkında ayrıntılı bilgi sunar.</span><span class="sxs-lookup"><span data-stu-id="13350-121">**Activity Group Report**: provides deep dives into attackers, their objectives and tactics.</span></span>
* <span data-ttu-id="13350-122">**Kampanya Raporu**: Belirli saldırı kampanyaların ayrıntılarına odaklanır.</span><span class="sxs-lookup"><span data-stu-id="13350-122">**Campaign Report**: focuses on details of specific attack campaigns.</span></span>
* <span data-ttu-id="13350-123">**Tehdit Özeti Raporu**: Yukarıdaki iki raporun tüm maddelerini kapsar.</span><span class="sxs-lookup"><span data-stu-id="13350-123">**Threat Summary Report**: covers all of the items in the previous two reports.</span></span>

<span data-ttu-id="13350-124">Bu tür bilgiler saldırının kaynağını, saldırganın niyetini ve ilerleyen dönemlerde bu riski azaltmak için yapılması gerekenlerin incelendiği bir soruşturmanın yapıldığı [olay yanıt](security-center-incident-response.md) sürecinde çok faydalı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="13350-124">This type of information is very useful during the [incident response](security-center-incident-response.md) process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

## <a name="how-to-access-the-threat-intelligence-report"></a><span data-ttu-id="13350-125">Tehdit zekası raporuna nasıl erişebilirim?</span><span class="sxs-lookup"><span data-stu-id="13350-125">How to access the threat intelligence report?</span></span>
<span data-ttu-id="13350-126">**Güvenlik uyarıları** kutucuğuna bakarak mevcut uyarılarınızı gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13350-126">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="13350-127">Azure Portal’ı açın ve her bir uyarı hakkında daha fazla ayrıntıya ulaşmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="13350-127">Open the Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="13350-128">Güvenlik Merkezi panosunda **Güvenlik uyarıları** kutucuğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="13350-128">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>
2. <span data-ttu-id="13350-129">Kutucuğa tıklayarak uyarılar hakkında daha fazla bilginin yer aldığı **Güvenlik uyarıları** dikey penceresini açın ve daha fazla bilgi almak istediğiniz güvenlik uyarısını seçin.</span><span class="sxs-lookup"><span data-stu-id="13350-129">Click the tile to open the **Security alerts** blade that contains more details about the alerts and click in the security alert that you want to obtain more information about.</span></span>

    ![Güvenlik uyarıları](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. <span data-ttu-id="13350-131">Bu durumda **Yürütülen şüpheli işlem** dikey penceresinde yer alan uyarı bilgileri aşağıdaki şekilde gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="13350-131">In this case the **Suspicious process executed** blade shows the details about the alert as shown in the figure below:</span></span>

    ![Güvenlik uyarısı ayrıntıları](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. <span data-ttu-id="13350-133">Güvenlik uyarılarındaki bilgi miktarı, uyarının türüne göre değişiklik gösterir.</span><span class="sxs-lookup"><span data-stu-id="13350-133">The amount of information available for each security alert will vary according to the type of alert.</span></span> <span data-ttu-id="13350-134">**RAPORLAR** alanında tehdit zekası raporunun bağlantısını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13350-134">In the **REPORTS** field you have a link to the threat intelligence report.</span></span> <span data-ttu-id="13350-135">Bağlantıya tıkladığınızda PDF dosyası yeni bir tarayıcı penceresinde açılacaktır.</span><span class="sxs-lookup"><span data-stu-id="13350-135">Click on it and another browser window will appear with PDF file.</span></span>

   ![Storage seçimi](./media/security-center-threat-report/security-center-threat-report-fig3.png)

<span data-ttu-id="13350-137">Buradan raporun PDF dosyasını indirebilir, algılanan güvenlik sorunu hakkında daha fazla bilgi edinebilir ve verilen bilgilere göre işlem yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13350-137">From here you can download the PDF for this report and read more about the security issue that was detected and take actions based on the information provided.</span></span>

## <a name="see-also"></a><span data-ttu-id="13350-138">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="13350-138">See also</span></span>
<span data-ttu-id="13350-139">Bu belgede Azure Güvenlik Merkezi Tehdit Zekası Raporlarının güvenlik uyarısı araştırmaları sırasında nasıl yardımcı olabileceğini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="13350-139">In this document, you learned how Azure Security Center Threat Intelligent Reports can help during an investigation about security alerts.</span></span> <span data-ttu-id="13350-140">Azure Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="13350-140">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="13350-141">[Azure Güvenlik Merkezi SSS](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="13350-141">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="13350-142">Hizmet kullanımı ile ilgili sık sorulan soruları bulun.</span><span class="sxs-lookup"><span data-stu-id="13350-142">Find frequently asked questions about using the service.</span></span>
* [<span data-ttu-id="13350-143">Olay Yanıtı için Azure Güvenlik Merkezi’nden Yararlanma</span><span class="sxs-lookup"><span data-stu-id="13350-143">Leveraging Azure Security Center for Incident Response</span></span>](security-center-incident-response.md)
* [<span data-ttu-id="13350-144">Azure Güvenlik Merkezi algılama özellikleri</span><span class="sxs-lookup"><span data-stu-id="13350-144">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* <span data-ttu-id="13350-145">[Azure Güvenlik Merkezi planlama ve işlemler kılavuzu](security-center-planning-and-operations-guide.md).</span><span class="sxs-lookup"><span data-stu-id="13350-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="13350-146">Azure Güvenlik Merkezi'ni benimsemek için tasarım ile ilgili dikkat edilmesi gerekenleri planlama ve anlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="13350-146">Learn how to plan and understand the design considerations to adopt Azure Security Center.</span></span>
* <span data-ttu-id="13350-147">[Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="13350-147">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span> <span data-ttu-id="13350-148">Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="13350-148">Learn how to manage and respond to security alerts.</span></span>
* [<span data-ttu-id="13350-149">Azure Güvenlik Merkezi'nde Güvenlik Olayını İşleme</span><span class="sxs-lookup"><span data-stu-id="13350-149">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* <span data-ttu-id="13350-150">[Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="13350-150">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="13350-151">Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulun.</span><span class="sxs-lookup"><span data-stu-id="13350-151">Find blog posts about Azure security and compliance.</span></span>
