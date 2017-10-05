---
title: "Azure DMZ örnek – yapı Nsg'ler ile basit DMZ | Microsoft Docs"
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
ms.openlocfilehash: ed172d552e1e4c9ee27c58abcd7ad2d98df21579
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="2a3ad-103">Örnek 1 – Nsg'ler ile klasik PowerShell kullanarak basit bir DMZ derleme</span><span class="sxs-lookup"><span data-stu-id="2a3ad-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="2a3ad-104">[Güvenlik sınırı en iyi yöntemler sayfasına dön][HOME]</span><span class="sxs-lookup"><span data-stu-id="2a3ad-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a3ad-105">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="2a3ad-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="2a3ad-106">Klasik - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a3ad-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="2a3ad-107">Bu örnekte basit DMZ dört Windows sunucuları ve ağ güvenlik grupları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="2a3ad-108">Bu örnek, her bir adımın daha derin bir anlayış sağlamak için ilgili PowerShell komutların her birini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-108">This example describes each of the relevant PowerShell commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="2a3ad-109">Ayrıca bir ayrıntılı sağlamak için bir trafik senaryosu bölümü olan adım adım çevre savunma katmanlar arasında nasıl trafiği devam eder.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-109">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="2a3ad-110">Son olarak, içindeki başvuruların sınamak ve çeşitli senaryolarıyla denemeler için bu ortamı oluşturmak için yönerge ve tam bir kod bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-110">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="2a3ad-111">![NSG ile giriş DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="2a3ad-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="2a3ad-112">Ortam açıklaması</span><span class="sxs-lookup"><span data-stu-id="2a3ad-112">Environment description</span></span>
<span data-ttu-id="2a3ad-113">Bu örnekte, bir abonelik aşağıdaki kaynaklar içeriyor:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="2a3ad-114">İki bulut hizmetlerini: "FrontEnd001" ve "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="2a3ad-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="2a3ad-115">Sanal ağ, "CorpNetwork" iki alt ağı; "Ön uç" ve "Arka uç"</span><span class="sxs-lookup"><span data-stu-id="2a3ad-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="2a3ad-116">Her iki alt ağa uygulanan ağ güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="2a3ad-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="2a3ad-117">Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="2a3ad-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="2a3ad-118">Uygulama arka uç sunucuları ("AppVM01", "AppVM02") temsil eden iki windows sunucuları</span><span class="sxs-lookup"><span data-stu-id="2a3ad-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="2a3ad-119">Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="2a3ad-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="2a3ad-120">References bölümünde bu örnekte açıklanan ortamı çoğunu derlemeler bir PowerShell komut dosyası yok.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-120">In the references section, there is a PowerShell script that builds most of the environment described in this example.</span></span> <span data-ttu-id="2a3ad-121">VM'ler ve sanal ağlar, derleme örnek komut dosyası tarafından yapılır rağmen değil açıklanmıştır bu belgede ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="2a3ad-122">Ortamı oluşturmak için;</span><span class="sxs-lookup"><span data-stu-id="2a3ad-122">To build the environment;</span></span>

1. <span data-ttu-id="2a3ad-123">References bölümünde bulunan ağ yapılandırma xml dosyasını kaydedin (adlar, konum ve IP adresleri verilen senaryo eşleşecek şekilde güncelleştirilir)</span><span class="sxs-lookup"><span data-stu-id="2a3ad-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="2a3ad-124">Kullanıcı değişkenleri (Abonelikleri, hizmet adlarını, vb. karşı) çalıştırılacak komut dosyasıdır ortamıyla eşleşecek şekilde güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="2a3ad-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="2a3ad-125">PowerShell komut dosyası yürütme</span><span class="sxs-lookup"><span data-stu-id="2a3ad-125">Execute the script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="2a3ad-126">PowerShell Betiği miktarlara bölge ağ yapılandırması xml dosyasında miktarlara bölge ile eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-126">The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>
>
>

<span data-ttu-id="2a3ad-127">Komut dosyasını başarıyla ek çalıştırır sonra isteğe bağlı adımlar izlenebilir, web sunucusu ve uygulama sunucusu bu DMZ yapılandırma ile test izin vermek için basit bir web uygulaması ile ayarlamak için iki komut dosyası başvuruları bölümünde bulunur.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-127">Once the script runs successfully additional optional steps may be taken, in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="2a3ad-128">Aşağıdaki bölümlerde ağ güvenlik grupları ve bunların Bu örnek için PowerShell Betiği anahtar satırları arasında adım adım ilerlemenizi sağlayarak işlevleri ayrıntılı bir açıklama belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-128">The following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of the PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="2a3ad-129">Ağ Güvenlik Grupları (NSG)</span><span class="sxs-lookup"><span data-stu-id="2a3ad-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="2a3ad-130">Bu örnekte, bir NSG grubu yerleşik ve altı kurallarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="2a3ad-131">Genel olarak bakıldığında, belirli "İzin ver" kurallarınızı önce oluşturmanız gerekir ve daha genel "Deny" kuralları en son.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-131">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="2a3ad-132">Kurallar öncelik atanmış belirtir ilk değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-132">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="2a3ad-133">Trafiği belirli bir kuralın uygulanacağı bulunduktan sonra başka hiçbir kural değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-133">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="2a3ad-134">NSG kuralları her (alt ağ perspektifinden) gelen veya giden yönde uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-134">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
> 
> 

<span data-ttu-id="2a3ad-135">Bildirimli olarak, aşağıdaki kural gelen trafik için oluşturulmakta:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-135">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="2a3ad-136">İç DNS trafiğinin (bağlantı noktası 53) izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="2a3ad-137">Her VM için RDP trafiğinin (3389 numaralı bağlantı noktası) Internet'ten izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-137">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="2a3ad-138">Web sunucusu (IIS01) için HTTP trafiğine (bağlantı noktası 80) Internet'ten izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-138">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="2a3ad-139">Tüm trafiği (tüm bağlantı noktaları) IIS01 AppVM1 izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-139">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="2a3ad-140">Tüm trafiği (tüm bağlantı noktaları) Internet'ten tüm VNet (her iki alt ağ) reddedildi</span><span class="sxs-lookup"><span data-stu-id="2a3ad-140">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="2a3ad-141">Tüm trafiği (tüm bağlantı noktaları) ön uç alt ağından arka uç alt ağa reddedildi</span><span class="sxs-lookup"><span data-stu-id="2a3ad-141">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="2a3ad-142">Bu kurallar ile bağlı her alt ağ için bir HTTP isteği hem kuralları 3, web sunucusu Internet'ten gelen ise (izin ver) ve 5 (uygulamak reddetme), ancak 3 kuralı, yalnızca geçerli olur ve kural 5 oyuna değil gelen daha yüksek öncelikli olduğundan.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-142">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="2a3ad-143">Bu nedenle web sunucusuna HTTP isteği izin verilir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-143">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="2a3ad-144">Bu aynı trafiği DNS01 sunucunun erişmeye, kural 5 (Reddet) uygulamak için ilk olacaktır ve trafiği sunucuya geçirmeniz izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-144">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="2a3ad-145">Kural 6 (Reddet) arka uç alt ağına (dışında izin verilen trafiği kurallarında 1 ve 4) Konuşmayı gelen ön uç alt ağ blokları, bu kural kümesine durumda arka uç ağ saldırgan ön uç web uygulamasında arka uç "korumalı" ağa (yalnızca AppVM01 sunucuda kullanıma sunulan kaynakları) erişimi sınırlı bir saldırganın güvenlik ihlalleri korur.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-145">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="2a3ad-146">İnternet giden trafiğe izin veren varsayılan bir giden kuralı yok.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-146">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="2a3ad-147">Bu örnekte, biz giden trafiğe izin vermek ve herhangi bir giden kuralı değiştirme değil.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="2a3ad-148">Her iki yönde trafik kilitlemek için kullanıcı tanımlı yönlendirme gereklidir ve "Örnek 3" üzerinde incelediniz [güvenlik sınırı en iyi yöntemler sayfası][HOME].</span><span class="sxs-lookup"><span data-stu-id="2a3ad-148">To lock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="2a3ad-149">Her kural aşağıdaki gibi daha ayrıntılı olarak ele (**Not**: dolar işareti aşağıdaki liste başlayarak herhangi bir öğeye (örneğin: $NSGName) kullanıcı tanımlı bir değişken başvurusu bölümünde bu belgenin betikten):</span><span class="sxs-lookup"><span data-stu-id="2a3ad-149">Each rule is discussed in more detail as follows (**Note**: any item in the following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="2a3ad-150">İlk ağ güvenlik grubu kuralları tutmak için yerleşik gerekir:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-150">First a Network Security Group must be built to hold the rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="2a3ad-151">Bu örnekte ilk kural DNS sunucusu arka uç alt ağdaki tüm iç ağ arasında DNS trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-151">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="2a3ad-152">Kural bazı önemli parametreleri içerir:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-152">The rule has some important parameters:</span></span>
   
   * <span data-ttu-id="2a3ad-153">"Tür" trafik akışı hangi yönde bu kural etkinleşir belirtir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="2a3ad-154">Perspektifinden (bağlı olarak bu NSG burada bağlı) alt ağ ya da sanal makinenin yönü olur.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-154">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="2a3ad-155">Bu nedenle türüdür "Giriş" ve trafik alt girerek, kural geçerli olur ve alt ağdan çıkan trafiğe etkilenmemiştir bu kural tarafından varsa.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-155">Thus if Type is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="2a3ad-156">"Öncelik" bir trafik akışı değerlendirileceğini sırasını belirler.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-156">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="2a3ad-157">Düşük sayı öncelik o kadar yüksektir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-157">The lower the number the higher the priority.</span></span> <span data-ttu-id="2a3ad-158">Belirli bir trafik akışı için bir kural uygulandığı zaman başka hiçbir kural işlenir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-158">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="2a3ad-159">Bu nedenle bir kural öncelik 1 ile trafiğine izin verir ve trafiği, öncelik 2 olan bir kural reddeder ve her iki kural trafiğe uygulanır durumunda trafik akışı için izin verilir (Kural 1 yüksek önceliğe sahip olduğundan etkisi sürdü ve başka hiçbir kural uygulanan).</span><span class="sxs-lookup"><span data-stu-id="2a3ad-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="2a3ad-160">Bu kural tarafından etkilenen trafiği engellendi veya izin verilen "Eylem" belirtir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="2a3ad-161">Bu kural RDP bağlantı noktasına bağlı alt ağ üzerinde herhangi bir sunucuda internet'ten akış RDP trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-161">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> <span data-ttu-id="2a3ad-162">Bu kural adres öneklerini iki özel tür kullanır; "Vırtual_network" ve "INTERNET."</span><span class="sxs-lookup"><span data-stu-id="2a3ad-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="2a3ad-163">Bu etiketler adres öneklerinin daha büyük bir kategori adres için kolay bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-163">These tags are an easy way to address a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="2a3ad-164">Bu kural, web sunucusu isabet gelen internet trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-164">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="2a3ad-165">Bu kural, yönlendirme davranışını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-165">This rule does not change the routing behavior.</span></span> <span data-ttu-id="2a3ad-166">Kuralın yalnızca geçirmek için IIS01 giden trafiğe izin verir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-166">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="2a3ad-167">Bu nedenle Internet trafiği bu kural izin ve daha fazla kural işlemeyi durdur hedef olarak web sunucusunun sahip.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-167">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="2a3ad-168">(Öncelikle kuralında 140 diğer tüm gelen Internet trafiğini engellendi).</span><span class="sxs-lookup"><span data-stu-id="2a3ad-168">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="2a3ad-169">Yalnızca HTTP trafiğini işlemek, yalnızca hedef bağlantı noktası 80 izin vermek için bu kural daha fazla kısıtlanmasını.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-169">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet to $VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="2a3ad-170">Bu kural AppVM01 sunucuya daha yeni bir kural bloklarını arka uç trafiği diğer ön uç IIS01 sunucudan geçmesine trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-170">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="2a3ad-171">Bu kural, bağlantı noktasının eklenmesi gereken biliniyorsa geliştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-171">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="2a3ad-172">IIS sunucusu yalnızca SQL Server'da AppVM01 basarsa, örneğin, hedef bağlantı noktası aralığı değiştirildiği "*" (tüm) böylece web uygulaması hiç tehlikeye AppVM01 üzerinde daha küçük bir gelen saldırı yüzeyini sağlar 1433 (SQL bağlantı noktası) için.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-172">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] to $VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="2a3ad-173">Bu kural, ağ üzerindeki herhangi bir sunucuya internet'ten trafiği engeller.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-173">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="2a3ad-174">Öncelikle 110 ve 120 kurallarıyla etkisi yalnızca gelen Internet trafiği güvenlik duvarı ve RDP bağlantı noktalarını sunucularda ve blokları şey izin vermektir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-174">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="2a3ad-175">Bu kural, tüm beklenmeyen akışlar engellemek için bir "yedek" kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-175">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $VNetName VNet from the Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="2a3ad-176">Son bir kural arka uç alt ağına ön uç alt ağından trafiği engeller.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-176">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="2a3ad-177">Bu kural yalnızca bir gelen kuralı olduğundan, geriye doğru trafiğinin (Başlangıç ön uç için arka uç) izin verilir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="2a3ad-178">Trafik senaryoları</span><span class="sxs-lookup"><span data-stu-id="2a3ad-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="2a3ad-179">(*İzin verilen*) web sunucusu Internet'e</span><span class="sxs-lookup"><span data-stu-id="2a3ad-179">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="2a3ad-180">Bir Internet kullanıcı FrontEnd001.CloudApp.Net (Internet'e yönelik bulut hizmeti) istekler bir HTTP sayfası</span><span class="sxs-lookup"><span data-stu-id="2a3ad-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="2a3ad-181">Bulut hizmeti geçişleri trafiğini açık uç noktasını IIS01 doğru bağlantı noktası 80 üzerinden (web sunucusu)</span><span class="sxs-lookup"><span data-stu-id="2a3ad-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="2a3ad-182">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2a3ad-183">NSG kural 1 (DNS) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-183">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="2a3ad-184">NSG kuralı 2 (RDP) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-184">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="2a3ad-185">NSG kural 3 (IIS01 Internet'e) için geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-185">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="2a3ad-186">İç IP adresi web sunucusunun IIS01 (10.0.1.5) trafiği isabetler</span><span class="sxs-lookup"><span data-stu-id="2a3ad-186">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="2a3ad-187">IIS01 web trafiği için dinleme, bu isteği alır ve isteği işlemeye başlıyor</span><span class="sxs-lookup"><span data-stu-id="2a3ad-187">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="2a3ad-188">IIS01 SQL Server AppVM01 hakkında bilgi için sorar</span><span class="sxs-lookup"><span data-stu-id="2a3ad-188">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="2a3ad-189">Ön uç alt ağda hiçbir giden kuralları olduğundan, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="2a3ad-190">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-190">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2a3ad-191">NSG kural 1 (DNS) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-191">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="2a3ad-192">NSG kuralı 2 (RDP) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-192">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="2a3ad-193">NSG kural 3 (Internet güvenlik duvarı için) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-193">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="2a3ad-194">NSG kuralı 4 (IIS01 AppVM01 için) uygulamak, trafiğine izin verilir, kural işleme Durdur</span><span class="sxs-lookup"><span data-stu-id="2a3ad-194">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="2a3ad-195">AppVM01 SQL sorgusu alır ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="2a3ad-195">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="2a3ad-196">Arka uç alt ağda hiçbir giden kuralları olduğundan, yanıt izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-196">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="2a3ad-197">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="2a3ad-198">Gelen için geçerli NSG kural yok NSG hiçbiri uygulama kuralları için ön uç alt ağa, arka uç alt ağından gelen trafik</span><span class="sxs-lookup"><span data-stu-id="2a3ad-198">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="2a3ad-199">Alt ağlar arasında trafiğe izin varsayılan sistem kuralı, trafiğine izin bu trafiği olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-199">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="2a3ad-200">IIS sunucusu SQL yanıtı alır ve HTTP yanıtı tamamlar ve istek sahibine gönderir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-200">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
13. <span data-ttu-id="2a3ad-201">Hiçbir giden kuralları olduğundan ön uç alt ağda yanıt izin verilir ve internet kullanıcı istenen web sayfasının alır.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-201">Since there are no outbound rules on the Frontend subnet the response is allowed, and the internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="2a3ad-202">(*İzin verilen*) arka uç için RDP</span><span class="sxs-lookup"><span data-stu-id="2a3ad-202">(*Allowed*) RDP to backend</span></span>
1. <span data-ttu-id="2a3ad-203">Sunucu Yöneticisi internet üzerindeki AppVM01 xxxxx rastgele atanan bağlantı noktası numarası (atanan bağlantı noktası, Azure portal veya PowerShell aracılığıyla bulunabilir) AppVM01 için RDP olduğu BackEnd001.CloudApp.Net:xxxxx üzerinde RDP oturumu istekleri</span><span class="sxs-lookup"><span data-stu-id="2a3ad-203">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="2a3ad-204">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2a3ad-205">NSG kural 1 (DNS) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-205">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="2a3ad-206">NSG kuralı 2 (RDP) uygulamak için izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="2a3ad-207">Hiçbir giden kuralları, varsayılan kuralları uygula ve dönüş trafiğine izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="2a3ad-208">RDP oturumu etkin</span><span class="sxs-lookup"><span data-stu-id="2a3ad-208">RDP session is enabled</span></span>
5. <span data-ttu-id="2a3ad-209">Kullanıcı adı ve parola AppVM01 isteyen</span><span class="sxs-lookup"><span data-stu-id="2a3ad-209">AppVM01 prompts for the user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="2a3ad-210">(*İzin verilen*) Web sunucusu DNS araması DNS sunucusunda</span><span class="sxs-lookup"><span data-stu-id="2a3ad-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="2a3ad-211">Sunucu, IIS01, www.data.gov bir veri akışı gereksinimlerini ancak adresini çözümlemek için gereksinimlerini web.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="2a3ad-212">Ağ yapılandırma için VNet listeleri DNS01 (arka uç alt ağda 10.0.2.4) birincil DNS sunucusu olarak IIS01 DNS isteği için DNS01 gönderir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-212">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="2a3ad-213">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="2a3ad-214">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="2a3ad-215">NSG kural 1 (DNS) uygulamak için izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="2a3ad-216">DNS sunucusu isteği alır</span><span class="sxs-lookup"><span data-stu-id="2a3ad-216">DNS server receives the request</span></span>
6. <span data-ttu-id="2a3ad-217">DNS sunucusu önbelleğe adresi yoksa ve bir kök DNS sunucusu internet'te sorar</span><span class="sxs-lookup"><span data-stu-id="2a3ad-217">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="2a3ad-218">Hiçbir giden kuralları arka uç alt ağdaki trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="2a3ad-219">Bu oturumda dahili olarak başlatıldı beri Internet DNS sunucusu yanıt, yanıt izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-219">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="2a3ad-220">DNS sunucusu yanıtı önbelleğe alır ve geri IIS01 ilk isteğine yanıt verir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-220">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="2a3ad-221">Hiçbir giden kuralları arka uç alt ağdaki trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="2a3ad-222">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="2a3ad-223">Gelen için geçerli NSG kural yok NSG hiçbiri uygulama kuralları için ön uç alt ağa, arka uç alt ağından gelen trafik</span><span class="sxs-lookup"><span data-stu-id="2a3ad-223">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="2a3ad-224">Trafiğe izin için alt ağlar arasında trafiğe izin varsayılan sistem kuralı bu trafiği olanak tanır</span><span class="sxs-lookup"><span data-stu-id="2a3ad-224">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="2a3ad-225">IIS01 DNS01 yanıtı alır</span><span class="sxs-lookup"><span data-stu-id="2a3ad-225">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="2a3ad-226">(*İzin verilen*) Web sunucusu erişimini dosyasını AppVM01 üzerinde</span><span class="sxs-lookup"><span data-stu-id="2a3ad-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="2a3ad-227">Bir dosyanın AppVM01 IIS01 sorar</span><span class="sxs-lookup"><span data-stu-id="2a3ad-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="2a3ad-228">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="2a3ad-229">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-229">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2a3ad-230">NSG kural 1 (DNS) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-230">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="2a3ad-231">NSG kuralı 2 (RDP) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-231">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="2a3ad-232">NSG kural 3 (IIS01 Internet'e) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-232">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="2a3ad-233">NSG kuralı 4 (IIS01 AppVM01 için) uygulamak, trafiğine izin verilir, kural işleme Durdur</span><span class="sxs-lookup"><span data-stu-id="2a3ad-233">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="2a3ad-234">AppVM01 isteği alır ve (erişim yetkisi varsayılarak) dosyası ile yanıt verir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-234">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="2a3ad-235">Arka uç alt ağda hiçbir giden kuralları olduğundan, yanıt izin verilir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-235">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="2a3ad-236">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2a3ad-237">Gelen için geçerli NSG kural yok NSG hiçbiri uygulama kuralları için ön uç alt ağa, arka uç alt ağından gelen trafik</span><span class="sxs-lookup"><span data-stu-id="2a3ad-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="2a3ad-238">Alt ağlar arasında trafiğe izin varsayılan sistem kuralı, trafiğine izin bu trafiği olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="2a3ad-239">IIS sunucu dosya alır</span><span class="sxs-lookup"><span data-stu-id="2a3ad-239">The IIS server receives the file</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="2a3ad-240">(*Reddedildi*) arka uç sunucusuna Web</span><span class="sxs-lookup"><span data-stu-id="2a3ad-240">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="2a3ad-241">Bir Internet kullanıcı BackEnd001.CloudApp.Net hizmeti aracılığıyla AppVM01 bir dosyaya erişmeyi dener</span><span class="sxs-lookup"><span data-stu-id="2a3ad-241">An internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="2a3ad-242">Dosya Paylaşımı için açık uç nokta yok olduğundan, bu trafiği bulut hizmeti geçirmek değil'yı ve tarafından sunucuya ulaşmak olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="2a3ad-242">Since there are no endpoints open for file share, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="2a3ad-243">Uç noktaları için herhangi bir nedenle açıksa, NSG kural 5 (sanal ağa Internet) bu trafiği engeller</span><span class="sxs-lookup"><span data-stu-id="2a3ad-243">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="2a3ad-244">(*Reddedildi*) DNS sunucusunda Web DNS araması</span><span class="sxs-lookup"><span data-stu-id="2a3ad-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="2a3ad-245">Bir iç DNS kaydında DNS01 BackEnd001.CloudApp.Net hizmeti aracılığıyla aramak bir internet kullanıcı çalışır</span><span class="sxs-lookup"><span data-stu-id="2a3ad-245">An internet user tries to look up an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="2a3ad-246">DNS için açık uç nokta yok olduğundan, bu trafiği bulut hizmeti geçirmek değil'yı ve tarafından sunucuya ulaşmak olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="2a3ad-246">Since there are no endpoints open for DNS, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="2a3ad-247">Uç noktaları için herhangi bir nedenle açıksa, NSG kural 5 (sanal ağa Internet) bu trafiği engeller (Not: Bu kural 1 (DNS), iki nedenden dolayı geçerli değil, ilk kaynak adresi Internet, bu kural yalnızca kaynağı olarak yerel vnet'e uygulanır, hiçbir zaman trafiği reddetmeye böylece de bu kural bir izin verme kuralı)</span><span class="sxs-lookup"><span data-stu-id="2a3ad-247">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="2a3ad-248">(*Reddedildi*) Web güvenlik duvarı üzerinden SQL erişimi</span><span class="sxs-lookup"><span data-stu-id="2a3ad-248">(*Denied*) Web to SQL access through firewall</span></span>
1. <span data-ttu-id="2a3ad-249">Bir Internet kullanıcının SQL verileri FrontEnd001.CloudApp.Net (Internet'e yönelik bulut hizmeti) ' ister.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="2a3ad-250">SQL için açık uç nokta yok olduğundan bu trafiği bulut hizmeti geçip geçmeyeceğini değil ve güvenlik duvarı ulaşmak olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="2a3ad-250">Since there are no endpoints open for SQL, this traffic would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="2a3ad-251">Uç noktaları için herhangi bir nedenle açıksa, ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-251">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="2a3ad-252">NSG kural 1 (DNS) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-252">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="2a3ad-253">NSG kuralı 2 (RDP) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-253">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="2a3ad-254">NSG kural 3 (IIS01 Internet'e) için geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="2a3ad-254">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="2a3ad-255">Trafik isabetler IIS01 iç IP adresi (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="2a3ad-255">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="2a3ad-256">IIS01 1433 numaralı bağlantı noktasını, dolayısıyla isteğine yanıt olarak dinlemede değil</span><span class="sxs-lookup"><span data-stu-id="2a3ad-256">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="2a3ad-257">Sonuç</span><span class="sxs-lookup"><span data-stu-id="2a3ad-257">Conclusion</span></span>
<span data-ttu-id="2a3ad-258">Bu örnek, arka uç alt ağından gelen trafiği yalıtma, nispeten basit ve düz ileriye doğru bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-258">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="2a3ad-259">Daha fazla örnekler ve ağ güvenlik sınırları genel bir bakış bulunabilir [burada][HOME].</span><span class="sxs-lookup"><span data-stu-id="2a3ad-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="2a3ad-260">Başvurular</span><span class="sxs-lookup"><span data-stu-id="2a3ad-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="2a3ad-261">Ana komut dosyası ve ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-261">Main script and network config</span></span>
<span data-ttu-id="2a3ad-262">Tam komut dosyasını bir PowerShell komut dosyası kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-262">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="2a3ad-263">Ağ Yapılandırma "NetworkConf1.xml." adlı bir dosyaya kaydet</span><span class="sxs-lookup"><span data-stu-id="2a3ad-263">Save the Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="2a3ad-264">Kullanıcı tanımlı değişkenleri gerektiği gibi değiştirin ve betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-264">Modify the user-defined variables as needed and run the script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="2a3ad-265">Tam komut dosyası</span><span class="sxs-lookup"><span data-stu-id="2a3ad-265">Full script</span></span>
<span data-ttu-id="2a3ad-266">Bu komut dosyası, kullanıcı tanımlı değişkenlere bağlı olur;</span><span class="sxs-lookup"><span data-stu-id="2a3ad-266">This script will, based on the user-defined variables;</span></span>

1. <span data-ttu-id="2a3ad-267">Bir Azure aboneliğine Bağlanma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-267">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="2a3ad-268">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-268">Create a storage account</span></span>
3. <span data-ttu-id="2a3ad-269">VNet ve ağ yapılandırma dosyasında tanımlanan iki alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-269">Create a VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="2a3ad-270">Dört windows server Vm'lerinin oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="2a3ad-271">NSG dahil olmak üzere yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="2a3ad-271">Configure NSG including:</span></span>
   * <span data-ttu-id="2a3ad-272">Bir NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-272">Creating an NSG</span></span>
   * <span data-ttu-id="2a3ad-273">Kuralları ile doldurma</span><span class="sxs-lookup"><span data-stu-id="2a3ad-273">Populating it with rules</span></span>
   * <span data-ttu-id="2a3ad-274">NSG için uygun alt ağları bağlama</span><span class="sxs-lookup"><span data-stu-id="2a3ad-274">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="2a3ad-275">Bu PowerShell Betiği, bir bilgisayar veya sunucu, Internet'e yerel olarak çalıştırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a3ad-276">Bu komut dosyasını çalıştırdığınızda, uyarı veya PowerShell'de pop diğer bilgilendirici iletileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="2a3ad-277">Yalnızca hata iletileri kırmızı sorunu nedeni edilir.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-277">Only error messages in red are cause for concern.</span></span>
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
   - One server on the FrontEnd Subnet
   - Three Servers on the BackEnd Subnet
   - Network Security Groups to allow/deny traffic patterns as declared

  Before running script, ensure the network configuration file is created in
  the directory referenced by $NetworkConfigFile variable (or update the
  variable to reflect the path and file name of the config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  the appropriate layer(s) of protection. This script serves as an example of some
  of the techniques that can be used, but should not be used for all scenarios. You
  are responsible to assess your security needs and the appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes to reflect your subscription and services
  # Invalid options will fail in the validation section

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
    # Note: To ensure proper NSG Rule creation later in this script:
    #       - The Web Server must be VM 0
    #       - The AppVM1 Server must be VM 1
    #       - The DNS server must be VM 3
    #
    #       Otherwise the NSG rules in the last section of this
    #       script will need to be changed to match the modified
    #       VM array numbers ($i) so the NSG Rule IP addresses
    #       are aligned to the associated VM IP addresses.

    # VM 0 - The Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - The First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - The Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - The DNS Server
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

  # Update Subscription Pointer to New Storage Account
    Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation variable is correct and the network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see the above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

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
    Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

  # Build the NSG
    Write-Host "Building the NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) to $($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign the NSG to the Subnets
        Write-Host "Binding the NSG to both subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on the IIS Server)
  # Install Backend resource (Run Post-Build Script on the AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="2a3ad-278">Ağ yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="2a3ad-278">Network config file</span></span>
<span data-ttu-id="2a3ad-279">Güncelleştirilmiş konumu ile bu xml dosyasını kaydedin ve bağlantıyı önceki komut $NetworkConfigFile değişkeninde bu dosyaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2a3ad-279">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the preceding script.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="2a3ad-280">Örnek uygulama komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="2a3ad-280">Sample application scripts</span></span>
<span data-ttu-id="2a3ad-281">Bu ve diğer çevre örnekleri için örnek bir uygulama yüklemek isterseniz, bir aşağıdaki bağlantıda sağlanmış: [örnek uygulama betiği][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="2a3ad-281">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a3ad-282">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a3ad-282">Next steps</span></span>
* <span data-ttu-id="2a3ad-283">Güncelleştirme ve XML dosyasını kaydedin</span><span class="sxs-lookup"><span data-stu-id="2a3ad-283">Update and save XML file</span></span>
* <span data-ttu-id="2a3ad-284">Ortamı oluşturmak için PowerShell betiğini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2a3ad-284">Run the PowerShell script to build the environment</span></span>
* <span data-ttu-id="2a3ad-285">Örnek uygulamayı yükle</span><span class="sxs-lookup"><span data-stu-id="2a3ad-285">Install the sample application</span></span>
* <span data-ttu-id="2a3ad-286">Bu DMZ aracılığıyla farklı trafik akışları test etme</span><span class="sxs-lookup"><span data-stu-id="2a3ad-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
<span data-ttu-id="2a3ad-287">[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "NSG ile giriş DMZ"</span><span class="sxs-lookup"><span data-stu-id="2a3ad-287">[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Inbound DMZ with NSG"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

