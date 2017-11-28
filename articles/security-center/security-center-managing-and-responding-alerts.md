---
title: "Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme | Microsoft Docs"
description: "Bu belge, güvenlik uyarılarını yönetmek ve yanıtlamak için Azure Güvenlik Merkezi işlevlerini kullanmanıza yardımcı olur."
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
ms.openlocfilehash: 56fcfbfdbe15749132ba6a27861142fd564063c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-and-responding-to-security-alerts-in-azure-security-center"></a><span data-ttu-id="f9c7d-103">Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama</span><span class="sxs-lookup"><span data-stu-id="f9c7d-103">Managing and responding to security alerts in Azure Security Center</span></span>
<span data-ttu-id="f9c7d-104">Bu belge, güvenlik uyarılarını yönetmeniz ve yanıtlamanız için Azure Güvenlik Merkezi’ni kullanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-104">This document helps you use Azure Security Center to manage and respond to security alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c7d-105">Gelişmiş algılamaları etkinleştirmek için Azure Güvenlik Merkezi Standart sürümüne yükseltme yapın.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-105">To enable advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="f9c7d-106">60 günlük ücretsiz deneme sürümü mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-106">A free 60-day trial is available.</span></span> <span data-ttu-id="f9c7d-107">Yükseltmek için [Güvenlik İlkesi](security-center-policies.md)’nde Fiyatlandırma Katmanı’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-107">To upgrade, select Pricing Tier in the [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="f9c7d-108">Daha fazla bilgi için bkz. [Azure Güvenlik Merkezi fiyatlandırması](security-center-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="f9c7d-108">See [Azure Security Center pricing](security-center-pricing.md) to learn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="f9c7d-109">Güvenlik uyarıları nedir?</span><span class="sxs-lookup"><span data-stu-id="f9c7d-109">What are security alerts?</span></span>
<span data-ttu-id="f9c7d-110">Güvenlik Merkezi, gerçek tehditleri algılamak ve hatalı pozitif sonuçları azaltmak için Azure kaynaklarınızdan, ağınızdan ve güvenlik duvarı ve uç nokta koruma çözümleri gibi bağlı iş ortağı çözümlerinden günlük verilerini otomatik olarak toplar, çözümler ve tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives.</span></span> <span data-ttu-id="f9c7d-111">Öncelikli güvenlik uyarıları listesi, sorunu hızlıca araştırmanız gereken bilgiler ve saldırıyı düzeltme hakkındaki önerilerle birlikte Güvenlik Merkezi'nde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-111">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="f9c7d-112">Güvenlik Merkezi algılama özelliklerinin nasıl çalıştığı hakkında daha fazla bilgi için [Azure Güvenlik Merkezi Algılama Özellikleri](security-center-detection-capabilities.md) konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="f9c7d-113">Güvenlik ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="f9c7d-113">Managing security alerts</span></span>
<span data-ttu-id="f9c7d-114">**Güvenlik uyarıları** kutucuğuna bakarak mevcut uyarılarınızı gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-114">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="f9c7d-115">Azure Portal’ı açın ve her bir uyarı hakkında daha fazla ayrıntıya ulaşmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f9c7d-115">Open Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="f9c7d-116">Güvenlik Merkezi panosunda **Güvenlik uyarıları** kutucuğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-116">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Güvenlik Merkezi'nde güvenlik uyarıları kutucuğu](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="f9c7d-118">Aşağıda gösterildiği gibi, uyarılar hakkında daha fazla ayrıntı içeren **Güvenlik uyarıları** dikey penceresini açmak için kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-118">Click the tile to open the **Security alerts** blade that contains more details about the alerts as shown below.</span></span>

   ![Güvenlik Merkezi'nde Güvenlik uyarıları dikey penceresi](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="f9c7d-120">Bu dikey pencerenin alt bölümünde her bir uyarı için ayrıntılar bulunur.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-120">In the bottom part of this blade are the details for each alert.</span></span> <span data-ttu-id="f9c7d-121">Sıralamak için hangi sütuna göre sıralamak istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-121">To sort, click the column that you want to sort by.</span></span> <span data-ttu-id="f9c7d-122">Her sütunun tanımı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f9c7d-122">The definition for each column is given below:</span></span>

* <span data-ttu-id="f9c7d-123">**Açıklama**: Uyarının kısa bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-123">**Description**: A brief explanation of the alert.</span></span>
* <span data-ttu-id="f9c7d-124">**Sayı**: Belirtilmiş türün belirli bir günde algılanan tüm uyarılarının listesi.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="f9c7d-125">**Algılayan**: Uyarıyı tetiklemekten sorumlu hizmet.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-125">**Detected by**: The service that was responsible for triggering the alert.</span></span>
* <span data-ttu-id="f9c7d-126">**Tarih**: Olayın gerçekleştiği tarih</span><span class="sxs-lookup"><span data-stu-id="f9c7d-126">**Date**: The date that the event occurred.</span></span>
* <span data-ttu-id="f9c7d-127">**Durum**: Bu uyarı için geçerli durum.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-127">**State**: The current state for that alert.</span></span> <span data-ttu-id="f9c7d-128">İki tür durum mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="f9c7d-128">There are two types of states:</span></span>
  * <span data-ttu-id="f9c7d-129">**Etkin**: Güvenlik uyarısı algılandı.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-129">**Active**: The security alert has been detected.</span></span>
* <span data-ttu-id="f9c7d-130">**Önem derecesi**: Yüksek, orta veya düşük önem düzeyi.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-130">**Severity**: The severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="f9c7d-131">Uyarıları filtreleme</span><span class="sxs-lookup"><span data-stu-id="f9c7d-131">Filtering alerts</span></span>
<span data-ttu-id="f9c7d-132">Tarihe, duruma ve önem derecesine göre uyarıları filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="f9c7d-133">Filtreleme uyarıları, güvenlik uyarıları gösterimi kapsamını daraltmanızın gerektiği senaryolar için faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-133">Filtering alerts can be useful for scenarios where you need to narrow the scope of security alerts show.</span></span> <span data-ttu-id="f9c7d-134">Örneğin, sistemde olası bir ihlali araştırdığınız için son 24 saatte oluşan güvenlik uyarılarını ele almak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-134">For example, you might you want to address security alerts that occurred in the last 24 hours because you are investigating a potential breach in the system.</span></span>

1. <span data-ttu-id="f9c7d-135">**Güvenlik Uyarıları** dikey penceresindeki **Filtreleme**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-135">Click **Filter** on the **Security Alerts** blade.</span></span> <span data-ttu-id="f9c7d-136">**Filtreleme** dikey penceresi açılır ve görmek istediğiniz tarih, durum ve önem derecesi değerlerini seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-136">The **Filter** blade opens and you select the date, state, and severity values you wish to see.</span></span>

    ![Güvenlik Merkezi'nde uyarıları filtreleme](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-to-security-alerts"></a><span data-ttu-id="f9c7d-138">Güvenlik uyarılarını yanıtlama</span><span class="sxs-lookup"><span data-stu-id="f9c7d-138">Respond to security alerts</span></span>
<span data-ttu-id="f9c7d-139">Uyarıyı tetikleyen olay(lar) ve saldırıyı düzeltmek için (varsa) hangi adımları atmanız gerektiği hakkında daha fazla bilgi edinmek için bir güvenlik uyarısı seçin.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-139">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="f9c7d-140">Güvenlik uyarıları, türe ve tarihe göre gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="f9c7d-141">Güvenlik uyarısına tıklandığında gruplanan uyarıların listesini içeren dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-141">Clicking a security alert will open a blade containing a list of the grouped alerts.</span></span>

![Azure Güvenlik Merkezi'nde güvenlik uyarılarını yanıtlama](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="f9c7d-143">Bu durumda, tetiklenen uyarılar şüpheli Uzak Masaüstü Protokolü (RDP) etkinliğine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-143">In this case, the alerts that were triggered refer to suspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="f9c7d-144">Birinci sütunda hangi kaynakların saldırıya uğradığı; ikinci sütunda kaynağın kaç kez saldırıya uğradığı; üçüncü sütunda saldırının zamanı; dördüncü sütunda uyarının durumu ve beşinci sütunda saldırının önem derecesi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-144">The first column shows which resources were attacked; the second shows how many times the resource was attacked; the third shows the time of the attack; the fourth shows state of the alert; and the fifth shows the severity of the attack.</span></span> <span data-ttu-id="f9c7d-145">Bu bilgileri gözden geçirdikten sonra, saldırıya uğrayan kaynağa tıkladığınızda yeni bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-145">After reviewing this information, click the resource that was attacked and a new blade will open.</span></span>

![Azure Güvenlik Merkezi'nde güvenlik uyarıları hakkında ne yapılacağına ilişkin öneriler](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="f9c7d-147">Bu dikey pencerenin **Açıklama** alanında bu olay hakkında daha fazla ayrıntı bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-147">In the **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="f9c7d-148">Bu ek ayrıntılar, güvenlik uyarısını neyin tetiklediği, hedef kaynak, uygulanabilirse kaynak IP adresi ve düzeltmeye ilişkin öneriler hakkında öngörüler sunar.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-148">These additional details offer insight into what triggered the security alert, the target resource, when applicable the source IP address, and recommendations about how to remediate.</span></span>  <span data-ttu-id="f9c7d-149">Windows güvenlik olayı günlüklerinin tümü IP adresi içermediğinden, bazı durumlarda kaynak IP adresi boştur (yoktur).</span><span class="sxs-lookup"><span data-stu-id="f9c7d-149">In some instances, the source IP address will be empty (not available) because not all Windows security events logs include the IP address.</span></span>

<span data-ttu-id="f9c7d-150">Güvenlik Merkezi tarafından önerilen düzeltme, güvenlik uyarısına göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-150">The remediation suggested by Security Center will vary according to the security alert.</span></span> <span data-ttu-id="f9c7d-151">Bazı durumlarda, önerilen düzeltmeyi uygulamak için diğer Azure işlevlerini kullanmak zorunda kalabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-151">In some cases, you may have to use other Azure capabilities to implement the recommended remediation.</span></span> <span data-ttu-id="f9c7d-152">Örneğin, bu saldırıya ilişkin düzeltme, [ağ ACL'si](../virtual-network/virtual-networks-acl.md) veya [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) kuralı kullanarak bu saldırıyı gerçekleştiren IP adresini kara listeye almaktır.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-152">For example, the remediation for this attack is to blacklist the IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c7d-153">Farklı uyarı türleri hakkında daha fazla bilgi için [Azure Güvenlik Merkezi'nde Türe Göre Güvenlik Uyarıları](security-center-alerts-type.md) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-153">For more information on the different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="f9c7d-154">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-154">See also</span></span>
<span data-ttu-id="f9c7d-155">Bu belgede, Güvenlik Merkezi'nde güvenlik ilkelerinin nasıl yapılandırılacağını öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-155">In this document, you learned how to configure security policies in Security Center.</span></span> <span data-ttu-id="f9c7d-156">Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:</span><span class="sxs-lookup"><span data-stu-id="f9c7d-156">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="f9c7d-157">Azure Güvenlik Merkezi'nde Güvenlik Olayını İşleme</span><span class="sxs-lookup"><span data-stu-id="f9c7d-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="f9c7d-158">Azure Güvenlik Merkezi Algılama Özellikleri</span><span class="sxs-lookup"><span data-stu-id="f9c7d-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="f9c7d-159">Azure Güvenlik Merkezi Planlama ve İşlemler Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="f9c7d-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="f9c7d-160">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) - Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="f9c7d-161">[Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c7d-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
