---
title: "aaaIntroduction tooAzure Güvenlik Merkezi | Microsoft Docs"
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
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a><span data-ttu-id="26f5a-103">Giriş tooAzure Güvenlik Merkezi</span><span class="sxs-lookup"><span data-stu-id="26f5a-103">Introduction tooAzure Security Center</span></span>
<span data-ttu-id="26f5a-104">Azure Güvenlik Merkezi, önemli işlevleri ve nasıl çalıştığı hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="26f5a-104">Learn about Azure Security Center, its key capabilities, and how it works.</span></span>

> [!NOTE]
> <span data-ttu-id="26f5a-105">İçinde erken Haziran 2017'den itibaren Güvenlik Merkezi hello Microsoft İzleme Aracısı toocollect kullanmak ve verileri depolamak.</span><span class="sxs-lookup"><span data-stu-id="26f5a-105">Beginning in early June 2017, Security Center will use hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="26f5a-106">Bkz: [Azure Güvenlik Merkezi platformu geçiş](security-center-platform-migration.md) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="26f5a-106">See [Azure Security Center Platform Migration](security-center-platform-migration.md) toolearn more.</span></span> <span data-ttu-id="26f5a-107">Bu makaledeki Hello bilgiler geçiş toohello sonra Microsoft İzleme Aracısı Güvenlik Merkezi işlevlerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="26f5a-107">hello information in this article represents Security Center functionality after transition toohello Microsoft Monitoring Agent.</span></span>
>
>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="26f5a-108">Azure Güvenlik Merkezi nedir?</span><span class="sxs-lookup"><span data-stu-id="26f5a-108">What is Azure Security Center?</span></span>
 <span data-ttu-id="26f5a-109">Güvenlik Merkezi engellemek, algılamanıza ve Artırılmış görünürlük aracılığıyla toothreats hello Azure kaynaklarınızın güvenliğini denetlemenize yanıtlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="26f5a-109">Security Center helps you prevent, detect, and respond toothreats with increased visibility into and control over hello security of your Azure resources.</span></span> <span data-ttu-id="26f5a-110">Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.</span><span class="sxs-lookup"><span data-stu-id="26f5a-110">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

## <a name="key-capabilities"></a><span data-ttu-id="26f5a-111">Temel işlevler</span><span class="sxs-lookup"><span data-stu-id="26f5a-111">Key capabilities</span></span>
 <span data-ttu-id="26f5a-112">Güvenlik Merkezi, kullanımı kolay ve etkili tehdit tooAzure içinde yerleşik olan önleme, saptama ve yanıt özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="26f5a-112">Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in tooAzure.</span></span> <span data-ttu-id="26f5a-113">Temel işlevler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="26f5a-113">Key capabilities are:</span></span>

| <span data-ttu-id="26f5a-114">Aşama</span><span class="sxs-lookup"><span data-stu-id="26f5a-114">Stage</span></span> | <span data-ttu-id="26f5a-115">Özellik</span><span class="sxs-lookup"><span data-stu-id="26f5a-115">Capability</span></span> |
| --- | --- |
| <span data-ttu-id="26f5a-116">Önleme</span><span class="sxs-lookup"><span data-stu-id="26f5a-116">Prevent</span></span> |<span data-ttu-id="26f5a-117">İzleyiciler, ayrıca Azure kaynaklarınızın güvenlik durumunu hello</span><span class="sxs-lookup"><span data-stu-id="26f5a-117">Monitors hello security state of your Azure resources</span></span> |
| <span data-ttu-id="26f5a-118">Önleme</span><span class="sxs-lookup"><span data-stu-id="26f5a-118">Prevent</span></span> | <span data-ttu-id="26f5a-119">Şirketinizin güvenlik gereksinimlerine, hello tür kullanın ve verilerinizin duyarlılığına hello uygulamaları, Azure aboneliklerinize için ilkeler tanımlar</span><span class="sxs-lookup"><span data-stu-id="26f5a-119">Defines policies for your Azure subscriptions based on your company’s security requirements, hello types of applications that you use, and hello sensitivity of your data</span></span> |
| <span data-ttu-id="26f5a-120">Önleme</span><span class="sxs-lookup"><span data-stu-id="26f5a-120">Prevent</span></span> | <span data-ttu-id="26f5a-121">İlke temelli kullandığı güvenlik önerileri tooguide hizmet sahiplerini hello süreci uygulama gerekli denetimleri</span><span class="sxs-lookup"><span data-stu-id="26f5a-121">Uses policy-driven security recommendations tooguide service owners through hello process of implementing needed controls</span></span> |
| <span data-ttu-id="26f5a-122">Önleme</span><span class="sxs-lookup"><span data-stu-id="26f5a-122">Prevent</span></span> | <span data-ttu-id="26f5a-123">Microsoft ve ortaklarından güvenlik hizmetlerini ve gereçlerini hızlı bir şekilde dağıtır</span><span class="sxs-lookup"><span data-stu-id="26f5a-123">Rapidly deploys security services and appliances from Microsoft and partners</span></span> |
| <span data-ttu-id="26f5a-124">Algılama</span><span class="sxs-lookup"><span data-stu-id="26f5a-124">Detect</span></span> |<span data-ttu-id="26f5a-125">Azure kaynaklarını, hello ağ ve kötü amaçlı yazılımdan koruma programları ve güvenlik duvarları gibi iş ortağı çözümlerinden güvenlik verilerini analiz eder ve otomatik olarak toplar</span><span class="sxs-lookup"><span data-stu-id="26f5a-125">Automatically collects and analyzes security data from your Azure resources, hello network, and partner solutions like antimalware programs and firewalls</span></span> |
| <span data-ttu-id="26f5a-126">Algılama</span><span class="sxs-lookup"><span data-stu-id="26f5a-126">Detect</span></span> | <span data-ttu-id="26f5a-127">Microsoft ürünleri ve Hizmetleri, Microsoft dijital Suçlar birimi (DCU), hello hello Microsoft Güvenlik Yanıt Merkezi (MSRC)'ten ve dış akışların kullandığı genel tehdit</span><span class="sxs-lookup"><span data-stu-id="26f5a-127">Uses global threat intelligence from Microsoft products and services, hello Microsoft Digital Crimes Unit (DCU), hello Microsoft Security Response Center (MSRC), and external feeds</span></span> |
| <span data-ttu-id="26f5a-128">Algılama</span><span class="sxs-lookup"><span data-stu-id="26f5a-128">Detect</span></span> | <span data-ttu-id="26f5a-129">Machine learning ve davranış analizi dahil olmak üzere gelişmiş analizler uygular</span><span class="sxs-lookup"><span data-stu-id="26f5a-129">Applies advanced analytics, including machine learning and behavioral analysis</span></span> |
| <span data-ttu-id="26f5a-130">Yanıtlama</span><span class="sxs-lookup"><span data-stu-id="26f5a-130">Respond</span></span> |<span data-ttu-id="26f5a-131">Öncelikli güvenlik olayları/uyarıları sağlar</span><span class="sxs-lookup"><span data-stu-id="26f5a-131">Provides prioritized security incidents/alerts</span></span> |
| <span data-ttu-id="26f5a-132">Yanıtlama</span><span class="sxs-lookup"><span data-stu-id="26f5a-132">Respond</span></span> | <span data-ttu-id="26f5a-133">Merhaba kaynağı hello saldırı ve etkilenen kaynakları Öngörüler sunar</span><span class="sxs-lookup"><span data-stu-id="26f5a-133">Offers insights into hello source of hello attack and impacted resources</span></span> |
| <span data-ttu-id="26f5a-134">Yanıtlama</span><span class="sxs-lookup"><span data-stu-id="26f5a-134">Respond</span></span> | <span data-ttu-id="26f5a-135">Toostop geçerli saldırıyı hello ve gelecekteki saldırıların önlenmesine yardımcı yöntemler önerir</span><span class="sxs-lookup"><span data-stu-id="26f5a-135">Suggests ways toostop hello current attack and help prevent future attacks</span></span> |

## <a name="introductory-walkthrough"></a><span data-ttu-id="26f5a-136">Tanıtıcı kılavuz</span><span class="sxs-lookup"><span data-stu-id="26f5a-136">Introductory walkthrough</span></span>

> [!NOTE]
> <span data-ttu-id="26f5a-137">Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="26f5a-137">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="26f5a-138">Bu belge hakkında adım adım kılavuz değildir.</span><span class="sxs-lookup"><span data-stu-id="26f5a-138">This document is not a step-by-step guide.</span></span>
>
>

 <span data-ttu-id="26f5a-139">Merhaba Güvenlik Merkezi erişim [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="26f5a-139">You access Security Center from hello [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="26f5a-140">[Toohello Portalı'nda oturum](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="26f5a-140">[Sign in toohello portal](https://portal.azure.com).</span></span> <span data-ttu-id="26f5a-141">Merhaba ana portal menüsünün altında toohello kaydırma **Güvenlik Merkezi** seçeneği veya select hello **Güvenlik Merkezi** toohello portalı panosunun önceden sabitlenmiş döşeme.</span><span class="sxs-lookup"><span data-stu-id="26f5a-141">Under hello main portal menu, scroll toohello **Security Center** option or select hello **Security Center** tile that you previously pinned toohello portal dashboard.</span></span>

![Azure portalında güvenlik kutucuğu][1]

<span data-ttu-id="26f5a-143">Güvenlik Merkezi'nde güvenlik ilkelerini ayarlayabilir, güvenlik yapılandırmalarını izleyebilir ve güvenlik uyarıları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26f5a-143">From Security Center, you can set security policies, monitor security configurations, and view security alerts.</span></span>

### <a name="security-policies"></a><span data-ttu-id="26f5a-144">Güvenlik ilkeleri</span><span class="sxs-lookup"><span data-stu-id="26f5a-144">Security policies</span></span>
<span data-ttu-id="26f5a-145">Tooyour şirketinizin güvenlik gereksinimlerine göre Azure aboneliklerinize ilkeleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26f5a-145">You can define policies for your Azure subscriptions according tooyour company's security requirements.</span></span> <span data-ttu-id="26f5a-146">Ayrıca bunları kullanmakta olduğunuz uygulama toohello tür veya hello veri toohello duyarlılığını her abonelik uyarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26f5a-146">You can also tailor them toohello types of applications you're using or toohello sensitivity of hello data in each subscription.</span></span> <span data-ttu-id="26f5a-147">Örneğin, geliştirme veya test etme için kullanılan kaynaklar, üretim uygulamaları için kullanılanlardan farklı güvenlik gereksinimlerine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="26f5a-147">For example, resources used for development or testing may have different security requirements than those used for production applications.</span></span> <span data-ttu-id="26f5a-148">Benzer şekilde, PII gibi düzenlenen veriler içeren uygulamalar, daha yüksek bir güvenlik düzeyi gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="26f5a-148">Likewise, applications with regulated data like PII may require a higher level of security.</span></span>

> [!NOTE]
> <span data-ttu-id="26f5a-149">toomodify bir güvenlik ilkesi Güvenlik Yöneticisi veya hello aboneliğinin sahibi veya Katılımcısı olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="26f5a-149">toomodify a security policy, you must be a Security Administrator or hello subscription's Owner or Contributor.</span></span> <span data-ttu-id="26f5a-150">rolleri ve Güvenlik Merkezi, izin verilen eylemleri hakkında daha fazla toolearn bkz [Azure Güvenlik Merkezi'nde izinleri](security-center-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="26f5a-150">toolearn more about roles and allowed actions in Security Center, see [Permissions in Azure Security Center](security-center-permissions.md).</span></span>
>
>

<span data-ttu-id="26f5a-151">Merhaba üzerinde **Güvenlik Merkezi** dikey penceresinde, select hello **İlkesi** Abonelikleriniz ve kaynak grupları listesi için.</span><span class="sxs-lookup"><span data-stu-id="26f5a-151">On hello **Security Center** blade, select hello **Policy** tile for a list of your subscriptions and resource groups.</span></span>   

![Güvenlik Merkezi dikey penceresi][2]

<span data-ttu-id="26f5a-153">Merhaba üzerinde **Güvenlik İlkesi** dikey penceresinde bir abonelik tooview hello ilkesi ayrıntıları'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="26f5a-153">On hello **Security policy** blade, select a subscription tooview hello policy details.</span></span>

<span data-ttu-id="26f5a-154">**Veri toplama** bir güvenlik ilkesi için veri toplama sağlar.</span><span class="sxs-lookup"><span data-stu-id="26f5a-154">**Data collection** enables data collection for a security policy.</span></span> <span data-ttu-id="26f5a-155">Etkinleştirildiğinde şunlar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="26f5a-155">Enabling provides:</span></span>

* <span data-ttu-id="26f5a-156">Sanal makineler (VM'ler), günlük tüm tarama güvenlik izleme ve öneriler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="26f5a-156">Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.</span></span>
* <span data-ttu-id="26f5a-157">Analiz ve tehdit algılama için güvenlik olaylarının toplanması.</span><span class="sxs-lookup"><span data-stu-id="26f5a-157">Collection of security events for analysis and threat detection.</span></span>

> [!NOTE]
> <span data-ttu-id="26f5a-158">Veri toplama hello abonelik düzeyinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="26f5a-158">Data collection is configured at hello subscription level.</span></span>
>
>

<span data-ttu-id="26f5a-159">Seçin **önleme İlkesi** tooopen hello **önleme İlkesi** dikey.</span><span class="sxs-lookup"><span data-stu-id="26f5a-159">Select **Prevention policy** tooopen hello **Prevention policy** blade.</span></span> <span data-ttu-id="26f5a-160">**İçin önerileri göster** hello kaynakları hello abonelik içindeki hello güvenlik gereksinimlerine göre toosee istediğiniz toomonitor ve hello önerileri istediğiniz hello güvenlik denetimlerini seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="26f5a-160">**Show recommendations for** lets you choose hello security controls that you want toomonitor and hello recommendations that you want toosee based on hello security needs of hello resources within hello subscription.</span></span>

### <a name="security-recommendations"></a><span data-ttu-id="26f5a-161">Güvenlik önerileri</span><span class="sxs-lookup"><span data-stu-id="26f5a-161">Security recommendations</span></span>
 <span data-ttu-id="26f5a-162">Güvenlik Merkezi, Azure kaynaklarını tooidentify olası güvenlik açıklarını hello güvenlik durumunu çözümler.</span><span class="sxs-lookup"><span data-stu-id="26f5a-162">Security Center analyzes hello security state of your Azure resources tooidentify potential security vulnerabilities.</span></span> <span data-ttu-id="26f5a-163">Öneriler listesi gerekli denetimlerin yapılandırılması hello işleminde size rehberlik eder.</span><span class="sxs-lookup"><span data-stu-id="26f5a-163">A list of recommendations guides you through hello process of configuring needed controls.</span></span> <span data-ttu-id="26f5a-164">Örneklere şunlar dahildir:</span><span class="sxs-lookup"><span data-stu-id="26f5a-164">Examples include:</span></span>

* <span data-ttu-id="26f5a-165">Kötü amaçlı yazılımdan koruma sağlama toohelp tanımlamak ve kötü amaçlı yazılım kaldırma</span><span class="sxs-lookup"><span data-stu-id="26f5a-165">Provisioning antimalware toohelp identify and remove malicious software</span></span>
* <span data-ttu-id="26f5a-166">Ağ güvenlik gruplarını ve kurallarını toocontrol trafiği tooVMs yapılandırma</span><span class="sxs-lookup"><span data-stu-id="26f5a-166">Configuring network security groups and rules toocontrol traffic tooVMs</span></span>
* <span data-ttu-id="26f5a-167">Web uygulaması güvenlik duvarı toohelp, web uygulamalarınızı hedefleyen saldırılara karşı korumaya sağlama</span><span class="sxs-lookup"><span data-stu-id="26f5a-167">Provisioning of web application firewalls toohelp defend against attacks that target your web applications</span></span>
* <span data-ttu-id="26f5a-168">Eksik sistem güncelleştirmelerini dağıtma</span><span class="sxs-lookup"><span data-stu-id="26f5a-168">Deploying missing system updates</span></span>
* <span data-ttu-id="26f5a-169">Önerilen taban çizgileri hello eşleşmeyen işletim sistemi yapılandırmalarını ele alma</span><span class="sxs-lookup"><span data-stu-id="26f5a-169">Addressing OS configurations that do not match hello recommended baselines</span></span>

<span data-ttu-id="26f5a-170">Merhaba tıklatın **önerileri** için öneriler listesi.</span><span class="sxs-lookup"><span data-stu-id="26f5a-170">Click hello **Recommendations** tile for a list of recommendations.</span></span> <span data-ttu-id="26f5a-171">Her öneri tooview ek bilgiler veya tootake eylem tooresolve hello Çıkış'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="26f5a-171">Click each recommendation tooview additional information or tootake action tooresolve hello issue.</span></span>

![Azure Güvenlik Merkezi'nde güvenlik önerileri][5]

### <a name="security-state-of-azure-resources"></a><span data-ttu-id="26f5a-173">Azure kaynakların güvenlik durumu</span><span class="sxs-lookup"><span data-stu-id="26f5a-173">Security state of Azure resources</span></span>
<span data-ttu-id="26f5a-174">Merhaba **önleme** başlangıç Panosu bölümü hello VM'ler, web uygulamaları ve diğer kaynakları da dahil olmak üzere kaynak türüne göre hello ortamın genel güvenlik duruşunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="26f5a-174">hello **Prevention** section of hello dashboard shows hello overall security posture of hello environment by resource type, including VMs, web applications, and other resources.</span></span>   

<span data-ttu-id="26f5a-175">Altında bir kaynak türü seçin **önleme** tooview tanımlanan olası güvenlik açıkları listesi dahil olmak üzere daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="26f5a-175">Select a resource type under **Prevention** tooview more information, including a list of any potential security vulnerabilities that have been identified.</span></span> <span data-ttu-id="26f5a-176">(**İşlem** hello aşağıdaki örnekte seçilir.)</span><span class="sxs-lookup"><span data-stu-id="26f5a-176">(**Compute** is selected in hello example below.)</span></span>

![Kaynak durumu kutucuğu][6]

### <a name="security-alerts"></a><span data-ttu-id="26f5a-178">Güvenlik uyarıları</span><span class="sxs-lookup"><span data-stu-id="26f5a-178">Security alerts</span></span>
 <span data-ttu-id="26f5a-179">Güvenlik Merkezi otomatik olarak toplar, analiz eder ve Azure kaynakları, hello ağ ve kötü amaçlı yazılımdan koruma programları ve güvenlik duvarları gibi iş ortağı çözümlerinden günlük verilerini tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="26f5a-179">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and partner solutions like antimalware programs and firewalls.</span></span> <span data-ttu-id="26f5a-180">Tehditler algılandığında bir güvenlik uyarısı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="26f5a-180">When threats are detected, a security alert is created.</span></span> <span data-ttu-id="26f5a-181">Örneklere şunların algılanması dahildir:</span><span class="sxs-lookup"><span data-stu-id="26f5a-181">Examples include detection of:</span></span>

* <span data-ttu-id="26f5a-182">Bilinen kötü amaçlı IP adresleri ile iletişim kuran tehlikeye atılmış VM'ler</span><span class="sxs-lookup"><span data-stu-id="26f5a-182">Compromised VMs communicating with known malicious IP addresses</span></span>
* <span data-ttu-id="26f5a-183">Windows hata raporlama kullanılarak algılanan gelişmiş kötü amaçlı yazılım</span><span class="sxs-lookup"><span data-stu-id="26f5a-183">Advanced malware detected by using Windows error reporting</span></span>
* <span data-ttu-id="26f5a-184">Sanal makineleri karşı deneme yanılma saldırıları</span><span class="sxs-lookup"><span data-stu-id="26f5a-184">Brute force attacks against VMs</span></span>
* <span data-ttu-id="26f5a-185">Tümleşik kötü amaçlı yazılımdan koruma programlarından ve güvenlik duvarlarından güvenlik uyarıları</span><span class="sxs-lookup"><span data-stu-id="26f5a-185">Security alerts from integrated antimalware programs and firewalls</span></span>

<span data-ttu-id="26f5a-186">Tıklatmak hello **güvenlik uyarıları** döşeme öncelikli uyarıların bir listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="26f5a-186">Clicking hello **Security alerts** tile displays a list of prioritized alerts.</span></span>

![Güvenlik uyarıları][7]

<span data-ttu-id="26f5a-188">Bir uyarıyı seçtiğinizde gösterilir hello saldırı ve ilgili öneriler hakkında daha fazla bilgi tooremediate onu.</span><span class="sxs-lookup"><span data-stu-id="26f5a-188">Selecting an alert shows more information about hello attack and suggestions for how tooremediate it.</span></span>

![Güvenlik uyarısı ayrıntıları][8]

### <a name="partner-solutions"></a><span data-ttu-id="26f5a-190">İş ortağı çözümleri</span><span class="sxs-lookup"><span data-stu-id="26f5a-190">Partner solutions</span></span>
<span data-ttu-id="26f5a-191">Merhaba **iş ortağı çözümleri** Azure aboneliğinizle tümleşik iş ortağı çözümlerinizin bakışta hello güvenlik durumunu izleme kutucuğu sağlar.</span><span class="sxs-lookup"><span data-stu-id="26f5a-191">hello **Partner solutions** tile lets you monitor at a glance hello security state of your partner solutions integrated with your Azure subscription.</span></span> <span data-ttu-id="26f5a-192">Güvenlik Merkezi hello çözümlerden gelen uyarıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="26f5a-192">Security Center displays alerts coming from hello solutions.</span></span>

<span data-ttu-id="26f5a-193">Select hello **iş ortağı çözümleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="26f5a-193">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="26f5a-194">Tüm bağlı iş ortağı çözümlerinin listesini görüntüleyen bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="26f5a-194">A blade opens displaying a list of all connected partner solutions.</span></span>

![İş ortağı çözümleri][9]

## <a name="get-started"></a><span data-ttu-id="26f5a-196">başlarken</span><span class="sxs-lookup"><span data-stu-id="26f5a-196">Get started</span></span>
<span data-ttu-id="26f5a-197">Güvenlik Merkezi ile çalışmaya tooget abonelik tooMicrosoft Azure gerekir.</span><span class="sxs-lookup"><span data-stu-id="26f5a-197">tooget started with Security Center, you need a subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="26f5a-198">Güvenlik Merkezi, Azure aboneliğiniz ile etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="26f5a-198">Security Center is enabled with your Azure subscription.</span></span> <span data-ttu-id="26f5a-199">Bir aboneliğiniz yoksa [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26f5a-199">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

 <span data-ttu-id="26f5a-200">Merhaba Güvenlik Merkezi erişim [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span><span class="sxs-lookup"><span data-stu-id="26f5a-200">You access Security Center from hello [Azure portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="26f5a-201">Merhaba bkz [portal belgeleri](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="26f5a-201">See hello [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn more.</span></span>

<span data-ttu-id="26f5a-202">[Azure Güvenlik Merkezi ile çalışmaya başlama](security-center-get-started.md) hızlı bir şekilde hello güvenlik izleme ve ilke yönetimi bileşenleri Güvenlik Merkezi sırasında size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="26f5a-202">[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through hello security-monitoring and policy-management components of Security Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26f5a-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="26f5a-203">Next steps</span></span>
<span data-ttu-id="26f5a-204">Bu belgede, sunulan tooSecurity Merkezi, önemli işlevleri ve nasıl tooget başlatılacağını yoktu.</span><span class="sxs-lookup"><span data-stu-id="26f5a-204">In this document, you were introduced tooSecurity Center, its key capabilities, and how tooget started.</span></span> <span data-ttu-id="26f5a-205">toolearn daha kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="26f5a-205">toolearn more, see hello following resources:</span></span>

* <span data-ttu-id="26f5a-206">[Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) — öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="26f5a-206">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="26f5a-207">[Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) — nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="26f5a-207">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="26f5a-208">[Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) — nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="26f5a-208">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="26f5a-209">[Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) — öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.</span><span class="sxs-lookup"><span data-stu-id="26f5a-209">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="26f5a-210">[Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) — nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="26f5a-210">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="26f5a-211">[Azure Güvenlik Merkezi veri güvenliği](security-center-data-security.md) -verilerin yönetilmesi ve diğer Güvenlik Merkezi'nde korunması nasıl öğrenin.</span><span class="sxs-lookup"><span data-stu-id="26f5a-211">[Azure Security Center data security](security-center-data-security.md) - Learn how data is managed and safeguarded in Security Center.</span></span>
* <span data-ttu-id="26f5a-212">[Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26f5a-212">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="26f5a-213">[Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) — hello en son Azure güvenlik haberlerini ve bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="26f5a-213">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

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
