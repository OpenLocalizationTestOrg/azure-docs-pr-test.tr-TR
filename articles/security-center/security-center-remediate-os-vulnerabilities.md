---
title: "Azure Güvenlik Merkezi güvenlik açıkları OS düzeltme | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi öneriyi uygulamayı gösterilmiştir ** düzeltmek OS güvenlik açıkları **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="99358-103">İşletim sistemi güvenlik açıkları Azure Güvenlik Merkezi'nde Düzelt</span><span class="sxs-lookup"><span data-stu-id="99358-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="99358-104">Azure Güvenlik Merkezi günlük VM saldırı karşısında daha savunmasız hale getirebilecek ve bu güvenlik açıklarına değinen yapılandırma değişiklikleri önerir yapılandırmalar için sanal makine (VM) işletim sistemi (OS) çözümler.</span><span class="sxs-lookup"><span data-stu-id="99358-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span></span> <span data-ttu-id="99358-105">Güvenlik Merkezi, VM işletim sistemi yapılandırması önerilen yapılandırma kuralları eşleşmediğinde güvenlik açıkları gidermek önerir.</span><span class="sxs-lookup"><span data-stu-id="99358-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="99358-106">İzlenmekte olan belirli yapılandırmalar hakkında daha fazla bilgi için bkz: [önerilen yapılandırma kuralları listesi](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="99358-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="99358-107">Öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="99358-107">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="99358-108">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="99358-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="99358-109">Bu belge hakkında adım adım kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="99358-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="99358-110">İçinde **önerileri** dikey penceresinde, select **düzeltmek OS güvenlik açıkları**.</span><span class="sxs-lookup"><span data-stu-id="99358-110">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="99358-111">![İşletim sistemi güvenlik açıklarını düzeltin][1]</span><span class="sxs-lookup"><span data-stu-id="99358-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="99358-112">**Düzeltmek OS güvenlik açıkları** dikey penceresi açılır ve Vm'lerinizi önerilen yapılandırma kuralları eşleşmeyen işletim sistemi yapılandırmalarını ile listeler.</span><span class="sxs-lookup"><span data-stu-id="99358-112">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span></span>  <span data-ttu-id="99358-113">Her bir VM dikey tanımlar:</span><span class="sxs-lookup"><span data-stu-id="99358-113">For each VM, the blade identifies:</span></span>

   * <span data-ttu-id="99358-114">**BAŞARISIZ kuralları** --VM işletim sistemi yapılandırmasını başarısız kuralları sayısı.</span><span class="sxs-lookup"><span data-stu-id="99358-114">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span></span>
   * <span data-ttu-id="99358-115">**En son tarama zamanı** --Güvenlik Merkezi VM işletim sistemi yapılandırmasını son tarama saati ve tarihi.</span><span class="sxs-lookup"><span data-stu-id="99358-115">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span></span>
   * <span data-ttu-id="99358-116">**Durum** --güvenlik açığı geçerli durumu:</span><span class="sxs-lookup"><span data-stu-id="99358-116">**STATE** -- The current state of the vulnerability:</span></span>

     * <span data-ttu-id="99358-117">Açık: Güvenlik açığı henüz ele alınmadı</span><span class="sxs-lookup"><span data-stu-id="99358-117">Open: The vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="99358-118">Devam ediyor: Güvenlik açığı uygulanmakta olan, sizin tarafınızdan herhangi bir eylem gerekli</span><span class="sxs-lookup"><span data-stu-id="99358-118">In Progress: The vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="99358-119">Çözüm: Bu güvenlik açığı zaten giderilmiş (sorun çözüldükten sonra girdi gri renkte görüntülenir)</span><span class="sxs-lookup"><span data-stu-id="99358-119">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span></span>
   * <span data-ttu-id="99358-120">**Önem DERECESİ** --tüm güvenlik açıkları bir güvenlik açığının ele alınması gerekiyor ancak hemen ilgilenilmesi gerekmiyor anlamı bir düşük önem derecesi için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="99358-120">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="99358-121">Bir VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="99358-121">Select a VM.</span></span> <span data-ttu-id="99358-122">Bu VM için bir dikey pencere açar ve başarısız olan kuralları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="99358-122">A blade for that VM opens and displays the rules that have failed.</span></span>
   <span data-ttu-id="99358-123">![Başarısız olan yapılandırma kuralları][2]</span><span class="sxs-lookup"><span data-stu-id="99358-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="99358-124">Bir kural seçin.</span><span class="sxs-lookup"><span data-stu-id="99358-124">Select a rule.</span></span> <span data-ttu-id="99358-125">Bu örnekte seçin **parola, karmaşıklık gereksinimlerini karşılamalıdır**.</span><span class="sxs-lookup"><span data-stu-id="99358-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="99358-126">Başarısız kuralı ve etkisi açıklayan bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="99358-126">A blade opens describing the failed rule and the impact.</span></span> <span data-ttu-id="99358-127">Ayrıntıları gözden geçirin ve işletim sistemi yapılandırmalarının nasıl uygulanacağını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="99358-127">Review the details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="99358-128">![Başarısız kuralı için açıklama][3]</span><span class="sxs-lookup"><span data-stu-id="99358-128">![Description for the failed rule][3]</span></span>

  <span data-ttu-id="99358-129">Güvenlik Merkezi, yapılandırma kuralları için benzersiz tanımlayıcı atamak için Common Configuration Enumeration (CCE) kullanır.</span><span class="sxs-lookup"><span data-stu-id="99358-129">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="99358-130">Aşağıdaki bilgiler bu dikey pencerede sağlanır:</span><span class="sxs-lookup"><span data-stu-id="99358-130">The following information is provided on this blade:</span></span>

  - <span data-ttu-id="99358-131">ADI--Kural adı</span><span class="sxs-lookup"><span data-stu-id="99358-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="99358-132">Önem DERECESİ--Kritik, önemli ya da uyarı CCE önem derecesi değeri</span><span class="sxs-lookup"><span data-stu-id="99358-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="99358-133">CCIED--CCE kuralı için benzersiz bir tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="99358-133">CCIED -- CCE unique identifier for the rule</span></span>
  - <span data-ttu-id="99358-134">AÇIKLAMASI--Kural açıklaması</span><span class="sxs-lookup"><span data-stu-id="99358-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="99358-135">Güvenlik AÇIĞI - Açıklama güvenlik açığı veya kural uygulanmamış durumunda riski</span><span class="sxs-lookup"><span data-stu-id="99358-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="99358-136">ETKİSİ--kuralı uygulandığında iş etkisi</span><span class="sxs-lookup"><span data-stu-id="99358-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="99358-137">BEKLENEN değer--Güvenlik Merkezi kural karşı VM OS yapılandırmanızı inceler, beklenen değer</span><span class="sxs-lookup"><span data-stu-id="99358-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="99358-138">Kural işlemi--VM OS yapılandırmanızın kural karşı Çözümleme sırasında Güvenlik Merkezi tarafından kullanılan kuralı işlemi</span><span class="sxs-lookup"><span data-stu-id="99358-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="99358-139">Gerçek değer--VM OS yapılandırmanızı kural karşı analizini sonra değer döndürdü.</span><span class="sxs-lookup"><span data-stu-id="99358-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="99358-140">Değerlendirme sonucu –-analiz sonucu: geçirmek, başarısız</span><span class="sxs-lookup"><span data-stu-id="99358-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="99358-141">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="99358-141">See also</span></span>
<span data-ttu-id="99358-142">Bu makalede "Düzelt işletim sistemi güvenlik açıkları." Güvenlik Merkezi öneriyi uygulamayı nasıl oluşturulacağını gösterir</span><span class="sxs-lookup"><span data-stu-id="99358-142">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="99358-143">Yapılandırma kuralları gözden geçirebilirsiniz [burada](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="99358-143">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="99358-144">Güvenlik Merkezi, yapılandırma kuralları için benzersiz tanımlayıcı atamak için CCE (ortak yapılandırma sıralaması) kullanır.</span><span class="sxs-lookup"><span data-stu-id="99358-144">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="99358-145">Ziyaret [CCE](https://nvd.nist.gov/cce/index.cfm) daha fazla bilgi için site.</span><span class="sxs-lookup"><span data-stu-id="99358-145">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="99358-146">Güvenlik Merkezi hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="99358-146">To learn more about Security Center, see the following resources:</span></span>

* <span data-ttu-id="99358-147">[Azure Güvenlik Merkezi'nde desteklenen platformlar](security-center-os-coverage.md) -desteklenen Windows ve Linux VM'ler listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="99358-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="99358-148">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="99358-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="99358-149">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) -önerilerin Azure kaynaklarınızı korumanıza nasıl yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="99358-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="99358-150">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) -Azure kaynaklarınızın sistem durumunu izlemek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="99358-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="99358-151">[Yönetme ve Azure Güvenlik Merkezi'nde güvenlik uyarılarını yanıtlama](security-center-managing-and-responding-alerts.md) -yönetme ve güvenlik uyarılarını yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="99358-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="99358-152">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) -iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="99358-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="99358-153">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99358-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="99358-154">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) -Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99358-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
