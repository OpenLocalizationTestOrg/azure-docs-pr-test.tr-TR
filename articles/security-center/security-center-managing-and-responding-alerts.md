---
title: "Azure Güvenlik Merkezi'nde güvenlik uyarılarını aaaManage | Microsoft Docs"
description: "Bu belge, toouse Azure Güvenlik Merkezi özellikleri toomanage yardımcı olur ve toosecurity uyarıları yanıt."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a><span data-ttu-id="c7814-103">Yönetme ve Azure Güvenlik Merkezi'nde toosecurity uyarılarını yanıt</span><span class="sxs-lookup"><span data-stu-id="c7814-103">Managing and responding toosecurity alerts in Azure Security Center</span></span>
<span data-ttu-id="c7814-104">Bu belge, Azure Güvenlik Merkezi toomanage kullanın ve toosecurity uyarıları yanıtlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c7814-104">This document helps you use Azure Security Center toomanage and respond toosecurity alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="c7814-105">Gelişmiş tooenable algılama, yükseltme tooAzure Güvenlik Merkezi standart.</span><span class="sxs-lookup"><span data-stu-id="c7814-105">tooenable advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="c7814-106">60 günlük ücretsiz deneme sürümü mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="c7814-106">A free 60-day trial is available.</span></span> <span data-ttu-id="c7814-107">tooupgrade, hello select fiyatlandırma katmanı [Güvenlik İlkesi](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c7814-107">tooupgrade, select Pricing Tier in hello [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="c7814-108">Bkz: [Azure Güvenlik Merkezi fiyatlandırma](security-center-pricing.md) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="c7814-108">See [Azure Security Center pricing](security-center-pricing.md) toolearn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="c7814-109">Güvenlik uyarıları nedir?</span><span class="sxs-lookup"><span data-stu-id="c7814-109">What are security alerts?</span></span>
<span data-ttu-id="c7814-110">Güvenlik Merkezi otomatik olarak toplar, çözümler, Azure kaynaklarınızı, hello ağ günlük verilerini tümleşir ve güvenlik duvarı ve endpoint protection çözümleri toodetect gerçek tehditleri gibi iş ortağı çözümlerinden bağlı ve hatalı pozitif sonuçları azaltmak.</span><span class="sxs-lookup"><span data-stu-id="c7814-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="c7814-111">Öncelikli güvenlik uyarıları listesi hello birlikte Güvenlik Merkezi'nde gösterilen tooquickly gereksinim duyduğunuz bilgileri araştırın hello sorun ve nasıl için öneriler tooremediate saldırının.</span><span class="sxs-lookup"><span data-stu-id="c7814-111">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem and recommendations for how tooremediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="c7814-112">Güvenlik Merkezi algılama özelliklerinin nasıl çalıştığı hakkında daha fazla bilgi için [Azure Güvenlik Merkezi Algılama Özellikleri](security-center-detection-capabilities.md) konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="c7814-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="c7814-113">Güvenlik ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="c7814-113">Managing security alerts</span></span>
<span data-ttu-id="c7814-114">Merhaba bakarak mevcut uyarılarınızı gözden geçirebilirsiniz **güvenlik uyarıları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="c7814-114">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="c7814-115">Azure Portalı'nı açın ve her uyarı hakkında daha fazla ayrıntı toosee hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c7814-115">Open Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="c7814-116">Merhaba Güvenlik Merkezi panosunda hello görürsünüz **güvenlik uyarıları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="c7814-116">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Güvenlik Merkezi'nde güvenlik uyarıları kutucuğu](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="c7814-118">Merhaba döşeme tooopen hello tıklatın **güvenlik uyarıları** hello hakkında daha fazla ayrıntı içeren dikey penceresi aşağıda gösterildiği gibi uyarır.</span><span class="sxs-lookup"><span data-stu-id="c7814-118">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts as shown below.</span></span>

   ![Güvenlik Merkezi'nde Hello güvenlik uyarıları dikey penceresi](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="c7814-120">Merhaba alt kısmında bu dikey hello ayrıntıları her uyarı için ' dir.</span><span class="sxs-lookup"><span data-stu-id="c7814-120">In hello bottom part of this blade are hello details for each alert.</span></span> <span data-ttu-id="c7814-121">toosort, toosort tarafından istediğiniz hello sütunu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c7814-121">toosort, click hello column that you want toosort by.</span></span> <span data-ttu-id="c7814-122">Her sütunun Hello tanımı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c7814-122">hello definition for each column is given below:</span></span>

* <span data-ttu-id="c7814-123">**Açıklama**: hello uyarının kısa bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="c7814-123">**Description**: A brief explanation of hello alert.</span></span>
* <span data-ttu-id="c7814-124">**Sayı**: Belirtilmiş türün belirli bir günde algılanan tüm uyarılarının listesi.</span><span class="sxs-lookup"><span data-stu-id="c7814-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="c7814-125">**Tarafından algılanan**: Merhaba hello uyarıyı tetiklemekten sorumlu hizmet.</span><span class="sxs-lookup"><span data-stu-id="c7814-125">**Detected by**: hello service that was responsible for triggering hello alert.</span></span>
* <span data-ttu-id="c7814-126">**Tarih**: hello tarih hello olay oluştu.</span><span class="sxs-lookup"><span data-stu-id="c7814-126">**Date**: hello date that hello event occurred.</span></span>
* <span data-ttu-id="c7814-127">**Durum**: Merhaba bu uyarı için geçerli durumu.</span><span class="sxs-lookup"><span data-stu-id="c7814-127">**State**: hello current state for that alert.</span></span> <span data-ttu-id="c7814-128">İki tür durum mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="c7814-128">There are two types of states:</span></span>
  * <span data-ttu-id="c7814-129">**Etkin**: hello güvenlik uyarısı algılandı.</span><span class="sxs-lookup"><span data-stu-id="c7814-129">**Active**: hello security alert has been detected.</span></span>
* <span data-ttu-id="c7814-130">**Önem derecesi**: hello önem düzeyi yüksek, Orta veya düşük olabilir.</span><span class="sxs-lookup"><span data-stu-id="c7814-130">**Severity**: hello severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="c7814-131">Uyarıları filtreleme</span><span class="sxs-lookup"><span data-stu-id="c7814-131">Filtering alerts</span></span>
<span data-ttu-id="c7814-132">Tarihe, duruma ve önem derecesine göre uyarıları filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7814-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="c7814-133">Uyarıları filtreleme toonarrow hello güvenlik uyarıları gösterimi kapsamını ihtiyaç duyacağınız senaryoları için faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c7814-133">Filtering alerts can be useful for scenarios where you need toonarrow hello scope of security alerts show.</span></span> <span data-ttu-id="c7814-134">Örneğin, yapabileceğiniz hello sistemde olası bir ihlali Araştırdığınız için son 24 saat hello oluşan tooaddress güvenlik uyarıları istiyor.</span><span class="sxs-lookup"><span data-stu-id="c7814-134">For example, you might you want tooaddress security alerts that occurred in hello last 24 hours because you are investigating a potential breach in hello system.</span></span>

1. <span data-ttu-id="c7814-135">Tıklatın **filtre** hello üzerinde **güvenlik uyarıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="c7814-135">Click **Filter** on hello **Security Alerts** blade.</span></span> <span data-ttu-id="c7814-136">Merhaba **filtre** dikey penceresi açılır ve toosee istediğiniz hello tarih, durum ve önem derecesi değerlerini seçin.</span><span class="sxs-lookup"><span data-stu-id="c7814-136">hello **Filter** blade opens and you select hello date, state, and severity values you wish toosee.</span></span>

    ![Güvenlik Merkezi'nde uyarıları filtreleme](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a><span data-ttu-id="c7814-138">Yanıt toosecurity uyarıları</span><span class="sxs-lookup"><span data-stu-id="c7814-138">Respond toosecurity alerts</span></span>
<span data-ttu-id="c7814-139">Bir güvenlik uyarısı toolearn seçin, adımlar varsa tetikleyen hello uyarı ve hangi hello olaylar hakkında daha fazla tootake tooremediate saldırının gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="c7814-139">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="c7814-140">Güvenlik uyarıları, türe ve tarihe göre gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="c7814-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="c7814-141">Güvenlik uyarısına tıklandığında gruplanan hello uyarıları listesini içeren dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="c7814-141">Clicking a security alert will open a blade containing a list of hello grouped alerts.</span></span>

![Azure Güvenlik Merkezi'nde toosecurity uyarılarını yanıtlama](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="c7814-143">Bu durumda, tetiklenen hello uyarıları toosuspicious Uzak Masaüstü Protokolü (RDP) etkinliğine bakın.</span><span class="sxs-lookup"><span data-stu-id="c7814-143">In this case, hello alerts that were triggered refer toosuspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="c7814-144">Merhaba ilk sütun hangi kaynakların saldırıya gösterir; Merhaba, ikinci hello kaynak Saldırıya uğrayan kaç kez gösterir; Merhaba üçüncü hello zaman hello saldırı gösterir; Merhaba dördüncü hello uyarının durumunu gösterir; ve hello beşinci hello saldırı hello önemini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c7814-144">hello first column shows which resources were attacked; hello second shows how many times hello resource was attacked; hello third shows hello time of hello attack; hello fourth shows state of hello alert; and hello fifth shows hello severity of hello attack.</span></span> <span data-ttu-id="c7814-145">Bu bilgileri gözden geçirdikten sonra Saldırıya uğrayan hello kaynağa tıklayın ve yeni bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="c7814-145">After reviewing this information, click hello resource that was attacked and a new blade will open.</span></span>

![Azure Güvenlik Merkezi'nde güvenlik hakkında ne toodo uyarılar için öneriler](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="c7814-147">Merhaba, **açıklama** bu dikey pencerenin alanında bu olay hakkında daha fazla ayrıntı bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7814-147">In hello **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="c7814-148">Geçerli hello kaynak IP adresi ve öneriler konusunda bu ek ayrıntılar hangi tetiklenen hello Güvenlik Uyarısı, hello hedef kaynak, bir anlayış teklif tooremediate.</span><span class="sxs-lookup"><span data-stu-id="c7814-148">These additional details offer insight into what triggered hello security alert, hello target resource, when applicable hello source IP address, and recommendations about how tooremediate.</span></span>  <span data-ttu-id="c7814-149">Bazı durumlarda, hello kaynak IP adresi boştur (yoktur) tüm Windows güvenlik olayı günlüklerinin hello IP adresi içermediğinden.</span><span class="sxs-lookup"><span data-stu-id="c7814-149">In some instances, hello source IP address will be empty (not available) because not all Windows security events logs include hello IP address.</span></span>

<span data-ttu-id="c7814-150">Güvenlik Merkezi tarafından önerilen hello düzeltme according toohello güvenlik uyarısı değişir.</span><span class="sxs-lookup"><span data-stu-id="c7814-150">hello remediation suggested by Security Center will vary according toohello security alert.</span></span> <span data-ttu-id="c7814-151">Bazı durumlarda, diğer Azure işlevlerini tooimplement toouse olabilir hello düzeltme önerilir.</span><span class="sxs-lookup"><span data-stu-id="c7814-151">In some cases, you may have toouse other Azure capabilities tooimplement hello recommended remediation.</span></span> <span data-ttu-id="c7814-152">Örneğin, Bu saldırının kullanarak bu saldırıyı oluşturma tooblacklist başlangıç IP adresi için düzeltme hello bir [ağ ACL'si](../virtual-network/virtual-networks-acl.md) veya [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) kuralı.</span><span class="sxs-lookup"><span data-stu-id="c7814-152">For example, hello remediation for this attack is tooblacklist hello IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="c7814-153">Merhaba farklı türde bir uyarı hakkında daha fazla bilgi için okuma [göre türü Azure Güvenlik Merkezi'nde güvenlik uyarılarını](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="c7814-153">For more information on hello different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="c7814-154">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c7814-154">See also</span></span>
<span data-ttu-id="c7814-155">Bu belgede, nasıl öğrenilen Güvenlik Merkezi'nde güvenlik ilkelerini tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c7814-155">In this document, you learned how tooconfigure security policies in Security Center.</span></span> <span data-ttu-id="c7814-156">Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="c7814-156">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="c7814-157">Azure Güvenlik Merkezi'nde Güvenlik Olayını İşleme</span><span class="sxs-lookup"><span data-stu-id="c7814-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="c7814-158">Azure Güvenlik Merkezi Algılama Özellikleri</span><span class="sxs-lookup"><span data-stu-id="c7814-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="c7814-159">Azure Güvenlik Merkezi Planlama ve İşlemler Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="c7814-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="c7814-160">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7814-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c7814-161">[Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7814-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
