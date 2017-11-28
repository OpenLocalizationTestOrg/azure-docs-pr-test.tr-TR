---
title: "bir güvenlik duvarı ve Nsg'ler uygulamalarla aaaDMZ örnek – yapı DMZ tooprotect | Microsoft Docs"
description: "DMZ bir güvenlik duvarı ve ağ güvenlik grupları (NSG) ile derleme"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="1f7e8-103">Örnek 2 – çevre tooprotect bir güvenlik duvarı ve Nsg'ler uygulamalarla yapı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-103">Example 2 – Build a DMZ tooprotect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="1f7e8-104">[Dönüş toohello güvenlik sınırı en iyi uygulamalar sayfası][HOME]</span><span class="sxs-lookup"><span data-stu-id="1f7e8-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="1f7e8-105">Bu örnek, bir güvenlik duvarı, dört windows sunucuları ve ağ güvenlik grupları ile DMZ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="1f7e8-106">Bu da her hello ilgili komutları tooprovide her adımın daha derin bir anlayış yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="1f7e8-107">Ayrıca vardır bir trafik senaryo bölüm tooprovide ayrıntılı bir adım adım derinlemesine savunma hello katmanları üzerinden trafik geçer nasıl DMZ hello.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="1f7e8-108">Son olarak, hello references bölümünde hello tam kod ve yönerge toobuild bu ortam tootest çeşitli senaryoları ile deneme ise.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="1f7e8-109">![NVA ve NSG gelen DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="1f7e8-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="1f7e8-110">Ortam açıklaması</span><span class="sxs-lookup"><span data-stu-id="1f7e8-110">Environment Description</span></span>
<span data-ttu-id="1f7e8-111">Bu örnekte hello aşağıdakileri içeren bir abonelik vardır:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="1f7e8-112">İki bulut hizmetlerini: "FrontEnd001" ve "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="1f7e8-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="1f7e8-113">Bir sanal ağ "CorpNetwork" iki alt ağ ile: "Ön uç" ve "Arka uç"</span><span class="sxs-lookup"><span data-stu-id="1f7e8-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="1f7e8-114">Tek bir ağ güvenlik uygulanan tooboth alt ağları olan Grup</span><span class="sxs-lookup"><span data-stu-id="1f7e8-114">A single Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="1f7e8-115">Bu örnekte Barracuda NextGen Firewall bir ağ sanal gereç toohello ön uç alt bağlı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected toohello Frontend subnet</span></span>
* <span data-ttu-id="1f7e8-116">Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="1f7e8-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="1f7e8-117">Uygulama geri temsil eden iki windows sunucuları sunucuları ("AppVM01", "AppVM02") end</span><span class="sxs-lookup"><span data-stu-id="1f7e8-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="1f7e8-118">Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="1f7e8-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="1f7e8-119">Bu örnek birçok farklı ağ sanal Gereçleri Bu örnek için kullanılabilecek hello bir Barracuda NextGen Firewall kullansa da.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-119">Although this example uses a Barracuda NextGen Firewall, many of hello different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="1f7e8-120">Merhaba başvurular bölümünde yukarıda açıklanan hello ortamı çoğunu oluşturacak bir PowerShell komut dosyası yok.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-120">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="1f7e8-121">Yapı hello VM'ler ve sanal ağlar, bu belgede ayrıntılı hello örnek komut dosyası tarafından yapılır rağmen açıklanmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="1f7e8-122">toobuild hello ortamı:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-122">toobuild hello environment:</span></span>

1. <span data-ttu-id="1f7e8-123">(Adları, konum ve IP adreslerini toomatch verilen hello senaryo güncelleştirilmiş) hello başvurular bölümüne dahil hello ağ yapılandırma xml dosyasını kaydedin</span><span class="sxs-lookup"><span data-stu-id="1f7e8-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="1f7e8-124">Güncelleştirme hello kullanıcı değişkenleri hello betik toomatch hello ortamı hello komut olan toobe Çalıştır (Abonelikleri, hizmet adlarını vb. karşı)</span><span class="sxs-lookup"><span data-stu-id="1f7e8-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="1f7e8-125">PowerShell'de Hello komut dosyası yürütme</span><span class="sxs-lookup"><span data-stu-id="1f7e8-125">Execute hello script in PowerShell</span></span>

<span data-ttu-id="1f7e8-126">**Not**: hello PowerShell Betiği miktarlara hello bölge hello ağ yapılandırması xml dosyasında miktarlara hello bölge eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-126">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="1f7e8-127">Merhaba komut dosyası başarıyla çalıştıktan sonra sonrası betik adımları izleyerek hello izlenebilir:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-127">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="1f7e8-128">Merhaba güvenlik duvarı kuralları ayarlamak, bu başlıklı hello aşağıdaki bölümde ele alınmıştır: güvenlik duvarı kuralları.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-128">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="1f7e8-129">İsteğe bağlı olarak iki komut dosyaları tooset hello web sunucusu ve uygulama sunucusu bu DMZ yapılandırma ile test basit bir web uygulaması tooallow ile Merhaba başvurular bölümünde bulunur.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-129">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="1f7e8-130">Merhaba sonraki bölümde hello betikleri deyimleri göreli tooNetwork güvenlik grupları çoğunu açıklar.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-130">hello next section explains most of hello scripts statements relative tooNetwork Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="1f7e8-131">Ağ Güvenlik Grupları (NSG)</span><span class="sxs-lookup"><span data-stu-id="1f7e8-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="1f7e8-132">Bu örnekte, bir NSG grubu yerleşik ve altı kurallarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="1f7e8-133">Genel olarak bakıldığında, belirli "İzin ver" kurallarınızı ilk oluşturun ve daha genel "Deny" kuralları son hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-133">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="1f7e8-134">öncelik atanmış hello hangi kuralları ilk olarak değerlendirilir belirler.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-134">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="1f7e8-135">Trafik tooapply tooa belirli kural bulunduktan sonra başka hiçbir kural değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-135">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="1f7e8-136">NSG kuralları hello ikisinde uygulayabileceğiniz gelen veya giden yön (Merhaba alt hello açısından).</span><span class="sxs-lookup"><span data-stu-id="1f7e8-136">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="1f7e8-137">Bildirimli olarak, kurallar aşağıdaki hello gelen trafik için oluşturulmakta:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-137">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="1f7e8-138">İç DNS trafiğinin (bağlantı noktası 53) izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="1f7e8-139">Merhaba Internet tooany VM gelen RDP trafiğine (3389 numaralı bağlantı noktası) izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-139">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="1f7e8-140">Merhaba Internet toohello NVA (Güvenlik Duvarı) gelen HTTP trafiği (bağlantı noktası 80) izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-140">HTTP traffic (port 80) from hello Internet toohello NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="1f7e8-141">IIS01 tooAppVM1 tüm trafiği (tüm bağlantı noktaları) izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-141">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="1f7e8-142">Merhaba Internet toohello tüm trafiği (tüm bağlantı noktaları) tüm sanal ağ (her iki alt ağ) reddedildi</span><span class="sxs-lookup"><span data-stu-id="1f7e8-142">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="1f7e8-143">Merhaba ön uç alt toohello arka uç alt ağından gelen tüm trafiği (tüm bağlantı noktaları) reddedildi</span><span class="sxs-lookup"><span data-stu-id="1f7e8-143">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="1f7e8-144">Bu kuralları ilişkili tooeach alt ağ ile bir HTTP isteği hello Internet toohello web sunucusundan gelen ise her ikisi de kuralları 3 (izin verin) ve 5 (uygulamak reddetme), ancak 3 kuralı, yalnızca geçerli olur ve kural 5 oyuna değil gelen daha yüksek öncelikli olduğundan.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-144">With these rules bound tooeach subnet, if a HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="1f7e8-145">Bu nedenle hello HTTP isteği toohello güvenlik duvarı izin.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-145">Thus hello HTTP request would be allowed toohello firewall.</span></span> <span data-ttu-id="1f7e8-146">Bu aynı trafiği tooreach hello DNS01 sunucusunu denemeden ise hello ilk tooapply ve hello trafiği toopass toohello sunucu verilmez kural 5 (Reddet) olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-146">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="1f7e8-147">Toohello arka uç alt (dışında izin verilen trafiği kurallarında 1 ve 4) Konuşmayı gelen 6 (Reddet) blokları hello Frontend alt ağı kural, bir saldırganın güvenlik ihlalleri hello web uygulamasına hello ön uç hello saldırganın yoktur durumunda bu hello arka uç ağ korur sınırlı erişim toohello arka uç "ağ (yalnızca tooresources hello AppVM01 sunucu üzerinde gösterilen) korumalı".</span><span class="sxs-lookup"><span data-stu-id="1f7e8-147">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="1f7e8-148">Toohello giden trafiğe izin veren varsayılan giden kural Internet.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-148">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="1f7e8-149">Bu örnekte, biz giden trafiğe izin vermek ve herhangi bir giden kuralı değiştirme değil.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="1f7e8-150">Her iki yönde trafik aşağı toolock, kullanıcı tanımlanan yönlendirme gereklidir, hello bulunabilir farklı bir örnekte keşfedilen bu [ana güvenlik sınırı belge][HOME].</span><span class="sxs-lookup"><span data-stu-id="1f7e8-150">toolock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in hello [main security boundary document][HOME].</span></span>

<span data-ttu-id="1f7e8-151">Merhaba yukarıda açıklanan NSG kuralları olan çok benzer toohello NSG kuralları [örnek 1 - yapı Nsg'ler ile basit DMZ][Example1].</span><span class="sxs-lookup"><span data-stu-id="1f7e8-151">hello above discussed NSG rules are very similar toohello NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="1f7e8-152">Lütfen her bir NSG kural ve onun özniteliklerini ayrıntılı bir bakış için bu belgedeki hello NSG açıklama gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-152">Please review hello NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="1f7e8-153">Güvenlik Duvarı Kuralları</span><span class="sxs-lookup"><span data-stu-id="1f7e8-153">Firewall Rules</span></span>
<span data-ttu-id="1f7e8-154">Bir yönetim istemcisi yüklü bir bilgisayar toomanage hello Güvenlik Duvarı'nı toobe gerekir ve gerekli hello yapılandırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-154">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="1f7e8-155">Merhaba, Güvenlik Duvarı (veya diğer NVA) belgelerinden satıcı nasıl toomanage hello üzerinde aygıt bakın.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-155">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="1f7e8-156">Bu bölümde Hello kalanı hello hello güvenlik duvarı yapılandırmasını kendisini hello satıcılar Yönetimi istemcisi (yani hello Azure portal veya PowerShell) aracılığıyla anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-156">hello remainder of this section will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="1f7e8-157">İstemci Yükleme ve bağlantı toohello Bu örnekte kullanılan Barracuda için yönergeler şurada bulunabilir: [Barracuda NG yönetici](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="1f7e8-157">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="1f7e8-158">Merhaba güvenlik duvarında kuralları iletme oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-158">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="1f7e8-159">Bu örnek yalnızca Internet trafiği bağlı toohello güvenlik duvarı ve toohello web sunucusuna yönlendirir olduğundan, yalnızca bir iletme NAT kuralı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-159">Since this example only routes internet traffic in-bound toohello firewall and then toohello web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="1f7e8-160">Merhaba Barracuda NextGen Firewall Bu örnek hello kullanılan üzerinde hedef NAT kuralı ("Dst NAT") toopass Bu trafik, kural olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-160">On hello Barracuda NextGen Firewall used in this example hello rule would be a Destination NAT rule (“Dst NAT”) toopass this traffic.</span></span>

<span data-ttu-id="1f7e8-161">toocreate hello aşağıdaki kural (veya var olan varsayılan kuralları doğrulayın), hello Barracuda NG yönetici istemci panodan başlatma, toohello yapılandırma sekmesine gidin, hello işletimsel yapılandırma bölümü Ruleset'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-161">toocreate hello following rule (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="1f7e8-162">Bir kılavuz olarak adlandırılan, "Ana kuralları" Merhaba Güvenlik Duvarı'nda etkin ve devre dışı bırakılan kuralları varolan hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-162">A grid called, “Main Rules” will show hello existing active and deactivated rules on hello firewall.</span></span> <span data-ttu-id="1f7e8-163">Merhaba sağ üst köşedeki bu kılavuz, küçük, yeşil olduğundan "+" düğmesini tıklatın, bu toocreate yeni bir kural tıklayın (Not: güvenlik duvarını "değişiklikleri kilitlenebilir", bir düğme "Kilitleme" olarak işaretlenmiş ve güncelleştirilemiyor toocreate olan veya kuralları düzenlemek, tıklatın görürseniz bu düğme çok "kilidini" Merhaba RuleSet ve düzenlenmesine izin verilir).</span><span class="sxs-lookup"><span data-stu-id="1f7e8-163">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello ruleset and allow editing).</span></span> <span data-ttu-id="1f7e8-164">Mevcut bir kuralı tooedit istiyorsanız, o kural seçin, sağ tıklayın ve kuralını Düzenle seçin.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-164">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="1f7e8-165">Yeni bir kural oluşturmak ve "WebTraffic" gibi bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="1f7e8-166">Merhaba hedef NAT kuralı simgesi şu şekilde görünür: ![hedef NAT simgesi][2]</span><span class="sxs-lookup"><span data-stu-id="1f7e8-166">hello Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="1f7e8-167">Merhaba kural kendisini şunun gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-167">hello rule itself would look something like this:</span></span>

<span data-ttu-id="1f7e8-168">![Güvenlik Duvarı Kuralı][3]</span><span class="sxs-lookup"><span data-stu-id="1f7e8-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="1f7e8-169">Burada isabet tooreach HTTP (80 veya 443 HTTPS için bağlantı noktası) çalışırken güvenlik duvarı hello herhangi bir gelen adresi gönderilecek hello güvenlik duvarının "DHCP1 yerel IP" arabirimi ve yeniden yönlendirilen toohello hello 10.0.1.5 IP adresi ile Web sunucusu.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-169">Here any inbound address that hits hello Firewall trying tooreach HTTP (port 80 or 443 for HTTPS) will be sent out hello Firewall’s “DHCP1 Local IP” interface and redirected toohello Web Server with hello IP Address of 10.0.1.5.</span></span> <span data-ttu-id="1f7e8-170">Merhaba trafiği 80 numaralı bağlantı noktası ve bağlantı noktası 80 üzerinde devam eden toohello web sunucusu üzerinde gelen bu yana hiçbir bağlantı noktası değişikliği gerekiyordu.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-170">Since hello traffic is coming in on port 80 and going toohello web server on port 80 no port change was needed.</span></span> <span data-ttu-id="1f7e8-171">Ancak, bizim Web sunucusu bağlantı noktası 8080 böylece çevirirken kulak varsa, hedef listesi 10.0.1.5:8080 neden olmuştur hello gelen bağlantı noktası 80 hello güvenlik duvarı tooinbound bağlantı noktası 8080 üzerinde hello web sunucusu hello.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-171">However, hello Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating hello inbound port 80 on hello firewall tooinbound port 8080 on hello web server.</span></span>

<span data-ttu-id="1f7e8-172">Bağlantı yöntemi de, hello hedef kural hello Internet'ten gelen için "Dinamik SNAT" en uygun olan miktarlara.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-172">A Connection Method should also be signified, for hello Destination Rule from hello Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="1f7e8-173">Yalnızca bir kural oluşturuldu ancak önceliği doğru ayarlandığından emin önemlidir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="1f7e8-174">Merhaba Güvenlik Duvarı'nda tüm kuralların hello kılavuzunda Yeni kuralın (aşağıda hello "BLOCKALL" kuralı) hello altta ise hiçbir zaman oyuna gelecektir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-174">If in hello grid of all rules on hello firewall this new rule is on hello bottom (below hello "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="1f7e8-175">Yeni oluşturulan hello kuralı web trafiği için hello BLOCKALL kuralı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-175">Ensure hello newly created rule for web traffic is above hello BLOCKALL rule.</span></span>

<span data-ttu-id="1f7e8-176">Merhaba kural oluşturulduktan sonra olmalıdır gönderilen toohello Güvenlik Duvarı'nı ve etkinleştirildi, bu değişiklik değil kazanacak hello kural yapılmazsa.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-176">Once hello rule is created, it must be pushed toohello firewall and then activated, if this is not done hello rule change will not take effect.</span></span> <span data-ttu-id="1f7e8-177">Merhaba itme ve etkinleştirme işlemi hello sonraki bölümde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-177">hello push and activation process is described in hello next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="1f7e8-178">Kural etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1f7e8-178">Rule Activation</span></span>
<span data-ttu-id="1f7e8-179">Merhaba ile ruleset tooadd bu kural değiştiren, hello ruleset olmalıdır toohello Güvenlik Duvarı'nı karşıya ve etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-179">With hello ruleset modified tooadd this rule, hello ruleset must be uploaded toohello firewall and activated.</span></span>

<span data-ttu-id="1f7e8-180">![Güvenlik duvarı kuralını etkinleştirme][4]</span><span class="sxs-lookup"><span data-stu-id="1f7e8-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="1f7e8-181">Merhaba üst sağ köşesinde hello management istemcisi düğmeleri oluşan bir küme var.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-181">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="1f7e8-182">Merhaba "değişiklikleri" Gönder düğmesi toosend değiştiren hello kuralları toohello güvenlik duvarı, ardından hello "Etkinleştir" düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-182">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="1f7e8-183">Merhaba güvenlik duvarı ruleset Hello etkinleştirme ile bu örnek ortamı yapı tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-183">With hello activation of hello firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="1f7e8-184">İsteğe bağlı olarak, hello post yapı hello betiklerde bölüm olabilir başvuruları tooadd bir uygulama toothis ortam tootest hello trafiği senaryolar aşağıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-184">Optionally, hello post build scripts in hello References section can be run tooadd an application toothis environment tootest hello below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f7e8-185">Bu, hello web sunucusuna doğrudan karşılaşır değil, kritik toorealize olur.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-185">It is critical toorealize that you will not hit hello web server directly.</span></span> <span data-ttu-id="1f7e8-186">Bir tarayıcı FrontEnd001.CloudApp.Net HTTP sayfası istediğinde, bu trafiği toohello Güvenlik Duvarı'nı değil hello hello HTTP uç noktası (bağlantı noktası 80) geçişleri web sunucusu.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, hello HTTP endpoint (port 80) passes this traffic toohello firewall not hello web server.</span></span> <span data-ttu-id="1f7e8-187">Güvenlik Duvarı hello sonra toohello kural according toohello Web sunucusu isteği NAT yukarıdaki oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-187">hello firewall then, according toohello rule created above, NATs that request toohello Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="1f7e8-188">Trafik senaryoları</span><span class="sxs-lookup"><span data-stu-id="1f7e8-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-tooweb-server-through-firewall"></a><span data-ttu-id="1f7e8-189">(İzin verilir) Web tooWeb sunucu güvenlik duvarı üzerinden</span><span class="sxs-lookup"><span data-stu-id="1f7e8-189">(Allowed) Web tooWeb Server through Firewall</span></span>
1. <span data-ttu-id="1f7e8-190">Internet kullanıcı istekleri HTTP sayfasına FrontEnd001.CloudApp.Net (Internet'e yönelik bulut hizmeti)</span><span class="sxs-lookup"><span data-stu-id="1f7e8-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="1f7e8-191">Bulut hizmeti geçiş trafiği 80 numaralı bağlantı noktasını toofirewall yerel arabirimdeki 10.0.1.4:80 üzerinde açık uç noktası aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="1f7e8-191">Cloud service passes traffic through open endpoint on port 80 toofirewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="1f7e8-192">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1f7e8-193">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="1f7e8-194">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="1f7e8-195">NSG kural 3 (Internet tooFirewall) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-195">NSG Rule 3 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="1f7e8-196">Merhaba Güvenlik Duvarı (10.0.1.4) iç IP adresi trafik isabetler</span><span class="sxs-lookup"><span data-stu-id="1f7e8-196">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="1f7e8-197">Güvenlik Duvarı iletme kuralı bkz: Bu bağlantı noktası 80 trafiği, toohello web sunucusuna IIS01 yönlendirir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-197">Firewall forwarding rule see this is port 80 traffic, redirects it toohello web server IIS01</span></span>
6. <span data-ttu-id="1f7e8-198">IIS01 web trafiği için dinleme, bu isteği alır ve hello isteği işlemeye başlıyor</span><span class="sxs-lookup"><span data-stu-id="1f7e8-198">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
7. <span data-ttu-id="1f7e8-199">IIS01 hello SQL Server AppVM01 hakkında bilgi için sorar</span><span class="sxs-lookup"><span data-stu-id="1f7e8-199">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="1f7e8-200">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="1f7e8-201">Merhaba arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-201">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1f7e8-202">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-202">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="1f7e8-203">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-203">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="1f7e8-204">NSG kuralı 3 (Internet tooFirewall) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-204">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="1f7e8-205">NSG kuralı 4 (IIS01 tooAppVM01) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-205">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="1f7e8-206">AppVM01 hello SQL sorgusu alır ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="1f7e8-206">AppVM01 receives hello SQL Query and responds</span></span>
11. <span data-ttu-id="1f7e8-207">Olduğundan hiçbir giden kuralları hello arka uç alt hello yanıt üzerinde izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-207">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
12. <span data-ttu-id="1f7e8-208">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="1f7e8-209">Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok</span><span class="sxs-lookup"><span data-stu-id="1f7e8-209">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="1f7e8-210">Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-210">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
13. <span data-ttu-id="1f7e8-211">Merhaba IIS sunucusu hello SQL yanıtı alır ve hello HTTP yanıtı tamamlar ve toohello istek gönderir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-211">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
14. <span data-ttu-id="1f7e8-212">Bir NAT oturumu hello Güvenlik Duvarı'ndan olduğundan, hello yanıt hedef Merhaba Güvenlik Duvarı'nı (başlangıçta) kalır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-212">Since this is a NAT session from hello firewall, hello response destination (initially) is for hello Firewall</span></span>
15. <span data-ttu-id="1f7e8-213">Merhaba güvenlik duvarı hello Web sunucusu hello yanıtı alır ve geri toohello Internet kullanıcı iletir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-213">hello firewall receives hello response from hello Web Server and forwards back toohello Internet User</span></span>
16. <span data-ttu-id="1f7e8-214">Olduğundan hiçbir giden kuralları hello ön uç alt hello yanıt üzerinde izin verilir ve hello web sayfasının hello Internet kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-214">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="1f7e8-215">(İzin verilir) RDP tooBackend</span><span class="sxs-lookup"><span data-stu-id="1f7e8-215">(Allowed) RDP tooBackend</span></span>
1. <span data-ttu-id="1f7e8-216">Sunucu Yöneticisi internet üzerindeki istekleri xxxxx RDP tooAppVM01 hello rastgele atanan bağlantı noktası numarası olduğu BackEnd001.CloudApp.Net:xxxxx üzerinde RDP oturumu tooAppVM01 (Merhaba atanan bağlantı noktası bulunabilir hello Azure Portal veya PowerShell aracılığıyla)</span><span class="sxs-lookup"><span data-stu-id="1f7e8-216">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="1f7e8-217">Güvenlik Duvarı yalnızca FrontEnd001.CloudApp.Net adresi hello üzerinde dinleme hello itibaren bu trafik akışı ile dahil değil</span><span class="sxs-lookup"><span data-stu-id="1f7e8-217">Since hello Firewall is only listening on hello FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="1f7e8-218">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1f7e8-219">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-219">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="1f7e8-220">NSG kuralı 2 (RDP) uygulamak için izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="1f7e8-221">Hiçbir giden kuralları, varsayılan kuralları uygula ve dönüş trafiğine izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="1f7e8-222">RDP oturumu etkin</span><span class="sxs-lookup"><span data-stu-id="1f7e8-222">RDP session is enabled</span></span>
6. <span data-ttu-id="1f7e8-223">Kullanıcı adı ve parolasını AppVM01 ister</span><span class="sxs-lookup"><span data-stu-id="1f7e8-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="1f7e8-224">(İzin verilir) DNS sunucusundaki Web sunucusu DNS araması</span><span class="sxs-lookup"><span data-stu-id="1f7e8-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="1f7e8-225">Sunucu, IIS01, gereksinimlerini www.data.gov bir veri akışı web ancak tooresolve adresi hello.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="1f7e8-226">Merhaba ağ yapılandırma hello VNet listeleri DNS01 (10.0.2.4 hello arka uç alt ağdaki) hello birincil DNS sunucusu olarak, IIS01 hello DNS isteği tooDNS01 gönderir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-226">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="1f7e8-227">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="1f7e8-228">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1f7e8-229">NSG kural 1 (DNS) uygulamak için izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="1f7e8-230">DNS sunucusu hello isteği alır</span><span class="sxs-lookup"><span data-stu-id="1f7e8-230">DNS server receives hello request</span></span>
6. <span data-ttu-id="1f7e8-231">DNS sunucusu önbelleğe hello adresi yoksa ve bir kök DNS sunucusu üzerinde hello ister Internet</span><span class="sxs-lookup"><span data-stu-id="1f7e8-231">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="1f7e8-232">Hiçbir giden kuralları arka uç alt ağdaki trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="1f7e8-233">Bu oturumda dahili olarak başlatıldı beri Internet DNS sunucusu yanıt, hello yanıt izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-233">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="1f7e8-234">DNS sunucusu hello yanıtı önbelleğe alır ve toohello ilk isteği geri tooIIS01 yanıt verir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-234">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="1f7e8-235">Hiçbir giden kuralları arka uç alt ağdaki trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="1f7e8-236">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="1f7e8-237">Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok</span><span class="sxs-lookup"><span data-stu-id="1f7e8-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="1f7e8-238">Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır</span><span class="sxs-lookup"><span data-stu-id="1f7e8-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="1f7e8-239">IIS01 hello yanıt DNS01 alır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-239">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="1f7e8-240">(İzin verilir) Web sunucusu erişimini dosyasını AppVM01 üzerinde</span><span class="sxs-lookup"><span data-stu-id="1f7e8-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="1f7e8-241">Bir dosyanın AppVM01 IIS01 sorar</span><span class="sxs-lookup"><span data-stu-id="1f7e8-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="1f7e8-242">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="1f7e8-243">Merhaba arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-243">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1f7e8-244">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-244">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="1f7e8-245">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-245">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="1f7e8-246">NSG kuralı 3 (Internet tooFirewall) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-246">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="1f7e8-247">NSG kuralı 4 (IIS01 tooAppVM01) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-247">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="1f7e8-248">AppVM01 hello isteğini alır ve (erişim yetkisi varsayılarak) dosyası ile yanıt verir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-248">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="1f7e8-249">Olduğundan hiçbir giden kuralları hello arka uç alt hello yanıt üzerinde izin verilir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-249">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
6. <span data-ttu-id="1f7e8-250">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1f7e8-251">Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok</span><span class="sxs-lookup"><span data-stu-id="1f7e8-251">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="1f7e8-252">Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-252">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="1f7e8-253">Merhaba IIS sunucu hello dosya alır</span><span class="sxs-lookup"><span data-stu-id="1f7e8-253">hello IIS server receives hello file</span></span>

#### <a name="denied-web-direct-tooweb-server"></a><span data-ttu-id="1f7e8-254">(Reddedildi) Web doğrudan tooWeb sunucu</span><span class="sxs-lookup"><span data-stu-id="1f7e8-254">(Denied) Web direct tooWeb Server</span></span>
<span data-ttu-id="1f7e8-255">Merhaba Web sunucusu, IIS01 ve hello Güvenlik Duvarı bu yana olan hello paylaştıkları aynı bulut hizmetine hello aynı genel kullanıma yönelik IP adresi.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-255">Since hello Web Server, IIS01, and hello Firewall are in hello same Cloud Service they share hello same public facing IP address.</span></span> <span data-ttu-id="1f7e8-256">Bu nedenle herhangi bir HTTP trafiğini yönlendirilmiş toohello güvenlik duvarı.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-256">Thus any HTTP traffic would be directed toohello firewall.</span></span> <span data-ttu-id="1f7e8-257">Merhaba isteği başarıyla sundu, ancak toohello Web sunucusu, kendisine geçirilen doğrudan bu tasarlandığı gibi dönülemez güvenlik duvarı hello ilk.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-257">While hello request would be successfully served, it cannot go directly toohello Web Server, it passed, as designed, through hello Firewall first.</span></span> <span data-ttu-id="1f7e8-258">Bkz: Merhaba trafik akışı için bu bölümdeki ilk senaryoda hello.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-258">See hello first Scenario in this section for hello traffic flow.</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="1f7e8-259">(Reddedildi) Web tooBackend sunucu</span><span class="sxs-lookup"><span data-stu-id="1f7e8-259">(Denied) Web tooBackend Server</span></span>
1. <span data-ttu-id="1f7e8-260">Internet kullanıcı tooaccess AppVM01 bir dosyada hello BackEnd001.CloudApp.Net hizmeti ile çalışır</span><span class="sxs-lookup"><span data-stu-id="1f7e8-260">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="1f7e8-261">Dosya Paylaşımı için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="1f7e8-261">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="1f7e8-262">NSG kural 5 (Internet tooVNet) Hello uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller</span><span class="sxs-lookup"><span data-stu-id="1f7e8-262">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="1f7e8-263">(Reddedildi) DNS sunucusundaki Web DNS araması</span><span class="sxs-lookup"><span data-stu-id="1f7e8-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="1f7e8-264">Internet kullanıcı toolookup DNS01 hello BackEnd001.CloudApp.Net hizmeti aracılığıyla bir iç DNS kaydını çalışır</span><span class="sxs-lookup"><span data-stu-id="1f7e8-264">Internet user tries toolookup an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="1f7e8-265">DNS için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="1f7e8-265">Since there are no endpoints open for DNS, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="1f7e8-266">NSG kural 5 (Internet tooVNet) Hello uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller (Not: Bu kural 1 (DNS), iki nedenden dolayı geçerli değil, ilk hello kaynak adresi Internet Merhaba, toohello yalnızca bu kuralın uygulanacağı hello olarak yerel VNet kaynak, aynı zamanda hiçbir zaman trafiği reddetmeye şekilde bir izin verme kuralı budur)</span><span class="sxs-lookup"><span data-stu-id="1f7e8-266">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="1f7e8-267">(Reddedildi) Güvenlik Duvarı aracılığıyla Web tooSQL erişimi</span><span class="sxs-lookup"><span data-stu-id="1f7e8-267">(Denied) Web tooSQL access through Firewall</span></span>
1. <span data-ttu-id="1f7e8-268">Internet kullanıcı SQL verileri FrontEnd001.CloudApp.Net (Internet'e yönelik bulut hizmeti) ' ister.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="1f7e8-269">SQL için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello güvenlik duvarı ulaşmak olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="1f7e8-269">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="1f7e8-270">Uç noktaları için herhangi bir nedenle açıksa, hello ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-270">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="1f7e8-271">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-271">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="1f7e8-272">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="1f7e8-272">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="1f7e8-273">NSG Kural 2 (Internet tooFirewall) uygulamak için izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="1f7e8-273">NSG Rule 2 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="1f7e8-274">Merhaba Güvenlik Duvarı (10.0.1.4) iç IP adresi trafik isabetler</span><span class="sxs-lookup"><span data-stu-id="1f7e8-274">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="1f7e8-275">Güvenlik Duvarı için SQL iletme kuralları yok ve trafik düşme hello</span><span class="sxs-lookup"><span data-stu-id="1f7e8-275">Firewall has no forwarding rules for SQL and drops hello traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="1f7e8-276">Sonuç</span><span class="sxs-lookup"><span data-stu-id="1f7e8-276">Conclusion</span></span>
<span data-ttu-id="1f7e8-277">Bu bir güvenlik duvarı ile uygulamanızı koruma ve hello arka uç alt ağından gelen trafiği yalıtma göreceli olarak doğrudan ileriye doğru bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-277">This is a relatively straight forward way of protecting your application with a firewall and isolating hello back end subnet from inbound traffic.</span></span>

<span data-ttu-id="1f7e8-278">Daha fazla örnekler ve ağ güvenlik sınırları genel bir bakış bulunabilir [burada][HOME].</span><span class="sxs-lookup"><span data-stu-id="1f7e8-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="1f7e8-279">Başvurular</span><span class="sxs-lookup"><span data-stu-id="1f7e8-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="1f7e8-280">Ana komut dosyası ve ağ yapılandırması</span><span class="sxs-lookup"><span data-stu-id="1f7e8-280">Main Script and Network Config</span></span>
<span data-ttu-id="1f7e8-281">Merhaba tam komut dosyası bir PowerShell komut dosyası kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-281">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="1f7e8-282">Merhaba ağ yapılandırma "NetworkConf2.xml" adlı bir dosyaya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-282">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="1f7e8-283">Merhaba kullanıcı tanımlı değişkenleri gerektiği gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-283">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="1f7e8-284">Merhaba komut dosyasını çalıştırın, ardından hello güvenlik duvarı kuralı kurulum yönergeleri yukarıdaki izleyin.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-284">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="1f7e8-285">Tam komut dosyası</span><span class="sxs-lookup"><span data-stu-id="1f7e8-285">Full Script</span></span>
<span data-ttu-id="1f7e8-286">Merhaba kullanıcı tanımlı değişkenleri esas alarak bu betiği olur:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-286">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="1f7e8-287">Tooan Azure aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="1f7e8-287">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="1f7e8-288">Yeni depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f7e8-288">Create a new storage account</span></span>
3. <span data-ttu-id="1f7e8-289">Yeni bir VNet ve hello ağ yapılandırma dosyasında tanımlanan iki alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f7e8-289">Create a new VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="1f7e8-290">4 windows server Vm'lerinin oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f7e8-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="1f7e8-291">NSG dahil olmak üzere yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="1f7e8-291">Configure NSG including:</span></span>
   * <span data-ttu-id="1f7e8-292">Bir NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f7e8-292">Creating a NSG</span></span>
   * <span data-ttu-id="1f7e8-293">Kuralları ile doldurma</span><span class="sxs-lookup"><span data-stu-id="1f7e8-293">Populating it with rules</span></span>
   * <span data-ttu-id="1f7e8-294">Merhaba NSG toohello uygun alt ağları bağlama</span><span class="sxs-lookup"><span data-stu-id="1f7e8-294">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="1f7e8-295">Bu PowerShell Betiği, bir bilgisayar veya sunucu, Internet'e yerel olarak çalıştırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f7e8-296">Bu komut dosyasını çalıştırdığınızda, uyarı veya PowerShell'de pop diğer bilgilendirici iletileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="1f7e8-297">Yalnızca hata iletileri kırmızı sorunu nedeni edilir.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-297">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
       - Three Servers on hello BackEnd Subnet
       - Network Security Groups tooallow/deny traffic patterns as declared

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Security requirements are different for each use case and can be addressed in a
      myriad of ways. Please be sure that any sensitive data or applications are behind
      hello appropriate layer(s) of protection. This script serves as an example of some
      of hello techniques that can be used, but should not be used for all scenarios. You
      are responsible tooassess your security needs and hello appropriate protections
      needed, and then effectively implement those protections.

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       myFirewall - 10.0.1.4
       IIS01      - 10.0.1.5

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
            -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
            -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
            -Protocol *

        # Assign hello NSG toohello Subnets
            Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="1f7e8-298">Ağ yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="1f7e8-298">Network Config File</span></span>
<span data-ttu-id="1f7e8-299">Güncelleştirilmiş konumla bu xml dosyasını kaydedin ve hello bağlantı toothis toohello $NetworkConfigFile değişkeni yukarıdaki hello komut dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1f7e8-299">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a><span data-ttu-id="1f7e8-300">Örnek uygulama komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="1f7e8-300">Sample Application Scripts</span></span>
<span data-ttu-id="1f7e8-301">Bu ve diğer çevre örnekleri için örnek bir uygulama tooinstall istiyorsanız, bir bağlantı aşağıdaki hello sağlanmış: [örnek uygulama betiği][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="1f7e8-301">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "NSG ile giriş DMZ"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Hedef NAT simgesi"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Güvenlik Duvarı Kuralı"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Güvenlik duvarı kuralını etkinleştirme"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
