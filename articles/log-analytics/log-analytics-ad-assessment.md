---
title: "Active Directory ortamınızı Azure günlük analizi ile en iyi duruma getirme | Microsoft Docs"
description: "Düzenli bir aralıkta risk ve sunucu ortamlarınızın durumunu değerlendirmek için Active Directory değerlendirme çözümü kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 97368f0b9e89ffd0cd982b6e8670d5a1f62ad42c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-active-directory-environment-with-the-active-directory-assessment-solution-in-log-analytics"></a><span data-ttu-id="2fc34-103">Active Directory ortamınızı günlük analizi Active Directory değerlendirme çözümde ile en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="2fc34-103">Optimize your Active Directory environment with the Active Directory Assessment solution in Log Analytics</span></span>

![AD değerlendirmesi simgesi](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

<span data-ttu-id="2fc34-105">Düzenli bir aralıkta risk ve sunucu ortamlarınızın durumunu değerlendirmek için Active Directory değerlendirme çözümü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fc34-105">You can use the Active Directory Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="2fc34-106">Bu makalede, yükleme ve olası sorunlar için düzeltme eylemleri yararlanabilmeniz çözüm kullanma yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="2fc34-106">This article helps you install and use the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="2fc34-107">Bu çözüm önerileri dağıtılan sunucu altyapınızı belirli öncelikli listesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="2fc34-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="2fc34-108">Öneriler dört arasında ayrılır hızlı bir şekilde Yardım odak alanlarına riski anlamak ve gerekli adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="2fc34-108">The recommendations are categorized across four focus areas, which help you quickly understand the risk and take action.</span></span>

<span data-ttu-id="2fc34-109">Öneriler bilgi ve müşteri ziyaretleriniz binlerce Microsoft mühendisleri tarafından elde edilen deneyimlerden dayanır.</span><span class="sxs-lookup"><span data-stu-id="2fc34-109">The recommendations are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="2fc34-110">Her bir öneri, bir sorun için neden önemli ve önerilen değişiklikleri uygulamak nasıl hakkında rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="2fc34-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="2fc34-111">Kuruluşunuz için en önemli ve ücretsiz ve sağlam bir risk ortam çalıştıran doğru ilerleme durumunuzu izlemenize odak alanlarına seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fc34-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="2fc34-112">Çözüm ekledik ve bir değerlendirme tamamlanan, Özet sonra odak alanlarına odaklanmak için bilgi gösterilir **AD değerlendirme** Panosu ortamınızdaki altyapısı için.</span><span class="sxs-lookup"><span data-stu-id="2fc34-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **AD Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="2fc34-113">Aşağıdaki bölümlerde bilgileri üzerinde nasıl kullanacağınızı **AD değerlendirme** Pano, burada görüntüleyebilir ve ardından uygulayın önerilen eylemler için Active Directory sunucu altyapınızı.</span><span class="sxs-lookup"><span data-stu-id="2fc34-113">The following sections describe how to use the information on the **AD Assessment** dashboard, where you can view and then take recommended actions for your Active Directory server infrastructure.</span></span>

![SQL değerlendirmesi döşeme görüntüsü](./media/log-analytics-ad-assessment/ad-tile.png)

![SQL değerlendirmesi Pano görüntüsü](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="2fc34-116">Yükleme ve çözüm yapılandırılıyor</span><span class="sxs-lookup"><span data-stu-id="2fc34-116">Installing and configuring the solution</span></span>
<span data-ttu-id="2fc34-117">Yüklemek ve çözümleri yapılandırmak için aşağıdaki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="2fc34-117">Use the following information to install and configure the solutions.</span></span>

* <span data-ttu-id="2fc34-118">Aracıları değerlendirilecek etki alanının üyesi olan etki alanı denetleyicilerinde yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-118">Agents must be installed on domain controllers that are members of the domain to be evaluated.</span></span>
* <span data-ttu-id="2fc34-119">Active Directory değerlendirme çözümü .NET Framework 4'ün desteklenen bir sürümünü gerektirir (4.5.2 veya üstü) bir OMS aracısı olan her bilgisayarda yüklü.</span><span class="sxs-lookup"><span data-stu-id="2fc34-119">The Active Directory Assessment solution requires a supported version of .NET Framework 4 (4.5.2 or above) installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="2fc34-120">OMS çalışma alanından Active Directory değerlendirme çözümü eklemek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) veya açıklanan işlemi kullanarak [Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="2fc34-120">Add the Active Directory Assessment solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>  <span data-ttu-id="2fc34-121">Başka bir yapılandırma işlemi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2fc34-121">There is no further configuration required.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2fc34-122">Çözüm ekledikten sonra aracıları sunucularıyla AdvisorAssessment.exe dosyası eklenir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-122">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="2fc34-123">Yapılandırma verilerini okuma ve işleme için bulutta OMS hizmetine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-123">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="2fc34-124">Mantığı alınan verilere uygulanır ve bulut hizmeti verilerini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="2fc34-124">Logic is applied to the received data and the cloud service records the data.</span></span>
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a><span data-ttu-id="2fc34-125">Active Directory değerlendirme veri toplama ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="2fc34-125">Active Directory Assessment data collection details</span></span>

<span data-ttu-id="2fc34-126">Active Directory değerlendirme etkinleştirdiğiniz aracıları kullanarak aşağıdaki kaynaklardan toplar:</span><span class="sxs-lookup"><span data-stu-id="2fc34-126">Active Directory Assessment collects data from the following sources using the agents that you have enabled:</span></span>

- <span data-ttu-id="2fc34-127">Kayıt defteri toplayıcıları</span><span class="sxs-lookup"><span data-stu-id="2fc34-127">Registry collectors</span></span>
- <span data-ttu-id="2fc34-128">LDAP toplayıcıları</span><span class="sxs-lookup"><span data-stu-id="2fc34-128">LDAP collectors</span></span>
- <span data-ttu-id="2fc34-129">.NET framework</span><span class="sxs-lookup"><span data-stu-id="2fc34-129">.NET Framework</span></span>
- <span data-ttu-id="2fc34-130">Olay günlüğü toplayıcıları</span><span class="sxs-lookup"><span data-stu-id="2fc34-130">Event log collectors</span></span>
- <span data-ttu-id="2fc34-131">Active Directory Hizmeti Arabirimleri (ADSI)</span><span class="sxs-lookup"><span data-stu-id="2fc34-131">Active Directory Service interfaces (ADSI)</span></span>
- <span data-ttu-id="2fc34-132">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fc34-132">Windows PowerShell</span></span>
- <span data-ttu-id="2fc34-133">Dosya veri toplayıcıları</span><span class="sxs-lookup"><span data-stu-id="2fc34-133">File data collectors</span></span>
- <span data-ttu-id="2fc34-134">Windows Yönetim Araçları (WMI)</span><span class="sxs-lookup"><span data-stu-id="2fc34-134">Windows Management Instrumentation (WMI)</span></span>
- <span data-ttu-id="2fc34-135">DCDIAG aracı API'si</span><span class="sxs-lookup"><span data-stu-id="2fc34-135">DCDIAG tool API</span></span>
- <span data-ttu-id="2fc34-136">Dosya Çoğaltma Hizmeti (NTFRS) API'si</span><span class="sxs-lookup"><span data-stu-id="2fc34-136">File Replication Service (NTFRS) API</span></span>
- <span data-ttu-id="2fc34-137">Özel C# kodu</span><span class="sxs-lookup"><span data-stu-id="2fc34-137">Custom C# code</span></span>


<span data-ttu-id="2fc34-138">Aşağıdaki tablo, Operations Manager (SCOM) gerekli olup olmadığını ve nasıl aracılar için veri toplama yöntemleri yapılandırmayı gösterir. genellikle veri bir aracı tarafından toplanır.</span><span class="sxs-lookup"><span data-stu-id="2fc34-138">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="2fc34-139">Platform</span><span class="sxs-lookup"><span data-stu-id="2fc34-139">platform</span></span> | <span data-ttu-id="2fc34-140">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="2fc34-140">Direct Agent</span></span> | <span data-ttu-id="2fc34-141">SCOM Aracısı</span><span class="sxs-lookup"><span data-stu-id="2fc34-141">SCOM agent</span></span> | <span data-ttu-id="2fc34-142">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="2fc34-142">Azure Storage</span></span> | <span data-ttu-id="2fc34-143">SCOM gerekli?</span><span class="sxs-lookup"><span data-stu-id="2fc34-143">SCOM required?</span></span> | <span data-ttu-id="2fc34-144">Yönetim grubu gönderilen SCOM Aracısı verileri</span><span class="sxs-lookup"><span data-stu-id="2fc34-144">SCOM agent data sent via management group</span></span> | <span data-ttu-id="2fc34-145">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="2fc34-145">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="2fc34-146">Windows</span><span class="sxs-lookup"><span data-stu-id="2fc34-146">Windows</span></span> |<span data-ttu-id="2fc34-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2fc34-147">&#8226;</span></span> |<span data-ttu-id="2fc34-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2fc34-148">&#8226;</span></span> |  |  |<span data-ttu-id="2fc34-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="2fc34-149">&#8226;</span></span> |<span data-ttu-id="2fc34-150">7 gün</span><span class="sxs-lookup"><span data-stu-id="2fc34-150">7 days</span></span> |

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="2fc34-151">Önerilerin nasıl önceliklendirilir anlama</span><span class="sxs-lookup"><span data-stu-id="2fc34-151">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="2fc34-152">Yapılan her öneri öneri göreceli önemini tanımlayan bir ağırlıklı değer verilir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-152">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="2fc34-153">Yalnızca 10 en önemli öneriler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-153">Only the 10 most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="2fc34-154">Ağırlıkları nasıl hesaplanır</span><span class="sxs-lookup"><span data-stu-id="2fc34-154">How weights are calculated</span></span>
<span data-ttu-id="2fc34-155">Ağırlık belirlemeyi üç anahtar faktörlerini temel alarak toplam değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2fc34-155">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="2fc34-156">*Olasılık* tanımlanan bir sorunun sorunlara neden olur.</span><span class="sxs-lookup"><span data-stu-id="2fc34-156">The *probability* that an issue identified causes problems.</span></span> <span data-ttu-id="2fc34-157">Daha yüksek olasılık öneri için daha büyük bir genel puan karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-157">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="2fc34-158">*Etkisi* kuruluşunuzdaki bir soruna neden olursa sorun.</span><span class="sxs-lookup"><span data-stu-id="2fc34-158">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="2fc34-159">Daha yüksek bir etkisi öneri için daha büyük bir genel puan karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-159">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="2fc34-160">*Çaba* öneriyi uygulamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-160">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="2fc34-161">Daha yüksek çaba öneri için daha küçük bir genel puan karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-161">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="2fc34-162">Her öneri ağırlıklı her odak alanı için kullanılabilir toplam puanı yüzdesi olarak ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-162">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="2fc34-163">Örneğin, bu öneri uygulama güvenlik ve uyumluluk odak alanında bir öneri %5 puanı varsa, genel güvenlik ve uyumluluk puan tarafından %5 artırır.</span><span class="sxs-lookup"><span data-stu-id="2fc34-163">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation increases your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="2fc34-164">Odak alanları</span><span class="sxs-lookup"><span data-stu-id="2fc34-164">Focus areas</span></span>
<span data-ttu-id="2fc34-165">**Güvenlik ve Uyumluluk** -bu odak alanı olası güvenlik tehditlerini ve ihlallerinden, şirket ilkelerini ve teknik ve yasal uyumluluk gereksinimleri için öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-165">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="2fc34-166">**Kullanılabilirlik ve iş sürekliliği** -bu odaklanılan alan hizmet kullanılabilirliği, altyapı ve iş koruması dayanıklılık için öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-166">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="2fc34-167">**Performans ve ölçeklenebilirlik** -bu odak alanı kuruluşunuzun yardımcı olacak öneriler gösterir BT altyapısı arttıkça, BT ortamınız geçerli performans gereksinimlerini karşıladığından ve altyapı değiştirmeye yanıt verebilmesini olduğundan emin olun gerekir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-167">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="2fc34-168">**Yükseltme, geçiş ve dağıtım** -bu odak alanı, yükseltme, geçirmek ve Active Directory mevcut altyapınızda dağıtmanıza yardımcı olacak öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-168">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy Active Directory to your existing infrastructure.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="2fc34-169">Her odaklanılan alan % 100 puanlı hedefleyin?</span><span class="sxs-lookup"><span data-stu-id="2fc34-169">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="2fc34-170">Olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-170">Not necessarily.</span></span> <span data-ttu-id="2fc34-171">Öneriler bilgi ve müşteri ziyaretleriniz binlerce arasında Microsoft mühendisleri tarafından elde edilen deneyimleri temel alır.</span><span class="sxs-lookup"><span data-stu-id="2fc34-171">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="2fc34-172">Ancak, iki sunucu altyapılar aynıdır ve özel öneriler için daha az veya uygun olabilir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-172">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="2fc34-173">Örneğin, bazı güvenlik önerileri sanal makinelerinizi Internet'e açık değildir, daha az ilgili olabilir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-173">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="2fc34-174">Bazı kullanılabilirlik öneriler düşük öncelik geçici veri toplama ve raporlama sağladığı hizmetler için daha az uygun olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-174">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="2fc34-175">Olgun bir iş için önemli olan sorunları bir başlangıcından daha az önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-175">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="2fc34-176">Hangi odak alanların önceliklerinizden olduğunu belirlemek ve, puanları zamanla nasıl değiştiğini adresindeki Ara isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fc34-176">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="2fc34-177">Her öneri neden önemli olduğu hakkında yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-177">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="2fc34-178">Öneri uygulama verilen BT hizmetlerinizi yapısını ve kuruluşunuzun iş gereksinimlerini sizin için uygun olup olmadığını değerlendirmek için bu yönergeleri kullanmanız.</span><span class="sxs-lookup"><span data-stu-id="2fc34-178">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="2fc34-179">Değerlendirme odak alanı önerileri kullanın</span><span class="sxs-lookup"><span data-stu-id="2fc34-179">Use assessment focus area recommendations</span></span>
<span data-ttu-id="2fc34-180">OMS içinde bir değerlendirme çözümü kullanmadan önce çözümü yüklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-180">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="2fc34-181">Daha fazla bilgi için çözümleri yükleme hakkında bkz [Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="2fc34-181">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="2fc34-182">Yüklendikten sonra OMS genel bakış sayfasında değerlendirme döşeme kullanarak önerileri özetini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fc34-182">After it is installed, you can view the summary of recommendations by using the Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="2fc34-183">Altyapınız ve ardından-ayrıntıya önerileri için özetlenmiş uyumluluk değerlendirmesi görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="2fc34-183">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="2fc34-184">Odak alanı için öneriler görüntülemek ve düzeltici işlemleri için</span><span class="sxs-lookup"><span data-stu-id="2fc34-184">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="2fc34-185">Üzerinde **genel bakış** sayfasında, **değerlendirme** döşeme sunucusu altyapınız için.</span><span class="sxs-lookup"><span data-stu-id="2fc34-185">On the **Overview** page, click the **Assessment** tile for your server infrastructure.</span></span>
2. <span data-ttu-id="2fc34-186">Üzerinde **değerlendirme** sayfasında odak alanı Kanatlar birinde özet bilgilerini inceleyin ve sonra bu odak alanı için öneriler görüntülemek için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2fc34-186">On the **Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="2fc34-187">Odak alanı sayfaları hiçbirinde ortamınız için öncelikli önerilerin görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fc34-187">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="2fc34-188">Önerinin altında tıklatın **etkilenen nesneleri** öneri neden yapılan hakkında ayrıntıları görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="2fc34-188">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="2fc34-189">![Değerlendirmesi önerileri görüntüsü](./media/log-analytics-ad-assessment/ad-focus.png)</span><span class="sxs-lookup"><span data-stu-id="2fc34-189">![image of Assessment recommendations](./media/log-analytics-ad-assessment/ad-focus.png)</span></span>
4. <span data-ttu-id="2fc34-190">Önerilen düzeltici eylemleri gerçekleştirebilirsiniz **önerilen eylemleri**.</span><span class="sxs-lookup"><span data-stu-id="2fc34-190">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="2fc34-191">Öğe ele önerilen eylemleri sonraki değerlendirmeleri kayıtları gerçekleştirilen ve uyumluluk puan artmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="2fc34-191">When the item has been addressed, later assessments records that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="2fc34-192">Düzeltilmiş öğeler görünür olarak **geçirilen nesneleri**.</span><span class="sxs-lookup"><span data-stu-id="2fc34-192">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="2fc34-193">Öneriler yoksay</span><span class="sxs-lookup"><span data-stu-id="2fc34-193">Ignore recommendations</span></span>
<span data-ttu-id="2fc34-194">Yoksay istediğiniz önerileri varsa, OMS önerileri değerlendirme sonuçlarında görünmesini engellemek için kullanacağı bir metin dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fc34-194">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="2fc34-195">Göz ardı eder önerileri tanımlamak için</span><span class="sxs-lookup"><span data-stu-id="2fc34-195">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="2fc34-196">Sunucunuzdan çalışma alanınıza oturum açın ve günlük arama açın.</span><span class="sxs-lookup"><span data-stu-id="2fc34-196">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="2fc34-197">Ortamınızdaki bilgisayarları için başarısız olan liste önerileri için aşağıdaki sorguyu kullanın.</span><span class="sxs-lookup"><span data-stu-id="2fc34-197">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> <span data-ttu-id="2fc34-198">Çalışma alanınız için yükseltildiyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sonra da yukarıdaki sorguda şu şekilde değiştirir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-198">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   <span data-ttu-id="2fc34-199">Günlük arama sorgusu gösteren ekran görüntüsü şöyledir: ![önerileri başarısız oldu](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="2fc34-199">Here's a screen shot showing the Log Search query: ![failed recommendations](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)</span></span>
2. <span data-ttu-id="2fc34-200">Yoksay istediğiniz önerileri seçin.</span><span class="sxs-lookup"><span data-stu-id="2fc34-200">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="2fc34-201">Sonraki yordamda Recommendationıd için değerleri kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="2fc34-201">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="2fc34-202">Oluşturma ve bir IgnoreRecommendations.txt metin dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="2fc34-202">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="2fc34-203">IgnoreRecommendations.txt adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2fc34-203">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="2fc34-204">Her Recommendationıd ayrı bir satırda yoksay ve sonra dosyayı kaydedip kapatın için günlük analizi istediğiniz her bir öneri için yazın veya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="2fc34-204">Paste or type each RecommendationId for each recommendation that you want Log Analytics to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="2fc34-205">Dosya aşağıdaki klasörde önerileri yoksaymak için OMS istediğiniz her bilgisayara yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="2fc34-205">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="2fc34-206">Microsoft Monitoring (doğrudan veya Operations Manager aracılığıyla bağlı) Agent - olan bilgisayarlarda *SystemDrive*: \Program izleme Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="2fc34-206">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="2fc34-207">Operations Manager yönetim sunucusunda - *SystemDrive*: \Program System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="2fc34-207">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="2fc34-208">Öneriler göz ardı edilir doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="2fc34-208">To verify that recommendations are ignored</span></span>
<span data-ttu-id="2fc34-209">Sonraki değerlendirme çalıştığında, varsayılan olarak 7 günde zamanlanmış sonra belirtilen önerileri işaretlenmiş *yoksayıldı* ve değerlendirme Panoda görünmez.</span><span class="sxs-lookup"><span data-stu-id="2fc34-209">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked *Ignored* and will not appear on the assessment dashboard.</span></span>

1. <span data-ttu-id="2fc34-210">Tüm yoksayılan öneriler listelemek için aşağıdaki günlük arama sorgularını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fc34-210">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> <span data-ttu-id="2fc34-211">Çalışma alanınız için yükseltildiyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sonra da yukarıdaki sorguda şu şekilde değiştirir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-211">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. <span data-ttu-id="2fc34-212">Daha sonra yoksayılan önerileri görmek istediğiniz karar verirseniz, tüm IgnoreRecommendations.txt dosyaları silin veya bunları RecommendationIDs kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fc34-212">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="ad-assessment-solutions-faq"></a><span data-ttu-id="2fc34-213">AD değerlendirmesi çözümleri hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="2fc34-213">AD Assessment solutions FAQ</span></span>
<span data-ttu-id="2fc34-214">*Sıklıkla bir değerlendirme çalışıyor mu?*</span><span class="sxs-lookup"><span data-stu-id="2fc34-214">*How often does an assessment run?*</span></span>

* <span data-ttu-id="2fc34-215">Değerlendirme 7 günde bir çalışır.</span><span class="sxs-lookup"><span data-stu-id="2fc34-215">The assessment runs every 7 days.</span></span>

<span data-ttu-id="2fc34-216">*Ne sıklıkta değerlendirme çalıştıran yapılandırmak için yolu var mı?*</span><span class="sxs-lookup"><span data-stu-id="2fc34-216">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="2fc34-217">Şu anda değil.</span><span class="sxs-lookup"><span data-stu-id="2fc34-217">Not at this time.</span></span>

<span data-ttu-id="2fc34-218">*I değerlendirme çözümünü ekledikten sonra başka bir sunucu için belirlediyseniz değerlendirileceğini?*</span><span class="sxs-lookup"><span data-stu-id="2fc34-218">*If another server for is discovered after I’ve added an assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="2fc34-219">Evet, bunu daha sonra gelen her 7 günde değerlendirildiği bulunduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="2fc34-219">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="2fc34-220">*Ne zaman bir sunucu kullanımdan alındığında değerlendirme kaldırılacak?*</span><span class="sxs-lookup"><span data-stu-id="2fc34-220">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="2fc34-221">Bir sunucu için 3 hafta veri göndermez, kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="2fc34-221">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="2fc34-222">*Veri toplama mu işlemin adı nedir?*</span><span class="sxs-lookup"><span data-stu-id="2fc34-222">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="2fc34-223">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="2fc34-223">AdvisorAssessment.exe</span></span>

<span data-ttu-id="2fc34-224">*Ne kadar süreyle verilerinin toplanmasını sürer?*</span><span class="sxs-lookup"><span data-stu-id="2fc34-224">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="2fc34-225">Gerçek veri toplama sunucusundaki yaklaşık 1 saat sürer.</span><span class="sxs-lookup"><span data-stu-id="2fc34-225">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="2fc34-226">Bu çok sayıda Active Directory sunucularını sahip sunucularda uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-226">It may take longer on servers that have a large number of Active Directory servers.</span></span>

<span data-ttu-id="2fc34-227">*Verileri toplandığında yapılandırmak için yolu var mı?*</span><span class="sxs-lookup"><span data-stu-id="2fc34-227">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="2fc34-228">Şu anda değil.</span><span class="sxs-lookup"><span data-stu-id="2fc34-228">Not at this time.</span></span>

<span data-ttu-id="2fc34-229">*Neden yalnızca ilk 10 önerileri görüntülemek?*</span><span class="sxs-lookup"><span data-stu-id="2fc34-229">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="2fc34-230">Görevler kapsamlı bir zorlamayı listesi vermek yerine, Önceliklendirilmiş önerileri adresleme odaklanmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="2fc34-230">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="2fc34-231">Bunları çözün sonra ek öneriler kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="2fc34-231">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="2fc34-232">Ayrıntılı listesini görmek isterseniz, tüm önerileri günlük arama özelliğini kullanarak görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2fc34-232">If you prefer to see the detailed list, you can view all recommendations using Log Search.</span></span>

<span data-ttu-id="2fc34-233">*Bir öneri yoksaymak için yolu var mı?*</span><span class="sxs-lookup"><span data-stu-id="2fc34-233">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="2fc34-234">Evet, bkz: [önerileri yoksay](#ignore-recommendations) yukarıdaki bölümde.</span><span class="sxs-lookup"><span data-stu-id="2fc34-234">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fc34-235">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2fc34-235">Next steps</span></span>
* <span data-ttu-id="2fc34-236">Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) ayrıntılı AD Değerlendirme verileri ve öneriler görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="2fc34-236">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed AD Assessment data and recommendations.</span></span>
