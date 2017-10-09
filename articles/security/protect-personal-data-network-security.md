---
title: "Azure ile kişisel veriler aaaProtect ağ güvenlik özellikleri | Microsoft Docs"
description: "Azure ağı güvenlik özellikleri kullanarak kişisel verilerini koruma"
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
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: be112a9408d327ccedf871656afe800fc7f775e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a><span data-ttu-id="62d6c-103">Ağ güvenlik özellikleri ile kişisel verileri koruma: Azure uygulama ağ geçidi ve ağ güvenlik grupları</span><span class="sxs-lookup"><span data-stu-id="62d6c-103">Protect personal data with network security features: Azure Application Gateway and Network Security Groups</span></span>

<span data-ttu-id="62d6c-104">Bu makalede, bilgi ve Azure uygulama ağ geçidi ve ağ güvenlik grupları tooprotect kişisel verileri kullanmanıza yardımcı olacak yordamlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="62d6c-104">This article provides information and procedures that will help you use Azure Application Gateway and Network Security Groups tooprotect personal data.</span></span>

<span data-ttu-id="62d6c-105">Bir önemli bir çok katmanlı güvenlik stratejisi tooprotect hello kişisel verilerin gizliliği SQL ekleme veya siteler arası komut dosyası gibi ortak güvenlik açıklarına karşı savunma öğedir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-105">An important element in a multi-layered security strategy tooprotect hello privacy of personal data is a defense against common vulnerability exploits such as SQL injection or cross-site scripting.</span></span> <span data-ttu-id="62d6c-106">Azure sanal ağınızın dışında tutma istenmeyen ağ trafiğini hassas verileri Microsoft Azure sağlar, Araçlar toohelp verilerinizi saldırganlara karşı korumak ve olası riski belirtebilen karşı korunmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="62d6c-106">Keeping unwanted network traffic out of your Azure virtual network helps protect against potential compromise of sensitive data, and Microsoft Azure gives you tools toohelp protect your data against attackers.</span></span>

## <a name="scenario"></a><span data-ttu-id="62d6c-107">Senaryo</span><span class="sxs-lookup"><span data-stu-id="62d6c-107">Scenario</span></span>

<span data-ttu-id="62d6c-108">Merhaba Amerika Birleşik Devletleri'nde yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello Akdeniz, Adriatic ve Baltık seas yanı sıra hello İngiliz Adaları arasında içinde genişletmektedir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="62d6c-109">İçinde furtherance Bu çalışmalarınızı, birkaç küçük ele geçirmiş İtalya, Almanya, Danimarka ve hello İngiltere dayanarak satırları İyi Yolculuklar partimize</span><span class="sxs-lookup"><span data-stu-id="62d6c-109">In furtherance of those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="62d6c-110">Merhaba şirket Microsoft hello'teki şirket verilerinin toostore bulut uygulamaları ve sanal makineler üzerinde işleyen ve bu verilere erişme çalıştırmak Azure kullanır.</span><span class="sxs-lookup"><span data-stu-id="62d6c-110">hello company uses Microsoft Azure toostore corporate data in hello cloud and run applications on virtual machines that process and access this data.</span></span> <span data-ttu-id="62d6c-111">Bu veriler, adlar, adresler, telefon numaraları gibi kişisel olarak tanımlanabilir bilgileri ve genel müşteri tabanı kredi kartı bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-111">This data includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="62d6c-112">Ayrıca tüm konumlarda adresleri, telefon numaralarını, vergi kimlik numaraları ve şirket çalışanlarının tıbbi bilgi gibi geleneksel İnsan Kaynakları bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-112">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="62d6c-113">Merhaba seyahat satır Ayrıca, kişisel bilgi tootrack ilişkileri geçerli ve geçmiş müşterilerle içeren büyük bir veritabanını ödül ve bağlılık programı üyeleri korur.</span><span class="sxs-lookup"><span data-stu-id="62d6c-113">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="62d6c-114">Şirket çalışanları erişim hello ağdan hello şirketin şubelere ve seyahat Merhaba Dünya bulunan aracıları toosome şirket kaynaklarına sahip ve Azure Vm'leri toointeract onunla içinde barındırılan web tabanlı uygulamalara kullanın.</span><span class="sxs-lookup"><span data-stu-id="62d6c-114">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources and use web-based applications hosted in Azure VMs toointeract with it.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="62d6c-115">Sorun bildirimi</span><span class="sxs-lookup"><span data-stu-id="62d6c-115">Problem statement</span></span>

<span data-ttu-id="62d6c-116">Hello şirket müşterilerin hello gizliliğini korumak gerekir ve kişisel veriler açığa çıkaran yazılım güvenlik açıklarından toorun kötü amaçlı kod yararlanma saldırganlar çalışanların kişisel verileri depolanan veya hello şirketin bulut tabanlı uygulamalar tarafından kullanılan.</span><span class="sxs-lookup"><span data-stu-id="62d6c-116">hello company must protect hello privacy of customers’ and employees’ personal data from attackers who exploit software vulnerabilities toorun malicious code that could expose personal data stored or used by hello company’s cloud-based applications.</span></span>

## <a name="company-goal"></a><span data-ttu-id="62d6c-117">Şirket hedefi</span><span class="sxs-lookup"><span data-stu-id="62d6c-117">Company goal</span></span>

<span data-ttu-id="62d6c-118">Merhaba yetkisiz kişilerin şirketin hedef tooensure şirket Azure sanal ağlar ve hello uygulamaları ve ortak güvenlik açıkları yararlanarak var. bulunan verileri erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="62d6c-118">hello company’s goal tooensure that unauthorized persons cannot access corporate Azure Virtual Networks and hello applications and data that reside there by exploiting common vulnerabilities.</span></span> 

## <a name="solutions"></a><span data-ttu-id="62d6c-119">Çözümler</span><span class="sxs-lookup"><span data-stu-id="62d6c-119">Solutions</span></span>

<span data-ttu-id="62d6c-120">Microsoft Azure sağlayan güvenlik mekanizmaları toohelp Azure sanal ağlar girmesini istenmeyen trafiği engelle.</span><span class="sxs-lookup"><span data-stu-id="62d6c-120">Microsoft Azure provides security mechanisms toohelp prevent unwanted traffic from entering Azure Virtual Networks.</span></span> <span data-ttu-id="62d6c-121">Gelen ve giden trafik, geleneksel güvenlik duvarları tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-121">Control of inbound and outbound traffic is traditionally performed by firewalls.</span></span> <span data-ttu-id="62d6c-122">Azure içinde basit dağıtılmış güvenlik duvarı olarak hareket hello uygulama ağ geçidi ile Merhaba Web uygulaması güvenlik duvarı ve ağ güvenlik grupları (NSG) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62d6c-122">In Azure, you can use hello Application Gateway with hello Web Application Firewall and Network Security Groups (NSG), which act as a simple distributed firewall.</span></span> <span data-ttu-id="62d6c-123">Bu araçları toodetect etkinleştirin ve istenmeyen ağ trafiği engelleyin.</span><span class="sxs-lookup"><span data-stu-id="62d6c-123">These tools enable you toodetect and block unwanted network traffic.</span></span>

### <a name="application-gatewayweb-application-firewall"></a><span data-ttu-id="62d6c-124">Uygulama ağ geçidi/Web uygulaması güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="62d6c-124">Application Gateway/Web Application Firewall</span></span>

<span data-ttu-id="62d6c-125">Merhaba [Web uygulaması güvenlik duvarı](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) hello (WAF) bileşeninin [Azure uygulama ağ geçidi](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) giderek ortak bilinen açıklarından kötü amaçlı saldırıları hedefleri olan web uygulamaları korur güvenlik açıkları.</span><span class="sxs-lookup"><span data-stu-id="62d6c-125">hello [Web Application Firewall](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) (WAF) component of hello [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) protects web applications, which are increasingly targets of malicious attacks that exploit common known vulnerabilities.</span></span> <span data-ttu-id="62d6c-126">Merkezi WAF hem web saldırılarına karşı korur ve uygulama değişiklikleri gerek kalmadan güvenlik yönetimini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-126">A centralized WAF both protects against web attacks and simplifies security management without requiring any application changes.</span></span>

<span data-ttu-id="62d6c-127">Azure WAF SQL ekleme, siteler arası komut dosyası, HTTP protokolü ihlali ve anormallikleri, bot, gezginleri, tarayıcılar, ortak uygulama yapılandırma hataları, HTTP hizmet reddi ve diğer ortak saldırıları gibi dahil olmak üzere çeşitli saldırı kategorilerini adresleri komut ekleme işlemi, HTTP Kaçakçılığı, HTTP yanıt bölme ve uzak dosya ekleme saldırıları isteyin.</span><span class="sxs-lookup"><span data-stu-id="62d6c-127">Azure WAF addresses various attack categories including SQL injection, cross site scripting, HTTP protocol violations and anomalies, bots, crawlers, scanners, common application misconfigurations, HTTP Denial of Service, and other common attacks such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attacks.</span></span> 

<span data-ttu-id="62d6c-128">Bir uygulama ağ geçidi ile WAF oluşturun veya WAF tooan varolan uygulama ağ geçidi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62d6c-128">You can create an application gateway with WAF, or add WAF tooan existing application gateway.</span></span> <span data-ttu-id="62d6c-129">Her iki durumda da, kendi alt Azure uygulama ağ geçidi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-129">In either case, Azure Application Gateway requires its own subnet.</span></span>

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a><span data-ttu-id="62d6c-130">WAF ile nasıl bir uygulama ağ geçidi oluşturulsun mu?</span><span class="sxs-lookup"><span data-stu-id="62d6c-130">How do I create an application gateway with WAF?</span></span> 

<span data-ttu-id="62d6c-131">toocreate etkin WAF sahip yeni bir uygulama ağ geçidi hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="62d6c-131">toocreate a new application gateway with WAF enabled, do hello following:</span></span>

1. <span data-ttu-id="62d6c-132">Günlük toohello Azure portal ve hello **Sık Kullanılanlar** hello portalının bölmesi **yeni**</span><span class="sxs-lookup"><span data-stu-id="62d6c-132">Log in toohello Azure portal and in hello **Favorites** pane of hello portal, click **New**</span></span>

2. <span data-ttu-id="62d6c-133">Merhaba, **yeni** dikey penceresinde tıklatın **ağ**.</span><span class="sxs-lookup"><span data-stu-id="62d6c-133">In hello **New** blade, click **Networking**.</span></span>

3. <span data-ttu-id="62d6c-134">Tıklatın **uygulama ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="62d6c-134">Click **Application Gateway**.</span></span>

4. <span data-ttu-id="62d6c-135">Toohello Azure portalına gidin **yeni \> ağ \> uygulama ağ geçidi.**</span><span class="sxs-lookup"><span data-stu-id="62d6c-135">Navigate toohello Azure portal, **click New \> Networking \> Application Gateway.**</span></span>

   ![Uygulama ağ geçidi oluşturma](media/protect-netsec/app-gateway-01.png)

5. <span data-ttu-id="62d6c-137">Merhaba, **Temelleri** görünür, dikey alanları izleyen Merhaba hello değerleri girin: ad, katmanı (standart veya WAF), SKU boyutunu (küçük, Orta veya büyük) örnek sayısını (2), yüksek kullanılabilirlik için abonelik, kaynak grubu, ve Konum.</span><span class="sxs-lookup"><span data-stu-id="62d6c-137">In hello **Basics** blade that appears, enter hello values for hello following fields: Name, Tier (Standard or WAF), SKU size (Small, Medium, or Large),  Instance count (2 for high availability), Subscription, Resource group, and Location.</span></span>

6. <span data-ttu-id="62d6c-138">Merhaba, **ayarları** altında görüntülenen dikey **sanal ağ**, tıklatın **sanal ağ seçin**.</span><span class="sxs-lookup"><span data-stu-id="62d6c-138">In hello **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="62d6c-139">Bu adımı açılır girin Seç sanal ağ dikey penceresinde hello.</span><span class="sxs-lookup"><span data-stu-id="62d6c-139">This step opens enter hello Choose virtual network blade.</span></span>

7. <span data-ttu-id="62d6c-140">Tıklatın **Yeni Oluştur** tooopen hello **sanal ağ oluştur** dikey.</span><span class="sxs-lookup"><span data-stu-id="62d6c-140">Click **Create new** tooopen hello **Create virtual network** blade.</span></span>

8. <span data-ttu-id="62d6c-141">Hello aşağıdaki değerleri girin: ad, adres alanı, alt ağ adı, alt ağ adres aralığı.</span><span class="sxs-lookup"><span data-stu-id="62d6c-141">Enter hello following values: Name, Address space, Subnet name, Subnet address range.</span></span> <span data-ttu-id="62d6c-142">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="62d6c-142">Click **OK**.</span></span>

9. <span data-ttu-id="62d6c-143">Merhaba üzerinde **ayarları** altında dikey **ön uç IP yapılandırmasını**, başlangıç IP adresi türü seçin.</span><span class="sxs-lookup"><span data-stu-id="62d6c-143">On hello **Settings** blade under **Frontend IP configuration**, choose hello IP address type.</span></span>

10. <span data-ttu-id="62d6c-144">Tıklatın **genel bir IP adresi seçin** sonra **yeni oluştur.**</span><span class="sxs-lookup"><span data-stu-id="62d6c-144">Click **Choose a public IP address,** then **Create new.**</span></span>

11. <span data-ttu-id="62d6c-145">Merhaba varsayılan değerini kabul edin ve tıklatın **Tamam.**</span><span class="sxs-lookup"><span data-stu-id="62d6c-145">Accept hello default value, and click **OK.**</span></span>

12. <span data-ttu-id="62d6c-146">Merhaba üzerinde **ayarları** altında dikey **dinleyici Yapılandırması**, HTTP veya HTTPS altında toouse seçin **Protokolü**.</span><span class="sxs-lookup"><span data-stu-id="62d6c-146">On hello **Settings** blade under **Listener configuration**, select toouse HTTP or HTTPS under **Protocol**.</span></span> <span data-ttu-id="62d6c-147">toouse HTTPS, bir sertifika gereklidir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-147">toouse HTTPS, a certificate is required.</span></span>

13. <span data-ttu-id="62d6c-148">Merhaba WAF belirli ayarlarını yapılandırabilirsiniz: **güvenlik duvarı durumu** (**etkin**) ve **güvenlik duvarı modu** (**önleme**).</span><span class="sxs-lookup"><span data-stu-id="62d6c-148">Configure hello WAF specific settings: **Firewall status** (**Enabled**) and **Firewall mode** (**Prevention**).</span></span> <span data-ttu-id="62d6c-149">Seçerseniz **algılama** hello modu olarak trafiği yalnızca günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-149">If you choose **Detection** as hello mode, traffic is only logged.</span></span>

14. <span data-ttu-id="62d6c-150">Gözden geçirme hello **Özet** sayfasında ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="62d6c-150">Review hello **Summary** page and click **OK**.</span></span> <span data-ttu-id="62d6c-151">Şimdi hello uygulama ağ geçidi sıraya ve oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="62d6c-151">Now hello application gateway is queued up and created.</span></span>

<span data-ttu-id="62d6c-152">Merhaba uygulama ağ geçidi oluşturulduktan sonra hello portalında tooit gidin ve hello uygulama ağ geçidi yapılandırmasını devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62d6c-152">After hello application gateway has been created, you can navigate tooit in hello portal and continue configuration of hello application gateway.</span></span>

![oluşturulan uygulama ağ geçidi](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-tooan-existing-application"></a><span data-ttu-id="62d6c-154">WAF tooan varolan uygulama nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="62d6c-154">How do I add WAF tooan existing application?</span></span>

<span data-ttu-id="62d6c-155">önleme modunda, var olan bir uygulama ağ geçidi toosupport WAF tooupdate hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="62d6c-155">tooupdate an existing application gateway toosupport WAF in prevention mode, do hello following:</span></span>

1. <span data-ttu-id="62d6c-156">Hello Azure portal'ın **Sık Kullanılanlar** bölmesinde tıklatın **tüm kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="62d6c-156">In hello Azure portal **Favorites** pane, click **All resources**.</span></span>

2. <span data-ttu-id="62d6c-157">Tıklatın hello hello varolan uygulama ağ geçidi **tüm kaynakları** dikey.</span><span class="sxs-lookup"><span data-stu-id="62d6c-157">Click hello existing Application Gateway in hello **All resources** blade.</span></span> 
>[!NOTE]
<span data-ttu-id="62d6c-158">Not: hello aboneliği zaten içinde birçok kaynak varsa, hello adı hello filtre adıyla girebilirsiniz...</span><span class="sxs-lookup"><span data-stu-id="62d6c-158">Note: If hello subscription you selected already has several resources in it, you can enter hello name in hello Filter by name…</span></span> <span data-ttu-id="62d6c-159">kutusunu tooeasily erişim hello DNS bölgesi.</span><span class="sxs-lookup"><span data-stu-id="62d6c-159">box tooeasily access hello DNS zone.</span></span>
3. <span data-ttu-id="62d6c-160">Tıklatın **Web uygulaması güvenlik duvarı** ve hello uygulama ağ geçidi ayarlarını güncelleştirin: **tooWAF katmanı yükseltme** (işaretli) **güvenlik duvarı durumu** (etkin)  **Güvenlik Duvarı modu** (önleme).</span><span class="sxs-lookup"><span data-stu-id="62d6c-160">Click **Web application firewall** and update hello application gateway settings: **Upgrade tooWAF Tier** (checked), **Firewall status** (enabled),     **Firewall mode** (Prevention).</span></span> <span data-ttu-id="62d6c-161">Tooconfigure etmeniz hello kural kümesini ve devre dışı kurallarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="62d6c-161">You also need tooconfigure hello rule set, and configure disabled rules.</span></span>

<span data-ttu-id="62d6c-162">Nasıl hakkında daha ayrıntılı bilgi için toocreate WAF sahip yeni bir uygulama ağ geçidi ve nasıl tooadd WAF tooan varolan uygulama ağ geçidi, bkz: [hello portalını kullanarak bir uygulama ağ geçidi ile web uygulaması güvenlik duvarı oluşturun.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)</span><span class="sxs-lookup"><span data-stu-id="62d6c-162">For more detailed information on how toocreate a new application gateway with WAF and how tooadd WAF tooan existing application gateway, see [Create an application gateway with web application firewall by using hello portal.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)</span></span>

### <a name="network-security-groups"></a><span data-ttu-id="62d6c-163">Ağ Güvenlik Grupları</span><span class="sxs-lookup"><span data-stu-id="62d6c-163">Network Security Groups</span></span>

<span data-ttu-id="62d6c-164">A [ağ güvenlik grubu](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) izin veren veya reddeden çok bağlı ağ trafiği tooresources güvenlik kuralları listesini içeren[Azure sanal ağlar](https://docs.microsoft.com/azure/virtual-network/) (VNet).</span><span class="sxs-lookup"><span data-stu-id="62d6c-164">A [network security group](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) contains a list of security rules that allow or deny network traffic tooresources connected too[Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/) (VNet).</span></span> <span data-ttu-id="62d6c-165">Nsg'ler ilişkili toosubnets veya tek tek sanal makineleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-165">NSGs can be associated toosubnets or individual VMs.</span></span> <span data-ttu-id="62d6c-166">Bir NSG'yi ilişkili tooa alt olduğunda hello kuralları tooall kaynaklara bağlı toohello alt uygulayın.</span><span class="sxs-lookup"><span data-stu-id="62d6c-166">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> <span data-ttu-id="62d6c-167">Trafik daha da bir NSG tooa VM veya NIC ilişkilendirerek kısıtlanabilir</span><span class="sxs-lookup"><span data-stu-id="62d6c-167">Traffic can further be restricted by also associating an NSG tooa VM or NIC.</span></span>

<span data-ttu-id="62d6c-168">Nsg'ler dört özellikleri içerir: ad, bölge, kaynak grubu ve kuralları.</span><span class="sxs-lookup"><span data-stu-id="62d6c-168">NSGs contain four properties: Name, Region, Resource group, and Rules.</span></span>
>[!Note]
<span data-ttu-id="62d6c-169">Bir NSG bir kaynak grubunda var ancak hello kaynak hello parçası olduğu sürece, herhangi bir kaynak grubunda ilişkili tooresources olabilir hello NSG olduğu Azure bölgesinin.</span><span class="sxs-lookup"><span data-stu-id="62d6c-169">Although an NSG exists in a resource group, it can be associated tooresources in any resource group, as long as hello resource is part of hello same Azure region as hello NSG.</span></span>

<span data-ttu-id="62d6c-170">NSG kuralları dokuz özellikler içeriyor: adı, Protokolü (TCP, UDP veya \*, ICMP yanı sıra UDP ve TCP içerir), kaynak bağlantı noktası aralığı, hedef bağlantı noktası aralığı, kaynak adres öneki, hedef adres ön eki, yönünü (gelen veya giden) öncelik ( 100 ile 4096 arasında) ve erişim türüne (izin verme veya reddetme).</span><span class="sxs-lookup"><span data-stu-id="62d6c-170">NSG rules contain nine properties: Name, Protocol (TCP, UDP, or \*, which includes ICMP as well as UDP and TCP), Source port range, Destination port range, Source address prefix, Destination address prefix, Direction (inbound or outbound), Priority (between 100 and 4096) and Access type (allow or deny).</span></span> <span data-ttu-id="62d6c-171">Tüm Nsg'ler silinmiş veya oluşturduğunuz hello kurallar tarafından geçersiz kılınmış varsayılan kurallar kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="62d6c-171">All NSGs contain a set of default rules that can be deleted, or overridden by hello rules you create.</span></span>

#### <a name="how-do-i-implement-nsgs"></a><span data-ttu-id="62d6c-172">Nsg'ler nasıl uygulansın mı?</span><span class="sxs-lookup"><span data-stu-id="62d6c-172">How do I implement NSGs?</span></span>

<span data-ttu-id="62d6c-173">Nsg'leri uygulamadan planlama gerektirir ve birkaç tasarım konuları dikkate tootake ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="62d6c-173">Implementing NSGs requires planning, and there are several design considerations you need tootake into account.</span></span> <span data-ttu-id="62d6c-174">Abonelik ve başına NSG kuralları başına Nsg'ler hello sayısını sınırlandırır bunlar; VNet ve alt ağ tasarımı, özel kurallar, ICMP trafiğine, alt ağları, yük Dengeleyiciler ve daha fazlasını katmanlarıyla yalıtım.</span><span class="sxs-lookup"><span data-stu-id="62d6c-174">These include limits on hello number of NSGs per subscription and rules per NSG; VNet and subnet design, special rules, ICMP traffic, isolation of tiers with subnets, load balancers, and more.</span></span>

<span data-ttu-id="62d6c-175">Planlama ve uygulama Nsg'ler ve bir örnek dağıtım senaryosu, daha fazla yönergeler için bkz [filtre ağ güvenlik grupları ile ağ trafiği.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)</span><span class="sxs-lookup"><span data-stu-id="62d6c-175">For more guidance in planning and implementing NSGs, and a sample deployment scenario, see [Filter network traffic with network security groups.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)</span></span>

#### <a name="how-do-i-create-rules-in-an-nsg"></a><span data-ttu-id="62d6c-176">Bir NSG'yi nasıl kurallar oluşturulsun mu?</span><span class="sxs-lookup"><span data-stu-id="62d6c-176">How do I create rules in an NSG?</span></span>

<span data-ttu-id="62d6c-177">toocreate gelen kuralları var olan bir NSG içinde izleyen hello:</span><span class="sxs-lookup"><span data-stu-id="62d6c-177">toocreate inbound rules in an existing NSG, do hello following:</span></span>

1. <span data-ttu-id="62d6c-178">Tıklatın **Gözat**ve ardından **ağ güvenlik grupları**.</span><span class="sxs-lookup"><span data-stu-id="62d6c-178">Click **Browse**, and then **Network security groups**.</span></span>

2. <span data-ttu-id="62d6c-179">Nsg'ler Hello listesinde tıklayın **NSG ön uç**ve ardından **gelen güvenlik kuralları.**</span><span class="sxs-lookup"><span data-stu-id="62d6c-179">In hello list of NSGs, click **NSG-FrontEnd**, and then **Inbound security rules.**</span></span>

3. <span data-ttu-id="62d6c-180">Gelen güvenlik kuralları Hello listesinde tıklayın **Ekle.**</span><span class="sxs-lookup"><span data-stu-id="62d6c-180">In hello list of Inbound security rules, click **Add.**</span></span>

4. <span data-ttu-id="62d6c-181">Alanları aşağıdaki hello başlangıç değerleri girin: ad, öncelik, kaynak, protokol, kaynak aralığı, hedef, hedef bağlantı noktası aralığı ve eylem.</span><span class="sxs-lookup"><span data-stu-id="62d6c-181">Enter hello values in hello following fields: Name, Priority, Source, Protocol, Source range, Destination, Destination port range, and Action.</span></span>

<span data-ttu-id="62d6c-182">Merhaba yeni kural hello NSG birkaç saniye sonra görünür.</span><span class="sxs-lookup"><span data-stu-id="62d6c-182">hello new rule will appear in hello NSG after a few seconds.</span></span>

![Ağ güvenlik kuralları](media/protect-netsec/inbound-security.png)

<span data-ttu-id="62d6c-184">Daha fazla yönergeleri toocreate Nsg'ler alt, kuralları oluşturma ve bir NSG bir ön uç ve arka uç alt ağı ile ilişkilendirmek için bkz [hello Azure portal kullanarak ağ güvenlik grupları oluşturun.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)</span><span class="sxs-lookup"><span data-stu-id="62d6c-184">For more instructions on how toocreate NSGs in subnets, create rules, and associate an NSG with a front-end and back-end subnet, see [Create network security groups using hello Azure portal.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)</span></span>

## <a name="next-steps"></a><span data-ttu-id="62d6c-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62d6c-185">Next steps</span></span>

[<span data-ttu-id="62d6c-186">Azure ağ güvenliği</span><span class="sxs-lookup"><span data-stu-id="62d6c-186">Azure Network Security</span></span>](https://azure.microsoft.com/blog/azure-network-security/)

[<span data-ttu-id="62d6c-187">Azure ağı en iyi güvenlik uygulamaları</span><span class="sxs-lookup"><span data-stu-id="62d6c-187">Azure Network Security Best Practices</span></span>](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[<span data-ttu-id="62d6c-188">Ağ güvenlik grubu hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="62d6c-188">Get information about a network security group</span></span>](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[<span data-ttu-id="62d6c-189">Web uygulaması Güvenlik Duvarı (WAF)</span><span class="sxs-lookup"><span data-stu-id="62d6c-189">Web application firewall (WAF)</span></span>](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
