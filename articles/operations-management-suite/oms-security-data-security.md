---
title: "aaaOperations Yönetim Paketi güvenlik ve denetim çözüm veri güvenliği | Microsoft Docs"
description: "Bu belgede verilerin Operations Management Suite Güvenlik ve Denetim Çözümünde nasıl yönetildiği ve korunduğu açıklanmaktadır."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="36605-103">Operations Management Suite Güvenlik ve Denetim çözümü veri güvenliği</span><span class="sxs-lookup"><span data-stu-id="36605-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="36605-104">toohelp müşteriler engellemenize, algılamanıza ve toothreats, yanıt [Operations Management Suite (OMS) güvenlik ve denetim çözümü](operations-management-suite-overview.md) içeren veri kaynaklarınızı ilgili işler ve toplar:</span><span class="sxs-lookup"><span data-stu-id="36605-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="36605-105">Güvenlik olay günlüğü</span><span class="sxs-lookup"><span data-stu-id="36605-105">Security event log</span></span>
* <span data-ttu-id="36605-106">Windows için Olay İzleme (ETW) olayları</span><span class="sxs-lookup"><span data-stu-id="36605-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="36605-107">AppLocker denetim olayları</span><span class="sxs-lookup"><span data-stu-id="36605-107">AppLocker auditing events</span></span>
* <span data-ttu-id="36605-108">Windows Güvenlik Duvarı günlüğü</span><span class="sxs-lookup"><span data-stu-id="36605-108">Windows Firewall log</span></span>
* <span data-ttu-id="36605-109">Gelişmiş Threat Analytics olayları</span><span class="sxs-lookup"><span data-stu-id="36605-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="36605-110">Temel değerlendirmesinin sonuçları</span><span class="sxs-lookup"><span data-stu-id="36605-110">Results of baseline assessment</span></span>
* <span data-ttu-id="36605-111">Kötü amaçlı yazılımdan koruma değerlendirmesinin sonuçları</span><span class="sxs-lookup"><span data-stu-id="36605-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="36605-112">Güncelleştirme/düzeltme eki değerlendirmesinin sonuçları</span><span class="sxs-lookup"><span data-stu-id="36605-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="36605-113">Merhaba aracısında açıkça etkin Syslog modüllerini akışlar</span><span class="sxs-lookup"><span data-stu-id="36605-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="36605-114">Önemli taahhütlerde tooprotect hello gizlilik ve bu verilerin güvenliğini vermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="36605-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="36605-115">Microsoft aynılarını toostrict uyumluluk ve güvenlik yönergelerine — toooperating hizmet kodlama gelen.</span><span class="sxs-lookup"><span data-stu-id="36605-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="36605-116">Bu makalede, OMS Güvenlik ve Denetim Çözümü'nde verilerin nasıl yönetildiği ve korunduğu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="36605-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="36605-117">Veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="36605-117">Data sources</span></span>
<span data-ttu-id="36605-118">OMS güvenlik ve denetim çözüm hello OMS Aracısı yüklendiği, sanal makineleri ve fiziksel bilgisayarların verilerini analiz eder.</span><span class="sxs-lookup"><span data-stu-id="36605-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="36605-119">OMS Güvenlik ve Denetim Çözümü; Windows olayı, denetim günlükleri, IIS günlükleri ve syslog iletileri gibi güvenlik olayları hakkında yapılandırma bilgilerini toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="36605-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="36605-120">Bu verilere örnek olarak işletim sistemi türü ve sürümü, devam eden işlemler, makine adı, IP adresleri, oturum açmış kullanıcı ve kiracı kimliği verilebilir.</span><span class="sxs-lookup"><span data-stu-id="36605-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="36605-121">Veri koruma</span><span class="sxs-lookup"><span data-stu-id="36605-121">Data protection</span></span>
<span data-ttu-id="36605-122">**Veriler arasında ayrım yapma**: veri hello hizmet boyunca her bir bileşende baz mantıksal olarak ayrı tutulur.</span><span class="sxs-lookup"><span data-stu-id="36605-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="36605-123">Tüm veriler kuruluşa göre etiketlenir.</span><span class="sxs-lookup"><span data-stu-id="36605-123">All data is tagged per organization.</span></span> <span data-ttu-id="36605-124">Bu etiketleme hello veri yaşam döngüsü boyunca devam ederse ve her hello hizmet katmanında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="36605-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="36605-125">**Veri erişimi**: tooprovide güvenlik önerileri ve olası güvenlik tehditlerini araştırmak, Microsoft personeli, toplanan veya hizmetleri tarafından analiz bilgiler erişebilir.</span><span class="sxs-lookup"><span data-stu-id="36605-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="36605-126">Biz toohello uyması [Microsoft çevrimiçi Hizmet Koşulları'nı](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) ve [gizlilik bildirimi](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), Microsoft olmayan müşteri verilerini veya kullanacağınız bilgileri, gelen tüm tanıtım veya benzer olduğunu belirtin Ticari amaçlarla.</span><span class="sxs-lookup"><span data-stu-id="36605-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="36605-127">tooprovide güvenlik önerileri ve olası güvenlik tehditlerini araştırmak, Microsoft personeli, toplanan veya hizmetleri tarafından analiz bilgiler erişebilir.</span><span class="sxs-lookup"><span data-stu-id="36605-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="36605-128">Yalnızca müşteri verileri, Azure ile bu hizmetleri sağlamayla uyumlu amaçlar da dahil olmak üzere Hizmetleri gerekli tooprovide olarak kullanırız.</span><span class="sxs-lookup"><span data-stu-id="36605-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="36605-129">Tüm hakları tooyour kendi verileri korur.</span><span class="sxs-lookup"><span data-stu-id="36605-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="36605-130">**Veri kullanımı**: Microsoft desenleri kullanır ve tehdit bilgileri birden çok görülen kiracılar tooenhance bizim önleme ve algılama yeteneklerini; biz açıklanan hello gizlilik taahhütlerine uygun olarak bunu bizim [gizlilik Deyimi](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="36605-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="36605-131">Veri konumu hello ilk OMS güvenlik ve denetim yapılandırma işleminin bir parçası olan hello çalışma alanı oluşturma sırasında hello OMS çalışma düzeyinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="36605-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="36605-132">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="36605-132">See also</span></span>
<span data-ttu-id="36605-133">Bu belgede, OMS'de verilerin nasıl yönetileceğine ve korunacağına ilişkin bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="36605-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="36605-134">OMS güvenlik ve denetim çözümü hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="36605-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="36605-135">Operations Management Suite'e (OMS) genel bakış</span><span class="sxs-lookup"><span data-stu-id="36605-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="36605-136">İzleme ve yanıt tooSecurity uyarıları Operations Management Suite güvenlik ve denetim çözümü</span><span class="sxs-lookup"><span data-stu-id="36605-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="36605-137">Operations Management Suite Güvenlik ve Denetim Çözümünde Kaynakları İzleme</span><span class="sxs-lookup"><span data-stu-id="36605-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

