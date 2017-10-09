---
title: "aaaAzure DMZ örnek – yapı Nsg'ler ile basit DMZ | Microsoft Docs"
description: "Bir çevre ağ güvenlik grupları (NSG) ile derleme"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="8dadd-103">Örnek 1 – Nsg'ler ile klasik PowerShell kullanarak basit bir DMZ derleme</span><span class="sxs-lookup"><span data-stu-id="8dadd-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="8dadd-104">[Dönüş toohello güvenlik sınırı en iyi uygulamalar sayfası][HOME]</span><span class="sxs-lookup"><span data-stu-id="8dadd-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8dadd-105">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="8dadd-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="8dadd-106">Klasik - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8dadd-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="8dadd-107">Bu örnekte basit DMZ dört Windows sunucuları ve ağ güvenlik grupları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8dadd-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="8dadd-108">Bu örnek hello ilgili PowerShell komutları tooprovide her adımın daha derin bir anlayış açıklar.</span><span class="sxs-lookup"><span data-stu-id="8dadd-108">This example describes each of hello relevant PowerShell commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="8dadd-109">Ayrıca vardır bir trafik senaryo bölüm tooprovide ayrıntılı bir adım adım derinlemesine savunma hello katmanları üzerinden trafik geçer nasıl DMZ hello.</span><span class="sxs-lookup"><span data-stu-id="8dadd-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="8dadd-110">Son olarak, hello references bölümünde hello tam kod ve yönerge toobuild bu ortam tootest çeşitli senaryoları ile deneme ise.</span><span class="sxs-lookup"><span data-stu-id="8dadd-110">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="8dadd-111">![NSG ile giriş DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="8dadd-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="8dadd-112">Ortam açıklaması</span><span class="sxs-lookup"><span data-stu-id="8dadd-112">Environment description</span></span>
<span data-ttu-id="8dadd-113">Bu örnekte, abonelik kaynakları aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="8dadd-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="8dadd-114">İki bulut hizmetlerini: "FrontEnd001" ve "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="8dadd-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="8dadd-115">Sanal ağ, "CorpNetwork" iki alt ağı; "Ön uç" ve "Arka uç"</span><span class="sxs-lookup"><span data-stu-id="8dadd-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="8dadd-116">Uygulanan tooboth alt ağıdır bir ağ güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="8dadd-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="8dadd-117">Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="8dadd-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="8dadd-118">Uygulama arka uç sunucuları ("AppVM01", "AppVM02") temsil eden iki windows sunucuları</span><span class="sxs-lookup"><span data-stu-id="8dadd-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="8dadd-119">Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="8dadd-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="8dadd-120">Merhaba references bölümünde bu örnekte açıklanan hello ortamı çoğunu derlemeler bir PowerShell komut dosyası yok.</span><span class="sxs-lookup"><span data-stu-id="8dadd-120">In hello references section, there is a PowerShell script that builds most of hello environment described in this example.</span></span> <span data-ttu-id="8dadd-121">Yapı hello VM'ler ve sanal ağlar, bu belgede ayrıntılı hello örnek komut dosyası tarafından yapılır rağmen açıklanmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="8dadd-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="8dadd-122">toobuild hello ortam;</span><span class="sxs-lookup"><span data-stu-id="8dadd-122">toobuild hello environment;</span></span>

1. <span data-ttu-id="8dadd-123">(Adları, konum ve IP adreslerini toomatch verilen hello senaryo güncelleştirilmiş) hello başvurular bölümüne dahil hello ağ yapılandırma xml dosyasını kaydedin</span><span class="sxs-lookup"><span data-stu-id="8dadd-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="8dadd-124">Güncelleştirme hello kullanıcı değişkenleri hello betik toomatch hello ortamı hello komut olan toobe Çalıştır (Abonelikleri, hizmet adlarını vb. karşı.)</span><span class="sxs-lookup"><span data-stu-id="8dadd-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="8dadd-125">PowerShell'de Hello komut dosyası yürütme</span><span class="sxs-lookup"><span data-stu-id="8dadd-125">Execute hello script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="8dadd-126">Merhaba PowerShell Betiği miktarlara hello bölge hello ağ yapılandırması xml dosyasında miktarlara hello bölge ile eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-126">hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>
>
>

<span data-ttu-id="8dadd-127">Merhaba komut dosyasını başarıyla ek çalıştırır sonra isteğe bağlı adımlar izlenebilir, hello references bölümünde hello web sunucusu ve uygulama sunucusu bu DMZ yapılandırma ile test basit bir web uygulaması tooallow ile iki komut dosyaları tooset.</span><span class="sxs-lookup"><span data-stu-id="8dadd-127">Once hello script runs successfully additional optional steps may be taken, in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="8dadd-128">Hello aşağıdaki bölümlerde ağ güvenlik grupları ve bunların Bu örnek için anahtar hello PowerShell Betiği satırları arasında adım adım ilerlemenizi sağlayarak işlevleri ayrıntılı bir açıklama belirtin.</span><span class="sxs-lookup"><span data-stu-id="8dadd-128">hello following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of hello PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="8dadd-129">Ağ Güvenlik Grupları (NSG)</span><span class="sxs-lookup"><span data-stu-id="8dadd-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="8dadd-130">Bu örnekte, bir NSG grubu yerleşik ve altı kurallarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="8dadd-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="8dadd-131">Genel olarak bakıldığında, belirli "İzin ver" kurallarınızı ilk oluşturun ve daha genel "Deny" kuralları son hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-131">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="8dadd-132">öncelik atanmış hello hangi kuralları ilk olarak değerlendirilir belirler.</span><span class="sxs-lookup"><span data-stu-id="8dadd-132">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="8dadd-133">Trafik tooapply tooa belirli kural bulunduktan sonra başka hiçbir kural değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-133">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="8dadd-134">NSG kuralları hello ikisinde uygulayabileceğiniz gelen veya giden yön (Merhaba alt hello açısından).</span><span class="sxs-lookup"><span data-stu-id="8dadd-134">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="8dadd-135">Bildirimli olarak, kurallar aşağıdaki hello gelen trafik için oluşturulmakta:</span><span class="sxs-lookup"><span data-stu-id="8dadd-135">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="8dadd-136">İç DNS trafiğinin (bağlantı noktası 53) izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="8dadd-137">Merhaba Internet tooany VM gelen RDP trafiğine (3389 numaralı bağlantı noktası) izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-137">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="8dadd-138">Itanium tabanlı sistemler için HTTP trafiğine (bağlantı noktası 80) hello Internet tooweb sunucusundan (IIS01) izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-138">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="8dadd-139">IIS01 tooAppVM1 tüm trafiği (tüm bağlantı noktaları) izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-139">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="8dadd-140">Merhaba Internet toohello tüm trafiği (tüm bağlantı noktaları) tüm sanal ağ (her iki alt ağ) reddedildi</span><span class="sxs-lookup"><span data-stu-id="8dadd-140">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="8dadd-141">Merhaba ön uç alt toohello arka uç alt ağından gelen tüm trafiği (tüm bağlantı noktaları) reddedildi</span><span class="sxs-lookup"><span data-stu-id="8dadd-141">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="8dadd-142">Bu kurallar ilişkili tooeach alt ağ ile bir HTTP isteği hello Internet toohello web sunucusundan gelen ise her ikisi de kuralları 3 (izin verin) ve 5 (uygulamak reddetme), ancak 3 kuralı, yalnızca geçerli olur ve kural 5 oyuna değil gelen daha yüksek öncelikli olduğundan.</span><span class="sxs-lookup"><span data-stu-id="8dadd-142">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="8dadd-143">Bu nedenle hello HTTP isteği toohello web sunucusu izin.</span><span class="sxs-lookup"><span data-stu-id="8dadd-143">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="8dadd-144">Bu aynı trafiği tooreach hello DNS01 sunucusunu denemeden ise hello ilk tooapply ve hello trafiği toopass toohello sunucu verilmez kural 5 (Reddet) olabilir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-144">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="8dadd-145">Kural 6 (Reddet) toohello arka uç alt (dışında izin verilen trafiği kurallarında 1 ve 4) Konuşmayı gelen hello ön uç alt ağ blokları, hello saldırganın bir saldırganın güvenlik ihlalleri hello web uygulamasına hello ön uç misiniz durumunda bu kural kümesine hello arka uç ağ korur. arka uç "Korumalı ağ (yalnızca tooresources hello AppVM01 sunucu üzerinde gösterilen)" erişim toohello sınırlı.</span><span class="sxs-lookup"><span data-stu-id="8dadd-145">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="8dadd-146">Toohello giden trafiğe izin veren varsayılan giden kural Internet.</span><span class="sxs-lookup"><span data-stu-id="8dadd-146">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="8dadd-147">Bu örnekte, biz giden trafiğe izin vermek ve herhangi bir giden kuralı değiştirme değil.</span><span class="sxs-lookup"><span data-stu-id="8dadd-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="8dadd-148">Her iki yönde trafik aşağı toolock, kullanıcı tanımlanan yönlendirme gereklidir ve "Örnek 3" Merhaba üzerinde incelediniz [güvenlik sınırı en iyi yöntemler sayfası][HOME].</span><span class="sxs-lookup"><span data-stu-id="8dadd-148">toolock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="8dadd-149">Her kural aşağıdaki gibi daha ayrıntılı olarak ele (**Not**: dolar işareti listesi başlayarak aşağıdaki hello herhangi bir öğeye (örneğin: $NSGName) kullanıcı tanımlı değişken hello başvuru bölümünde, bu belgenin hello betikten):</span><span class="sxs-lookup"><span data-stu-id="8dadd-149">Each rule is discussed in more detail as follows (**Note**: any item in hello following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="8dadd-150">İlk ağ güvenlik grubu toohold hello kuralları oluşturulmalıdır:</span><span class="sxs-lookup"><span data-stu-id="8dadd-150">First a Network Security Group must be built toohold hello rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="8dadd-151">Bu örnekte Hello ilk kural hello arka uç alt ağdaki tüm İç ağlara toohello DNS sunucusu arasında DNS trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-151">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="8dadd-152">Merhaba kuralı bazı önemli parametreler sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8dadd-152">hello rule has some important parameters:</span></span>
   
   * <span data-ttu-id="8dadd-153">"Tür" trafik akışı hangi yönde bu kural etkinleşir belirtir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="8dadd-154">Merhaba yönünü (bağlı olarak bu NSG burada bağlı) hello açısından hello alt ağı veya sanal makine değil.</span><span class="sxs-lookup"><span data-stu-id="8dadd-154">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="8dadd-155">Bu nedenle türüdür "Giriş" ve trafiği hello alt girerek, hello kuralın ve hello alt ağdan çıkan trafiğe etkilenmemiştir bu kural tarafından durumunda.</span><span class="sxs-lookup"><span data-stu-id="8dadd-155">Thus if Type is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="8dadd-156">"Öncelik" Merhaba sırasını trafik akışı değerlendirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="8dadd-156">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="8dadd-157">Merhaba alt hello sayı hello yüksek hello önceliği.</span><span class="sxs-lookup"><span data-stu-id="8dadd-157">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="8dadd-158">Tooa belirli bir trafik akışı bir kural uygulandığı zaman başka hiçbir kural işlenir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-158">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="8dadd-159">Bu nedenle öncelik 1 olan bir kural trafiğine izin verir ve trafiği, öncelik 2 olan bir kural reddeder ve tootraffic hem kuralları uygula durumunda hello trafiği tooflow izin (Kural 1 yüksek önceliğe sahip olduğundan etkisi sürdü ve başka hiçbir kural uygulanan).</span><span class="sxs-lookup"><span data-stu-id="8dadd-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="8dadd-160">Bu kural tarafından etkilenen trafiği engellendi veya izin verilen "Eylem" belirtir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="8dadd-161">Bu kural, alt ağ RDP trafiğine tooflow hello herhangi bir sunucuda hello Internet toohello RDP bağlantı noktasından bağlı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8dadd-161">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> <span data-ttu-id="8dadd-162">Bu kural adres öneklerini iki özel tür kullanır; "Vırtual_network" ve "INTERNET."</span><span class="sxs-lookup"><span data-stu-id="8dadd-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="8dadd-163">Bu etiketler kolay bir yolu tooaddress adres öneklerini daha büyük bir kategoride var.</span><span class="sxs-lookup"><span data-stu-id="8dadd-163">These tags are an easy way tooaddress a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="8dadd-164">Bu kural gelen Internet trafiği toohit hello web sunucusu sağlar.</span><span class="sxs-lookup"><span data-stu-id="8dadd-164">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="8dadd-165">Bu kural hello yönlendirme davranışını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="8dadd-165">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="8dadd-166">Merhaba kural yalnızca IIS01 toopass giden trafiğe izin verir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-166">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="8dadd-167">Bu nedenle hello Internet trafiği bu kural izin ve daha fazla kural işlemeyi durdur hedef olarak hello web sunucusunun sahip.</span><span class="sxs-lookup"><span data-stu-id="8dadd-167">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="8dadd-168">(Öncelikle hello kuralında 140 diğer tüm gelen Internet trafiğini engellendi).</span><span class="sxs-lookup"><span data-stu-id="8dadd-168">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="8dadd-169">Yalnızca HTTP trafiğini işlemek, bu kural başka olabilir kısıtlı tooonly hedef bağlantı noktası 80 izin verin.</span><span class="sxs-lookup"><span data-stu-id="8dadd-169">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="8dadd-170">Bu kural hello IIS01 sunucusundan trafiği toopass toohello AppVM01 sunucu izin verir; bir sonraki kural diğer tüm ön uç tooBackend trafiği engeller.</span><span class="sxs-lookup"><span data-stu-id="8dadd-170">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="8dadd-171">Bu kural, başlangıç bağlantı noktası biliniyorsa eklenmelidir tooimprove.</span><span class="sxs-lookup"><span data-stu-id="8dadd-171">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="8dadd-172">Merhaba IIS sunucusu yalnızca SQL Server'da AppVM01 basarsa, örneğin, hello hedef bağlantı noktası aralığı değiştirildiği "*" (tüm) too1433 (Merhaba SQL bağlantı noktası) böylece Merhaba web uygulaması hiç tehlikeye AppVM01 üzerinde daha küçük bir gelen saldırı yüzeyini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8dadd-172">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="8dadd-173">Bu kural hello Internet tooany sunucularından hello ağ üzerindeki trafiği engeller.</span><span class="sxs-lookup"><span data-stu-id="8dadd-173">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="8dadd-174">Hello kurallarıyla öncelikli 110 ve 120 hello etkisi tooallow yalnızca gelen Internet trafiği toohello güvenlik duvarı ve sunucularda RDP bağlantı noktalarını ve şey engeller.</span><span class="sxs-lookup"><span data-stu-id="8dadd-174">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="8dadd-175">Bu kural, "Ayrıcalık tanımayın" kural tooblock tüm beklenmeyen akışlar ' dir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-175">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="8dadd-176">Merhaba son kural hello ön uç alt toohello arka uç alt ağından trafiği engeller.</span><span class="sxs-lookup"><span data-stu-id="8dadd-176">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="8dadd-177">Bu kural yalnızca bir gelen kuralı olduğundan, geriye doğru trafiğinin (Merhaba arka uç toohello ön uç) izin verilir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="8dadd-178">Trafik senaryoları</span><span class="sxs-lookup"><span data-stu-id="8dadd-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="8dadd-179">(*İzin verilen*) Internet tooweb sunucusu</span><span class="sxs-lookup"><span data-stu-id="8dadd-179">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="8dadd-180">Bir Internet kullanıcı FrontEnd001.CloudApp.Net (Internet'e yönelik bulut hizmeti) istekler bir HTTP sayfası</span><span class="sxs-lookup"><span data-stu-id="8dadd-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="8dadd-181">Bulut hizmeti geçişleri trafiğini açık uç noktasını IIS01 doğru bağlantı noktası 80 üzerinden (Merhaba web sunucusu)</span><span class="sxs-lookup"><span data-stu-id="8dadd-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="8dadd-182">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="8dadd-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="8dadd-183">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="8dadd-183">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="8dadd-184">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="8dadd-184">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="8dadd-185">NSG kural 3 (Internet tooIIS01) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="8dadd-185">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="8dadd-186">İç IP adresi hello web sunucusunun IIS01 (10.0.1.5) trafiği isabetler</span><span class="sxs-lookup"><span data-stu-id="8dadd-186">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="8dadd-187">IIS01 web trafiği için dinleme, bu isteği alır ve hello isteği işlemeye başlıyor</span><span class="sxs-lookup"><span data-stu-id="8dadd-187">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="8dadd-188">IIS01 hello SQL Server AppVM01 hakkında bilgi için sorar</span><span class="sxs-lookup"><span data-stu-id="8dadd-188">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="8dadd-189">Ön uç alt ağda hiçbir giden kuralları olduğundan, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="8dadd-190">Merhaba arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="8dadd-190">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="8dadd-191">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="8dadd-191">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="8dadd-192">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="8dadd-192">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="8dadd-193">NSG kuralı 3 (Internet tooFirewall) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="8dadd-193">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="8dadd-194">NSG kuralı 4 (IIS01 tooAppVM01) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="8dadd-194">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="8dadd-195">AppVM01 hello SQL sorgusu alır ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="8dadd-195">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="8dadd-196">Merhaba arka uç alt ağda hiçbir giden kuralları olduğundan hello yanıt izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-196">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="8dadd-197">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="8dadd-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="8dadd-198">Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok</span><span class="sxs-lookup"><span data-stu-id="8dadd-198">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="8dadd-199">Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8dadd-199">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="8dadd-200">Merhaba IIS sunucusu hello SQL yanıtı alır ve hello HTTP yanıtı tamamlar ve toohello istek gönderir</span><span class="sxs-lookup"><span data-stu-id="8dadd-200">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
13. <span data-ttu-id="8dadd-201">Hello ön uç alt ağda hiçbir giden kuralları olduğundan hello yanıt izin verilir ve hello Internet kullanıcı hello web sayfasının alır.</span><span class="sxs-lookup"><span data-stu-id="8dadd-201">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="8dadd-202">(*İzin verilen*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="8dadd-202">(*Allowed*) RDP toobackend</span></span>
1. <span data-ttu-id="8dadd-203">Sunucu Yöneticisi internet üzerindeki istekleri xxxxx RDP tooAppVM01 hello rastgele atanan bağlantı noktası numarası olduğu BackEnd001.CloudApp.Net:xxxxx üzerinde RDP oturumu tooAppVM01 (Merhaba atanan bağlantı noktası bulunabilir hello Azure portal veya PowerShell aracılığıyla)</span><span class="sxs-lookup"><span data-stu-id="8dadd-203">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="8dadd-204">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="8dadd-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="8dadd-205">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="8dadd-205">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="8dadd-206">NSG kuralı 2 (RDP) uygulamak için izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="8dadd-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="8dadd-207">Hiçbir giden kuralları, varsayılan kuralları uygula ve dönüş trafiğine izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="8dadd-208">RDP oturumu etkin</span><span class="sxs-lookup"><span data-stu-id="8dadd-208">RDP session is enabled</span></span>
5. <span data-ttu-id="8dadd-209">AppVM01 hello kullanıcı adı ve parola isteyen</span><span class="sxs-lookup"><span data-stu-id="8dadd-209">AppVM01 prompts for hello user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="8dadd-210">(*İzin verilen*) Web sunucusu DNS araması DNS sunucusunda</span><span class="sxs-lookup"><span data-stu-id="8dadd-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="8dadd-211">Sunucu, IIS01, gereksinimlerini www.data.gov bir veri akışı web ancak tooresolve adresi hello.</span><span class="sxs-lookup"><span data-stu-id="8dadd-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="8dadd-212">Merhaba ağ yapılandırma hello VNet listeleri DNS01 (10.0.2.4 hello arka uç alt ağdaki) hello birincil DNS sunucusu olarak, IIS01 hello DNS isteği tooDNS01 gönderir</span><span class="sxs-lookup"><span data-stu-id="8dadd-212">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="8dadd-213">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="8dadd-214">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="8dadd-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="8dadd-215">NSG kural 1 (DNS) uygulamak için izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="8dadd-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="8dadd-216">DNS sunucusu hello isteği alır</span><span class="sxs-lookup"><span data-stu-id="8dadd-216">DNS server receives hello request</span></span>
6. <span data-ttu-id="8dadd-217">DNS sunucusu önbelleğe hello adresi yoksa ve bir kök DNS sunucusu üzerinde hello ister Internet</span><span class="sxs-lookup"><span data-stu-id="8dadd-217">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="8dadd-218">Hiçbir giden kuralları arka uç alt ağdaki trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="8dadd-219">Bu oturumda dahili olarak başlatıldı beri Internet DNS sunucusu yanıt, hello yanıt izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-219">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="8dadd-220">DNS sunucusu hello yanıtı önbelleğe alır ve toohello ilk isteği geri tooIIS01 yanıt verir</span><span class="sxs-lookup"><span data-stu-id="8dadd-220">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="8dadd-221">Hiçbir giden kuralları arka uç alt ağdaki trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="8dadd-222">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="8dadd-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="8dadd-223">Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok</span><span class="sxs-lookup"><span data-stu-id="8dadd-223">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="8dadd-224">Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır</span><span class="sxs-lookup"><span data-stu-id="8dadd-224">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="8dadd-225">IIS01 hello yanıt DNS01 alır.</span><span class="sxs-lookup"><span data-stu-id="8dadd-225">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="8dadd-226">(*İzin verilen*) Web sunucusu erişimini dosyasını AppVM01 üzerinde</span><span class="sxs-lookup"><span data-stu-id="8dadd-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="8dadd-227">Bir dosyanın AppVM01 IIS01 sorar</span><span class="sxs-lookup"><span data-stu-id="8dadd-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="8dadd-228">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="8dadd-229">Merhaba arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="8dadd-229">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="8dadd-230">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="8dadd-230">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="8dadd-231">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="8dadd-231">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="8dadd-232">NSG kuralı 3 (Internet tooIIS01) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="8dadd-232">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="8dadd-233">NSG kuralı 4 (IIS01 tooAppVM01) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="8dadd-233">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="8dadd-234">AppVM01 hello isteğini alır ve (erişim yetkisi varsayılarak) dosyası ile yanıt verir</span><span class="sxs-lookup"><span data-stu-id="8dadd-234">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="8dadd-235">Merhaba arka uç alt ağda hiçbir giden kuralları olduğundan hello yanıt izin verilir</span><span class="sxs-lookup"><span data-stu-id="8dadd-235">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="8dadd-236">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="8dadd-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="8dadd-237">Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok</span><span class="sxs-lookup"><span data-stu-id="8dadd-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="8dadd-238">Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8dadd-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="8dadd-239">Merhaba IIS sunucu hello dosya alır</span><span class="sxs-lookup"><span data-stu-id="8dadd-239">hello IIS server receives hello file</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="8dadd-240">(*Reddedildi*) Web toobackend sunucusu</span><span class="sxs-lookup"><span data-stu-id="8dadd-240">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="8dadd-241">Bir Internet kullanıcı tooaccess AppVM01 bir dosyada hello BackEnd001.CloudApp.Net hizmeti ile çalışır</span><span class="sxs-lookup"><span data-stu-id="8dadd-241">An internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="8dadd-242">Dosya Paylaşımı için açık uç nokta yok olduğundan, bu trafiği hello bulut hizmeti geçirmek değil'yı ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="8dadd-242">Since there are no endpoints open for file share, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="8dadd-243">NSG kural 5 (Internet tooVNet) Hello uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller</span><span class="sxs-lookup"><span data-stu-id="8dadd-243">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="8dadd-244">(*Reddedildi*) DNS sunucusunda Web DNS araması</span><span class="sxs-lookup"><span data-stu-id="8dadd-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="8dadd-245">Bir Internet kullanıcı çalıştığında toolook DNS01 hello BackEnd001.CloudApp.Net hizmeti aracılığıyla bir iç DNS kaydını ayarlama</span><span class="sxs-lookup"><span data-stu-id="8dadd-245">An internet user tries toolook up an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="8dadd-246">DNS için açık uç nokta yok olduğundan, bu trafiği hello bulut hizmeti geçirmek değil'yı ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="8dadd-246">Since there are no endpoints open for DNS, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="8dadd-247">NSG kural 5 (Internet tooVNet) Hello uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller (Not: Bu kural 1 (DNS), iki nedenden dolayı geçerli değil, ilk hello kaynak adresi Internet Merhaba, toohello yalnızca bu kuralın uygulanacağı hello olarak yerel VNet kaynak, aynı zamanda Bu kural bir izin verme kuralı olduğundan, hiçbir zaman trafiği reddetmeye)</span><span class="sxs-lookup"><span data-stu-id="8dadd-247">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="8dadd-248">(*Reddedildi*) Web güvenlik duvarı aracılığıyla tooSQL erişimi</span><span class="sxs-lookup"><span data-stu-id="8dadd-248">(*Denied*) Web tooSQL access through firewall</span></span>
1. <span data-ttu-id="8dadd-249">Bir Internet kullanıcının SQL verileri FrontEnd001.CloudApp.Net (Internet'e yönelik bulut hizmeti) ' ister.</span><span class="sxs-lookup"><span data-stu-id="8dadd-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="8dadd-250">SQL için açık uç nokta yok olduğundan, bu trafiği hello bulut hizmeti geçirmek değil'yı ve hello güvenlik duvarı ulaşmak olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="8dadd-250">Since there are no endpoints open for SQL, this traffic would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="8dadd-251">Uç noktaları için herhangi bir nedenle açıksa, hello ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="8dadd-251">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="8dadd-252">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="8dadd-252">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="8dadd-253">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="8dadd-253">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="8dadd-254">NSG kural 3 (Internet tooIIS01) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="8dadd-254">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="8dadd-255">İç IP adresi hello IIS01 (10.0.1.5) trafiği isabetler</span><span class="sxs-lookup"><span data-stu-id="8dadd-255">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="8dadd-256">Bağlantı noktası 1433, bu nedenle hiçbir yanıt toohello isteği IIS01 dinleme değil</span><span class="sxs-lookup"><span data-stu-id="8dadd-256">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="8dadd-257">Sonuç</span><span class="sxs-lookup"><span data-stu-id="8dadd-257">Conclusion</span></span>
<span data-ttu-id="8dadd-258">Bu örnek hello arka uç alt ağından gelen trafiği yalıtma, görece basit ve basit bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="8dadd-258">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="8dadd-259">Daha fazla örnekler ve ağ güvenlik sınırları genel bir bakış bulunabilir [burada][HOME].</span><span class="sxs-lookup"><span data-stu-id="8dadd-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="8dadd-260">Başvurular</span><span class="sxs-lookup"><span data-stu-id="8dadd-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="8dadd-261">Ana komut dosyası ve ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8dadd-261">Main script and network config</span></span>
<span data-ttu-id="8dadd-262">Merhaba tam komut dosyası bir PowerShell komut dosyası kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8dadd-262">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="8dadd-263">Merhaba ağ yapılandırma "NetworkConf1.xml." adlı bir dosyaya kaydet</span><span class="sxs-lookup"><span data-stu-id="8dadd-263">Save hello Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="8dadd-264">Merhaba kullanıcı tanımlı değişkenleri gerekli ve çalışma hello komut dosyası olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8dadd-264">Modify hello user-defined variables as needed and run hello script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="8dadd-265">Tam betik</span><span class="sxs-lookup"><span data-stu-id="8dadd-265">Full script</span></span>
<span data-ttu-id="8dadd-266">Kullanıcı tanımlı hello değişkenleri esas alarak bu betiği olur;</span><span class="sxs-lookup"><span data-stu-id="8dadd-266">This script will, based on hello user-defined variables;</span></span>

1. <span data-ttu-id="8dadd-267">Tooan Azure aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="8dadd-267">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="8dadd-268">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dadd-268">Create a storage account</span></span>
3. <span data-ttu-id="8dadd-269">VNet ve hello ağ yapılandırma dosyasında tanımlanan iki alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dadd-269">Create a VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="8dadd-270">Dört windows server Vm'lerinin oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dadd-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="8dadd-271">NSG dahil olmak üzere yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="8dadd-271">Configure NSG including:</span></span>
   * <span data-ttu-id="8dadd-272">Bir NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="8dadd-272">Creating an NSG</span></span>
   * <span data-ttu-id="8dadd-273">Kuralları ile doldurma</span><span class="sxs-lookup"><span data-stu-id="8dadd-273">Populating it with rules</span></span>
   * <span data-ttu-id="8dadd-274">Merhaba NSG toohello uygun alt ağları bağlama</span><span class="sxs-lookup"><span data-stu-id="8dadd-274">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="8dadd-275">Bu PowerShell Betiği, bir bilgisayar veya sunucu, Internet'e yerel olarak çalıştırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8dadd-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8dadd-276">Bu komut dosyasını çalıştırdığınızda, uyarı veya PowerShell'de pop diğer bilgilendirici iletileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="8dadd-277">Yalnızca hata iletileri kırmızı sorunu nedeni edilir.</span><span class="sxs-lookup"><span data-stu-id="8dadd-277">Only error messages in red are cause for concern.</span></span>
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
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

# User-Defined Global Variables
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
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
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
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
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
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="8dadd-278">Ağ yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="8dadd-278">Network config file</span></span>
<span data-ttu-id="8dadd-279">Güncelleştirilmiş konumla bu xml dosyasını kaydedin ve komut dosyası önceki hello hello bağlantı toothis dosya toohello $NetworkConfigFile değişkeni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8dadd-279">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello preceding script.</span></span>

```XML
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
```

#### <a name="sample-application-scripts"></a><span data-ttu-id="8dadd-280">Örnek uygulama komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="8dadd-280">Sample application scripts</span></span>
<span data-ttu-id="8dadd-281">Bu ve diğer çevre örnekleri için örnek bir uygulama tooinstall istiyorsanız, bir bağlantı aşağıdaki hello sağlanmış: [örnek uygulama betiği][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="8dadd-281">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dadd-282">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8dadd-282">Next steps</span></span>
* <span data-ttu-id="8dadd-283">Güncelleştirme ve XML dosyasını kaydedin</span><span class="sxs-lookup"><span data-stu-id="8dadd-283">Update and save XML file</span></span>
* <span data-ttu-id="8dadd-284">Merhaba PowerShell komut dosyası toobuild hello ortamı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="8dadd-284">Run hello PowerShell script toobuild hello environment</span></span>
* <span data-ttu-id="8dadd-285">Merhaba örnek uygulaması yükleme</span><span class="sxs-lookup"><span data-stu-id="8dadd-285">Install hello sample application</span></span>
* <span data-ttu-id="8dadd-286">Bu DMZ aracılığıyla farklı trafik akışları test etme</span><span class="sxs-lookup"><span data-stu-id="8dadd-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "NSG ile giriş DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

