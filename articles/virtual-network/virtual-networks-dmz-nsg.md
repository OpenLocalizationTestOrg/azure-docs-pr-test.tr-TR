---
title: "aaaAzure DMZ örnek – yapı Nsg'ler ile basit DMZ | Microsoft Docs"
description: "Bir çevre ağ güvenlik grupları (NSG) ile derleme"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="ef651-103">Örnek 1 – Nsg'ler ile bir Azure Resource Manager şablonu kullanarak basit bir DMZ derleme</span><span class="sxs-lookup"><span data-stu-id="ef651-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="ef651-104">[Dönüş toohello güvenlik sınırı en iyi uygulamalar sayfası][HOME]</span><span class="sxs-lookup"><span data-stu-id="ef651-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef651-105">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="ef651-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="ef651-106">Klasik - PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef651-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="ef651-107">Bu örnekte basit DMZ dört Windows sunucuları ve ağ güvenlik grupları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ef651-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="ef651-108">Bu örnek hello ilgili şablonu bölümleri tooprovide her adımın daha derin bir anlayış açıklar.</span><span class="sxs-lookup"><span data-stu-id="ef651-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="ef651-109">Trafik hello DMZ savunma hello katmanlar ile nasıl devam eder bir ayrıntılı adım adım bakış trafiği senaryo bölüm tooprovide bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef651-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="ef651-110">Son olarak, hello başvuruları hello tam şablon kodu ve yönergeleri toobuild bu ortam tootest ve çeşitli senaryoları ile deneme bölümündedir.</span><span class="sxs-lookup"><span data-stu-id="ef651-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="ef651-111">![NSG ile giriş DMZ][1]</span><span class="sxs-lookup"><span data-stu-id="ef651-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="ef651-112">Ortam açıklaması</span><span class="sxs-lookup"><span data-stu-id="ef651-112">Environment description</span></span>
<span data-ttu-id="ef651-113">Bu örnekte, abonelik kaynakları aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="ef651-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="ef651-114">Tek bir kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="ef651-114">A single resource group</span></span>
* <span data-ttu-id="ef651-115">Sanal ağı iki alt ağ ile; "Ön uç" ve "Arka uç"</span><span class="sxs-lookup"><span data-stu-id="ef651-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="ef651-116">Uygulanan tooboth alt ağıdır bir ağ güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="ef651-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="ef651-117">Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="ef651-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="ef651-118">Uygulama arka uç sunucuları ("AppVM01", "AppVM02") temsil eden iki windows sunucuları</span><span class="sxs-lookup"><span data-stu-id="ef651-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="ef651-119">Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="ef651-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="ef651-120">Merhaba uygulama web sunucusu ile ilişkili bir ortak IP adresi</span><span class="sxs-lookup"><span data-stu-id="ef651-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="ef651-121">Merhaba references bölümünde bu örnekte açıklanan hello ortamı derlemeler bir bağlantı tooan Azure Resource Manager şablonu yoktur.</span><span class="sxs-lookup"><span data-stu-id="ef651-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="ef651-122">Yapı hello VM'ler ve sanal ağlar, bu belgede ayrıntılı hello örnek şablon tarafından yapılan rağmen açıklanmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef651-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="ef651-123">**toobuild bu ortam** (ayrıntılı yönergeler olduğunda hello references bölümünde bu belgenin);</span><span class="sxs-lookup"><span data-stu-id="ef651-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="ef651-124">Dağıtma sırasında Azure Resource Manager şablonu hello: [Azure hızlı başlangıç şablonları][Template]</span><span class="sxs-lookup"><span data-stu-id="ef651-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="ef651-125">Merhaba örnek uygulamayı yükleyin: [örnek uygulama betiği][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="ef651-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="ef651-126">Bu örnekte, hello IIS sunucusu tooRDP tooany arka uç sunucuları, bir "atlama kutu." kullanılır</span><span class="sxs-lookup"><span data-stu-id="ef651-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="ef651-127">İlk RDP toohello IIS sunucusunu ve sonra hello IIS sunucu RDP toohello arka uç sunucu.</span><span class="sxs-lookup"><span data-stu-id="ef651-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="ef651-128">Alternatif olarak bir ortak IP her sunucu için daha kolay RDP NIC ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef651-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="ef651-129">Merhaba aşağıdaki bölümlerde hello ağ güvenlik grubu ve nasıl hello Azure Resource Manager şablonu anahtar satırları arasında adım adım ilerlemenizi sağlayarak bu örnek için işlevleri ayrıntılı bir açıklama sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ef651-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="ef651-130">Ağ Güvenlik Grupları (NSG)</span><span class="sxs-lookup"><span data-stu-id="ef651-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="ef651-131">Bu örnekte, bir NSG grubu yerleşik ve altı kurallarıyla yüklendi.</span><span class="sxs-lookup"><span data-stu-id="ef651-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="ef651-132">Genel olarak bakıldığında, belirli "İzin ver" kurallarınızı ilk oluşturun ve daha genel "Deny" kuralları son hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef651-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="ef651-133">öncelik atanmış hello hangi kuralları ilk olarak değerlendirilir belirler.</span><span class="sxs-lookup"><span data-stu-id="ef651-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="ef651-134">Trafik tooapply tooa belirli kural bulunduktan sonra başka hiçbir kural değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ef651-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="ef651-135">NSG kuralları hello ikisinde uygulayabileceğiniz gelen veya giden yön (Merhaba alt hello açısından).</span><span class="sxs-lookup"><span data-stu-id="ef651-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="ef651-136">Bildirimli olarak, kurallar aşağıdaki hello gelen trafik için oluşturulmakta:</span><span class="sxs-lookup"><span data-stu-id="ef651-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="ef651-137">İç DNS trafiğinin (bağlantı noktası 53) izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="ef651-138">Merhaba Internet tooany VM gelen RDP trafiğine (3389 numaralı bağlantı noktası) izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="ef651-139">Itanium tabanlı sistemler için HTTP trafiğine (bağlantı noktası 80) hello Internet tooweb sunucusundan (IIS01) izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="ef651-140">IIS01 tooAppVM1 tüm trafiği (tüm bağlantı noktaları) izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="ef651-141">Merhaba Internet toohello tüm trafiği (tüm bağlantı noktaları) tüm sanal ağ (her iki alt ağ) reddedildi</span><span class="sxs-lookup"><span data-stu-id="ef651-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="ef651-142">Merhaba ön uç alt toohello arka uç alt ağından gelen tüm trafiği (tüm bağlantı noktaları) reddedildi</span><span class="sxs-lookup"><span data-stu-id="ef651-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="ef651-143">Bu kurallar ilişkili tooeach alt ağ ile bir HTTP isteği hello Internet toohello web sunucusundan gelen ise her ikisi de kuralları 3 (izin verin) ve 5 (uygulamak reddetme), ancak 3 kuralı, yalnızca geçerli olur ve kural 5 oyuna değil gelen daha yüksek öncelikli olduğundan.</span><span class="sxs-lookup"><span data-stu-id="ef651-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="ef651-144">Bu nedenle hello HTTP isteği toohello web sunucusu izin.</span><span class="sxs-lookup"><span data-stu-id="ef651-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="ef651-145">Bu aynı trafiği tooreach hello DNS01 sunucusunu denemeden ise hello ilk tooapply ve hello trafiği toopass toohello sunucu verilmez kural 5 (Reddet) olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef651-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="ef651-146">Kural 6 (Reddet) toohello arka uç alt (dışında izin verilen trafiği kurallarında 1 ve 4) Konuşmayı gelen hello ön uç alt ağ blokları, hello saldırganın bir saldırganın güvenlik ihlalleri hello web uygulamasına hello ön uç misiniz durumunda bu kural kümesine hello arka uç ağ korur. arka uç "Korumalı ağ (yalnızca tooresources hello AppVM01 sunucu üzerinde gösterilen)" erişim toohello sınırlı.</span><span class="sxs-lookup"><span data-stu-id="ef651-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="ef651-147">Toohello giden trafiğe izin veren varsayılan giden kural Internet.</span><span class="sxs-lookup"><span data-stu-id="ef651-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="ef651-148">Bu örnekte, biz giden trafiğe izin vermek ve herhangi bir giden kuralı değiştirme değil.</span><span class="sxs-lookup"><span data-stu-id="ef651-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="ef651-149">Her iki yönde tooapply güvenlik ilkesi tootraffic, kullanıcı tanımlanan yönlendirme gereklidir ve "Örnek 3" Merhaba üzerinde incelediniz [güvenlik sınırı en iyi yöntemler sayfası][HOME].</span><span class="sxs-lookup"><span data-stu-id="ef651-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="ef651-150">Her kural aşağıdaki gibi daha ayrıntılı olarak ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="ef651-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="ef651-151">Ağ güvenlik grubu kaynak örneklenen toohold hello kuralları olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="ef651-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="ef651-152">Bu örnekte Hello ilk kural hello arka uç alt ağdaki tüm İç ağlara toohello DNS sunucusu arasında DNS trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="ef651-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="ef651-153">Merhaba kuralı bazı önemli parametreler sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ef651-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="ef651-154">"destinationAddressPrefix" - özel türde bir adres öneki "Varsayılan etiket" adlı kural kullanabilirsiniz, bu etiketler adres öneklerinin daha büyük bir kategori kolay bir yolu tooaddress sağlayan sistem tarafından sağlanan tanımlayıcılardır.</span><span class="sxs-lookup"><span data-stu-id="ef651-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="ef651-155">Bu kural kullandığı varsayılan etiket "Internet" Merhaba toosignify VNet hello dışında herhangi bir adres.</span><span class="sxs-lookup"><span data-stu-id="ef651-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="ef651-156">Diğer önek VirtualNetwork ve AzureLoadBalancer etiketleridir.</span><span class="sxs-lookup"><span data-stu-id="ef651-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="ef651-157">"Yönünü" trafik akışı hangi yönde bu kural etkinleşir belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef651-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="ef651-158">Merhaba yönünü (bağlı olarak bu NSG burada bağlı) hello açısından hello alt ağı veya sanal makine değil.</span><span class="sxs-lookup"><span data-stu-id="ef651-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="ef651-159">Bu nedenle yönü "Giriş" ve trafiği hello alt girerek, hello kuralın ve hello alt ağdan çıkan trafiğe etkilenmez bu kural tarafından durumunda.</span><span class="sxs-lookup"><span data-stu-id="ef651-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="ef651-160">"Öncelik" Merhaba sırasını trafik akışı değerlendirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="ef651-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="ef651-161">Merhaba alt hello sayı hello yüksek hello önceliği.</span><span class="sxs-lookup"><span data-stu-id="ef651-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="ef651-162">Tooa belirli bir trafik akışı bir kural uygulandığı zaman başka hiçbir kural işlenir.</span><span class="sxs-lookup"><span data-stu-id="ef651-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="ef651-163">Bu nedenle öncelik 1 olan bir kural trafiğine izin verir ve trafiği, öncelik 2 olan bir kural reddeder ve tootraffic hem kuralları uygula durumunda hello trafiği tooflow izin (Kural 1 yüksek önceliğe sahip olduğundan etkisi sürdü ve başka hiçbir kural uygulanan).</span><span class="sxs-lookup"><span data-stu-id="ef651-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="ef651-164">"Erişim" Bu kural tarafından etkilenen trafiği engellenen ("Deny") veya izin verilen ("izin ver") olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef651-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="ef651-165">Bu kural, alt ağ RDP trafiğine tooflow hello herhangi bir sunucuda hello Internet toohello RDP bağlantı noktasından bağlı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef651-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="ef651-166">Bu kural gelen Internet trafiği toohit hello web sunucusu sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef651-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="ef651-167">Bu kural hello yönlendirme davranışını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="ef651-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="ef651-168">Merhaba kural yalnızca IIS01 toopass giden trafiğe izin verir.</span><span class="sxs-lookup"><span data-stu-id="ef651-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="ef651-169">Bu nedenle hello Internet trafiği bu kural izin ve daha fazla kural işlemeyi durdur hedef olarak hello web sunucusunun sahip.</span><span class="sxs-lookup"><span data-stu-id="ef651-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="ef651-170">(Öncelikle hello kuralında 140 diğer tüm gelen Internet trafiğini engellendi).</span><span class="sxs-lookup"><span data-stu-id="ef651-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="ef651-171">Yalnızca HTTP trafiğini işlemek, bu kural başka olabilir kısıtlı tooonly hedef bağlantı noktası 80 izin verin.</span><span class="sxs-lookup"><span data-stu-id="ef651-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="ef651-172">Bu kural hello IIS01 sunucusundan trafiği toopass toohello AppVM01 sunucu izin verir; bir sonraki kural diğer tüm ön uç tooBackend trafiği engeller.</span><span class="sxs-lookup"><span data-stu-id="ef651-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="ef651-173">Bu kural, başlangıç bağlantı noktası biliniyorsa eklenmelidir tooimprove.</span><span class="sxs-lookup"><span data-stu-id="ef651-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="ef651-174">Merhaba IIS sunucusu yalnızca SQL Server'da AppVM01 basarsa, örneğin, hello hedef bağlantı noktası aralığı değiştirildiği "*" (tüm) too1433 (Merhaba SQL bağlantı noktası) böylece Merhaba web uygulaması hiç tehlikeye AppVM01 üzerinde daha küçük bir gelen saldırı yüzeyini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef651-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="ef651-175">Bu kural hello Internet tooany sunucularından hello ağ üzerindeki trafiği engeller.</span><span class="sxs-lookup"><span data-stu-id="ef651-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="ef651-176">Hello kurallarıyla öncelikli 110 ve 120 hello etkisi tooallow yalnızca gelen Internet trafiği toohello güvenlik duvarı ve sunucularda RDP bağlantı noktalarını ve şey engeller.</span><span class="sxs-lookup"><span data-stu-id="ef651-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="ef651-177">Bu kural, "Ayrıcalık tanımayın" kural tooblock tüm beklenmeyen akışlar ' dir.</span><span class="sxs-lookup"><span data-stu-id="ef651-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="ef651-178">Merhaba son kural hello ön uç alt toohello arka uç alt ağından trafiği engeller.</span><span class="sxs-lookup"><span data-stu-id="ef651-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="ef651-179">Bu kural yalnızca bir gelen kuralı olduğundan, geriye doğru trafiğinin (Merhaba arka uç toohello ön uç) izin verilir.</span><span class="sxs-lookup"><span data-stu-id="ef651-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="ef651-180">Trafik senaryoları</span><span class="sxs-lookup"><span data-stu-id="ef651-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="ef651-181">(*İzin verilen*) Internet tooweb sunucusu</span><span class="sxs-lookup"><span data-stu-id="ef651-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="ef651-182">NIC hello IIS01 NIC ile ilişkili hello hello ortak IP adresinden gelen HTTP sayfası bir Internet kullanıcı istekleri</span><span class="sxs-lookup"><span data-stu-id="ef651-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="ef651-183">Merhaba genel IP adresi trafik toohello VNet IIS01 doğru geçirir (Merhaba web sunucusu)</span><span class="sxs-lookup"><span data-stu-id="ef651-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="ef651-184">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="ef651-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="ef651-185">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="ef651-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="ef651-186">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="ef651-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="ef651-187">NSG kural 3 (Internet tooIIS01) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="ef651-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="ef651-188">İç IP adresi hello web sunucusunun IIS01 (10.0.1.5) trafiği isabetler</span><span class="sxs-lookup"><span data-stu-id="ef651-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="ef651-189">IIS01 web trafiği için dinleme, bu isteği alır ve hello isteği işlemeye başlıyor</span><span class="sxs-lookup"><span data-stu-id="ef651-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="ef651-190">IIS01 hello SQL Server AppVM01 hakkında bilgi için sorar</span><span class="sxs-lookup"><span data-stu-id="ef651-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="ef651-191">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="ef651-192">Merhaba arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="ef651-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="ef651-193">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="ef651-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="ef651-194">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="ef651-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="ef651-195">NSG kuralı 3 (Internet tooFirewall) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="ef651-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="ef651-196">NSG kuralı 4 (IIS01 tooAppVM01) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="ef651-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="ef651-197">AppVM01 hello SQL sorgusu alır ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="ef651-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="ef651-198">Merhaba arka uç alt ağda hiçbir giden kuralları olduğundan hello yanıt izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="ef651-199">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="ef651-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="ef651-200">Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok</span><span class="sxs-lookup"><span data-stu-id="ef651-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="ef651-201">Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ef651-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="ef651-202">Merhaba IIS sunucusu hello SQL yanıtı alır ve hello HTTP yanıtı tamamlar ve toohello isteyenin gönderir</span><span class="sxs-lookup"><span data-stu-id="ef651-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="ef651-203">Merhaba ön uç alt ağda hiçbir giden kuralları olduğundan, hello yanıt izin verilir ve hello web sayfasının hello Internet kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="ef651-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="ef651-204">(*İzin verilen*) RDP tooIIS sunucu</span><span class="sxs-lookup"><span data-stu-id="ef651-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="ef651-205">Bir sunucu yöneticisi internet üzerindeki bir RDP oturumu tooIIS01 NIC hello IIS01 (Bu genel IP adresi Portal veya PowerShell hello bulunabilir) NIC ile ilişkili hello hello genel IP adresi üzerinde istekleri</span><span class="sxs-lookup"><span data-stu-id="ef651-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="ef651-206">Merhaba genel IP adresi trafik toohello VNet IIS01 doğru geçirir (Merhaba web sunucusu)</span><span class="sxs-lookup"><span data-stu-id="ef651-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="ef651-207">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="ef651-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="ef651-208">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="ef651-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="ef651-209">NSG kuralı 2 (RDP) uygulamak için izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="ef651-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="ef651-210">Hiçbir giden kuralları, varsayılan kuralları uygula ve dönüş trafiğine izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="ef651-211">RDP oturumu etkin</span><span class="sxs-lookup"><span data-stu-id="ef651-211">RDP session is enabled</span></span>
6. <span data-ttu-id="ef651-212">IIS01 hello kullanıcı adı ve parola isteyen</span><span class="sxs-lookup"><span data-stu-id="ef651-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="ef651-213">Bu örnekte, hello IIS sunucusu tooRDP tooany arka uç sunucuları, bir "atlama kutu." kullanılır</span><span class="sxs-lookup"><span data-stu-id="ef651-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="ef651-214">İlk RDP toohello IIS sunucusunu ve sonra hello IIS sunucu RDP toohello arka uç sunucu.</span><span class="sxs-lookup"><span data-stu-id="ef651-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="ef651-215">(*İzin verilen*) Web sunucusu DNS araması DNS sunucusunda</span><span class="sxs-lookup"><span data-stu-id="ef651-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="ef651-216">Sunucu, IIS01, gereksinimlerini www.data.gov bir veri akışı web ancak tooresolve adresi hello.</span><span class="sxs-lookup"><span data-stu-id="ef651-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="ef651-217">Merhaba ağ yapılandırma hello VNet listeleri DNS01 (10.0.2.4 hello arka uç alt ağdaki) hello birincil DNS sunucusu olarak, IIS01 hello DNS isteği tooDNS01 gönderir</span><span class="sxs-lookup"><span data-stu-id="ef651-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="ef651-218">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="ef651-219">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="ef651-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="ef651-220">NSG kural 1 (DNS) uygulamak için izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="ef651-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="ef651-221">DNS sunucusu hello isteği alır</span><span class="sxs-lookup"><span data-stu-id="ef651-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="ef651-222">DNS sunucusu önbelleğe hello adresi yoksa ve bir kök DNS sunucusu üzerinde hello ister Internet</span><span class="sxs-lookup"><span data-stu-id="ef651-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="ef651-223">Hiçbir giden kuralları arka uç alt ağdaki trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="ef651-224">Bu oturumda dahili olarak başlatıldı beri Internet DNS sunucusu yanıt, hello yanıt izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="ef651-225">DNS sunucusu hello yanıtı önbelleğe alır ve toohello ilk isteği geri tooIIS01 yanıt verir</span><span class="sxs-lookup"><span data-stu-id="ef651-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="ef651-226">Hiçbir giden kuralları arka uç alt ağdaki trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="ef651-227">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="ef651-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="ef651-228">Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok</span><span class="sxs-lookup"><span data-stu-id="ef651-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="ef651-229">Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır</span><span class="sxs-lookup"><span data-stu-id="ef651-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="ef651-230">IIS01 hello yanıt DNS01 alır.</span><span class="sxs-lookup"><span data-stu-id="ef651-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="ef651-231">(*İzin verilen*) Web sunucusu erişimini dosyasını AppVM01 üzerinde</span><span class="sxs-lookup"><span data-stu-id="ef651-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="ef651-232">Bir dosyanın AppVM01 IIS01 sorar</span><span class="sxs-lookup"><span data-stu-id="ef651-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="ef651-233">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="ef651-234">Merhaba arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="ef651-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="ef651-235">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="ef651-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="ef651-236">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="ef651-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="ef651-237">NSG kuralı 3 (Internet tooIIS01) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="ef651-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="ef651-238">NSG kuralı 4 (IIS01 tooAppVM01) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="ef651-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="ef651-239">AppVM01 hello isteğini alır ve (erişim yetkisi varsayılarak) dosyası ile yanıt verir</span><span class="sxs-lookup"><span data-stu-id="ef651-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="ef651-240">Merhaba arka uç alt ağda hiçbir giden kuralları olduğundan hello yanıt izin verilir</span><span class="sxs-lookup"><span data-stu-id="ef651-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="ef651-241">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="ef651-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="ef651-242">Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok</span><span class="sxs-lookup"><span data-stu-id="ef651-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="ef651-243">Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ef651-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="ef651-244">Merhaba IIS sunucu hello dosya alır</span><span class="sxs-lookup"><span data-stu-id="ef651-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="ef651-245">(*Reddedildi*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="ef651-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="ef651-246">Bir Internet kullanıcı tooRDP tooserver AppVM01 çalışır</span><span class="sxs-lookup"><span data-stu-id="ef651-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="ef651-247">Bu sunucular NIC ile ilişkili herhangi bir ortak IP adresi olduğundan, bu trafiği hello VNet hiçbir zaman girersiniz ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="ef651-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="ef651-248">Bir ortak IP adresi herhangi bir nedenden dolayı etkinleştirilirse, NSG kuralı 2 (RDP) bu trafiği ancak olanak tanır</span><span class="sxs-lookup"><span data-stu-id="ef651-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="ef651-249">Bu örnekte, hello IIS sunucusu tooRDP tooany arka uç sunucuları, bir "atlama kutu." kullanılır</span><span class="sxs-lookup"><span data-stu-id="ef651-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="ef651-250">İlk RDP toohello IIS sunucusunu ve sonra hello IIS sunucu RDP toohello arka uç sunucu.</span><span class="sxs-lookup"><span data-stu-id="ef651-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="ef651-251">(*Reddedildi*) Web toobackend sunucusu</span><span class="sxs-lookup"><span data-stu-id="ef651-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="ef651-252">Bir Internet kullanıcı tooaccess AppVM01 dosyada çalışır</span><span class="sxs-lookup"><span data-stu-id="ef651-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="ef651-253">Bu sunucular NIC ile ilişkili herhangi bir ortak IP adresi olduğundan, bu trafiği hello VNet hiçbir zaman girersiniz ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="ef651-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="ef651-254">Bir ortak IP adresi herhangi bir nedenden dolayı etkinleştirilirse, NSG kural 5 (Internet tooVNet) bu trafiği engeller</span><span class="sxs-lookup"><span data-stu-id="ef651-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="ef651-255">(*Reddedildi*) DNS sunucusunda Web DNS araması</span><span class="sxs-lookup"><span data-stu-id="ef651-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="ef651-256">Bir Internet kullanıcı çalıştığında toolook DNS01 bir iç DNS kaydını ayarlama</span><span class="sxs-lookup"><span data-stu-id="ef651-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="ef651-257">Bu sunucular NIC ile ilişkili herhangi bir ortak IP adresi olduğundan, bu trafiği hello VNet hiçbir zaman girersiniz ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="ef651-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="ef651-258">Bir ortak IP adresi herhangi bir nedenden dolayı etkinleştirilirse, NSG kural 5 (Internet tooVNet) bu trafiği engeller (Not: is Internet hello ve kural 1 yalnızca toohello geçerlidir hello kaynak adresi istekleri için kuralı 1 (DNS) uygulanacak değil, yerel VNet hello kaynağı olarak)</span><span class="sxs-lookup"><span data-stu-id="ef651-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="ef651-259">(*Reddedildi*) hello web sunucusunda SQL erişimi</span><span class="sxs-lookup"><span data-stu-id="ef651-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="ef651-260">Bir Internet kullanıcının SQL veri IIS01 istekleri</span><span class="sxs-lookup"><span data-stu-id="ef651-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="ef651-261">Bu sunucular NIC ile ilişkili herhangi bir ortak IP adresi olduğundan, bu trafiği hello VNet hiçbir zaman girersiniz ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="ef651-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="ef651-262">Bir ortak IP adresi herhangi bir nedenden dolayı etkinleştirilirse, hello ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="ef651-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="ef651-263">NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="ef651-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="ef651-264">NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="ef651-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="ef651-265">NSG kural 3 (Internet tooIIS01) geçerli, izin verilen, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="ef651-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="ef651-266">İç IP adresi hello IIS01 (10.0.1.5) trafiği isabetler</span><span class="sxs-lookup"><span data-stu-id="ef651-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="ef651-267">Bağlantı noktası 1433, bu nedenle hiçbir yanıt toohello isteği IIS01 dinleme değil</span><span class="sxs-lookup"><span data-stu-id="ef651-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="ef651-268">Sonuç</span><span class="sxs-lookup"><span data-stu-id="ef651-268">Conclusion</span></span>
<span data-ttu-id="ef651-269">Bu örnek hello arka uç alt ağından gelen trafiği yalıtma, görece basit ve basit bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="ef651-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="ef651-270">Daha fazla örnekler ve ağ güvenlik sınırları genel bir bakış bulunabilir [burada][HOME].</span><span class="sxs-lookup"><span data-stu-id="ef651-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="ef651-271">Başvurular</span><span class="sxs-lookup"><span data-stu-id="ef651-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="ef651-272">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="ef651-272">Azure Resource Manager template</span></span>
<span data-ttu-id="ef651-273">Bu örnek, önceden tanımlanmış bir Azure Resource Manager şablonu Microsoft tarafından yönetilen bir GitHub deposunu kullanır ve toohello topluluk açın.</span><span class="sxs-lookup"><span data-stu-id="ef651-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="ef651-274">Bu şablon Github'dan sınırsız dağıtılabilir veya indirilir ve gereksinimlerinizi toofit değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="ef651-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="ef651-275">"azuredeploy.json." adlı hello dosyasında Hello ana şablon.</span><span class="sxs-lookup"><span data-stu-id="ef651-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="ef651-276">Bu şablon PowerShell veya CLI (Merhaba ilişkili "azuredeploy.parameters.json" dosyasıyla) gönderilebilir toodeploy bu şablonu.</span><span class="sxs-lookup"><span data-stu-id="ef651-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="ef651-277">Hello en kolay yolu toouse hello github'da hello README.md sayfasındaki "Dağıtma tooAzure" düğmesi olan bulabilirim.</span><span class="sxs-lookup"><span data-stu-id="ef651-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="ef651-278">Bu örnek GitHub ve hello Azure portal, derlemeler toodeploy hello şablon şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ef651-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="ef651-279">Tarayıcıdan toohello gidin [şablonu][Template]</span><span class="sxs-lookup"><span data-stu-id="ef651-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="ef651-280">Merhaba "Dağıtma tooAzure" düğmesine (veya hello "Görselleştir" düğmesine toosee bu şablonu grafik gösterimi) tıklatın</span><span class="sxs-lookup"><span data-stu-id="ef651-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="ef651-281">Merhaba parametreler dikey penceresinde Hello depolama hesabı, kullanıcı adı ve parola girin ve ardından **Tamam**</span><span class="sxs-lookup"><span data-stu-id="ef651-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="ef651-282">Bu dağıtım için bir kaynak grubu oluşturun (mevcut bir kullanabilirsiniz, ancak yeni bir en iyi sonuçlar için önerilir)</span><span class="sxs-lookup"><span data-stu-id="ef651-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="ef651-283">Gerekirse, sanal ağınızı hello abonelik ve konumda ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ef651-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="ef651-284">Tıklatın **yasal koşulları gözden geçir**hello koşullarını okuyun ve tıklatın **satın alma** tooagree.</span><span class="sxs-lookup"><span data-stu-id="ef651-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="ef651-285">Tıklatın **oluşturma** bu şablonu toobegin hello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="ef651-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="ef651-286">Merhaba dağıtım başarıyla tamamlandıktan sonra kaynak grubu içinde yapılandırılmış bu dağıtım toosee hello kaynaklar için oluşturulan toohello gidin.</span><span class="sxs-lookup"><span data-stu-id="ef651-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="ef651-287">Bu şablon RDP toohello IIS01 yalnızca sunucu (IIS01 için genel IP hello portalı üzerinde Bul hello) sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef651-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="ef651-288">Bu örnekte, hello IIS sunucusu tooRDP tooany arka uç sunucuları, bir "atlama kutu." kullanılır</span><span class="sxs-lookup"><span data-stu-id="ef651-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="ef651-289">İlk RDP toohello IIS sunucusunu ve sonra hello IIS sunucu RDP toohello arka uç sunucu.</span><span class="sxs-lookup"><span data-stu-id="ef651-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="ef651-290">tooremove bu dağıtım, delete hello kaynak grubu ve tüm alt kaynaklar da silinir.</span><span class="sxs-lookup"><span data-stu-id="ef651-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="ef651-291">Örnek uygulama komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="ef651-291">Sample application scripts</span></span>
<span data-ttu-id="ef651-292">Merhaba şablonu başarıyla çalıştıktan sonra bu DMZ yapılandırma ile test basit bir web uygulaması tooallow ile Merhaba web sunucusu ve uygulama sunucusu ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef651-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="ef651-293">tooinstall örnek bir uygulama bu ve diğer çevre örnekleri için bir sağlamış bağlantıyı izleyerek hello: [örnek uygulama betiği][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="ef651-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef651-294">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ef651-294">Next steps</span></span>

* <span data-ttu-id="ef651-295">Bu örnek dağıtma</span><span class="sxs-lookup"><span data-stu-id="ef651-295">Deploy this example</span></span>
* <span data-ttu-id="ef651-296">Merhaba örnek uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef651-296">Build hello sample application</span></span>
* <span data-ttu-id="ef651-297">Bu DMZ aracılığıyla farklı trafik akışları test etme</span><span class="sxs-lookup"><span data-stu-id="ef651-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "NSG ile giriş DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md