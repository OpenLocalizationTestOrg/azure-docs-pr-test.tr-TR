---
title: "Güvenlik Merkezi tehdit Intelligence rapor aaaAzure | Microsoft Docs"
description: "Bu belge, toouse Azure Güvenlik Merkezi tehdit akıllı raporları bir araştırma toofind sırasında bir güvenlik uyarısı ilgili daha fazla bilgi yardımcı olur."
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
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a><span data-ttu-id="d3b0f-103">Azure Güvenlik Merkezi Tehdit Zekası Raporu</span><span class="sxs-lookup"><span data-stu-id="d3b0f-103">Azure Security Center Threat Intelligence Report</span></span>
<span data-ttu-id="d3b0f-104">Bu belge, Azure Güvenlik Merkezi Tehdit Zekası Raporlarının, güvenlik uyarılarını oluşturan tehditler hakkında daha fazla bilgi edinmenize nasıl yardımcı olabileceğini açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-104">This document explains how Azure Security Center Threat Intelligent Reports can help you learn more about a threat that generated a security alert.</span></span>

## <a name="what-is-a-threat-intelligence-report"></a><span data-ttu-id="d3b0f-105">Tehdit zekası rapor nedir?</span><span class="sxs-lookup"><span data-stu-id="d3b0f-105">What is a threat intelligence report?</span></span>
<span data-ttu-id="d3b0f-106">Güvenlik Merkezi tehdit algılaması Azure kaynaklarını, hello ağ ve bağlı iş ortağı çözümlerinden güvenlik bilgileri izleme ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-106">Security Center threat detection works by monitoring security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="d3b0f-107">Genellikle birden fazla kaynaktan tooidentify tehditleri bilgileri ilişkilendirerek, bu bilgileri çözümler.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-107">It analyzes this information, often correlating information from multiple sources, tooidentify threats.</span></span> <span data-ttu-id="d3b0f-108">Bu işlem hello Güvenlik Merkezi bir parçasıdır [algılama özellikleri](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="d3b0f-108">This process is part of hello Security Center [detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="d3b0f-109">Güvenlik Merkezi tarafından bir tehdit algılandığında, belirli bir olay için düzeltme önerileri de dahil olmak üzere ayrıntılı bilgiler içeren bir [güvenlik uyarısı](security-center-managing-and-responding-alerts.md) tetikler.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-109">When Security Center identifies a threat, it will trigger a [security alert](security-center-managing-and-responding-alerts.md), which contains detailed information regarding a particular event, including suggestions for remediation.</span></span> <span data-ttu-id="d3b0f-110">tooassist olay yanıtlama ekipleri araştırmak ve tehditleri düzeltme, Güvenlik Merkezi, gibi bilgiler dahil olmak üzere algılandı hello tehdit hakkında bilgi içeren bir tehdit Intelligence rapor içerir:</span><span class="sxs-lookup"><span data-stu-id="d3b0f-110">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected, including information such as the:</span></span>

* <span data-ttu-id="d3b0f-111">Saldırganların kimliği veya bağlantıları (bu konuda bilgi varsa)</span><span class="sxs-lookup"><span data-stu-id="d3b0f-111">Attacker’s identity or associations (if this information is available)</span></span>
* <span data-ttu-id="d3b0f-112">Saldırganların hedefleri</span><span class="sxs-lookup"><span data-stu-id="d3b0f-112">Attackers’ objectives</span></span>
* <span data-ttu-id="d3b0f-113">Güncel ve geçmiş saldırı kampanyaları (bu konuda bilgi varsa)</span><span class="sxs-lookup"><span data-stu-id="d3b0f-113">Current and historical attack campaigns (if this information is available)</span></span>
* <span data-ttu-id="d3b0f-114">Saldırganların taktikleri, araçları ve yordamları</span><span class="sxs-lookup"><span data-stu-id="d3b0f-114">Attackers’ tactics, tools and procedures</span></span>
* <span data-ttu-id="d3b0f-115">URL’ler ve dosya karmaları gibi ilgili tehlike göstergeleri (IoC)</span><span class="sxs-lookup"><span data-stu-id="d3b0f-115">Associated indicators of compromise (IoC) such as URLs and file hashes</span></span>
* <span data-ttu-id="d3b0f-116">Merhaba endüstri ve coğrafi yaygınlığını tooassist victimology size Azure kaynaklarınızı risk altında olup olmadığını belirleme</span><span class="sxs-lookup"><span data-stu-id="d3b0f-116">Victimology, which is hello industry and geographic prevalence tooassist you in determining if your Azure resources are at risk</span></span>
* <span data-ttu-id="d3b0f-117">Azaltma ve düzeltme bilgileri</span><span class="sxs-lookup"><span data-stu-id="d3b0f-117">Mitigation and remediation information</span></span>

> [!NOTE]
> <span data-ttu-id="d3b0f-118">Merhaba miktarda bilgi herhangi bir rapordaki değişir; ayrıntı düzeyini Hello hello kötü amaçlı yazılımın etkinliği ve yaygınlığını dayanır.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-118">hello amount of information in any particular report will vary; hello level of detail is based on hello malware’s activity and prevalence.</span></span>
>
>

<span data-ttu-id="d3b0f-119">Güvenlik Merkezi according toohello saldırı değişebilir tehdit raporları üç tür vardır.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-119">Security Center has three types of threat reports, which can vary according toohello attack.</span></span> <span data-ttu-id="d3b0f-120">kullanılabilir Hello raporlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d3b0f-120">hello reports available are:</span></span>

* <span data-ttu-id="d3b0f-121">**Etkinlik Grubu Raporu**: Saldırganlar, amaçları ve taktikleri hakkında ayrıntılı bilgi sunar.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-121">**Activity Group Report**: provides deep dives into attackers, their objectives and tactics.</span></span>
* <span data-ttu-id="d3b0f-122">**Kampanya Raporu**: Belirli saldırı kampanyaların ayrıntılarına odaklanır.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-122">**Campaign Report**: focuses on details of specific attack campaigns.</span></span>
* <span data-ttu-id="d3b0f-123">**İş parçacığı özet raporu**: hello önceki iki raporlarında hello öğelerin tümünü kapsar.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-123">**Threat Summary Report**: covers all of hello items in hello previous two reports.</span></span>

<span data-ttu-id="d3b0f-124">Bu tür bilgiler hello sırasında faydalıdır [olay yanıtlama](security-center-incident-response.md) işlem, bir sürekli araştırma toounderstand hello kaynak hello saldırı, saldırganın hello sözleri ve ne olduğu toodo toomitigate bu ilerleyen sorun.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-124">This type of information is very useful during hello [incident response](security-center-incident-response.md) process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

## <a name="how-tooaccess-hello-threat-intelligence-report"></a><span data-ttu-id="d3b0f-125">Nasıl tooaccess tehdit Intelligence rapor hello?</span><span class="sxs-lookup"><span data-stu-id="d3b0f-125">How tooaccess hello threat intelligence report?</span></span>
<span data-ttu-id="d3b0f-126">Merhaba bakarak mevcut uyarılarınızı gözden geçirebilirsiniz **güvenlik uyarıları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-126">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="d3b0f-127">Hello Azure Portal'ı açın ve her uyarı hakkında daha fazla ayrıntı toosee hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d3b0f-127">Open hello Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="d3b0f-128">Merhaba Güvenlik Merkezi panosunda hello görürsünüz **güvenlik uyarıları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-128">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>
2. <span data-ttu-id="d3b0f-129">Merhaba döşeme tooopen hello tıklatın **güvenlik uyarıları** hello uyarılar hakkında daha fazla ayrıntı içeren ve daha fazla bilgi tooobtain istediğiniz hello güvenlik uyarısı tıklatın dikey hakkında.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-129">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts and click in hello security alert that you want tooobtain more information about.</span></span>

    ![Güvenlik uyarıları](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. <span data-ttu-id="d3b0f-131">Bu durumda hello **yürütülen şüpheli işlem** dikey penceresinde hello hello aşağıdaki çizimde gösterildiği gibi hello uyarı ayrıntılarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="d3b0f-131">In this case hello **Suspicious process executed** blade shows hello details about hello alert as shown in hello figure below:</span></span>

    ![Güvenlik uyarısı ayrıntıları](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. <span data-ttu-id="d3b0f-133">Merhaba miktarda bilgi her güvenlik uyarı için kullanılabilir uyarı according toohello türü değişir.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-133">hello amount of information available for each security alert will vary according toohello type of alert.</span></span> <span data-ttu-id="d3b0f-134">Merhaba, **RAPORLARI** alan bir bağlantı toohello tehdit yönetim bilgileri raporu vardır.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-134">In hello **REPORTS** field you have a link toohello threat intelligence report.</span></span> <span data-ttu-id="d3b0f-135">Bağlantıya tıkladığınızda PDF dosyası yeni bir tarayıcı penceresinde açılacaktır.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-135">Click on it and another browser window will appear with PDF file.</span></span>

   ![Storage seçimi](./media/security-center-threat-report/security-center-threat-report-fig3.png)

<span data-ttu-id="d3b0f-137">Buradan PDF için bu raporu ve okuma hello güvenlik hakkında daha fazla sorunu algılandı hello indirin ve sağlanan hello bilgilere göre eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-137">From here you can download hello PDF for this report and read more about hello security issue that was detected and take actions based on hello information provided.</span></span>

## <a name="see-also"></a><span data-ttu-id="d3b0f-138">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-138">See also</span></span>
<span data-ttu-id="d3b0f-139">Bu belgede Azure Güvenlik Merkezi Tehdit Zekası Raporlarının güvenlik uyarısı araştırmaları sırasında nasıl yardımcı olabileceğini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-139">In this document, you learned how Azure Security Center Threat Intelligent Reports can help during an investigation about security alerts.</span></span> <span data-ttu-id="d3b0f-140">Azure Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="d3b0f-140">toolearn more about Azure Security Center, see hello following:</span></span>

* <span data-ttu-id="d3b0f-141">[Azure Güvenlik Merkezi SSS](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d3b0f-141">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="d3b0f-142">Merhaba Hizmeti'ni kullanma hakkında sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-142">Find frequently asked questions about using hello service.</span></span>
* [<span data-ttu-id="d3b0f-143">Olay Yanıtı için Azure Güvenlik Merkezi’nden Yararlanma</span><span class="sxs-lookup"><span data-stu-id="d3b0f-143">Leveraging Azure Security Center for Incident Response</span></span>](security-center-incident-response.md)
* [<span data-ttu-id="d3b0f-144">Azure Güvenlik Merkezi algılama özellikleri</span><span class="sxs-lookup"><span data-stu-id="d3b0f-144">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* <span data-ttu-id="d3b0f-145">[Azure Güvenlik Merkezi planlama ve işlemler kılavuzu](security-center-planning-and-operations-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d3b0f-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="d3b0f-146">Bilgi nasıl tooplan ve hello tasarım konuları tooadopt Azure Güvenlik Merkezi anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-146">Learn how tooplan and understand hello design considerations tooadopt Azure Security Center.</span></span>
* <span data-ttu-id="d3b0f-147">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="d3b0f-147">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span> <span data-ttu-id="d3b0f-148">Bilgi nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-148">Learn how toomanage and respond toosecurity alerts.</span></span>
* [<span data-ttu-id="d3b0f-149">Azure Güvenlik Merkezi'nde Güvenlik Olayını İşleme</span><span class="sxs-lookup"><span data-stu-id="d3b0f-149">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* <span data-ttu-id="d3b0f-150">[Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="d3b0f-150">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="d3b0f-151">Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulun.</span><span class="sxs-lookup"><span data-stu-id="d3b0f-151">Find blog posts about Azure security and compliance.</span></span>
