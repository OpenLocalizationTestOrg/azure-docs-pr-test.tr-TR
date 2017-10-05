---
title: "Azure Güvenlik Merkezi'ne giriş | Microsoft Docs"
description: "Azure Güvenlik Merkezi, önemli işlevleri ve nasıl çalıştığı hakkında bilgi edinin."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 8951167213da6ab5341c1ca420353ec625ef5424
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-security-center"></a><span data-ttu-id="dd32c-103">Azure Güvenlik Merkezi'ne Giriş</span><span class="sxs-lookup"><span data-stu-id="dd32c-103">Introduction to Azure Security Center</span></span>
<span data-ttu-id="dd32c-104">Azure Güvenlik Merkezi, önemli işlevleri ve nasıl çalıştığı hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-104">Learn about Azure Security Center, its key capabilities, and how it works.</span></span>

> [!NOTE]
> <span data-ttu-id="dd32c-105">Haziran 2017'nin ilk günlerinden itibaren Güvenlik Merkezi, veri toplamak ve depolamak için Microsoft Monitoring Agent'ı kullanacak.</span><span class="sxs-lookup"><span data-stu-id="dd32c-105">Beginning in early June 2017, Security Center will use the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="dd32c-106">Daha fazla bilgi edinmek için [Azure Güvenlik Merkezi Platform Geçişi](security-center-platform-migration.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="dd32c-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) to learn more.</span></span> <span data-ttu-id="dd32c-107">Bu makaledeki bilgiler, Microsoft Monitoring Agent'a geçiş sonrasındaki Güvenlik Merkezi işlevselliğine yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-107">The information in this article represents Security Center functionality after transition to the Microsoft Monitoring Agent.</span></span>
>
>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="dd32c-108">Azure Güvenlik Merkezi nedir?</span><span class="sxs-lookup"><span data-stu-id="dd32c-108">What is Azure Security Center?</span></span>
 <span data-ttu-id="dd32c-109">Güvenlik Merkezi, artırılmış görünürlük aracılığıyla tehditleri engellemenize, algılamanıza ve yanıtlamanıza, ayrıca Azure kaynaklarınızın güvenliğini denetlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="dd32c-109">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="dd32c-110">Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.</span><span class="sxs-lookup"><span data-stu-id="dd32c-110">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="dd32c-111">Temel işlevler</span><span class="sxs-lookup"><span data-stu-id="dd32c-111">Key capabilities</span></span>
 <span data-ttu-id="dd32c-112">Güvenlik Merkezi, Azure'da yerleşik olan kullanımı kolay ve etkili tehdit önleme, saptama ve yanıtlama işlevlerini sunar.</span><span class="sxs-lookup"><span data-stu-id="dd32c-112">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in to Azure.</span></span> <span data-ttu-id="dd32c-113">Temel işlevler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dd32c-113">Key capabilities are:</span></span>

| <span data-ttu-id="dd32c-114">Aşama</span><span class="sxs-lookup"><span data-stu-id="dd32c-114">Stage</span></span> | <span data-ttu-id="dd32c-115">Özellik</span><span class="sxs-lookup"><span data-stu-id="dd32c-115">Capability</span></span> |
| --- | --- |
| <span data-ttu-id="dd32c-116">Önleme</span><span class="sxs-lookup"><span data-stu-id="dd32c-116">Prevent</span></span> |<span data-ttu-id="dd32c-117">Azure kaynaklarınızın güvenlik durumunu izler</span><span class="sxs-lookup"><span data-stu-id="dd32c-117">Monitors the security state of your Azure resources</span></span> |
| <span data-ttu-id="dd32c-118">Önleme</span><span class="sxs-lookup"><span data-stu-id="dd32c-118">Prevent</span></span> | <span data-ttu-id="dd32c-119">Azure aboneliklerinize şirketinizin güvenlik gereksinimlerine, uygulama türlerini bu kullanın ve verilerinizin duyarlılığına göre ilkeleri tanımlar</span><span class="sxs-lookup"><span data-stu-id="dd32c-119">Defines policies for your Azure subscriptions based on your company’s security requirements, the types of applications that you use, and the sensitivity of your data</span></span> |
| <span data-ttu-id="dd32c-120">Önleme</span><span class="sxs-lookup"><span data-stu-id="dd32c-120">Prevent</span></span> | <span data-ttu-id="dd32c-121">Gerekli denetimleri uygulama işlemi boyunca hizmet sahiplerine rehberlik etmek için ilke temelli güvenlik önerilerini kullanır</span><span class="sxs-lookup"><span data-stu-id="dd32c-121">Uses policy-driven security recommendations to guide service owners through the process of implementing needed controls</span></span> |
| <span data-ttu-id="dd32c-122">Önleme</span><span class="sxs-lookup"><span data-stu-id="dd32c-122">Prevent</span></span> | <span data-ttu-id="dd32c-123">Microsoft ve ortaklarından güvenlik hizmetlerini ve gereçlerini hızlı bir şekilde dağıtır</span><span class="sxs-lookup"><span data-stu-id="dd32c-123">Rapidly deploys security services and appliances from Microsoft and partners</span></span> |
| <span data-ttu-id="dd32c-124">Algılama</span><span class="sxs-lookup"><span data-stu-id="dd32c-124">Detect</span></span> |<span data-ttu-id="dd32c-125">Azure kaynaklarınızdan, ağdan ve kötü amaçlı yazılımdan koruma programları ve güvenlik duvarları gibi iş ortağı çözümlerinden güvenlik verilerini otomatik olarak çözümleyip toplar</span><span class="sxs-lookup"><span data-stu-id="dd32c-125">Automatically collects and analyzes security data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls</span></span> |
| <span data-ttu-id="dd32c-126">Algılama</span><span class="sxs-lookup"><span data-stu-id="dd32c-126">Detect</span></span> | <span data-ttu-id="dd32c-127">Microsoft ürünleri'ten ve Hizmetleri, Microsoft dijital Suçlar birimi (DCU), Microsoft Güvenlik Yanıt Merkezi (MSRC) ve dış akışların kullandığı genel tehdit</span><span class="sxs-lookup"><span data-stu-id="dd32c-127">Uses global threat intelligence from Microsoft products and services, the Microsoft Digital Crimes Unit (DCU), the Microsoft Security Response Center (MSRC), and external feeds</span></span> |
| <span data-ttu-id="dd32c-128">Algılama</span><span class="sxs-lookup"><span data-stu-id="dd32c-128">Detect</span></span> | <span data-ttu-id="dd32c-129">Machine learning ve davranış analizi dahil olmak üzere gelişmiş analizler uygular</span><span class="sxs-lookup"><span data-stu-id="dd32c-129">Applies advanced analytics, including machine learning and behavioral analysis</span></span> |
| <span data-ttu-id="dd32c-130">Yanıtlama</span><span class="sxs-lookup"><span data-stu-id="dd32c-130">Respond</span></span> |<span data-ttu-id="dd32c-131">Öncelikli güvenlik olayları/uyarıları sağlar</span><span class="sxs-lookup"><span data-stu-id="dd32c-131">Provides prioritized security incidents/alerts</span></span> |
| <span data-ttu-id="dd32c-132">Yanıtlama</span><span class="sxs-lookup"><span data-stu-id="dd32c-132">Respond</span></span> | <span data-ttu-id="dd32c-133">Saldırının kaynağı ve etkilenen kaynakları hakkında öngörüler sunar</span><span class="sxs-lookup"><span data-stu-id="dd32c-133">Offers insights into the source of the attack and impacted resources</span></span> |
| <span data-ttu-id="dd32c-134">Yanıtlama</span><span class="sxs-lookup"><span data-stu-id="dd32c-134">Respond</span></span> | <span data-ttu-id="dd32c-135">Geçerli saldırıyı durdurmaya ve gelecekteki saldırıları önlenmeye yönelik yöntemler önerir</span><span class="sxs-lookup"><span data-stu-id="dd32c-135">Suggests ways to stop the current attack and help prevent future attacks</span></span> |

## <a name="introductory-walkthrough"></a><span data-ttu-id="dd32c-136">Tanıtıcı kılavuz</span><span class="sxs-lookup"><span data-stu-id="dd32c-136">Introductory walkthrough</span></span>

> [!NOTE]
> <span data-ttu-id="dd32c-137">Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.</span><span class="sxs-lookup"><span data-stu-id="dd32c-137">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="dd32c-138">Bu belge hakkında adım adım kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-138">This document is not a step-by-step guide.</span></span>
>
>

 <span data-ttu-id="dd32c-139">Güvenlik Merkezi'ne [Azure portalından](https://azure.microsoft.com/features/azure-portal/) erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd32c-139">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="dd32c-140">[Portalı oturum açma](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd32c-140">[Sign in to the portal](https://portal.azure.com).</span></span> <span data-ttu-id="dd32c-141">Ana portal menü altında kaydırın **Güvenlik Merkezi** seçeneğini veya seçin **Güvenlik Merkezi** önceden portal panosuna sabitlediğiniz döşeme.</span><span class="sxs-lookup"><span data-stu-id="dd32c-141">Under the main portal menu, scroll to the **Security Center** option or select the **Security Center** tile that you previously pinned to the portal dashboard.</span></span>

![Azure portalında güvenlik kutucuğu][1]

<span data-ttu-id="dd32c-143">Güvenlik Merkezi'nde güvenlik ilkelerini ayarlayabilir, güvenlik yapılandırmalarını izleyebilir ve güvenlik uyarıları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd32c-143">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span></span>

### <a name="security-policies"></a><span data-ttu-id="dd32c-144">Güvenlik ilkeleri</span><span class="sxs-lookup"><span data-stu-id="dd32c-144">Security policies</span></span>
<span data-ttu-id="dd32c-145">Şirketinizin güvenlik gereksinimlerine göre Azure aboneliklerinize için ilkeleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd32c-145">You can define policies for your Azure subscriptions according to your company's security requirements.</span></span> <span data-ttu-id="dd32c-146">Bunları kullanmakta olduğunuz uygulama türlerine veya her bir abonelikteki verilerin duyarlılığına göre de uyarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd32c-146">You can also tailor them to the types of applications you're using or to the sensitivity of the data in each subscription.</span></span> <span data-ttu-id="dd32c-147">Örneğin, geliştirme veya test etme için kullanılan kaynaklar, üretim uygulamaları için kullanılanlardan farklı güvenlik gereksinimlerine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-147">For example, resources used for development or testing may have different security requirements than those used for production applications.</span></span> <span data-ttu-id="dd32c-148">Benzer şekilde, PII gibi düzenlenen veriler içeren uygulamalar, daha yüksek bir güvenlik düzeyi gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-148">Likewise, applications with regulated data like PII may require a higher level of security.</span></span>

> [!NOTE]
> <span data-ttu-id="dd32c-149">Güvenlik ilkesini değiştirmek için bir güvenlik yöneticisi veya aboneliğin sahibi veya katkıda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-149">To modify a security policy, you must be a Security Administrator or the subscription's Owner or Contributor.</span></span> <span data-ttu-id="dd32c-150">Rolleri hakkında daha fazla bilgi edinin ve Güvenlik Merkezi, Eylemler izin görmek için [Azure Güvenlik Merkezi'nde izinleri](security-center-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="dd32c-150">To learn more about roles and allowed actions in Security Center, see [Permissions in Azure Security Center](security-center-permissions.md).</span></span>
>
>

<span data-ttu-id="dd32c-151">**Güvenlik Merkezi** dikey penceresinde, aboneliklerinizin ve kaynak gruplarınızın bir listesi için **İlke** kutucuğunu seçin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-151">On the **Security Center** blade, select the **Policy** tile for a list of your subscriptions and resource groups.</span></span>   

![Güvenlik Merkezi dikey penceresi][2]

<span data-ttu-id="dd32c-153">Üzerinde **Güvenlik İlkesi** dikey penceresinde ilke ayrıntılarını görüntülemek için abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-153">On the **Security policy** blade, select a subscription to view the policy details.</span></span>

<span data-ttu-id="dd32c-154">**Veri toplama** bir güvenlik ilkesi için veri toplama sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd32c-154">**Data collection** enables data collection for a security policy.</span></span> <span data-ttu-id="dd32c-155">Etkinleştirildiğinde şunlar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="dd32c-155">Enabling provides:</span></span>

* <span data-ttu-id="dd32c-156">Sanal makineler (VM'ler), günlük tüm tarama güvenlik izleme ve öneriler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-156">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span></span>
* <span data-ttu-id="dd32c-157">Analiz ve tehdit algılama için güvenlik olaylarının toplanması.</span><span class="sxs-lookup"><span data-stu-id="dd32c-157">Collection of security events for analysis and threat detection.</span></span>

> [!NOTE]
> <span data-ttu-id="dd32c-158">Veri toplama abonelik düzeyinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="dd32c-158">Data collection is configured at the subscription level.</span></span>
>
>

<span data-ttu-id="dd32c-159">Seçin **önleme İlkesi** açmak için **önleme İlkesi** dikey.</span><span class="sxs-lookup"><span data-stu-id="dd32c-159">Select **Prevention policy** to open the **Prevention policy** blade.</span></span> <span data-ttu-id="dd32c-160">**İçin önerileri göster** izlemek istiyorsanız ve görmek istediğiniz önerileri Abonelikteki kaynakların güvenlik gereksinimlerine bağlı olan güvenlik denetimleri seçtiğiniz sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd32c-160">**Show recommendations for** lets you choose the security controls that you want to monitor and the recommendations that you want to see based on the security needs of the resources within the subscription.</span></span>

### <a name="security-recommendations"></a><span data-ttu-id="dd32c-161">Güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="dd32c-161">Security recommendations</span></span>
 <span data-ttu-id="dd32c-162">Güvenlik Merkezi, olası güvenlik açıklarını tanımlamak için Azure kaynaklarınızın güvenlik durumunu inceler.</span><span class="sxs-lookup"><span data-stu-id="dd32c-162">Security Center analyzes the security state of your Azure resources to identify potential security vulnerabilities.</span></span> <span data-ttu-id="dd32c-163">Gerekli denetimlerin yapılandırılması işlemi boyunca bir öneri listesi size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="dd32c-163">A list of recommendations guides you through the process of configuring needed controls.</span></span> <span data-ttu-id="dd32c-164">Örneklere şunlar dahildir:</span><span class="sxs-lookup"><span data-stu-id="dd32c-164">Examples include:</span></span>

* <span data-ttu-id="dd32c-165">Kötü amaçlı yazılımı tanımlama ve kaldırmada yardım etmesi için kötü amaçlı yazılımdan koruma yazılımı hazırlama</span><span class="sxs-lookup"><span data-stu-id="dd32c-165">Provisioning antimalware to help identify and remove malicious software</span></span>
* <span data-ttu-id="dd32c-166">Ağ güvenlik gruplarını ve kurallarını trafiği denetlemek VM'ler için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dd32c-166">Configuring network security groups and rules to control traffic to VMs</span></span>
* <span data-ttu-id="dd32c-167">Web uygulamalarınızı hedefleyen saldırılara karşı korumaya yardımcı olmak için web uygulaması güvenlik duvarı hazırlama</span><span class="sxs-lookup"><span data-stu-id="dd32c-167">Provisioning of web application firewalls to help defend against attacks that target your web applications</span></span>
* <span data-ttu-id="dd32c-168">Eksik sistem güncelleştirmelerini dağıtma</span><span class="sxs-lookup"><span data-stu-id="dd32c-168">Deploying missing system updates</span></span>
* <span data-ttu-id="dd32c-169">Önerilen taban çizgileriyle eşleşmeyen işletim sistemi yapılandırmalarını ele alma</span><span class="sxs-lookup"><span data-stu-id="dd32c-169">Addressing OS configurations that do not match the recommended baselines</span></span>

<span data-ttu-id="dd32c-170">Öneriler listesi için **Öneriler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dd32c-170">Click the **Recommendations** tile for a list of recommendations.</span></span> <span data-ttu-id="dd32c-171">Ek bilgileri görüntülemek veya sorunu çözmek amacıyla eyleme geçmek için önerilere tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dd32c-171">Click each recommendation to view additional information or to take action to resolve the issue.</span></span>

![Azure Güvenlik Merkezi'nde güvenlik önerileri][5]

### <a name="security-state-of-azure-resources"></a><span data-ttu-id="dd32c-173">Azure kaynakların güvenlik durumu</span><span class="sxs-lookup"><span data-stu-id="dd32c-173">Security state of Azure resources</span></span>
<span data-ttu-id="dd32c-174">**Önleme** VM'ler, web uygulamaları ve diğer kaynaklar dahil, bölümü kaynak türüne göre ortamın genel güvenlik duruşunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-174">The **Prevention** section of the dashboard shows the overall security posture of the environment by resource type, including VMs, web applications, and other resources.</span></span>   

<span data-ttu-id="dd32c-175">Altında bir kaynak türü seçin **önleme** tanımlanan olası güvenlik açıkları listesi dahil olmak üzere daha fazla bilgi görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="dd32c-175">Select a resource type under **Prevention** to view more information, including a list of any potential security vulnerabilities that have been identified.</span></span> <span data-ttu-id="dd32c-176">(**İşlem** aşağıdaki örnekte seçilir.)</span><span class="sxs-lookup"><span data-stu-id="dd32c-176">(**Compute** is selected in the example below.)</span></span>

![Kaynak durumu kutucuğu][6]

### <a name="security-alerts"></a><span data-ttu-id="dd32c-178">Güvenlik uyarıları</span><span class="sxs-lookup"><span data-stu-id="dd32c-178">Security alerts</span></span>
 <span data-ttu-id="dd32c-179">Güvenlik Merkezi, Azure kaynaklarınızdan, ağdan ve kötü amaçlı yazılımdan koruma programları ve güvenlik duvarları gibi iş ortağı çözümlerinden günlük verilerini otomatik olarak toplar, çözümler ve tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-179">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls.</span></span> <span data-ttu-id="dd32c-180">Tehditler algılandığında bir güvenlik uyarısı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="dd32c-180">When threats are detected, a security alert is created.</span></span> <span data-ttu-id="dd32c-181">Örneklere şunların algılanması dahildir:</span><span class="sxs-lookup"><span data-stu-id="dd32c-181">Examples include detection of:</span></span>

* <span data-ttu-id="dd32c-182">Bilinen kötü amaçlı IP adresleri ile iletişim kuran tehlikeye atılmış VM'ler</span><span class="sxs-lookup"><span data-stu-id="dd32c-182">Compromised VMs communicating with known malicious IP addresses</span></span>
* <span data-ttu-id="dd32c-183">Windows hata raporlama kullanılarak algılanan gelişmiş kötü amaçlı yazılım</span><span class="sxs-lookup"><span data-stu-id="dd32c-183">Advanced malware detected by using Windows error reporting</span></span>
* <span data-ttu-id="dd32c-184">Sanal makineleri karşı deneme yanılma saldırıları</span><span class="sxs-lookup"><span data-stu-id="dd32c-184">Brute force attacks against VMs</span></span>
* <span data-ttu-id="dd32c-185">Tümleşik kötü amaçlı yazılımdan koruma programlarından ve güvenlik duvarlarından güvenlik uyarıları</span><span class="sxs-lookup"><span data-stu-id="dd32c-185">Security alerts from integrated antimalware programs and firewalls</span></span>

<span data-ttu-id="dd32c-186">**Güvenlik uyarıları** kutucuğuna tıkladığınızda öncelikli uyarıların bir listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-186">Clicking the **Security alerts** tile displays a list of prioritized alerts.</span></span>

![Güvenlik uyarıları][7]

<span data-ttu-id="dd32c-188">Bir uyarının seçilmesi, saldırı hakkında daha fazla bilgi ve sorunun nasıl çözüleceği hakkında öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-188">Selecting an alert shows more information about the attack and suggestions for how to remediate it.</span></span>

![Güvenlik uyarısı ayrıntıları][8]

### <a name="partner-solutions"></a><span data-ttu-id="dd32c-190">İş ortağı çözümleri</span><span class="sxs-lookup"><span data-stu-id="dd32c-190">Partner solutions</span></span>
<span data-ttu-id="dd32c-191">**İş ortağı çözümleri** kutucuğu, Azure aboneliğinizle tümleşik iş ortağı çözümlerinizin güvenlik durumunu bir bakışta izlemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd32c-191">The **Partner solutions** tile lets you monitor at a glance the security state of your partner solutions integrated with your Azure subscription.</span></span> <span data-ttu-id="dd32c-192">Güvenlik Merkezi, çözümlerden gelen uyarıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dd32c-192">Security Center displays alerts coming from the solutions.</span></span>

<span data-ttu-id="dd32c-193">**İş ortağı çözümleri** kutucuğunu seçin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-193">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="dd32c-194">Tüm bağlı iş ortağı çözümlerinin listesini görüntüleyen bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="dd32c-194">A blade opens displaying a list of all connected partner solutions.</span></span>

![İş ortağı çözümleri][9]

## <a name="get-started"></a><span data-ttu-id="dd32c-196">başlarken</span><span class="sxs-lookup"><span data-stu-id="dd32c-196">Get started</span></span>
<span data-ttu-id="dd32c-197">Güvenlik Merkezi ile çalışmaya başlamak için Microsoft Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-197">To get started with Security Center, you need a subscription to Microsoft Azure.</span></span> <span data-ttu-id="dd32c-198">Güvenlik Merkezi, Azure aboneliğiniz ile etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="dd32c-198">Security Center is enabled with your Azure subscription.</span></span> <span data-ttu-id="dd32c-199">Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd32c-199">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

 <span data-ttu-id="dd32c-200">Güvenlik Merkezi'ne [Azure portalından](https://azure.microsoft.com/features/azure-portal/) erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd32c-200">You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="dd32c-201">Daha fazla bilgi edinmek için bkz. [portal belgeleri](https://azure.microsoft.com/documentation/services/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="dd32c-201">See the [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) to learn more.</span></span>

<span data-ttu-id="dd32c-202">[Azure Güvenlik Merkezi'ni kullanmaya başlama](security-center-get-started.md), Güvenlik Merkezi'nin güvenlik izleme ve ilke yönetimi bileşenlerinde size hızla rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd32c-202">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through the security-monitoring and policy-management components of Security Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd32c-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd32c-203">Next steps</span></span>
<span data-ttu-id="dd32c-204">Bu belgede Güvenlik Merkezi, temel işlevleri ve nasıl kullanmaya başlayacağınız size tanıtıldı.</span><span class="sxs-lookup"><span data-stu-id="dd32c-204">In this document, you were introduced to Security Center, its key capabilities, and how to get started.</span></span> <span data-ttu-id="dd32c-205">Daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="dd32c-205">To learn more, see the following resources:</span></span>

* <span data-ttu-id="dd32c-206">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) — Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-206">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="dd32c-207">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) — nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-207">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="dd32c-208">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) - Azure kaynaklarınızın sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-208">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="dd32c-209">[Yönetme ve Azure Güvenlik Merkezi'nde güvenlik uyarılarını yanıtlama](security-center-managing-and-responding-alerts.md) — yönetme ve güvenlik uyarılarını yanıtlama hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-209">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="dd32c-210">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-210">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="dd32c-211">[Azure Güvenlik Merkezi veri güvenliği](security-center-data-security.md) -verilerin yönetilmesi ve diğer Güvenlik Merkezi'nde korunması nasıl öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-211">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="dd32c-212">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) - Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd32c-212">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="dd32c-213">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) — en son Azure güvenlik haberlerini ve bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="dd32c-213">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
