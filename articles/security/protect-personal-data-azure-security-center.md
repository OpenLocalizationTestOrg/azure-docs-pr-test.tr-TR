---
title: "Azure Güvenlik Merkezi ile kişisel veriler aaaProtect | Microsoft Docs"
description: "Azure Güvenlik Merkezi'ni kullanarak kişisel verilerini koruma"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="a6768-103">Kişisel veriler ihlallerini ve saldırılarından korumak: Azure Güvenlik Merkezi</span><span class="sxs-lookup"><span data-stu-id="a6768-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="a6768-104">Bu makalede, nasıl toouse Azure Güvenlik Merkezi tooprotect kişisel verileri ihlallerini anlamanıza yardımcı olur ve saldırıları.</span><span class="sxs-lookup"><span data-stu-id="a6768-104">This article will help you understand how toouse Azure Security Center tooprotect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="a6768-105">Senaryo</span><span class="sxs-lookup"><span data-stu-id="a6768-105">Scenario</span></span> 

<span data-ttu-id="a6768-106">Merhaba Amerika Birleşik Devletleri, yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello İngiliz Adaları arasında yanı sıra hello Akdeniz ve Baltık seas genişletmektedir.</span><span class="sxs-lookup"><span data-stu-id="a6768-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="a6768-107">toohelp bu çaba içinde İtalya, Almanya, Danimarka ve hello İngiltere dayanarak birkaç küçük seyahat satırları aldı</span><span class="sxs-lookup"><span data-stu-id="a6768-107">toohelp in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="a6768-108">Merhaba şirket hello bulutta Microsoft Azure toostore şirket verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="a6768-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="a6768-109">Bu adlar, adresler, telefon numarası ve kredi kartı bilgileri gibi kişisel olarak tanımlanabilir bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="a6768-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="a6768-110">İnsan Kaynakları bilgi ayrıca gibi içerir:</span><span class="sxs-lookup"><span data-stu-id="a6768-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="a6768-111">Adresler</span><span class="sxs-lookup"><span data-stu-id="a6768-111">Addresses</span></span>
- <span data-ttu-id="a6768-112">Telefon numaraları</span><span class="sxs-lookup"><span data-stu-id="a6768-112">Phone numbers</span></span>
- <span data-ttu-id="a6768-113">Vergi kimlik numaraları</span><span class="sxs-lookup"><span data-stu-id="a6768-113">Tax identification numbers</span></span>
- <span data-ttu-id="a6768-114">Sağlık bilgileri</span><span class="sxs-lookup"><span data-stu-id="a6768-114">Medical information</span></span>

<span data-ttu-id="a6768-115">Merhaba seyahat satır de ödül ve bağlılık programı üyelerinin büyük bir veritabanı tutar.</span><span class="sxs-lookup"><span data-stu-id="a6768-115">hello cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="a6768-116">Şirket çalışanları erişim hello ağdan hello şirketin şubelere ve seyahat aracılar bulunan Merhaba Dünya toosome şirket kaynaklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="a6768-116">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>
<span data-ttu-id="a6768-117">Kişisel veriler hello ağ üzerinden bu konumları ve hello Microsoft Veri Merkezi arasında geçen.</span><span class="sxs-lookup"><span data-stu-id="a6768-117">Personal data travels across hello network between these locations and hello Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="a6768-118">Sorun bildirimi</span><span class="sxs-lookup"><span data-stu-id="a6768-118">Problem statement</span></span>

<span data-ttu-id="a6768-119">Hello Azure kaynaklarını saldırılar hello tehlikesi endişe bir şirkettir.</span><span class="sxs-lookup"><span data-stu-id="a6768-119">hello company is concerned about hello threat of attacks on their Azure resources.</span></span> <span data-ttu-id="a6768-120">Müşterilerin ve çalışanların kişisel veriler toounauthorized kişi tooprevent riskini isterler.</span><span class="sxs-lookup"><span data-stu-id="a6768-120">They want tooprevent exposure of customers’ and employees’ personal data toounauthorized persons.</span></span> <span data-ttu-id="a6768-121">Hem önleme ve yanıt/düzeltme işlemi, hem de bulut kaynakları bir etkili şekilde toomonitor hello devam eden güvenlik kılavuzu isterler.</span><span class="sxs-lookup"><span data-stu-id="a6768-121">They want guidance on both prevention and response/remediation, as well as an effective way toomonitor hello ongoing security of their cloud resources.</span></span>
<span data-ttu-id="a6768-122">Güçlü bir günümüzün karmaşık ve organize saldırganlara karşı savunma hattı ihtiyaç duyar.</span><span class="sxs-lookup"><span data-stu-id="a6768-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="a6768-123">Şirket hedefi</span><span class="sxs-lookup"><span data-stu-id="a6768-123">Company goal</span></span>

<span data-ttu-id="a6768-124">Merhaba şirketin hedeflerine müşterilerin ve çalışanların kişisel verilerin tooensure hello gizliliği tehditlerine karşı koruma tarafından biridir.</span><span class="sxs-lookup"><span data-stu-id="a6768-124">One of hello company’s goals is tooensure hello privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="a6768-125">İhlali toomitigate toosigns etkisi hello hemen hedeflerine toorespond biridir.</span><span class="sxs-lookup"><span data-stu-id="a6768-125">One of their goals is toorespond immediately toosigns of breach toomitigate hello impact.</span></span> <span data-ttu-id="a6768-126">Geçerli güvenlik durumunu tooassess hello şekilde gerektirir, savunmasız yapılandırmaları tanımlamak ve düzeltmek.</span><span class="sxs-lookup"><span data-stu-id="a6768-126">It requires a way tooassess hello current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="a6768-127">Çözümler</span><span class="sxs-lookup"><span data-stu-id="a6768-127">Solutions</span></span>

<span data-ttu-id="a6768-128">Microsoft Azure Güvenlik Merkezi (ASC) bir tümleşik güvenlik izleme ve ilke yönetimi çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6768-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="a6768-129">Bu, kullanımı kolay ve etkili tehdit önleme, saptama ve yanıtlama işlevlerini sunar.</span><span class="sxs-lookup"><span data-stu-id="a6768-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="a6768-130">Önleme</span><span class="sxs-lookup"><span data-stu-id="a6768-130">Prevention</span></span>

<span data-ttu-id="a6768-131">ASC tooset güvenlik ilkeleri etkinleştirerek açıklarına, yalnızca zaman erişim sağlamak ve güvenlik önerilerini uygulama yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a6768-131">ASC helps you prevent breaches by enabling you tooset security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="a6768-132">Bir güvenlik ilkesi hello belirtilen hello içindeki kaynaklar için önerilen denetimleri kümesini tanımlayan abonelik.</span><span class="sxs-lookup"><span data-stu-id="a6768-132">A security policy defines hello set of controls recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="a6768-133">Tam zamanında erişim gelen trafiği tooyour Azure VM'ler, etkilenme tooattacks azaltma aşağı kullanılan toolock olabilir.</span><span class="sxs-lookup"><span data-stu-id="a6768-133">Just in time access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks.</span></span> <span data-ttu-id="a6768-134">Güvenlik önerileri hello Azure kaynaklarınızın güvenlik durumunu çözümledikten sonra ASC tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a6768-134">Security recommendations are created by ASC after analyzing hello security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="a6768-135">Güvenlik ilkeleri ASC nasıl ayarlarım?</span><span class="sxs-lookup"><span data-stu-id="a6768-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="a6768-136">Her bir abonelik için güvenlik ilkeleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6768-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="a6768-137">bir güvenlik ilkesi toomodify sahibi veya katkıda bu aboneliğin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6768-137">toomodify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="a6768-138">Hello Azure portalı, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="a6768-138">In hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="a6768-139">Seçin **İlkesi** hello ASC panosunda.</span><span class="sxs-lookup"><span data-stu-id="a6768-139">Select **Policy** in hello ASC dashboard.</span></span>

2. <span data-ttu-id="a6768-140">Tooenable hello İlkesi istediğiniz hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="a6768-140">Select hello subscription on which you want tooenable hello policy.</span></span>

3. <span data-ttu-id="a6768-141">Seçin **önleme İlkesi** abonelik başına tooconfigure ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="a6768-141">Choose **Prevention policy** tooconfigure policies per subscription.</span></span> <span data-ttu-id="a6768-142">**Sanal makinelerden veri toplama** çok ayarlanmalıdır**üzerinde.**</span><span class="sxs-lookup"><span data-stu-id="a6768-142">**Collect data from virtual machines** should be set too**On.**</span></span>

4. <span data-ttu-id="a6768-143">Merhaba, **önleme İlkesi** seçenekleri, select **üzerinde** hello abonelik için uygun olan tooenable hello güvenlik önerileri.</span><span class="sxs-lookup"><span data-stu-id="a6768-143">In hello **Prevention policy** options, select **On** tooenable hello security recommendations that are relevant for hello subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="a6768-144">Daha ayrıntılı yönergeler ve etkinleştirilebilir hello İlkesi önerileri bir açıklaması için bkz: [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="a6768-144">For more detailed instructions and an explanation of each of hello policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="a6768-145">Zaman erişim (JIT) nasıl sadece yapılandırırım?</span><span class="sxs-lookup"><span data-stu-id="a6768-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="a6768-146">JIT etkinleştirilmişse, Güvenlik Merkezi bir NSG kuralı oluşturarak Azure VM'ler gelen trafiği tooyour kilitler.</span><span class="sxs-lookup"><span data-stu-id="a6768-146">When JIT is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="a6768-147">Merhaba bağlantı noktalarını seçmek aşağı gelen trafiği üzerinde hello VM toowhich kilitlenir.</span><span class="sxs-lookup"><span data-stu-id="a6768-147">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="a6768-148">toouse JIT erişmek için aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="a6768-148">toouse JIT access, do hello following:</span></span>

1. <span data-ttu-id="a6768-149">Select hello **zaman VM erişim döşemesinin sadece** hello ASC dikey.</span><span class="sxs-lookup"><span data-stu-id="a6768-149">Select hello **Just in time VM access tile** on hello ASC blade.</span></span>

2. <span data-ttu-id="a6768-150">Select hello **önerilen** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a6768-150">Select hello **Recommended** tab.</span></span>

3. <span data-ttu-id="a6768-151">Altında **VM'ler**, hello VM'ler tooenable istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="a6768-151">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="a6768-152">Bir onay işareti sonraki tooa VM koyar.</span><span class="sxs-lookup"><span data-stu-id="a6768-152">This puts a checkmark next tooa VM.</span></span> 
4. <span data-ttu-id="a6768-153">Seçin **etkinleştirmek JIT** vm'lerde.</span><span class="sxs-lookup"><span data-stu-id="a6768-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="a6768-154">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="a6768-154">Select **Save**.</span></span>

<span data-ttu-id="a6768-155">Daha sonra JIT için etkinleştirilen ASC önerir hello varsayılan bağlantı noktalarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6768-155">Then you can see hello default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="a6768-156">Ayrıca, ekleyebilir ve tooenable hello yalnızca zaman çözümü istediğiniz yeni bir bağlantı noktası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a6768-156">You can also add and configure a new port on which you want tooenable hello just in time solution.</span></span> <span data-ttu-id="a6768-157">Merhaba **saat VM erişimi hemen** hello Güvenlik Merkezi parçasında JIT erişimi için yapılandırılan VM hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6768-157">hello **Just in time VM access** tile in hello Security Center shows hello number of VMs configured for JIT access.</span></span> <span data-ttu-id="a6768-158">Ayrıca, geçen hafta hello yapılan onaylanan erişim istekleri hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6768-158">It also shows hello number of approved access requests made in hello last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="a6768-159">Yönergeler için toodo bunu ve zaman Access'te sadece hakkında ek bilgi için bkz [tam zamanında kullanarak sanal makine erişimini yönetme.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="a6768-159">For instructions on how toodo this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="a6768-160">ASC güvenlik önerileri nasıl uygulansın mı?</span><span class="sxs-lookup"><span data-stu-id="a6768-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="a6768-161">Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde öneriler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a6768-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="a6768-162">Merhaba önerileri gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk.</span><span class="sxs-lookup"><span data-stu-id="a6768-162">hello recommendations guide you through hello process of configuring hello needed controls.</span></span> 
1. <span data-ttu-id="a6768-163">Select hello **önerileri** döşeme hello ASC Panoda.</span><span class="sxs-lookup"><span data-stu-id="a6768-163">Select hello **Recommendations** tile on hello ASC dashboard.</span></span>

2. <span data-ttu-id="a6768-164">Her satır bir öneri temsil ettiği bir tablo biçiminde gösterilen hello önerileri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="a6768-164">View hello recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="a6768-165">toofilter önerileri seçin **filtre** ve toosee istediğiniz hello önem ve durum değerleri seçin.</span><span class="sxs-lookup"><span data-stu-id="a6768-165">toofilter recommendations, select **Filter** and select hello severity and state values you wish toosee.</span></span>

4. <span data-ttu-id="a6768-166">toodismiss geçerli olmayan bir öneri, sağ tıklatın ve seçin **atla.**</span><span class="sxs-lookup"><span data-stu-id="a6768-166">toodismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="a6768-167">Hangi öneri önce uygulanması gereken değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="a6768-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="a6768-168">Öncelik sırasına göre Hello önerileri geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="a6768-168">Apply hello recommendations in order of priority.</span></span>

<span data-ttu-id="a6768-169">Olası önerileri ve nasıl kılavuzlarına listesi için bkz tooapply her [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="a6768-169">For a list of possible recommendations and walk-throughs on how tooapply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="a6768-170">Algılama ile yanıtı</span><span class="sxs-lookup"><span data-stu-id="a6768-170">Detection and Response</span></span>

<span data-ttu-id="a6768-171">Bir tehdit algılandıktan sonra toorespond mümkün olan en kısa sürede istediğiniz şekilde algılama ile yanıtı birlikte gidin.</span><span class="sxs-lookup"><span data-stu-id="a6768-171">Detection and response go together, as you want toorespond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="a6768-172">ASC tehdit algılama, Azure kaynaklarını, hello ağ ve bağlı iş ortağı çözümlerinden güvenlik bilgileri otomatik olarak toplayarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="a6768-172">ASC threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="a6768-173">Saldırganlar yeni ve giderek karmaşık ortaya çıkardıkça ASC kendi algılama algoritmalarını hızlı bir şekilde güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6768-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="a6768-174">Tehdit algılama ASC'ın nasıl çalıştığı hakkında daha ayrıntılı bilgi için bkz: [Azure Güvenlik Merkezi algılama özellikleri](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="a6768-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="a6768-175">Nasıl yönetmek ve toosecurity uyarıları yanıt?</span><span class="sxs-lookup"><span data-stu-id="a6768-175">How do I manage and respond toosecurity alerts?</span></span>

<span data-ttu-id="a6768-176">Öncelikli güvenlik uyarıları listesi hello birlikte Güvenlik Merkezi'nde gösterilen tooquickly gereksinim duyduğunuz bilgileri hello sorunu araştırın.</span><span class="sxs-lookup"><span data-stu-id="a6768-176">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem.</span></span> <span data-ttu-id="a6768-177">Güvenlik Merkezi, ayrıca nasıl için öneriler içerir tooremediate saldırının.</span><span class="sxs-lookup"><span data-stu-id="a6768-177">Security Center also includes recommendations for how tooremediate an attack.</span></span> <span data-ttu-id="a6768-178">Güvenlik Uyarıları, aşağıdaki hello yapmak toomanage:</span><span class="sxs-lookup"><span data-stu-id="a6768-178">toomanage your security alerts, do hello following:</span></span>

1. <span data-ttu-id="a6768-179">Select hello **güvenlik uyarıları** döşeme hello ASC panosunda.</span><span class="sxs-lookup"><span data-stu-id="a6768-179">Select hello **Security alerts** tile in hello ASC dashboard.</span></span> <span data-ttu-id="a6768-180">Her uyarı ayrıntılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6768-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="a6768-181">Tarih, durum ve önem derecesi göre toofilter uyarıları seçin **filtre** ve toosee istediğiniz hello değerleri seçin.</span><span class="sxs-lookup"><span data-stu-id="a6768-181">toofilter alerts based on date, state, and severity, select **Filter** and then select hello values you want toosee.</span></span>

3. <span data-ttu-id="a6768-182">toorespond tooan uyarı, onu seçin, hello bilgileri gözden geçirin ve sonra Saldırıya uğrayan hello kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="a6768-182">toorespond tooan alert, select it and review hello information, then select hello resource that was attacked.</span></span>

4. <span data-ttu-id="a6768-183">Merhaba, **açıklama** alan, önerilen düzeltmeyi dahil ayrıntılarını göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a6768-183">In hello **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="a6768-184">Daha ayrıntılı yanıt veren toosecurity uyarılar hakkında yönergeler için bkz: [yönetme ve yanıt toosecurity Azure Güvenlik Merkezi'nde uyarıları.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="a6768-184">For more detailed instructions on responding toosecurity alerts, see [Managing and responding toosecurity alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="a6768-185">Güvenlik Uyarıları araştırırken daha fazla yardım için hello şirket kendi SIEM çözümüyle ASC uyarıları tümleşebilir kullanılarak [Azure günlük tümleştirme](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="a6768-185">For further help in investigating security alerts, hello company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="a6768-186">Güvenlik olayları nasıl yönetebilirim?</span><span class="sxs-lookup"><span data-stu-id="a6768-186">How do I manage security incidents?</span></span>

<span data-ttu-id="a6768-187">ASC bir güvenlik olayı sonlandırma zinciri desenlerle Hizala tüm uyarıların bir kaynak için bir toplama ' dir.</span><span class="sxs-lookup"><span data-stu-id="a6768-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="a6768-188">Bir olay, tooobtain sağlayan hello ilgili uyarıların listesi, her oluşumu hakkında daha fazla bilgi görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6768-188">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="a6768-189">Olaylar, güvenlik uyarıları kutucuğu hello ve dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="a6768-189">Incidents appear in hello Security Alerts tile and blade.</span></span>

<span data-ttu-id="a6768-190">tooreview ve güvenlik olayları yönetmek için aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="a6768-190">tooreview and manage security incidents, do hello following:</span></span>

1. <span data-ttu-id="a6768-191">Select hello **güvenlik uyarıları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="a6768-191">Select hello **Security alerts** tile.</span></span> <span data-ttu-id="a6768-192">bir güvenlik olayı algılanırsa, hello güvenlik uyarıları grafiğin altında görünür.</span><span class="sxs-lookup"><span data-stu-id="a6768-192">if a security incident is detected, it will appear under hello security alerts graph.</span></span> <span data-ttu-id="a6768-193">Diğer uyarılardan farklı bir simge sahip olur.</span><span class="sxs-lookup"><span data-stu-id="a6768-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="a6768-194">Bu güvenlik olayı hakkında daha fazla ayrıntı Hello olay toosee seçin.</span><span class="sxs-lookup"><span data-stu-id="a6768-194">Select hello incident toosee more details about this security incident.</span></span> <span data-ttu-id="a6768-195">Ek ayrıntılar dahil tam açıklamasını, kendi önem derecesi, kendi geçerli durumunda, saldırıya hello kaynak, hello düzeltme adımları hello olay için ve bu olayın eklenmiş olan uyarılar hello.</span><span class="sxs-lookup"><span data-stu-id="a6768-195">Additional details include its full description, its severity, its current state, hello attacked resource, hello remediation steps for hello incident, and hello alerts that were included in this incident.</span></span>

<span data-ttu-id="a6768-196">Toosee filtreleyebilirsiniz **olaylar yalnızca**, **yalnızca uyarıları**, veya **her ikisi de**.</span><span class="sxs-lookup"><span data-stu-id="a6768-196">You can filter toosee **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a><span data-ttu-id="a6768-197">Merhaba tehdit Intelligence rapor nasıl erişirim?</span><span class="sxs-lookup"><span data-stu-id="a6768-197">How do I access hello Threat Intelligence Report?</span></span>

<span data-ttu-id="a6768-198">ASC birden çok kaynakları tooidentify tehditlere karşı bilgileri analiz eder.</span><span class="sxs-lookup"><span data-stu-id="a6768-198">ASC analyzes information from multiple sources tooidentify threats.</span></span> <span data-ttu-id="a6768-199">tooassist olay yanıtlama ekipleri araştırmak ve tehditleri düzeltme, Güvenlik Merkezi algılandı hello tehdit hakkında bilgi içeren bir tehdit Intelligence rapor içerir.</span><span class="sxs-lookup"><span data-stu-id="a6768-199">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected.</span></span>

<span data-ttu-id="a6768-200">Güvenlik Merkezi üç tür saldırı değişebilir tehdit rapor vardır.</span><span class="sxs-lookup"><span data-stu-id="a6768-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="a6768-201">kullanılabilir Hello raporlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a6768-201">hello reports available are:</span></span>

- <span data-ttu-id="a6768-202">Etkinlik grubu raporu: saldırganlar, hedefler ve taktiği derin çekecek sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6768-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="a6768-203">Kampanya raporu: belirli saldırı Kampanyalar ayrıntılarını odaklanır.</span><span class="sxs-lookup"><span data-stu-id="a6768-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="a6768-204">İş parçacığı özet raporu: hello önceki iki raporlarındaki tüm öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a6768-204">Threat Summary Report: covers all items in hello previous two reports.</span></span>

<span data-ttu-id="a6768-205">Bu tür bilgiler hello olay yanıtlama işlemi sırasında çok kullanışlı, bir sürekli araştırma toounderstand hello kaynak hello saldırı olduğunda, saldırganın sözleri ve hangi toodo toomitigate, bu sorunu taşıma İleri hello.</span><span class="sxs-lookup"><span data-stu-id="a6768-205">This type of information is very useful during hello incident response process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

1. <span data-ttu-id="a6768-206">tooaccess hello tehdit bilgileri bildirmek için aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="a6768-206">tooaccess hello threat intelligence report, do hello following:</span></span>

2. <span data-ttu-id="a6768-207">Select hello **güvenlik uyarıları** döşeme hello ASC Panoda.</span><span class="sxs-lookup"><span data-stu-id="a6768-207">Select hello **Security alerts** tile on hello ASC dashboard.</span></span>

3. <span data-ttu-id="a6768-208">Daha fazla bilgi tooobtain istediğiniz hello güvenlik uyarısı seçin.</span><span class="sxs-lookup"><span data-stu-id="a6768-208">Select hello security alert for which you want tooobtain more information.</span></span>

4. <span data-ttu-id="a6768-209">Merhaba, **raporları** hello bağlantı toohello tehdit Intelligence rapor'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a6768-209">In hello **Reports** field, click hello link toohello threat intelligence report.</span></span>

5. <span data-ttu-id="a6768-210">Bu indirebilirsiniz hello PDF dosyasını açar.</span><span class="sxs-lookup"><span data-stu-id="a6768-210">This will open hello PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="a6768-211">Merhaba ASC tehdit Intelligence rapor hakkında ek bilgi için bkz: [Azure Güvenlik Merkezi tehdit Intelligence rapor.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="a6768-211">For additional information about hello ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="a6768-212">Değerlendirme</span><span class="sxs-lookup"><span data-stu-id="a6768-212">Assessment</span></span>

<span data-ttu-id="a6768-213">toohelp test etme, değerlendirme ve güvenlikle ilgili tutumunuzu değerlendirmesine ASC Qualys ile tümleşik güvenlik açığı değerlendirmesi için bulut aracıları, sanal makine önerileri bileşen bir parçası olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6768-213">toohelp with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="a6768-214">Merhaba Qualys Aracısı Güvenlik Açığı ve sistem durumu izleme verilerini tooASC geri gönderen güvenlik açığı veri toohello Qualys yönetim platformu, raporlar.</span><span class="sxs-lookup"><span data-stu-id="a6768-214">hello Qualys agent reports vulnerability data toohello Qualys management platform, which then sends vulnerability and health monitoring data back tooASC.</span></span> <span data-ttu-id="a6768-215">bir güvenlik açığı değerlendirmesi çözümü hello görüntülenir öneri tooadd hello **önerileri** dikey penceresinde hello ASC Panoda.</span><span class="sxs-lookup"><span data-stu-id="a6768-215">hello recommendation tooadd a vulnerability assessment solution is displayed in hello **Recommendations** blade on hello ASC dashboard.</span></span>

<span data-ttu-id="a6768-216">Merhaba güvenlik açığı değerlendirmesi çözüm hello hedef VM yüklendikten sonra Güvenlik Merkezi taramaları VM toodetect hello ve sistem ve uygulama güvenlik açıklarını belirleme.</span><span class="sxs-lookup"><span data-stu-id="a6768-216">After hello vulnerability assessment solution is installed on hello target VM, Security Center scans hello VM toodetect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="a6768-217">Sorunları hello altında gösterilen algılanan **sanal makine önerileri** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="a6768-217">Detected issues are shown under hello **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="a6768-218">Bir güvenlik açığı değerlendirmesi çözümü nasıl uygulansın mı?</span><span class="sxs-lookup"><span data-stu-id="a6768-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="a6768-219">Bir sanal makine zaten dağıtılmış bir tümleşik güvenlik açığı değerlendirmesi çözüm yoksa, Güvenlik Merkezi yüklü olmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="a6768-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="a6768-220">Merhaba üzerinde hello ASC panosunda **önerileri** dikey penceresinde, select **bir güvenlik açığı değerlendirmesi çözüme ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="a6768-220">In hello ASC dashboard, on hello **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="a6768-221">Merhaba VM'ler tooinstall hello güvenlik açığı değerlendirmesi çözüm istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="a6768-221">Select hello VMs where you want tooinstall hello vulnerability assessment solution.</span></span>

3. <span data-ttu-id="a6768-222">Tıklayın **[sayısı] Vm'lerinde yükleyin.**</span><span class="sxs-lookup"><span data-stu-id="a6768-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="a6768-223">Hello Azure Marketi veya altındaki bir iş ortağı çözümü seçin **varolan bir çözümü kullanın** seçin **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="a6768-223">Select a partner solution in hello Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="a6768-224">Hello hello otomatik güncelleştirme ayarlarını açıp kapatabilirsiniz **iş ortağı çözümleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="a6768-224">You can turn hello auto update settings on or off in hello **Partner Solutions** blade.</span></span>

<span data-ttu-id="a6768-225">Daha ayrıntılı yönergeler için tooimplement bir güvenlik açığı değerlendirmesi çözüm bkz [Azure Güvenlik Merkezi'nde Güvenlik Açığı değerlendirmesi.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="a6768-225">For further instructions on how tooimplement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6768-226">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6768-226">Next steps</span></span>

- [<span data-ttu-id="a6768-227">Azure Güvenlik Merkezi Hızlı Başlangıç Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="a6768-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="a6768-228">Giriş tooAzure Güvenlik Merkezi</span><span class="sxs-lookup"><span data-stu-id="a6768-228">Introduction tooAzure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="a6768-229">Azure Güvenlik Merkezi uyarılarını Azure günlük tümleştirme ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="a6768-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="a6768-230">Artırma Azure Güvenlik Merkezi ile tümleşik güvenlik açığı değerlendirmesi</span><span class="sxs-lookup"><span data-stu-id="a6768-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
