---
title: "Azure Güvenlik Merkezi'nde aaaRemediate işletim sistemi güvenlik açıkları | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi öneri gösterir. ** düzeltmek OS güvenlik açıkları **."
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
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="2a5c2-103">İşletim sistemi güvenlik açıkları Azure Güvenlik Merkezi'nde Düzelt</span><span class="sxs-lookup"><span data-stu-id="2a5c2-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="2a5c2-104">Azure Güvenlik Merkezi çözümler günlük, sanal makine (VM) işletim sistemi (OS) yapabilir yapılandırmaları VM hello için daha savunmasız tooattack ve önerir yapılandırmasını açıklarından tooaddress değiştirir.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make hello VM more vulnerable tooattack and recommends configuration changes tooaddress these vulnerabilities.</span></span> <span data-ttu-id="2a5c2-105">Güvenlik Merkezi, VM işletim sistemi yapılandırması yapılandırma kuralları önerilen hello eşleşmediğinde güvenlik açıkları gidermek önerir.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match hello recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="2a5c2-106">İzlenmekte olan hello belirli yapılandırmalar hakkında daha fazla bilgi için bkz: Merhaba [önerilen yapılandırma kuralları listesi](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="2a5c2-106">For more information on hello specific configurations being monitored, see hello [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="2a5c2-107">Merhaba öneriyi uygulamayı</span><span class="sxs-lookup"><span data-stu-id="2a5c2-107">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="2a5c2-108">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="2a5c2-109">Bu belge hakkında adım adım kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="2a5c2-110">Merhaba, **önerileri** dikey penceresinde, select **düzeltmek OS güvenlik açıkları**.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-110">In hello **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="2a5c2-111">![İşletim sistemi güvenlik açıklarını düzeltin][1]</span><span class="sxs-lookup"><span data-stu-id="2a5c2-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="2a5c2-112">Merhaba **düzeltmek OS güvenlik açıkları** dikey penceresi açılır ve yapılandırma kuralları önerilen hello eşleşmeyen işletim sistemi yapılandırmalarını ile sanal makineleri listeler.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-112">hello **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match hello recommended configuration rules.</span></span>  <span data-ttu-id="2a5c2-113">Her bir VM hello dikey tanımlar:</span><span class="sxs-lookup"><span data-stu-id="2a5c2-113">For each VM, hello blade identifies:</span></span>

   * <span data-ttu-id="2a5c2-114">**BAŞARISIZ kuralları** --hello VM işletim sistemi yapılandırmasını hello kuralların sayısını başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-114">**FAILED RULES** -- hello number of rules that hello VM's OS configuration failed.</span></span>
   * <span data-ttu-id="2a5c2-115">**En son tarama zamanı** --hello tarih ve Güvenlik Merkezi hello VM'ın işletim sistemi yapılandırması son tarama zamanı.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-115">**LAST SCAN TIME** -- hello date and time that Security Center last scanned hello VM’s OS configuration.</span></span>
   * <span data-ttu-id="2a5c2-116">**Durum** --hello hello güvenlik açığı geçerli durumu:</span><span class="sxs-lookup"><span data-stu-id="2a5c2-116">**STATE** -- hello current state of hello vulnerability:</span></span>

     * <span data-ttu-id="2a5c2-117">Açık: hello güvenlik açığı henüz ele alınmadı</span><span class="sxs-lookup"><span data-stu-id="2a5c2-117">Open: hello vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="2a5c2-118">Devam ediyor: hello güvenlik açığı uygulanmakta olan, sizin tarafınızdan herhangi bir eylem gerekli</span><span class="sxs-lookup"><span data-stu-id="2a5c2-118">In Progress: hello vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="2a5c2-119">Çözümlendi: hello güvenlik açığı zaten giderilmiş (Merhaba sorun çözüldükten sonra hello girdi gri renkte görüntülenir)</span><span class="sxs-lookup"><span data-stu-id="2a5c2-119">Resolved: hello vulnerability was already addressed (when hello issue has been resolved, hello entry is grayed out)</span></span>
   * <span data-ttu-id="2a5c2-120">**Önem DERECESİ** --tüm güvenlik açıkları bir güvenlik açığının ele alınması gerekiyor ancak hemen ilgilenilmesi gerekmiyor anlamına düşük tooa önemini ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-120">**SEVERITY** -- All vulnerabilities are set tooa severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="2a5c2-121">Bir VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-121">Select a VM.</span></span> <span data-ttu-id="2a5c2-122">Bir dikey pencere söz konusu VM açar ve başarısız olan hello kurallarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-122">A blade for that VM opens and displays hello rules that have failed.</span></span>
   <span data-ttu-id="2a5c2-123">![Başarısız olan yapılandırma kuralları][2]</span><span class="sxs-lookup"><span data-stu-id="2a5c2-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="2a5c2-124">Bir kural seçin.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-124">Select a rule.</span></span> <span data-ttu-id="2a5c2-125">Bu örnekte seçin **parola, karmaşıklık gereksinimlerini karşılamalıdır**.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="2a5c2-126">Açıklayan başarısız hello kuralı ve hello etkisi bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-126">A blade opens describing hello failed rule and hello impact.</span></span> <span data-ttu-id="2a5c2-127">Merhaba ayrıntılarını gözden geçirin ve işletim sistemi yapılandırmalarının nasıl uygulanacağını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-127">Review hello details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="2a5c2-128">![Merhaba başarısız kuralı için açıklama][3]</span><span class="sxs-lookup"><span data-stu-id="2a5c2-128">![Description for hello failed rule][3]</span></span>

  <span data-ttu-id="2a5c2-129">Güvenlik Merkezi Common Configuration Enumeration (CCE) tooassign benzersiz tanımlayıcıları için yapılandırma kuralları kullanır.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-129">Security Center uses Common Configuration Enumeration (CCE) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="2a5c2-130">Aşağıdaki bilgilerle hello bu dikey pencerede sağlanır:</span><span class="sxs-lookup"><span data-stu-id="2a5c2-130">hello following information is provided on this blade:</span></span>

  - <span data-ttu-id="2a5c2-131">ADI--Kural adı</span><span class="sxs-lookup"><span data-stu-id="2a5c2-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="2a5c2-132">Önem DERECESİ--Kritik, önemli ya da uyarı CCE önem derecesi değeri</span><span class="sxs-lookup"><span data-stu-id="2a5c2-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="2a5c2-133">CCIED--CCE hello kuralı için benzersiz bir tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="2a5c2-133">CCIED -- CCE unique identifier for hello rule</span></span>
  - <span data-ttu-id="2a5c2-134">AÇIKLAMASI--Kural açıklaması</span><span class="sxs-lookup"><span data-stu-id="2a5c2-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="2a5c2-135">Güvenlik AÇIĞI - Açıklama güvenlik açığı veya kural uygulanmamış durumunda riski</span><span class="sxs-lookup"><span data-stu-id="2a5c2-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="2a5c2-136">ETKİSİ--kuralı uygulandığında iş etkisi</span><span class="sxs-lookup"><span data-stu-id="2a5c2-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="2a5c2-137">BEKLENEN değer--Güvenlik Merkezi hello kural karşı VM OS yapılandırmanızı inceler, beklenen değer</span><span class="sxs-lookup"><span data-stu-id="2a5c2-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="2a5c2-138">Kural işlemi--VM OS yapılandırmanızın hello kural karşı Çözümleme sırasında Güvenlik Merkezi tarafından kullanılan kuralı işlemi</span><span class="sxs-lookup"><span data-stu-id="2a5c2-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="2a5c2-139">Gerçek değer--VM OS yapılandırmanızı hello kural karşı analizini sonra değer döndürdü.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="2a5c2-140">Değerlendirme sonucu –-analiz sonucu: geçirmek, başarısız</span><span class="sxs-lookup"><span data-stu-id="2a5c2-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="2a5c2-141">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-141">See also</span></span>
<span data-ttu-id="2a5c2-142">Bu makalede, nasıl tooimplement hello Güvenlik Merkezi öneri "Düzelt işletim sistemi güvenlik açıkları." gösterdi.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-142">This article showed you how tooimplement hello Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="2a5c2-143">Yapılandırma kuralları hello kümesi gözden geçirebilirsiniz [burada](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="2a5c2-143">You can review hello set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="2a5c2-144">Güvenlik Merkezi CCE (ortak yapılandırma sıralaması) tooassign benzersiz tanımlayıcıları için yapılandırma kuralları kullanır.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-144">Security Center uses CCE (Common Configuration Enumeration) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="2a5c2-145">Merhaba ziyaret [CCE](https://nvd.nist.gov/cce/index.cfm) daha fazla bilgi için site.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-145">Visit hello [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="2a5c2-146">Güvenlik Merkezi hakkında daha fazla toolearn kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="2a5c2-146">toolearn more about Security Center, see hello following resources:</span></span>

* <span data-ttu-id="2a5c2-147">[Azure Güvenlik Merkezi'nde desteklenen platformlar](security-center-os-coverage.md) -desteklenen Windows ve Linux VM'ler listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="2a5c2-148">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="2a5c2-149">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) -önerilerin Azure kaynaklarınızı korumanıza nasıl yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="2a5c2-150">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) -nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="2a5c2-151">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) -öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-151">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="2a5c2-152">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) -nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="2a5c2-153">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="2a5c2-154">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) -Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5c2-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
