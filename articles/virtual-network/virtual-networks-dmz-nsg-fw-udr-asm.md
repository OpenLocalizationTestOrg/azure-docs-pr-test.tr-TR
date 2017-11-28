---
title: "bir güvenlik duvarı, UDR ve NSG ağlarla aaaDMZ örnek – yapı DMZ tooProtect | Microsoft Docs"
description: "Bir güvenlik duvarı ile DMZ derleme, kullanıcı tanımlı yönlendirme (UDR) ve ağ güvenlik grupları (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="4b866-103">Örnek 3 – bir güvenlik duvarı, UDR ve NSG ağlarla DMZ tooProtect derleme</span><span class="sxs-lookup"><span data-stu-id="4b866-103">Example 3 – Build a DMZ tooProtect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="4b866-104">[Dönüş toohello güvenlik sınırı en iyi uygulamalar sayfası][HOME]</span><span class="sxs-lookup"><span data-stu-id="4b866-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="4b866-105">Bu örnek, bir güvenlik duvarı, dört windows sunucuları, kullanıcı tanımlı yönlendirme, IP iletimi ve ağ güvenlik grupları ile DMZ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4b866-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="4b866-106">Bu da her hello ilgili komutları tooprovide her adımın daha derin bir anlayış yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="4b866-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="4b866-107">Ayrıca vardır bir trafik senaryo bölüm tooprovide ayrıntılı bir adım adım derinlemesine savunma hello katmanları üzerinden trafik geçer nasıl DMZ hello.</span><span class="sxs-lookup"><span data-stu-id="4b866-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="4b866-108">Son olarak, hello references bölümünde hello tam kod ve yönerge toobuild bu ortam tootest çeşitli senaryoları ile deneme ise.</span><span class="sxs-lookup"><span data-stu-id="4b866-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="4b866-109">![Çift yönlü DMZ NVA, NSG ve UDR][1]</span><span class="sxs-lookup"><span data-stu-id="4b866-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="4b866-110">Ortam Kurulumu</span><span class="sxs-lookup"><span data-stu-id="4b866-110">Environment Setup</span></span>
<span data-ttu-id="4b866-111">Bu örnekte hello aşağıdakileri içeren bir abonelik vardır:</span><span class="sxs-lookup"><span data-stu-id="4b866-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="4b866-112">Üç bulut hizmetlerini: "SecSvc001", "FrontEnd001" ve "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="4b866-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="4b866-113">Bir sanal ağ "CorpNetwork" üç alt ağ ile: "SecNet", "Ön uç" ve "Arka uç"</span><span class="sxs-lookup"><span data-stu-id="4b866-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="4b866-114">Bu örnekte bir güvenlik duvarı, bir ağ sanal gereç toohello SecNet alt bağlı</span><span class="sxs-lookup"><span data-stu-id="4b866-114">A network virtual appliance, in this example a firewall, connected toohello SecNet subnet</span></span>
* <span data-ttu-id="4b866-115">Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="4b866-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="4b866-116">Uygulama geri temsil eden iki windows sunucuları sunucuları ("AppVM01", "AppVM02") end</span><span class="sxs-lookup"><span data-stu-id="4b866-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="4b866-117">Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="4b866-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="4b866-118">Merhaba başvurular bölümünde yukarıda açıklanan hello ortamı çoğunu oluşturacak bir PowerShell komut dosyası yok.</span><span class="sxs-lookup"><span data-stu-id="4b866-118">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="4b866-119">Yapı hello VM'ler ve sanal ağlar, bu belgede ayrıntılı hello örnek komut dosyası tarafından yapılır rağmen açıklanmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="4b866-119">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="4b866-120">toobuild hello ortamı:</span><span class="sxs-lookup"><span data-stu-id="4b866-120">toobuild hello environment:</span></span>

1. <span data-ttu-id="4b866-121">(Adları, konum ve IP adreslerini toomatch verilen hello senaryo güncelleştirilmiş) hello başvurular bölümüne dahil hello ağ yapılandırma xml dosyasını kaydedin</span><span class="sxs-lookup"><span data-stu-id="4b866-121">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="4b866-122">Güncelleştirme hello kullanıcı değişkenleri hello betik toomatch hello ortamı hello komut olan toobe Çalıştır (Abonelikleri, hizmet adlarını vb. karşı)</span><span class="sxs-lookup"><span data-stu-id="4b866-122">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="4b866-123">PowerShell'de Hello komut dosyası yürütme</span><span class="sxs-lookup"><span data-stu-id="4b866-123">Execute hello script in PowerShell</span></span>

<span data-ttu-id="4b866-124">**Not**: hello PowerShell Betiği miktarlara hello bölge hello ağ yapılandırması xml dosyasında miktarlara hello bölge eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b866-124">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="4b866-125">Merhaba komut dosyası başarıyla çalıştıktan sonra sonrası betik adımları izleyerek hello izlenebilir:</span><span class="sxs-lookup"><span data-stu-id="4b866-125">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="4b866-126">Merhaba güvenlik duvarı kuralları ayarlamak, bu başlıklı hello aşağıdaki bölümde ele alınmıştır: güvenlik duvarı kuralı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="4b866-126">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="4b866-127">İsteğe bağlı olarak iki komut dosyaları tooset hello web sunucusu ve uygulama sunucusu bu DMZ yapılandırma ile test basit bir web uygulaması tooallow ile Merhaba başvurular bölümünde bulunur.</span><span class="sxs-lookup"><span data-stu-id="4b866-127">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="4b866-128">Merhaba komut dosyası başarıyla çalıştıktan sonra hello güvenlik duvarı kuralları tamamlandı toobe gerekir, bu başlıklı hello bölümde ele alınmıştır: güvenlik duvarı kuralları.</span><span class="sxs-lookup"><span data-stu-id="4b866-128">Once hello script runs successfully hello firewall rules will need toobe completed, this is covered in hello section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="4b866-129">Kullanıcı tanımlı yönlendirme (UDR)</span><span class="sxs-lookup"><span data-stu-id="4b866-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="4b866-130">Varsayılan olarak, sistem yolları aşağıdaki hello olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="4b866-130">By default, hello following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="4b866-131">Merhaba VNETLocal hello tanımlanan adres ön hello VNet (IE, her belirli VNet nasıl tanımlandığına bağlı olarak VNet tooVNet değiştirilecek), belirli bir ağ için her zaman olur.</span><span class="sxs-lookup"><span data-stu-id="4b866-131">hello VNETLocal is always hello defined address prefix(es) of hello VNet for that specific network (ie it will change from VNet tooVNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="4b866-132">Merhaba kalan sistem yolları statik ve yukarıdaki varsayılan.</span><span class="sxs-lookup"><span data-stu-id="4b866-132">hello remaining system routes are static and default as above.</span></span>

<span data-ttu-id="4b866-133">Öncelik, ettirilmesi yollar hello en uzun ön ek eşleşmesi (LPM) yöntemiyle işlenir, böylece hello hello tablosunda en belirgin yolu hedef adres verilen tooa geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="4b866-133">As for priority, routes are processed via hello Longest Prefix Match (LPM) method, thus hello most specific route in hello table would apply tooa given destination address.</span></span>

<span data-ttu-id="4b866-134">Bu nedenle, trafiği (örneğin toohello DNS01 sunucusu 10.0.2.4) hello yerel ağ (10.0.0.0/16) hello VNet tooits hedef toohello 10.0.0.0/16 rota son üzerinden yönlendirilecektir.</span><span class="sxs-lookup"><span data-stu-id="4b866-134">Therefore, traffic (for example toohello DNS01 server, 10.0.2.4) intended for hello local network (10.0.0.0/16) would be routed across hello VNet tooits destination due toohello 10.0.0.0/16 route.</span></span> <span data-ttu-id="4b866-135">Diğer bir deyişle, 10.0.2.4 için hello 10.0.0.0/16 yol hello en belirgin, hello 10.0.0.0/8 ve 0.0.0.0/0 de geçerli olabilir, ancak daha az belirli olduğundan bu trafiği etkilemez olsa bile yoldur.</span><span class="sxs-lookup"><span data-stu-id="4b866-135">In other words, for 10.0.2.4, hello 10.0.0.0/16 route is hello most specific route, even though hello 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="4b866-136">Bu nedenle hello trafiği too10.0.2.4 yerel VNet hello ve yalnızca toohello hedef yol bir sonraki atlama olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b866-136">Thus hello traffic too10.0.2.4 would have a next hop of hello local VNet and simply route toohello destination.</span></span>

<span data-ttu-id="4b866-137">Trafik tasarlanmıştır 10.1.1.1 için örneğin, hello 10.0.0.0/16 rota olmayacaktır uygularsanız, ancak hello 10.0.0.0/8 hello en belirgin olacaktır ve bu hello trafiği olacaktır ("siyah holed") hello sonraki atlama değeri Null olduğundan bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="4b866-137">If traffic was intended for 10.1.1.1 for example, hello 10.0.0.0/16 route wouldn’t apply, but hello 10.0.0.0/8 would be hello most specific, and this hello traffic would be dropped (“black holed”) since hello next hop is Null.</span></span> 

<span data-ttu-id="4b866-138">Merhaba hedef tooany hello Null önekleri veya hello VNETLocal önekleri uygulayın kaydetmedi ve hello az belirli izlersiniz yönlendirmek, 0.0.0.0/0 ve toohello hello sonraki atlama olarak Internet ve böylece Azure'nın Internet kenar çıkışı yönlendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="4b866-138">If hello destination didn’t apply tooany of hello Null prefixes or hello VNETLocal prefixes, then it would follow hello least specific route, 0.0.0.0/0 and be routed out toohello Internet as hello next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="4b866-139">Merhaba rota tablosunda iki aynı önekleri varsa hello tercih sırasına göre hello yolları "kaynak" özniteliğine dayanarak hello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4b866-139">If there are two identical prefixes in hello route table, hello following is hello order of preference based on hello routes “source” attribute:</span></span>

1. <span data-ttu-id="4b866-140">"Değerinin VirtualAppliance" = kullanıcı tanımlı yol el ile eklenen toohello tablosu</span><span class="sxs-lookup"><span data-stu-id="4b866-140">"VirtualAppliance" = A User Defined Route manually added toohello table</span></span>
2. <span data-ttu-id="4b866-141">"VPNGateway" dinamik rota (BGP), karma ağlarla kullanıldığında = hello dinamik Protokolü otomatik olarak eşlenmiş ağ değişiklikleri yansıtır gibi dinamik ağ protokolü tarafından eklenen, bu yollar zaman içinde değişebilir</span><span class="sxs-lookup"><span data-stu-id="4b866-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as hello dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="4b866-142">"Varsayılan" Merhaba sistem yolları = hello rota tabloda yukarıda gösterildiği gibi yerel VNet ve hello statik girişleri hello.</span><span class="sxs-lookup"><span data-stu-id="4b866-142">“Default” = hello System Routes, hello local VNet and hello static entries as shown in hello route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="4b866-143">Gelen şirket içi toobe yönlendirilmiş tooa ağ sanal gereç (NVA) trafiği ve giden ExpressRoute ve VPN ağ geçitleri tooforce ile artık kullanıcı tanımlı yönlendirme (UDR) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b866-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways tooforce outbound and inbound cross-premises traffic toobe routed tooa network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-hello-local-routes"></a><span data-ttu-id="4b866-144">Merhaba yerel yollar oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b866-144">Creating hello local routes</span></span>
<span data-ttu-id="4b866-145">Bu örnekte, iki yönlendirme tablolarını gereklidir, her biri hello ön uç ve arka uç alt ağlar için.</span><span class="sxs-lookup"><span data-stu-id="4b866-145">In this example, two routing tables are needed, one each for hello Frontend and Backend subnets.</span></span> <span data-ttu-id="4b866-146">Her tablo için alt ağ verilen hello uygun statik yollar ile yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4b866-146">Each table is loaded with static routes appropriate for hello given subnet.</span></span> <span data-ttu-id="4b866-147">Bu örnek Hello amaçla her tablo üç yol vardır:</span><span class="sxs-lookup"><span data-stu-id="4b866-147">For hello purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="4b866-148">Tanımlanan bir sonraki atlama tooallow yerel alt ağ trafiği toobypass hello güvenlik duvarı olmayan yerel alt ağ trafiği</span><span class="sxs-lookup"><span data-stu-id="4b866-148">Local subnet traffic with no Next Hop defined tooallow local subnet traffic toobypass hello firewall</span></span>
2. <span data-ttu-id="4b866-149">Bir sonraki güvenlik duvarı olarak tanımlanan atlama ile sanal ağ trafiği, bu yerel VNet trafiği tooroute doğrudan veren hello varsayılan kuralı geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="4b866-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides hello default rule that allows local VNet traffic tooroute directly</span></span>
3. <span data-ttu-id="4b866-150">Bir sonraki atlama ile tüm kalan trafiği (0/0) güvenlik duvarı hello olarak tanımlanan</span><span class="sxs-lookup"><span data-stu-id="4b866-150">All remaining traffic (0/0) with a Next Hop defined as hello firewall</span></span>

<span data-ttu-id="4b866-151">Merhaba yönlendirme tablolarını oluşturulduktan sonra bunların ilişkili tootheir alt ağlardır.</span><span class="sxs-lookup"><span data-stu-id="4b866-151">Once hello routing tables are created they are bound tootheir subnets.</span></span> <span data-ttu-id="4b866-152">Merhaba ön uç için alt ağ yönlendirme tablosu, oluşturup bağlı sonra toohello alt aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="4b866-152">For hello Frontend subnet routing table, once created and bound toohello subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="4b866-153">Bu örnek için kullanılan toobuild hello rota tablosundan hello aşağıdaki komutlar, kullanıcı tanımlı yol eklemek ve hello rota tablosu tooa alt ağa bağlamak (Not; dolar işareti ile başlayan altındaki öğeleri (örn: $BESubnet) hello komut dosyasından kullanıcı tanımlı değişkenler Merhaba başvuru bölümü, bu belgenin):</span><span class="sxs-lookup"><span data-stu-id="4b866-153">For this example, hello following commands are used toobuild hello route table, add a user defined route, and then bind hello route table tooa subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="4b866-154">İlk hello temel yönlendirme tablosu oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b866-154">First hello base routing table must be created.</span></span> <span data-ttu-id="4b866-155">Bu kod parçacığında hello arka uç alt ağ için hello tablosu hello oluşturulmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4b866-155">This snippet shows hello creation of hello table for hello Backend subnet.</span></span> <span data-ttu-id="4b866-156">Merhaba komut dosyasında karşılık gelen bir tablo için hello ön uç alt da oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4b866-156">In hello script, a corresponding table is also created for hello Frontend subnet.</span></span>
   
     <span data-ttu-id="4b866-157">AzureRouteTable yeni-ad $BERouteTableName '</span><span class="sxs-lookup"><span data-stu-id="4b866-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="4b866-158">Merhaba yol tablosu oluşturulduktan sonra belirli kullanıcı tanımlı yollar eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-158">Once hello route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="4b866-159">Bu konuda kırpılmış, tüm trafik (0.0.0.0/0) (bir $VMIP [0], başlangıç IP adresi hello sanal gereç önceki hello komut dosyasında oluşturulduğunda atanan kullanılan toopass değişkendir) hello sanal gereç aracılığıyla yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-159">In this snipped, all traffic (0.0.0.0/0) will be routed through hello virtual appliance (a variable, $VMIP[0], is used toopass in hello IP address assigned when hello virtual appliance was created earlier in hello script).</span></span> <span data-ttu-id="4b866-160">Merhaba komut dosyasında karşılık gelen bir kural hello ön uç tablosunda da oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4b866-160">In hello script, a corresponding rule is also created in hello Frontend table.</span></span>
   
     <span data-ttu-id="4b866-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="4b866-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="4b866-162">Rota girişi yukarıda Hello kılar hello varsayılan "0.0.0.0/0" yol, ancak hala hangi belirleyebilmesini varolan hello varsayılan 10.0.0.0/16 kuralı trafiği hello VNet tooroute içinde doğrudan toohello hedef ve toohello ağ sanal gereç.</span><span class="sxs-lookup"><span data-stu-id="4b866-162">hello above route entry will override hello default "0.0.0.0/0" route, but hello default 10.0.0.0/16 rule still existing which would allow traffic within hello VNet tooroute directly toohello destination and not toohello Network Virtual Appliance.</span></span> <span data-ttu-id="4b866-163">toocorrect bu davranışı hello izleyin kural eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b866-163">toocorrect this behavior hello follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="4b866-164">Bu noktada yaptığınız bir seçim toobe yoktur.</span><span class="sxs-lookup"><span data-stu-id="4b866-164">At this point there is a choice toobe made.</span></span> <span data-ttu-id="4b866-165">İki yoldan yukarıda hello ile tüm trafik değerlendirmesi, tek bir alt ağ içindeki bile trafiği için Güvenlik Duvarı'nı toohello yönlendirilecek.</span><span class="sxs-lookup"><span data-stu-id="4b866-165">With hello above two routes all traffic will route toohello firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="4b866-166">Üçüncü, belirli bir kural eklenebilir hello Güvenlik Duvarı'nı müdahalesi olmadan yerel olarak bir alt ağ tooroute içinde tooallow trafiği ancak bu, istenebilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-166">This may be desired, however tooallow traffic within a subnet tooroute locally without involvement from hello firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="4b866-167">Bu yol var bildiren herhangi bir adresi destine hello yerel alt ağ yalnızca için rota doğrudan (NextHopType VNETLocal =).</span><span class="sxs-lookup"><span data-stu-id="4b866-167">This route states that any address destine for hello local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="4b866-168">Son olarak, oluşturulur ve kullanıcı tanımlı yollar ile doldurulur hello yönlendirme tablosunu ile Merhaba tablo şimdi ilişkili tooa alt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-168">Finally, with hello routing table created and populated with a user defined routes, hello table must now be bound tooa subnet.</span></span> <span data-ttu-id="4b866-169">Hello komut dosyasında hello ön uç yol tablosu da ilişkili toohello Frontend alt ağı var.</span><span class="sxs-lookup"><span data-stu-id="4b866-169">In hello script, hello front end route table is also bound toohello Frontend subnet.</span></span> <span data-ttu-id="4b866-170">Merhaba bağlama betik hello arka uç alt ağ için aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4b866-170">Here is hello binding script for hello back end subnet.</span></span>
   
     <span data-ttu-id="4b866-171">Set-AzureSubnetRouteTable - VirtualNetworkName $VNetName '</span><span class="sxs-lookup"><span data-stu-id="4b866-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="4b866-172">IP İletimi</span><span class="sxs-lookup"><span data-stu-id="4b866-172">IP Forwarding</span></span>
<span data-ttu-id="4b866-173">Bir yardımcı özelliği tooUDR olduğu IP iletimi.</span><span class="sxs-lookup"><span data-stu-id="4b866-173">A companion feature tooUDR, is IP Forwarding.</span></span> <span data-ttu-id="4b866-174">Bu özellikle tooreceive trafiğe izin veren bir sanal gereç ayarda toohello Gereci ele ve bu trafiği tooits ultimate hedef iletin.</span><span class="sxs-lookup"><span data-stu-id="4b866-174">This is a setting on a Virtual Appliance that allows it tooreceive traffic not specifically addressed toohello appliance and then forward that traffic tooits ultimate destination.</span></span>

<span data-ttu-id="4b866-175">AppVM01 trafiğinden istek toohello DNS01 sunucusu yaparsa örnek olarak, bu toohello güvenlik duvarı UDR rota.</span><span class="sxs-lookup"><span data-stu-id="4b866-175">As an example, if traffic from AppVM01 makes a request toohello DNS01 server, UDR would route this toohello firewall.</span></span> <span data-ttu-id="4b866-176">Etkin IP iletimi ile hello trafiği hello DNS01 hedef (10.0.2.4) için hello Gereci (10.0.0.4) tarafından kabul ve olması tooits ultimate hedef (10.0.2.4) iletilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-176">With IP Forwarding enabled, hello traffic for hello DNS01 destination (10.0.2.4) will be accepted by hello appliance (10.0.0.4) and then forwarded tooits ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="4b866-177">Merhaba yol tablosu hello güvenlik duvarı hello sonraki atlama olarak olmasına rağmen hello üzerinde Güvenlik Duvarı etkin IP iletimi, trafiği hello Gereci tarafından kabul değil.</span><span class="sxs-lookup"><span data-stu-id="4b866-177">Without IP Forwarding enabled on hello Firewall, traffic would not be accepted by hello appliance even though hello route table has hello firewall as hello next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4b866-178">Kritik tooremember tooenable IP iletimi kullanıcı tanımlı yönlendirme ile birlikte olur.</span><span class="sxs-lookup"><span data-stu-id="4b866-178">It’s critical tooremember tooenable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="4b866-179">IP iletimi ayarlama tek bir komut ve VM oluşturma zamanında yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="4b866-180">Hello için bu örnek hello kod parçacığını akışını hello komut dosyasının hello sonuna doğru olduğundan ve hello UDR komutları ile gruplandırılmış:</span><span class="sxs-lookup"><span data-stu-id="4b866-180">For hello flow of this example hello code snippet is towards hello end of hello script and grouped with hello UDR commands:</span></span>

1. <span data-ttu-id="4b866-181">Sanal gereç olan hello VM örneği çağrısı, Güvenlik Duvarı bu durumda hello ve IP iletimini etkinleştirme (Not; dolar işareti kırmızı başlayarak herhangi bir öğeye (örn: $VMName[0]), bu belgenin hello başvuru bölümünde hello komut dosyasından bir kullanıcı tanımlı değişkendir.</span><span class="sxs-lookup"><span data-stu-id="4b866-181">Call hello VM instance that is your virtual appliance, hello firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="4b866-182">köşeli ayraçlar [0] sıfır Merhaba, temsil VM'ler, hello dizideki hello örnek komut dosyası toowork değişiklik yapmadan için ilk VM Merhaba, ilk VM (VM 0) olmalıdır hello hello Güvenlik Duvarı):</span><span class="sxs-lookup"><span data-stu-id="4b866-182">hello zero in brackets, [0], represents hello first VM in hello array of VMs, for hello example script toowork without modification, hello first VM (VM 0) must be hello firewall):</span></span>
   
     <span data-ttu-id="4b866-183">Get-AzureVM-$ServiceName [0] [0] $VMName - ServiceName adı | \`</span><span class="sxs-lookup"><span data-stu-id="4b866-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="4b866-184">Ağ Güvenlik Grupları (NSG)</span><span class="sxs-lookup"><span data-stu-id="4b866-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="4b866-185">Bu örnekte, bir NSG grubu yerleşik ve tek bir kural ile yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4b866-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="4b866-186">Bu grup ise yalnızca toohello ön uç ve arka uç alt ağlar (değil SecNet hello) bağlı.</span><span class="sxs-lookup"><span data-stu-id="4b866-186">This group is then bound only toohello Frontend and Backend subnets (not hello SecNet).</span></span> <span data-ttu-id="4b866-187">Bildirimli olarak kural aşağıdaki hello üretiliyor:</span><span class="sxs-lookup"><span data-stu-id="4b866-187">Declaratively hello following rule is being built:</span></span>

1. <span data-ttu-id="4b866-188">Merhaba Internet toohello tüm trafiği (tüm bağlantı noktaları) tüm sanal ağ (tüm alt ağlar) reddedildi</span><span class="sxs-lookup"><span data-stu-id="4b866-188">Any traffic (all ports) from hello Internet toohello entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="4b866-189">Nsg'ler Bu örnekte kullanılan cihazın ana amacı el ile yetersizliğini karşı savunma ikincil bir katmanı olarak olsa da.</span><span class="sxs-lookup"><span data-stu-id="4b866-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="4b866-190">Hello Internet tooeither hello ön uç gelen tüm trafiği tooblock istiyoruz veya arka uç alt ağlar, trafiği yalnızca hello SecNet alt toohello güvenlik duvarı akış (ve ardından IF uygun toohello ön uç veya arka uç alt ağlar).</span><span class="sxs-lookup"><span data-stu-id="4b866-190">We want tooblock all inbound traffic from hello internet tooeither hello Frontend or Backend subnets, traffic should only flow through hello SecNet subnet toohello firewall (and then if appropriate on toohello Frontend or Backend subnets).</span></span> <span data-ttu-id="4b866-191">Ayrıca, bir yerde, hello UDR kurallarla ön uç veya arka uç alt hello yaptı tüm trafik toohello Güvenlik Duvarı (teşekkürler tooUDR) yönlendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="4b866-191">Plus, with hello UDR rules in place, any traffic that did make it into hello Frontend or Backend subnets would be directed out toohello firewall (thanks tooUDR).</span></span> <span data-ttu-id="4b866-192">Merhaba Güvenlik Duvarı'nı bu asimetrik bir akış halinde görür ve hello giden trafiği bırakma.</span><span class="sxs-lookup"><span data-stu-id="4b866-192">hello firewall would see this as an asymmetric flow and would drop hello outbound traffic.</span></span> <span data-ttu-id="4b866-193">Bu nedenle üç katmanlı güvenlik koruma hello ön uç ve arka uç alt ağları vardır; 1) hiçbir açık uç noktalarda hello FrontEnd001 ve BackEnd001 bulut Hizmetleri, 2) Nsg'ler reddetme trafiği hello 3) hello güvenlik duvarı asimetrik trafiğini atar.</span><span class="sxs-lookup"><span data-stu-id="4b866-193">Thus there are three layers of security protecting hello Frontend and Backend subnets; 1) no open endpoints on hello FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from hello Internet, 3) hello firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="4b866-194">Bu örnekte hello ağ güvenlik grubu ile ilgili bir ilginç noktası, yalnızca bir kural, aşağıda gösterilen hello güvenlik alt ağ içeren toodeny Internet trafiği toohello tüm sanal ağ olan içermesidir.</span><span class="sxs-lookup"><span data-stu-id="4b866-194">One interesting point regarding hello Network Security Group in this example is that it contains only one rule, shown below, which is toodeny internet traffic toohello entire virtual network which would include hello Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="4b866-195">NSG, yalnızca hello toohello ön uç ve arka uç alt ağları bağlı olduğundan, hello kural trafiğinde ancak işlenen değil toohello güvenlik alt ağ gelen.</span><span class="sxs-lookup"><span data-stu-id="4b866-195">However, since hello NSG is only bound toohello Frontend and Backend subnets, hello rule isn’t processed on traffic inbound toohello Security subnet.</span></span> <span data-ttu-id="4b866-196">Sonuç olarak, NSG gerçekleştirilemeyen hello toohello güvenlik alt ağa bağlı olduğundan hello NSG Kuralı Internet trafiği tooany adres Vnet'in hello üzerinde söyler. olsa bile, trafik toohello güvenlik alt ağ akar.</span><span class="sxs-lookup"><span data-stu-id="4b866-196">As a result, even though hello NSG rule says no Internet traffic tooany address on hello VNet, because hello NSG was never bound toohello Security subnet, traffic will flow toohello Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="4b866-197">Güvenlik Duvarı Kuralları</span><span class="sxs-lookup"><span data-stu-id="4b866-197">Firewall Rules</span></span>
<span data-ttu-id="4b866-198">Merhaba güvenlik duvarında kuralları iletme oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b866-198">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="4b866-199">Merhaba güvenlik duvarı engelleme veya iletme tüm gelen, giden ve içi-VNet trafiği olduğundan birçok güvenlik duvarı kuralları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b866-199">Since hello firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="4b866-200">Ayrıca, tüm gelen trafiği hello güvenlik hizmeti genel IP adresi karşılaşır (farklı bağlantı noktalarını), toobe hello güvenlik duvarı tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="4b866-200">Also, all inbound traffic will hit hello Security Service public IP address (on different ports), toobe processed by hello firewall.</span></span> <span data-ttu-id="4b866-201">Toodiagram hello mantıksal akışları hello alt ağları ve güvenlik duvarı kuralları tooavoid olacak yeniden çalışma ihtimalinden daha sonra ayarlama önce bir en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="4b866-201">A best practice is toodiagram hello logical flows before setting up hello subnets and firewall rules tooavoid rework later.</span></span> <span data-ttu-id="4b866-202">Hello aşağıdaki şekilde hello güvenlik duvarı kuralları bu örnek için mantıksal bir görünümünü gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4b866-202">hello following figure is a logical view of hello firewall rules for this example:</span></span>

<span data-ttu-id="4b866-203">![Mantıksal görünümünü hello güvenlik duvarı kuralları][2]</span><span class="sxs-lookup"><span data-stu-id="4b866-203">![Logical View of hello Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="4b866-204">Ağ sanal gereç kullanılan hello üzerinde bağlı olarak, hello yönetim bağlantı noktalarını değişir.</span><span class="sxs-lookup"><span data-stu-id="4b866-204">Based on hello Network Virtual Appliance used, hello management ports will vary.</span></span> <span data-ttu-id="4b866-205">Barracuda NextGen Firewall başvurulan Bu örnekte, bağlantı noktası 22, 801 ve 807 kullanır.</span><span class="sxs-lookup"><span data-stu-id="4b866-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="4b866-206">Lütfen kullanılan hello aygıt yönetimi için kullanılan hello Gereci satıcı belgelerine toofind hello tam bağlantı noktalarını bakın.</span><span class="sxs-lookup"><span data-stu-id="4b866-206">Please consult hello appliance vendor documentation toofind hello exact ports used for management of hello device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="4b866-207">Mantıksal kural açıklaması</span><span class="sxs-lookup"><span data-stu-id="4b866-207">Logical Rule Description</span></span>
<span data-ttu-id="4b866-208">Merhaba mantıksal Yukarıdaki diyagramda, hello güvenlik duvarı hello yalnızca o alt ağdaki kaynaktır ve bu diyagramda hello güvenlik duvarı kuralları ve nasıl mantıksal olarak izin ver veya Reddet trafik akışına ve hello gerçek yönlendirilmiş yol değil gösteren hello güvenlik alt ağ gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="4b866-208">In hello logical diagram above, hello security subnet is not shown since hello firewall is hello only resource on that subnet, and this diagram is showing hello firewall rules and how they logically allow or deny traffic flows and not hello actual routed path.</span></span> <span data-ttu-id="4b866-209">Ayrıca, daha kolay okunabilir olması için yerel IP adresi hello iki sekizlisinin hello RDP trafiğine yüksek aralıklı bağlantı noktaları (8014 – 8026) olduğundan ve bundan seçili toosomewhat Hizala ile hello için seçilen hello dış bağlantı noktalarını en son (örneğin yerel sunucu adresi 10.0.1.4 ilişkili olduğu dış bağlantı noktası 8014), ancak daha yüksek herhangi çakışmayan bağlantı noktaları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-209">Also, hello external ports selected for hello RDP traffic are higher ranged ports (8014 – 8026) and were selected toosomewhat align with hello last two octets of hello local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="4b866-210">Bu örnek için 7 tür kuralların ihtiyacımız, bu kural türleri aşağıda açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="4b866-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="4b866-211">Dış kuralları (için gelen trafiği):</span><span class="sxs-lookup"><span data-stu-id="4b866-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="4b866-212">Güvenlik Duvarı Yönetimi kuralı: Bu uygulama yeniden yönlendirme kuralı hello ağ sanal gereç trafiği toopass toohello yönetim bağlantı noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="4b866-212">Firewall Management Rule: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance.</span></span>
  2. <span data-ttu-id="4b866-213">RDP kuralları (her windows server için): Bu dört kurallar (her sunucu için bir tane) hello Yönetimi tek tek sunucular RDP aracılığıyla izin verir.</span><span class="sxs-lookup"><span data-stu-id="4b866-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of hello individual servers via RDP.</span></span> <span data-ttu-id="4b866-214">Bu ayrıca hello kullanılan ağ sanal gereç hello yeteneklerini bağlı olarak tek bir kural içine paketlenmiş.</span><span class="sxs-lookup"><span data-stu-id="4b866-214">This could also be bundled into one rule depending on hello capabilities of hello Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="4b866-215">Uygulama trafiği kuralları: İki uygulama trafiği kuralları, hello hello ön uç web trafiği için ilk ve ikinci hello arka uç trafiği (örneğin web sunucusu toodata katmanı) için hello vardır.</span><span class="sxs-lookup"><span data-stu-id="4b866-215">Application Traffic Rules: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="4b866-216">Bu kurallar Hello yapılandırmasını hello ağ mimarisi (sunucularınızı yerleştirildiği) ve (hangi yönde hello trafik akışlarının ve hangi bağlantı noktalarının kullanılacağını) trafiği akışı değişir.</span><span class="sxs-lookup"><span data-stu-id="4b866-216">hello configuration of these rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="4b866-217">Merhaba ilk kural hello gerçek uygulama trafiği tooreach hello uygulama sunucusu izin verir.</span><span class="sxs-lookup"><span data-stu-id="4b866-217">hello first rule will allow hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="4b866-218">Merhaba diğer kurallar izin verirken, güvenlik, yönetim, vb. için uygulama ne hello uygulamaları dış kullanıcı ve hizmet tooaccess izin kurallardır.</span><span class="sxs-lookup"><span data-stu-id="4b866-218">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="4b866-219">Bu örnek için bağlantı noktası 80 üzerinde tek bir web sunucusu yoktur, böylece bir tek uygulama güvenlik duvarını gelen trafiği toohello dış IP, toohello web sunucuları iç IP adresi yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span> <span data-ttu-id="4b866-220">Hello vardı NAT trafiği oturumu yeniden yönlendirilen toohello iç sunucu.</span><span class="sxs-lookup"><span data-stu-id="4b866-220">hello redirected traffic session would be NAT’d toohello internal server.</span></span>
     * <span data-ttu-id="4b866-221">İkinci uygulama trafik kuralı hello herhangi bir bağlantı arka uç kural tooallow hello Web sunucusu tootalk toohello AppVM01 sunucu (ancak değil AppVM02) hello.</span><span class="sxs-lookup"><span data-stu-id="4b866-221">hello second Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="4b866-222">İç kurallardan (içi-VNet trafiği)</span><span class="sxs-lookup"><span data-stu-id="4b866-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="4b866-223">Giden tooInternet kuralı: Bu kural herhangi bir ağ trafiğinden toopass seçili toohello ağlar izin verir.</span><span class="sxs-lookup"><span data-stu-id="4b866-223">Outbound tooInternet Rule: This rule will allow traffic from any network toopass toohello selected networks.</span></span> <span data-ttu-id="4b866-224">Bu genellikle varsayılan bir kural zaten hello güvenlik duvarı, ancak devre dışı durumdayken kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-224">This rule is usually a default rule already on hello firewall, but in a disabled state.</span></span> <span data-ttu-id="4b866-225">Bu kural, bu örnek için etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="4b866-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="4b866-226">DNS kuralı: Bu kural yalnızca DNS (bağlantı noktası 53) trafiği toopass toohello DNS sunucusu sağlar.</span><span class="sxs-lookup"><span data-stu-id="4b866-226">DNS Rule: This rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="4b866-227">Merhaba ön uç toohello arka uç çoğu trafiğinden engellenen bu ortam için bu kural tüm yerel alt ağ üzerinden DNS özellikle sağlar.</span><span class="sxs-lookup"><span data-stu-id="4b866-227">For this environment most traffic from hello Frontend toohello Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="4b866-228">Alt ağ tooSubnet kuralı: herhangi bir sunucuda hello arka uç alt tooconnect tooany sunucusu hello ön uç alt ağdaki (ancak hello geriye doğru değil) tooallow bu kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-228">Subnet tooSubnet Rule: This rule is tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet (but not hello reverse).</span></span>
* <span data-ttu-id="4b866-229">Yedek operatördür kuralı (yukarıdaki hello birini karşılamıyor trafiği):</span><span class="sxs-lookup"><span data-stu-id="4b866-229">Fail-safe Rule (for traffic that doesn’t meet any of hello above):</span></span>
  1. <span data-ttu-id="4b866-230">Tüm trafik kuralı Reddet: Bu her zaman son bir kural hello (bakımından öncelik) olmalıdır ve trafik akışlarına şekilde toomatch bu kural tarafından bırakılacak kuralları önceki hello hiçbirini başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4b866-230">Deny All Traffic Rule: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="4b866-231">Bu varsayılan bir kural ve genellikle etkin, değişikliğe genellikle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4b866-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="4b866-232">Merhaba ikinci uygulama trafik kuralı, herhangi bir bağlantı için bu örneği kolay izin verilir, gerçek senaryo hello bu kural, kullanılan tooreduce hello saldırı yüzeyini en belirli bağlantı noktasının ve adres aralıkları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-232">On hello second application traffic rule, any port is allowed for easy of this example, in a real scenario hello most specific port and address ranges should be used tooreduce hello attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="4b866-233">Tüm kuralları yukarıda hello oluşturulduktan sonra tooreview hello her kural tooensure trafiğin önceliğini izin verilen veya istendiği gibi reddedilen önemlidir.</span><span class="sxs-lookup"><span data-stu-id="4b866-233">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="4b866-234">Bu örnekte, hello öncelik sırasına göre kurallardır.</span><span class="sxs-lookup"><span data-stu-id="4b866-234">For this example, hello rules are in priority order.</span></span> <span data-ttu-id="4b866-235">Merhaba güvenlik duvarı kuralları toomis sipariş son dışında kilitli kolay toobe olur.</span><span class="sxs-lookup"><span data-stu-id="4b866-235">It's easy toobe locked out of hello firewall due toomis-ordered rules.</span></span> <span data-ttu-id="4b866-236">En azından hello Yönetimi hello güvenlik duvarı kendisi için her zaman hello mutlak en yüksek öncelik kuralı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4b866-236">At a minimum, ensure hello management for hello firewall itself is always hello absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="4b866-237">Kural önkoşulları</span><span class="sxs-lookup"><span data-stu-id="4b866-237">Rule Prerequisites</span></span>
<span data-ttu-id="4b866-238">Merhaba sanal makine çalışan hello Güvenlik Duvarı için önkoşul vardır ortak uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="4b866-238">One prerequisite for hello Virtual Machine running hello firewall are public endpoints.</span></span> <span data-ttu-id="4b866-239">Merhaba güvenlik duvarı tooprocess trafiği için hello uygun ortak bitiş noktalarının açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b866-239">For hello firewall tooprocess traffic hello appropriate public endpoints must be open.</span></span> <span data-ttu-id="4b866-240">Bu örnekte trafiğin üç tür vardır; 1) yönetim trafiğini toocontrol hello güvenlik duvarı ve güvenlik duvarı kuralları, 2) RDP trafiğine toocontrol hello windows sunucuları ve 3) uygulama trafiği.</span><span class="sxs-lookup"><span data-stu-id="4b866-240">There are three types of traffic in this example; 1) Management traffic toocontrol hello firewall and firewall rules, 2) RDP traffic toocontrol hello windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="4b866-241">Merhaba üç sütun üst hello trafik türlerinin hello güvenlik duvarı kuralları mantıksal görünümünü yarısı bunlar.</span><span class="sxs-lookup"><span data-stu-id="4b866-241">These are hello three columns of traffic types in hello upper half of logical view of hello firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b866-242">Burada anahtar takeway tooremember olduğundan, **tüm** trafiği hello güvenlik duvarı üzerinden gelen.</span><span class="sxs-lookup"><span data-stu-id="4b866-242">A key takeway here is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="4b866-243">Bunu tooremote Masaüstü toohello IIS01 sunucu, onu hello ön uç bulut hizmeti ve hello ön uç alt tooaccess tooRDP toohello güvenlik duvarı üzerinde ihtiyacımız bu sunucu olsa bile 8014 bağlantı noktası ve hello güvenlik duvarı tooroute hello RDP isteği dahili izin toohello IIS01 RDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="4b866-243">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="4b866-244">Merhaba "Azure portal'ın Bağlan düğmesini olduğu için hiçbir doğrudan RDP yolu tooIIS01 (Merhaba portal görebilirsiniz uzaklığa kadar) çalışmaz".</span><span class="sxs-lookup"><span data-stu-id="4b866-244">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="4b866-245">Tüm bağlantılar yani hello Internet toohello güvenlik hizmeti ve bir bağlantı noktası, örneğin secscv001.cloudapp.net:xxxx (başvuru hello hello eşleme harici bağlantı noktası, iç IP ve bağlantı noktası diyagramı yukarıda) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4b866-245">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference hello above diagram for hello mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="4b866-246">Bir uç nokta hello zaman VM oluşturma ya da açılabilir veya yapı hello örnek komut dosyasında yapılan ve aşağıda bu kod parçacığında gösterildiği gibi post (Not; herhangi bir dolar işareti öğesi başlayarak (örn: $VMName[$i]) olan bir kullanıcı tanımlı değişken hello referen hello betikten Bu belgenin CE bölümü.</span><span class="sxs-lookup"><span data-stu-id="4b866-246">An endpoint can be opened either at hello time of VM creation or post build as is done in hello example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="4b866-247">köşeli ayraçlar [$i] "$i" Hello hello dizi sayısını VM'ler dizisindeki belirli bir VM'yi temsil eder):</span><span class="sxs-lookup"><span data-stu-id="4b866-247">hello “$i” in brackets, [$i], represents hello array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="4b866-248">Değişkenleri, ancak uç noktalar toohello kullanımı, son değil açıkça burada gösterilen ancak **yalnızca** hello güvenlik bulut hizmeti üzerinde açılır.</span><span class="sxs-lookup"><span data-stu-id="4b866-248">Although not clearly shown here due toohello use of variables, but endpoints are **only** opened on hello Security Cloud Service.</span></span> <span data-ttu-id="4b866-249">Tüm gelen trafiği işlenir tooensure budur (yönlendirilmiş NAT bırakılan) hello güvenlik duvarı tarafından.</span><span class="sxs-lookup"><span data-stu-id="4b866-249">This is tooensure that all inbound traffic is handled (routed, NAT'd, dropped) by hello firewall.</span></span>

<span data-ttu-id="4b866-250">Bir yönetim istemcisi yüklü bir bilgisayar toomanage hello Güvenlik Duvarı'nı toobe gerekir ve gerekli hello yapılandırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4b866-250">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="4b866-251">Merhaba, Güvenlik Duvarı (veya diğer NVA) belgelerinden satıcı nasıl toomanage hello üzerinde aygıt bakın.</span><span class="sxs-lookup"><span data-stu-id="4b866-251">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="4b866-252">Bu bölümde ve hello sonraki bölümde, güvenlik duvarı kuralları oluşturma, Hello kalanı hello hello güvenlik duvarı yapılandırmasını kendisini hello satıcılar Yönetimi istemcisi (yani hello Azure portal veya PowerShell) aracılığıyla anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4b866-252">hello remainder of this section and hello next section, Firewall Rules Creation, will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="4b866-253">İstemci Yükleme ve bağlantı toohello Bu örnekte kullanılan Barracuda için yönergeler şurada bulunabilir: [Barracuda NG yönetici](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="4b866-253">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="4b866-254">Merhaba güvenlik duvarı üzerine ancak güvenlik duvarı kuralları oluşturmadan önce oturum sonra oluşturma hello kuralları kolaylaştırabilir iki önkoşul nesne sınıfları vardır; Ağ & hizmeti nesneleri.</span><span class="sxs-lookup"><span data-stu-id="4b866-254">Once logged onto hello firewall but before creating firewall rules, there are two prerequisite object classes that can make creating hello rules easier; Network & Service objects.</span></span>

<span data-ttu-id="4b866-255">Bu örnekte, üç adlandırılmış ağ nesneleri tanımlı (Merhaba Frontend alt ağı ve hello arka uç alt ağ, ayrıca hello hello DNS sunucusunun IP adresi için bir ağ nesnesi için bir) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-255">For this example, three named network objects should be defined (one for hello Frontend subnet and hello Backend subnet, also a network object for hello IP address of hello DNS server).</span></span> <span data-ttu-id="4b866-256">Adlandırılmış ağ toocreate; Merhaba Barracuda NG yönetici istemci panodan başlayarak, toohello yapılandırma sekmesine gidin, hello işletimsel yapılandırma bölümü Ruleset, ardından "Ağlar" Merhaba güvenlik duvarı nesneleri menüsünün altında'ı tıklatın, ardından yeni hello Düzenle ağları menüde tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4b866-256">toocreate a named network; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Networks” under hello Firewall Objects menu, then click New in hello Edit Networks menu.</span></span> <span data-ttu-id="4b866-257">Merhaba ağ nesnesi artık, hello adını ve hello önekini ekleyerek oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="4b866-257">hello network object can now be created, by adding hello name and hello prefix:</span></span>

<span data-ttu-id="4b866-258">![Bir ön uç ağ nesnesi oluşturun][3]</span><span class="sxs-lookup"><span data-stu-id="4b866-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="4b866-259">Bu hello FrontEnd alt ağı için bir adlandırılmış ağ oluşturur, benzer bir nesne de hello arka uç alt oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-259">This will create a named network for hello FrontEnd subnet, a similar object should be created for hello BackEnd subnet as well.</span></span> <span data-ttu-id="4b866-260">Şimdi hello alt hello güvenlik duvarı kuralları ada göre daha kolay başvurulabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-260">Now hello subnets can be more easily referenced by name in hello firewall rules.</span></span>

<span data-ttu-id="4b866-261">Merhaba DNS sunucu nesnesi için:</span><span class="sxs-lookup"><span data-stu-id="4b866-261">For hello DNS Server Object:</span></span>

<span data-ttu-id="4b866-262">![Bir DNS sunucusu nesnesi oluşturun][4]</span><span class="sxs-lookup"><span data-stu-id="4b866-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="4b866-263">Bu tek IP adresi başvurusu DNS kuralı hello belgenin devamındaki kullanılmadan.</span><span class="sxs-lookup"><span data-stu-id="4b866-263">This single IP address reference will be utilized in a DNS rule later in hello document.</span></span>

<span data-ttu-id="4b866-264">Merhaba ikinci önkoşul nesneleri Hizmetleri nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="4b866-264">hello second prerequisite objects are Services objects.</span></span> <span data-ttu-id="4b866-265">Bunlar, her sunucu için hello RDP bağlantı noktaları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4b866-265">These will represent hello RDP connection ports for each server.</span></span> <span data-ttu-id="4b866-266">Merhaba varolan RDP hizmet nesnesi ilişkili toohello varsayılan RDP bağlantı noktası olduğundan, 3389, yeni hizmetler hello dış bağlantı noktalarından (8014-8026) tooallow trafiği oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-266">Since hello existing RDP service object is bound toohello default RDP port, 3389, new Services can be created tooallow traffic from hello external ports (8014-8026).</span></span> <span data-ttu-id="4b866-267">Merhaba yeni bağlantı noktaları ayrıca toohello varolan RDP hizmeti eklenemedi, ancak tanıtım kolaylığı için her sunucu için tek bir kuralı oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-267">hello new ports could also be added toohello existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="4b866-268">bir sunucu için yeni bir RDP kural toocreate; Merhaba Barracuda NG yönetici istemci panodan başlangıç toohello yapılandırma sekmesine gidin, hello işletimsel yapılandırma bölümü Ruleset, tıklatın ardından hello güvenlik duvarı nesneleri menüsünde hello hizmetlerin listesini aşağı kaydırın altında "Hizmetler"'i tıklatın ve hello seçin "RDP" hizmet.</span><span class="sxs-lookup"><span data-stu-id="4b866-268">toocreate a new RDP rule for a server; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Services” under hello Firewall Objects menu, scroll down hello list of services and select hello “RDP” service.</span></span> <span data-ttu-id="4b866-269">Sağ tıklayın ve kopyalayın, sonra sağ tıklatın ve Yapıştır seçin.</span><span class="sxs-lookup"><span data-stu-id="4b866-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="4b866-270">Düzenlenebilir bir RDP Copy1 hizmet nesnesi artık yok.</span><span class="sxs-lookup"><span data-stu-id="4b866-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="4b866-271">RDP Copy1 sağ tıklayın ve Düzenle'yi seçin, hizmet penceresi aşağıda gösterildiği gibi açılır nesnesi Düzenle hello:</span><span class="sxs-lookup"><span data-stu-id="4b866-271">Right-click RDP-Copy1 and select Edit, hello Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="4b866-272">![Varsayılan RDP kuralı kopyası][5]</span><span class="sxs-lookup"><span data-stu-id="4b866-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="4b866-273">Merhaba değerler sonra düzenlenen toorepresent hello RDP hizmeti belirli bir sunucu olabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-273">hello values can then be edited toorepresent hello RDP service for a specific server.</span></span> <span data-ttu-id="4b866-274">Varsayılan yukarıda AppVM01 hello için RDP kural değiştirilmiş tooreflect yeni bir hizmet adı, açıklama, olmalıdır ve dış RDP bağlantı noktası kullanılan hello Şekil 8 diyagramı (Not: hello bağlantı noktalarını hello RDP varsayılan bağlantı noktasının bu amaçla kullanılan 3389 toohello dış değiştirildi belirli AppVM01 hello dış bağlantı noktasının hello durumda sunucudur 8025) hello değiştirilmiş hizmeti aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4b866-274">For AppVM01 hello above default RDP rule should be modified tooreflect a new Service Name, Description, and external RDP Port used in hello Figure 8 diagram (Note: hello ports are changed from hello RDP default of 3389 toohello external port being used for this specific server, in hello case of AppVM01 hello external Port is 8025) hello modified service is shown below:</span></span>

<span data-ttu-id="4b866-275">![AppVM01 kuralı][6]</span><span class="sxs-lookup"><span data-stu-id="4b866-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="4b866-276">Bu işlem, yinelenen toocreate sunucuları kalan hello için RDP Hizmetleri olmalıdır; AppVM02, DNS01 ve IIS01.</span><span class="sxs-lookup"><span data-stu-id="4b866-276">This process must be repeated toocreate RDP Services for hello remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="4b866-277">Bu hizmetler Hello oluşturulmasını hello kural oluşturma daha basit ve daha belirgin hello sonraki bölümde hale getirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-277">hello creation of these Services will make hello Rule creation simpler and more obvious in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="4b866-278">Bir RDP hizmeti hello Güvenlik Duvarı için iki nedenden dolayı gerekli değildir; 1) ilk hello güvenlik duvarı VM olduğu bir Linux tabanlı görüntüsü SSH bağlantı noktası 22 RDP ve 2) bağlantı noktası 22 yerine VM yönetimi için kullanılabilir ve diğer yönetim bağlantı noktalarına iki hello tooallow yönetim bağlantısı için aşağıda açıklanan ilk yönetim kuralında izin verilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-278">An RDP service for hello Firewall is not needed for two reasons; 1) first hello firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in hello first management rule described below tooallow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="4b866-279">Güvenlik duvarı kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b866-279">Firewall Rules Creation</span></span>
<span data-ttu-id="4b866-280">Bu örnekte kullanılan güvenlik duvarı kuralları üç tür vardır, hepsinin ayrı simgeler vardır:</span><span class="sxs-lookup"><span data-stu-id="4b866-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="4b866-281">Merhaba uygulama yeniden yönlendirme kuralı: ![uygulama yeniden yönlendirme simgesi][7]</span><span class="sxs-lookup"><span data-stu-id="4b866-281">hello Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="4b866-282">Merhaba hedef NAT kuralı: ![hedef NAT simgesi][8]</span><span class="sxs-lookup"><span data-stu-id="4b866-282">hello Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="4b866-283">Merhaba geçişi kuralı: ![geçirmek simgesi][9]</span><span class="sxs-lookup"><span data-stu-id="4b866-283">hello Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="4b866-284">Bu kural hakkında daha fazla bilgi hello Barracuda web sitesinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-284">More information on these rules can be found at hello Barracuda web site.</span></span>

<span data-ttu-id="4b866-285">toocreate kuralları aşağıdaki hello (veya var olan varsayılan kuralları doğrulayın), hello Barracuda NG yönetici istemci panodan başlatma, toohello yapılandırma sekmesine gidin, hello işletimsel yapılandırma bölümü Ruleset'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4b866-285">toocreate hello following rules (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="4b866-286">Bir kılavuz olarak adlandırılan, "Ana kuralları" Merhaba etkin ve devre dışı bırakılan kuralları bu Güvenlik Duvarı'nda mevcut gösterir.</span><span class="sxs-lookup"><span data-stu-id="4b866-286">A grid called, “Main Rules” will show hello existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="4b866-287">Merhaba sağ üst köşedeki bu kılavuz, küçük, yeşil olduğundan "+" düğmesini tıklatın, bu toocreate yeni bir kural tıklayın (Not: güvenlik duvarını "değişiklikleri kilitlenebilir", bir düğme "Kilit" olarak işaretlenmiş ve güncelleştirilemiyor toocreate olan veya kuralları düzenlemek, bu düğmeye tıkladığınızda görürseniz çok "kilidini" kural se hello t ve düzenlenmesine izin verilir).</span><span class="sxs-lookup"><span data-stu-id="4b866-287">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello rule set and allow editing).</span></span> <span data-ttu-id="4b866-288">Mevcut bir kuralı tooedit istiyorsanız, o kural seçin, sağ tıklayın ve kuralını Düzenle seçin.</span><span class="sxs-lookup"><span data-stu-id="4b866-288">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="4b866-289">Kurallarınızı oluşturulan ve/veya değiştirilmiş sonra olmalıdırlar gönderilen toohello Güvenlik Duvarı'nı ve etkinleştirildi, bu değişiklikler değil kazanacak hello kural yapılmazsa.</span><span class="sxs-lookup"><span data-stu-id="4b866-289">Once your rules are created and/or modified, they must be pushed toohello firewall and then activated, if this is not done hello rule changes will not take effect.</span></span> <span data-ttu-id="4b866-290">Merhaba itme ve etkinleştirme işlemi hello ayrıntıları kural açıklamaları açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4b866-290">hello push and activation process is described below hello details rule descriptions.</span></span>

<span data-ttu-id="4b866-291">Bu örnekte aşağıdaki gibi açıklanmıştır her kural gerekli toocomplete Hello özellikleri:</span><span class="sxs-lookup"><span data-stu-id="4b866-291">hello specifics of each rule required toocomplete this example are described as follows:</span></span>

* <span data-ttu-id="4b866-292">**Güvenlik Duvarı yönetimi kural**: Bu uygulama yeniden yönlendirme kuralı trafiği hello ağ sanal gereç, bu örnekte Barracuda NextGen Firewall toopass toohello yönetim bağlantı noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="4b866-292">**Firewall Management Rule**: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="4b866-293">801, 807 ve isteğe bağlı olarak 22 Hello yönetim bağlantı noktalarıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-293">hello management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="4b866-294">Merhaba iç ve dış bağlantı noktaları olan hello aynı (yani hiçbir bağlantı noktası çevirisi).</span><span class="sxs-lookup"><span data-stu-id="4b866-294">hello external and internal ports are hello same (i.e. no port translation).</span></span> <span data-ttu-id="4b866-295">Bu kural, Kurulum MGMT erişim, varsayılan bir kural ve varsayılan (olarak Barracuda NextGen Firewall sürüm 6.1) etkinleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="4b866-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="4b866-296">![Güvenlik Duvarı Yönetimi kuralı][10]</span><span class="sxs-lookup"><span data-stu-id="4b866-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="4b866-297">Merhaba bu kuralın kaynak adres alanında herhangi, hello yönetim IP adres aralıklarını bilinen, bu kapsamı azaltma ayrıca hello saldırı yüzeyini toohello yönetim bağlantı noktalarını azaltmak.</span><span class="sxs-lookup"><span data-stu-id="4b866-297">hello source address space in this rule is Any, if hello management IP address ranges are known, reducing this scope would also reduce hello attack surface toohello management ports.</span></span>
> 
> 

* <span data-ttu-id="4b866-298">**RDP kuralları**: Bu hedef NAT kuralları tek tek sunucular RDP aracılığıyla hello yönetimini izin.</span><span class="sxs-lookup"><span data-stu-id="4b866-298">**RDP Rules**:  These Destination NAT rules will allow management of hello individual servers via RDP.</span></span>
  <span data-ttu-id="4b866-299">Bu kural dört gereken kritik alanları toocreate vardır:</span><span class="sxs-lookup"><span data-stu-id="4b866-299">There are four critical fields needed toocreate this rule:</span></span>
  
  1. <span data-ttu-id="4b866-300">Kaynak – tooallow RDP yerden hello başvurusu "Any" Merhaba kaynak alanında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4b866-300">Source – tooallow RDP from anywhere, hello reference “Any” is used in hello Source field.</span></span>
  2. <span data-ttu-id="4b866-301">Merhaba dış bağlantı noktaları toohello sunucuları yerel IP adresi ve tooport 3386 (Merhaba varsayılan RDP bağlantı noktası) yeniden yönlendirme, hizmeti – uygun hizmeti nesnesi, bu durumda "AppVM01 RDP" daha önce oluşturduğunuz hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="4b866-301">Service – use hello appropriate Service Object created earlier, in this case “AppVM01 RDP”, hello external ports redirect toohello servers local IP address and tooport 3386 (hello default RDP port).</span></span> <span data-ttu-id="4b866-302">RDP erişim tooAppVM01 için bu belirli kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-302">This specific rule is for RDP access tooAppVM01.</span></span>
  3. <span data-ttu-id="4b866-303">Hedef – hello olmalıdır *hello Güvenlik Duvarı'nda yerel bağlantı noktası*, "DCHP 1 yerel IP" ya da statik IP kullanıyorsanız eth0.</span><span class="sxs-lookup"><span data-stu-id="4b866-303">Destination – should be hello *local port on hello firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="4b866-304">Başlangıç sıra numarası (eth0, eth1, vb.), ağ Gereci birden çok yerel arabirimi varsa, farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-304">hello ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="4b866-305">Bu hello bağlantı noktasıdır hello güvenlik duvarı göndermesinin (olabilir aynı bağlantı noktasını almayı hello hello), hello gerçek yönlendirilmiş hedefi olan hello hedef listesinin alanında.</span><span class="sxs-lookup"><span data-stu-id="4b866-305">This is hello port hello firewall is sending out from (may be hello same as hello receiving port), hello actual routed destination is in hello Target List field.</span></span>
  4. <span data-ttu-id="4b866-306">Yeniden yönlendirme – Bu bölümde tooultimately bu trafiği burada yeniden yönlendirme hello sanal gereç söyler.</span><span class="sxs-lookup"><span data-stu-id="4b866-306">Redirection – this section tells hello virtual appliance where tooultimately redirect this traffic.</span></span> <span data-ttu-id="4b866-307">Merhaba basit yeniden yönlendirme tooplace hello IP ve bağlantı noktası (isteğe bağlı) hello hedef liste alanda ' dir.</span><span class="sxs-lookup"><span data-stu-id="4b866-307">hello simplest redirection is tooplace hello IP and Port (optional) in hello Target List field.</span></span> <span data-ttu-id="4b866-308">Bağlantı noktası yok hello gelen istekte kullanılan hello hedef bağlantı noktası ise olacaktır (IE hiçbir çevirisi), bir bağlantı noktası başlangıç bağlantı noktası belirlendiyse kullanılan de NAT birlikte hello IP adresi olur.</span><span class="sxs-lookup"><span data-stu-id="4b866-308">If no port is used hello destination port on hello inbound request will be used (ie no translation), if a port is designated hello port will also be NAT’d along with hello IP address.</span></span>
     
     <span data-ttu-id="4b866-309">![Güvenlik Duvarı RDP kuralı][11]</span><span class="sxs-lookup"><span data-stu-id="4b866-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="4b866-310">Dört RDP kuralları toplam oluşturulan toobe gerekir:</span><span class="sxs-lookup"><span data-stu-id="4b866-310">A total of four RDP rules will need toobe created:</span></span> 
     
     | <span data-ttu-id="4b866-311">Kural Adı</span><span class="sxs-lookup"><span data-stu-id="4b866-311">Rule Name</span></span> | <span data-ttu-id="4b866-312">Sunucu</span><span class="sxs-lookup"><span data-stu-id="4b866-312">Server</span></span> | <span data-ttu-id="4b866-313">Hizmet</span><span class="sxs-lookup"><span data-stu-id="4b866-313">Service</span></span> | <span data-ttu-id="4b866-314">Hedef listesi</span><span class="sxs-lookup"><span data-stu-id="4b866-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="4b866-315">RDP IIS01</span><span class="sxs-lookup"><span data-stu-id="4b866-315">RDP-to-IIS01</span></span> |<span data-ttu-id="4b866-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="4b866-316">IIS01</span></span> |<span data-ttu-id="4b866-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="4b866-317">IIS01 RDP</span></span> |<span data-ttu-id="4b866-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="4b866-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="4b866-319">RDP DNS01</span><span class="sxs-lookup"><span data-stu-id="4b866-319">RDP-to-DNS01</span></span> |<span data-ttu-id="4b866-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="4b866-320">DNS01</span></span> |<span data-ttu-id="4b866-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="4b866-321">DNS01 RDP</span></span> |<span data-ttu-id="4b866-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="4b866-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="4b866-323">RDP AppVM01</span><span class="sxs-lookup"><span data-stu-id="4b866-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="4b866-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="4b866-324">AppVM01</span></span> |<span data-ttu-id="4b866-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="4b866-325">AppVM01 RDP</span></span> |<span data-ttu-id="4b866-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="4b866-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="4b866-327">RDP AppVM02</span><span class="sxs-lookup"><span data-stu-id="4b866-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="4b866-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="4b866-328">AppVM02</span></span> |<span data-ttu-id="4b866-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="4b866-329">AppVm02 RDP</span></span> |<span data-ttu-id="4b866-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="4b866-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="4b866-331">Merhaba kaynak Hello kapsamını ve hizmet alanları aşağı daraltma hello saldırı yüzeyini azaltır.</span><span class="sxs-lookup"><span data-stu-id="4b866-331">Narrowing down hello scope of hello Source and Service fields will reduce hello attack surface.</span></span> <span data-ttu-id="4b866-332">işlevselliği sağlayacak en sınırlı hello kapsam kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-332">hello most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="4b866-333">**Uygulama trafik kurallarını**: iki uygulama trafiği kuralları, hello hello ön uç web trafiği için ilk ve ikinci hello arka uç trafiği (örneğin web sunucusu toodata katmanı) için hello vardır.</span><span class="sxs-lookup"><span data-stu-id="4b866-333">**Application Traffic Rules**: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="4b866-334">Bu kurallar hello ağ mimarisi (sunucularınızı yerleştirildiği) ve (hangi yönde hello trafik akışlarının ve hangi bağlantı noktalarının kullanılacağını) trafiği akışı değişir.</span><span class="sxs-lookup"><span data-stu-id="4b866-334">These rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="4b866-335">Önce ele alınan hello ön uç web trafiği için kuraldır:</span><span class="sxs-lookup"><span data-stu-id="4b866-335">First discussed is hello front end rule for web traffic:</span></span>
  
    <span data-ttu-id="4b866-336">![Güvenlik Duvarı Web kuralı][12]</span><span class="sxs-lookup"><span data-stu-id="4b866-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="4b866-337">Bu hedef NAT kuralı hello gerçek uygulama trafiği tooreach hello uygulama sunucusu sağlar.</span><span class="sxs-lookup"><span data-stu-id="4b866-337">This Destination NAT rule allows hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="4b866-338">Merhaba diğer kurallar izin verirken, güvenlik, yönetim, vb. için uygulama ne hello uygulamaları dış kullanıcı ve hizmet tooaccess izin kurallardır.</span><span class="sxs-lookup"><span data-stu-id="4b866-338">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="4b866-339">Bu örnek için bağlantı noktası 80 üzerinde bir tek bir web sunucusu olduğundan, böylece hello tek uygulama güvenlik duvarını gelen trafiği toohello dış IP, toohello web sunucuları iç IP adresi yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-339">For this example, there is a single web server on port 80, thus hello single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span>
  
    <span data-ttu-id="4b866-340">**Not**: hello hedef listesi alanına atanan bağlantı noktası yok, bu nedenle hello gelen bağlantı noktası 80 (veya hello seçili hizmet için 443'tür) hello web sunucusu hello yönlendirilmesini kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="4b866-340">**Note**: that there is no port assigned in hello Target List field, thus hello inbound port 80 (or 443 for hello Service selected) will be used in hello redirection of hello web server.</span></span> <span data-ttu-id="4b866-341">Merhaba web sunucusunun farklı bir bağlantı noktasında dinleme, örneğin 8080 bağlantı noktası, hello hedef listesi alan güncelleştirilmiş too10.0.1.4:8080 tooallow hello bağlantı noktası yeniden yönlendirmesi için de olabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-341">If hello web server is listening on a different port, for example port 8080, hello Target List field could be updated too10.0.1.4:8080 tooallow for hello Port redirection as well.</span></span>
  
    <span data-ttu-id="4b866-342">sonraki uygulama trafik kuralı hello herhangi bir hizmeti arka uç kural tooallow hello Web sunucusu tootalk toohello AppVM01 sunucu (ancak değil AppVM02) hello:</span><span class="sxs-lookup"><span data-stu-id="4b866-342">hello next Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="4b866-343">![Güvenlik Duvarı AppVM01 kuralı][13]</span><span class="sxs-lookup"><span data-stu-id="4b866-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="4b866-344">Bu geçiş kuralı hello web uygulama tarafından gerek duyulan tüm Protokolü tooaccess verileri kullanarak tüm IIS sunucusunda hello ön uç alt tooreach hello AppVM01 (IP adresi 10.0.2.5) herhangi bir bağlantı noktasında verir.</span><span class="sxs-lookup"><span data-stu-id="4b866-344">This Pass rule allows any IIS server on hello Frontend subnet tooreach hello AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol tooaccess data needed by hello web application.</span></span>
  
    <span data-ttu-id="4b866-345">Bu ekran görüntüsü, bir "\<taşınmaya açık\>" Merhaba hedef alan toosignify 10.0.2.5 hello hedef olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4b866-345">In this screen shot an "\<explicit-dest\>" is used in hello Destination field toosignify 10.0.2.5 as hello destination.</span></span> <span data-ttu-id="4b866-346">Bu şunlardan biri olabilir gösterildiği gibi veya açık adlı ağ (Merhaba DNS sunucusu hello önkoşulları içinde'da yapıldığı gibi) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4b866-346">This could be either explicit as shown or a named Network Object (as was done in hello prerequisites for hello DNS server).</span></span> <span data-ttu-id="4b866-347">Toowhich yöntemi kullanılacağından bu toohello hello Güvenlik Duvarı'nın yöneticisidir.</span><span class="sxs-lookup"><span data-stu-id="4b866-347">This is up toohello administrator of hello firewall as toowhich method will be used.</span></span> <span data-ttu-id="4b866-348">tooadd Explict Desitnation olarak 10.0.2.5 çift hello ilk boş satır altında \<taşınmaya açık\> ve açılır hello penceresinde hello adresini girin.</span><span class="sxs-lookup"><span data-stu-id="4b866-348">tooadd 10.0.2.5 as an Explict Desitnation, double-click on hello first blank row under \<explicit-dest\> and enter hello address in hello window that pops up.</span></span>
  
    <span data-ttu-id="4b866-349">Böylece Hello bağlantı yöntemini çok ayarlayabilirsiniz bu dahili trafiği olduğundan geçirmek bu kural, NAT gerekli "No SNAT".</span><span class="sxs-lookup"><span data-stu-id="4b866-349">With this Pass Rule, no NAT is needed since this is internal traffic, so hello Connection Method can be set too"No SNAT".</span></span>
  
    <span data-ttu-id="4b866-350">**Not**: hello kaynak bu kuralda ağdır hello FrontEnd alt ağı üzerinde herhangi bir kaynak yalnızca olacaktır bir veya daha belirli toothose tam IP adreslerinin yerine web sunucuları, kaynak olabilir bir ağ nesnesi bilinen belirli sayıda oluşturduysanız toobe ön uç alt ağın tamamını Hello.</span><span class="sxs-lookup"><span data-stu-id="4b866-350">**Note**: hello Source network in this rule is any resource on hello FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created toobe more specific toothose exact IP addresses instead of hello entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="4b866-351">Bu kural "Tüm" toomake örnek uygulama daha kolay toosetup hello ve kullanmak hello hizmeti kullanıyorsa, bu da Icmpv4 izin verir (ping) tek bir kural.</span><span class="sxs-lookup"><span data-stu-id="4b866-351">This rule uses hello service “Any” toomake hello sample application easier toosetup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="4b866-352">Ancak, önerilen bir uygulama değildir.</span><span class="sxs-lookup"><span data-stu-id="4b866-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="4b866-353">Merhaba bağlantı noktalarını ve protokolleri ("Hizmetler") bu sınırından uygulama işlemi tooreduce hello saldırı yüzeyini veren daraltılmış toohello minimum mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b866-353">hello ports and protocols (“Services”) should be narrowed toohello minimum possible that allows application operation tooreduce hello attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="4b866-354">Bu kural kullanılan bir hedef açık başvuru gösterir, ancak hello güvenlik duvarı yapılandırmasını tutarlı bir yaklaşım kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout hello firewall configuration.</span></span> <span data-ttu-id="4b866-355">Ağ nesnesi adlı bu hello kullanılabilir boyunca daha kolay okunabilir olması ve desteklenebilirlik için önerilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-355">It is recommended that hello named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="4b866-356">Merhaba açık taşınmaya kullanılan burada yalnızca tooshow bir alternatif başvuru yöntemidir ve (özellikle karmaşık yapılandırmalar için) genellikle önerilmez.</span><span class="sxs-lookup"><span data-stu-id="4b866-356">hello explicit-dest is used here only tooshow an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="4b866-357">**Giden tooInternet kural**: Bu geçirmek kuralı izin ver hiçbir kaynak ağ toopass toohello seçili hedef ağ trafiği.</span><span class="sxs-lookup"><span data-stu-id="4b866-357">**Outbound tooInternet Rule**: This Pass rule will allow traffic from any Source network toopass toohello selected Destination networks.</span></span> <span data-ttu-id="4b866-358">Bu kural hello Barracuda NextGen Güvenlik Duvarı'nda genellikle zaten varsayılan kural, ancak devre dışı durumda.</span><span class="sxs-lookup"><span data-stu-id="4b866-358">This rule is a default rule usually already on hello Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="4b866-359">Bu kurala sağ hello etkinleştirme kural komutu erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b866-359">Right-clicking on this rule can access hello Activate Rule command.</span></span> <span data-ttu-id="4b866-360">Burada gösterilen hello kural hello önkoşul bölüm bu kural, bu belge toohello kaynak özniteliğinin başvurular olarak oluşturulan değiştirilmiş tooadd hello iki yerel alt ağları olmuştur.</span><span class="sxs-lookup"><span data-stu-id="4b866-360">hello rule shown here has been modified tooadd hello two local subnets that were created as references in hello prerequisite section of this document toohello Source attribute of this rule.</span></span>
  
    <span data-ttu-id="4b866-361">![Giden güvenlik duvarı kuralı][14]</span><span class="sxs-lookup"><span data-stu-id="4b866-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="4b866-362">**DNS kuralı**: Bu geçirmek kural yalnızca DNS (bağlantı noktası 53) trafiği toopass toohello DNS sunucusu izin verir.</span><span class="sxs-lookup"><span data-stu-id="4b866-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="4b866-363">Bu kural, hello ön uç toohello arka uç çoğu trafiğinden engellenen bu ortam için DNS özellikle sağlar.</span><span class="sxs-lookup"><span data-stu-id="4b866-363">For this environment most traffic from hello FrontEnd toohello BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="4b866-364">![Güvenlik Duvarı DNS kuralı][15]</span><span class="sxs-lookup"><span data-stu-id="4b866-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="4b866-365">**Not**: Bu ekran görüntüsü hello bağlantı yöntemini bulunur.</span><span class="sxs-lookup"><span data-stu-id="4b866-365">**Note**: In this screen shot hello Connection Method is included.</span></span> <span data-ttu-id="4b866-366">Bu kural iç IP toointernal IP adresi trafiği için olduğundan, hiçbir NATing gerekli değildir, bu hello bağlantı yönteminin çok ayarlandığını bu geçişi kuralı için "Hayır SNAT".</span><span class="sxs-lookup"><span data-stu-id="4b866-366">Because this rule is for internal IP toointernal IP address traffic, no NATing is required, this hello Connection Method is set too“No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="4b866-367">**Alt ağ tooSubnet kural**: Bu geçirmek etkinleştirildi varsayılan bir kural kuralıdır ve herhangi bir sunucuya geri hello uç alt tooconnect tooany sunucusu üzerinde değiştirilmiş tooallow hello ön uç alt.</span><span class="sxs-lookup"><span data-stu-id="4b866-367">**Subnet tooSubnet Rule**: This Pass rule is a default rule that has been activated and modified tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet.</span></span> <span data-ttu-id="4b866-368">Bu kural tüm iç trafiği olduğundan Hello bağlantı yöntemini tooNo SNAT ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-368">This rule is all internal traffic so hello Connection Method can be set tooNo SNAT.</span></span>
  
    <span data-ttu-id="4b866-369">![Güvenlik Duvarı içi sanal ağ kuralı][16]</span><span class="sxs-lookup"><span data-stu-id="4b866-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="4b866-370">**Not**: hello çift yönlü onay kutusu işaretli (veya, çoğu kurallarında işaretli değil), bu "tek yönlü" kural sağlar, bu kural için önemli budur, bir bağlantı hello arka uç alt toohello ön uç ağ üzerinden başlatılabilir ancak ters hello değil.</span><span class="sxs-lookup"><span data-stu-id="4b866-370">**Note**: hello Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from hello back end subnet toohello front end network, but not hello reverse.</span></span> <span data-ttu-id="4b866-371">Bu onay kutusu işaretli değilse bu kural bizim mantıksal diyagramdan istenmediği çift yönlü trafiği etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="4b866-372">**Reddetme tüm trafik kuralı**: Bu her zaman son bir kural hello (bakımından öncelik) olmalıdır ve trafik başarısız toomatch kuralları önceki hello hiçbirini akışlar, bu nedenle, bu kural tarafından düşürülür.</span><span class="sxs-lookup"><span data-stu-id="4b866-372">**Deny All Traffic Rule**: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="4b866-373">Bu varsayılan bir kural ve genellikle etkin, değişikliğe genellikle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4b866-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="4b866-374">![Güvenlik duvarı kuralı Reddet][17]</span><span class="sxs-lookup"><span data-stu-id="4b866-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b866-375">Tüm kuralları yukarıda hello oluşturulduktan sonra tooreview hello her kural tooensure trafiğin önceliğini izin verilen veya istendiği gibi reddedilen önemlidir.</span><span class="sxs-lookup"><span data-stu-id="4b866-375">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="4b866-376">Bu örnekte, hello hello hello Barracuda Management istemcisi kurallarında iletme, ana kılavuz görüntülenmelidir hello sırayla kurallardır.</span><span class="sxs-lookup"><span data-stu-id="4b866-376">For this example, hello rules are in hello order they should appear in hello Main Grid of forwarding rules in hello Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="4b866-377">Kural etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4b866-377">Rule Activation</span></span>
<span data-ttu-id="4b866-378">Merhaba değiştiren ruleset toohello belirtimiyle hello mantığı diyagramı, hello ruleset olmalıdır toohello Güvenlik Duvarı'nı karşıya ve ardından etkinleştirildi.</span><span class="sxs-lookup"><span data-stu-id="4b866-378">With hello ruleset modified toohello specification of hello logic diagram, hello ruleset must be uploaded toohello firewall and then activated.</span></span>

<span data-ttu-id="4b866-379">![Güvenlik duvarı kuralını etkinleştirme][18]</span><span class="sxs-lookup"><span data-stu-id="4b866-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="4b866-380">Merhaba üst sağ köşesinde hello management istemcisi düğmeleri oluşan bir küme var.</span><span class="sxs-lookup"><span data-stu-id="4b866-380">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="4b866-381">Merhaba "değişiklikleri" Gönder düğmesi toosend değiştiren hello kuralları toohello güvenlik duvarı, ardından hello "Etkinleştir" düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4b866-381">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="4b866-382">Merhaba güvenlik duvarı ruleset Hello etkinleştirme ile bu örnek ortamı yapı tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="4b866-382">With hello activation of hello firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="4b866-383">Trafik senaryoları</span><span class="sxs-lookup"><span data-stu-id="4b866-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4b866-384">Bir anahtar takeway tooremember olduğundan, **tüm** trafiği hello güvenlik duvarı üzerinden gelen.</span><span class="sxs-lookup"><span data-stu-id="4b866-384">A key takeway is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="4b866-385">Bunu tooremote Masaüstü toohello IIS01 sunucu, onu hello ön uç bulut hizmeti ve hello ön uç alt tooaccess tooRDP toohello güvenlik duvarı üzerinde ihtiyacımız bu sunucu olsa bile 8014 bağlantı noktası ve hello güvenlik duvarı tooroute hello RDP isteği dahili izin toohello IIS01 RDP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="4b866-385">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="4b866-386">Merhaba "Azure portal'ın Bağlan düğmesini olduğu için hiçbir doğrudan RDP yolu tooIIS01 (Merhaba portal görebilirsiniz uzaklığa kadar) çalışmaz".</span><span class="sxs-lookup"><span data-stu-id="4b866-386">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="4b866-387">Tüm bağlantılar yani hello Internet toohello güvenlik hizmeti ve bir bağlantı noktası, örneğin secscv001.cloudapp.net:xxxx olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4b866-387">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="4b866-388">Bu senaryolarda, güvenlik duvarı kuralları aşağıdaki hello yerinde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="4b866-388">For these scenarios, hello following firewall rules should be in place:</span></span>

1. <span data-ttu-id="4b866-389">Güvenlik Duvarı Yönetimi</span><span class="sxs-lookup"><span data-stu-id="4b866-389">Firewall Management</span></span>
2. <span data-ttu-id="4b866-390">RDP tooIIS01</span><span class="sxs-lookup"><span data-stu-id="4b866-390">RDP tooIIS01</span></span>
3. <span data-ttu-id="4b866-391">RDP tooDNS01</span><span class="sxs-lookup"><span data-stu-id="4b866-391">RDP tooDNS01</span></span>
4. <span data-ttu-id="4b866-392">RDP tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="4b866-392">RDP tooAppVM01</span></span>
5. <span data-ttu-id="4b866-393">RDP tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="4b866-393">RDP tooAppVM02</span></span>
6. <span data-ttu-id="4b866-394">Web uygulaması trafiği toohello</span><span class="sxs-lookup"><span data-stu-id="4b866-394">App Traffic toohello Web</span></span>
7. <span data-ttu-id="4b866-395">Uygulama trafiği tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="4b866-395">App Traffic tooAppVM01</span></span>
8. <span data-ttu-id="4b866-396">Giden toohello Internet</span><span class="sxs-lookup"><span data-stu-id="4b866-396">Outbound toohello Internet</span></span>
9. <span data-ttu-id="4b866-397">Ön uç tooDNS01</span><span class="sxs-lookup"><span data-stu-id="4b866-397">Frontend tooDNS01</span></span>
10. <span data-ttu-id="4b866-398">İçi alt ağ trafiği (yalnızca arka uç toofront ucu)</span><span class="sxs-lookup"><span data-stu-id="4b866-398">Intra-Subnet Traffic (back end toofront end only)</span></span>
11. <span data-ttu-id="4b866-399">Tümünü Reddet</span><span class="sxs-lookup"><span data-stu-id="4b866-399">Deny All</span></span>

<span data-ttu-id="4b866-400">Hello gerçek güvenlik duvarı ruleset, büyük olasılıkla başka birçok kurala toplama toothese vardır, olanları burada listelenen hello daha hello kurallarında belirtilen herhangi bir güvenlik duvarını ayrıca farklı öncelik numaraları gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b866-400">hello actual firewall ruleset will most likely have many other rules in addition toothese, hello rules on any given firewall will also have different priority numbers than hello ones listed here.</span></span> <span data-ttu-id="4b866-401">Bu liste ve ilişkili numaralar yalnızca bu on kurallar ve bunları arasında hello göreli öncelik arasında tooprovide ilgi markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-401">This list and associated numbers are tooprovide relevance between just these eleven rules and hello relative priority amongst them.</span></span> <span data-ttu-id="4b866-402">Diğer bir deyişle; Merhaba gerçek Güvenlik Duvarı'nı, kural numarası 5 olabilir, ancak hello "Güvenlik duvarı Yönetimi" kural altında ve bu listeyi hello amacı ile hizalamaya hello "RDP tooDNS01" kural üstünde olduğu sürece hello "RDP tooIIS01" olabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-402">In other words; on hello actual firewall, hello “RDP tooIIS01” may be rule number 5, but as long as it’s below hello “Firewall Management” rule and above hello “RDP tooDNS01” rule it would align with hello intention of this list.</span></span> <span data-ttu-id="4b866-403">Başlangıç listesi, büyük bir de kısaltma izin vererek senaryolar aşağıda hello yardımcı olur; Örneğin "FW kuralı 9 (DNS)".</span><span class="sxs-lookup"><span data-stu-id="4b866-403">hello list will also aid in hello below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="4b866-404">Ayrıca okumanızdır dört RDP kuralları topluca olacaktır hello olarak adlandırılan, "RDP kuralları hello" Merhaba trafik senaryo ilgisiz tooRDP olduğunda.</span><span class="sxs-lookup"><span data-stu-id="4b866-404">Also for brevity, hello four RDP rules will be collectively called, “hello RDP rules” when hello traffic scenario is unrelated tooRDP.</span></span>

<span data-ttu-id="4b866-405">Ağ güvenlik grupları yerinde gelen Internet trafiği hello ön uç ve arka uç alt ağları olduğunu da geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="4b866-405">Also recall that Network Security Groups are in-place for inbound internet traffic on hello Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="4b866-406">(İzin verilir) Internet tooWeb sunucu</span><span class="sxs-lookup"><span data-stu-id="4b866-406">(Allowed) Internet tooWeb Server</span></span>
1. <span data-ttu-id="4b866-407">Internet kullanıcı istekleri HTTP sayfasına SecSvc001.CloudApp.Net (Internet'e yönelik bulut hizmeti)</span><span class="sxs-lookup"><span data-stu-id="4b866-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="4b866-408">Bulut hizmeti geçiş trafiği 80 numaralı bağlantı noktasını toofirewall arabirimde 10.0.0.4:80 açık uç noktası aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="4b866-408">Cloud service passes traffic through open endpoint on port 80 toofirewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="4b866-409">Sistem NSG kuralları trafiği toofirewall izin verecek şekilde tooSecurity alt ağ, hiçbir NSG atanan</span><span class="sxs-lookup"><span data-stu-id="4b866-409">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="4b866-410">Merhaba Güvenlik Duvarı (10.0.1.4) iç IP adresi trafik isabetler</span><span class="sxs-lookup"><span data-stu-id="4b866-410">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="4b866-411">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="4b866-412">FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-412">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="4b866-413">FW kuralları 2-5 (RDP kurallar) yok, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="4b866-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="4b866-414">FW kural 6 (uygulama: Web) uygulama trafiğine izin verilir, güvenlik duvarı NAT onu too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="4b866-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it too10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="4b866-415">Merhaba ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-415">hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4b866-416">Olmayan NSG kural 1'i (blok Internet) uygulama (Bu trafiği NAT edildi hello güvenlik duvarı tarafından gerekir, böylece hello kaynak adresi şimdi hello güvenlik alt ağ üzerinde olan hello güvenlik duvarı ve hello ön uç alt ağa göre NSG toobe "yerel" trafik görülen ve böylece izin verilir), toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="4b866-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Frontend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="4b866-417">Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="4b866-417">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="4b866-418">IIS01 web trafiği için dinleme, bu isteği alır ve hello isteği işlemeye başlıyor</span><span class="sxs-lookup"><span data-stu-id="4b866-418">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
8. <span data-ttu-id="4b866-419">Arka uç alt ağdaki bir FTP oturumunun tooAppVM01 tooinitiates IIS01 çalışır</span><span class="sxs-lookup"><span data-stu-id="4b866-419">IIS01 attempts tooinitiates an FTP session tooAppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="4b866-420">ön uç alt ağdaki Hello UDR rota hello güvenlik duvarı hello sonraki atlama yapar</span><span class="sxs-lookup"><span data-stu-id="4b866-420">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
10. <span data-ttu-id="4b866-421">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="4b866-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="4b866-422">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="4b866-423">FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-423">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="4b866-424">FW kuralı 2-5 (RDP kurallar) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="4b866-425">FW kural 6 (uygulama: Web) uygulamak için değil, toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="4b866-425">FW Rule 6 (App: Web) doesn’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="4b866-426">FW kural 7 ' (uygulama: arka uç) uygulama trafiğine izin verilir, güvenlik duvarı iletir trafiği too10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="4b866-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic too10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="4b866-427">Merhaba arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-427">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="4b866-428">NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-428">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="4b866-429">Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="4b866-429">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="4b866-430">AppVM01 hello isteği alır ve hello oturumu başlatır ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="4b866-430">AppVM01 receives hello request and initiates hello session and responds</span></span>
14. <span data-ttu-id="4b866-431">arka uç alt ağdaki Hello UDR rota hello güvenlik duvarı hello sonraki atlama yapar</span><span class="sxs-lookup"><span data-stu-id="4b866-431">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
15. <span data-ttu-id="4b866-432">Olduğundan giden hiçbir NSG kuralları hello arka uç alt hello yanıt üzerinde izin verilir</span><span class="sxs-lookup"><span data-stu-id="4b866-432">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
16. <span data-ttu-id="4b866-433">Bu trafik üzerinde döndürüyor çünkü kurulan oturum hello güvenlik duvarı hello yanıt geri toohello web sunucusu (IIS01) geçirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-433">Because this is returning traffic on an established session hello firewall passes hello response back toohello web server (IIS01)</span></span>
17. <span data-ttu-id="4b866-434">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="4b866-435">NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-435">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="4b866-436">Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="4b866-436">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="4b866-437">Hello IIS sunucusu hello yanıtı alır, AppVM01 hello işlemle tamamlar ve yapı hello HTTP yanıtı tamamlandıktan, toohello istek sahibi gönderilen bu HTTP yanıtı</span><span class="sxs-lookup"><span data-stu-id="4b866-437">hello IIS server receives hello response, completes hello transaction with AppVM01, and then completes building hello HTTP response, this HTTP response is sent toohello requestor</span></span>
19. <span data-ttu-id="4b866-438">Olduğundan giden hiçbir NSG kuralları hello ön uç alt hello yanıt üzerinde izin verilir</span><span class="sxs-lookup"><span data-stu-id="4b866-438">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
20. <span data-ttu-id="4b866-439">HTTP yanıt isabet hello güvenlik duvarı hello ve bu hello yanıt tooan kurulmuş olduğundan NAT oturum hello güvenlik duvarı tarafından kabul edilir</span><span class="sxs-lookup"><span data-stu-id="4b866-439">hello HTTP response hits hello firewall, and because this is hello response tooan established NAT session is accepted by hello firewall</span></span>
21. <span data-ttu-id="4b866-440">Merhaba güvenlik duvarı hello yanıt geri toohello Internet kullanıcı ardından yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-440">hello firewall then redirects hello response back toohello Internet User</span></span>
22. <span data-ttu-id="4b866-441">Hiçbir giden NSG kuralları veya UDR atlama olduğundan hello ön uç alt ağda hello yanıt izin verilir ve hello web sayfasının hello Internet kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="4b866-441">Since there are no outbound NSG rules or UDR hops on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-internet-rdp-toobackend"></a><span data-ttu-id="4b866-442">(İzin verilir) Internet RDP tooBackend</span><span class="sxs-lookup"><span data-stu-id="4b866-442">(Allowed) Internet RDP tooBackend</span></span>
1. <span data-ttu-id="4b866-443">Sunucu Yöneticisi Internet üzerinde RDP oturumu tooAppVM01 8025 hello "RDP tooAppVM01" güvenlik duvarı kuralı için hello kullanıcıya atanan bağlantı noktası numarası olduğu SecSvc001.CloudApp.Net:8025 aracılığıyla istekleri</span><span class="sxs-lookup"><span data-stu-id="4b866-443">Server Admin on internet requests RDP session tooAppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is hello user assigned port number for hello “RDP tooAppVM01” firewall rule</span></span>
2. <span data-ttu-id="4b866-444">Hello bulut hizmeti, bağlantı noktası 8025 toofirewall 10.0.0.4:8025 arabirimde üzerinde hello açık uç noktası üzerinden trafiğe geçirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-444">hello cloud service passes traffic through hello open endpoint on port 8025 toofirewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="4b866-445">Sistem NSG kuralları trafiği toofirewall izin verecek şekilde tooSecurity alt ağ, hiçbir NSG atanan</span><span class="sxs-lookup"><span data-stu-id="4b866-445">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="4b866-446">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="4b866-447">FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-447">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="4b866-448">FW Kural 2 (RDP IIS) için geçerli değildir, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-448">FW Rule 2 (RDP IIS) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="4b866-449">FW kuralı 3 (RDP DNS01) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="4b866-449">FW Rule 3 (RDP DNS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="4b866-450">FW kuralı 4 (RDP AppVM01) uygulamak için trafik verilir, güvenlik duvarı NAT onu too10.0.2.5:3386 (AppVM01 üzerinde RDP noktasına)</span><span class="sxs-lookup"><span data-stu-id="4b866-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it too10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="4b866-451">Merhaba arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-451">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4b866-452">Olmayan NSG kural 1'i (blok Internet) uygulama (Bu trafiği NAT edildi hello güvenlik duvarı tarafından gerekir, böylece hello kaynak adresi şimdi hello güvenlik alt ağ üzerinde olan hello güvenlik duvarı ve hello arka uç alt ağa göre NSG toobe "yerel" trafik görülen ve böylece izin verilir), toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="4b866-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Backend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="4b866-453">Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="4b866-453">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="4b866-454">AppVM01 RDP trafiği için dinleme ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="4b866-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="4b866-455">Giden hiçbir NSG kuralları, varsayılan kuralları uygula ve dönüş trafiğine izin verilir</span><span class="sxs-lookup"><span data-stu-id="4b866-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="4b866-456">UDR giden trafiği toohello güvenlik duvarı hello sonraki atlama olarak yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-456">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
9. <span data-ttu-id="4b866-457">Bu trafik üzerinde döndürüyor çünkü kurulan oturum hello güvenlik duvarı hello yanıt geri toohello Internet kullanıcı geçirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-457">Because this is returning traffic on an established session hello firewall passes hello response back toohello internet user</span></span>
10. <span data-ttu-id="4b866-458">RDP oturumu etkin</span><span class="sxs-lookup"><span data-stu-id="4b866-458">RDP session is enabled</span></span>
11. <span data-ttu-id="4b866-459">Kullanıcı adı ve parolasını AppVM01 ister</span><span class="sxs-lookup"><span data-stu-id="4b866-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="4b866-460">(İzin verilir) DNS sunucusundaki Web sunucusu DNS araması</span><span class="sxs-lookup"><span data-stu-id="4b866-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="4b866-461">Sunucu, IIS01, gereksinimlerini www.data.gov bir veri akışı web ancak tooresolve adresi hello.</span><span class="sxs-lookup"><span data-stu-id="4b866-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="4b866-462">Merhaba ağ yapılandırma hello VNet listeleri DNS01 (10.0.2.4 hello arka uç alt ağdaki) hello birincil DNS sunucusu olarak, IIS01 hello DNS isteği tooDNS01 gönderir</span><span class="sxs-lookup"><span data-stu-id="4b866-462">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="4b866-463">UDR giden trafiği toohello güvenlik duvarı hello sonraki atlama olarak yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-463">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
4. <span data-ttu-id="4b866-464">Giden hiçbir NSG kuralları ilişkili toohello Frontend alt ağı olan, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="4b866-464">No outbound NSG rules are bound toohello Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="4b866-465">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="4b866-466">FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-466">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="4b866-467">FW kuralı 2-5 (RDP kurallar) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="4b866-468">FW kuralları 6 ve 7 (uygulama kuralları) uygulama, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-468">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="4b866-469">FW kural 8 (tooInternet) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="4b866-469">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="4b866-470">FW kural 9 (DNS) geçerli, trafiğe izin verilir, güvenlik duvarı trafiği too10.0.2.4 (DNS01) iletir</span><span class="sxs-lookup"><span data-stu-id="4b866-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic too10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="4b866-471">Merhaba arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-471">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4b866-472">NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-472">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="4b866-473">Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="4b866-473">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="4b866-474">DNS sunucusu hello isteği alır</span><span class="sxs-lookup"><span data-stu-id="4b866-474">DNS server receives hello request</span></span>
8. <span data-ttu-id="4b866-475">DNS sunucusu önbelleğe hello adresi yoksa ve bir kök DNS sunucusu üzerinde hello ister Internet</span><span class="sxs-lookup"><span data-stu-id="4b866-475">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
9. <span data-ttu-id="4b866-476">UDR giden trafiği toohello güvenlik duvarı hello sonraki atlama olarak yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4b866-476">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
10. <span data-ttu-id="4b866-477">Giden hiçbir NSG kuralları arka uç alt ağdaki trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="4b866-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="4b866-478">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="4b866-479">FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-479">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="4b866-480">FW kuralı 2-5 (RDP kurallar) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="4b866-481">FW kuralları 6 ve 7 (uygulama kuralları) uygulama, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-481">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="4b866-482">FW kural 8 (tooInternet) geçerli, trafiğe izin verilir, oturum SNAT hello Internet DNS sunucusunda tooroot çıkışı</span><span class="sxs-lookup"><span data-stu-id="4b866-482">FW Rule 8 (tooInternet) does apply, traffic is allowed, session is SNAT out tooroot DNS server on hello Internet</span></span>
12. <span data-ttu-id="4b866-483">Bu oturumda hello Güvenlik Duvarı'ndan başlatılan olduğundan, Internet DNS sunucusu yanıt, hello yanıt hello güvenlik duvarı tarafından kabul edilir</span><span class="sxs-lookup"><span data-stu-id="4b866-483">Internet DNS server responds, since this session was initiated from hello firewall, hello response is accepted by hello firewall</span></span>
13. <span data-ttu-id="4b866-484">Yerleşik bir oturum olarak hello güvenlik duvarı sunucusu, DNS01 başlatma hello yanıt toohello iletir.</span><span class="sxs-lookup"><span data-stu-id="4b866-484">As this is an established session, hello firewall forwards hello response toohello initiating server, DNS01</span></span>
14. <span data-ttu-id="4b866-485">Merhaba arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-485">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="4b866-486">NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-486">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="4b866-487">Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="4b866-487">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="4b866-488">Merhaba DNS sunucusu ve hello yanıtı önbelleğe alır ve toohello ilk isteği geri tooIIS01 yanıt verir</span><span class="sxs-lookup"><span data-stu-id="4b866-488">hello DNS server receives and caches hello response, and then responds toohello initial request back tooIIS01</span></span>
16. <span data-ttu-id="4b866-489">arka uç alt ağdaki Hello UDR rota hello güvenlik duvarı hello sonraki atlama yapar</span><span class="sxs-lookup"><span data-stu-id="4b866-489">hello UDR route on backend subnet makes hello firewall hello next hop</span></span>
17. <span data-ttu-id="4b866-490">Giden hiçbir NSG kuralları hello arka uç alt ağda var, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="4b866-490">No outbound NSG rules exist on hello Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="4b866-491">Bu yerleşik bir oturum hello Güvenlik Duvarı'nda, hello yanıt hello Güvenlik Duvarı'nı geri toohello IIS sunucu tarafından iletilen</span><span class="sxs-lookup"><span data-stu-id="4b866-491">This is an established session on hello firewall, hello response is forwarded by hello firewall back toohello IIS server</span></span>
19. <span data-ttu-id="4b866-492">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="4b866-493">Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok</span><span class="sxs-lookup"><span data-stu-id="4b866-493">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="4b866-494">Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır</span><span class="sxs-lookup"><span data-stu-id="4b866-494">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
20. <span data-ttu-id="4b866-495">IIS01 hello yanıt DNS01 alır.</span><span class="sxs-lookup"><span data-stu-id="4b866-495">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-backend-server-toofrontend-server"></a><span data-ttu-id="4b866-496">(İzin verilir) Arka uç sunucusu tooFrontend</span><span class="sxs-lookup"><span data-stu-id="4b866-496">(Allowed) Backend server tooFrontend server</span></span>
1. <span data-ttu-id="4b866-497">Windows dosya Gezgini üzerinden hello IIS01 sunucu doğrudan bir dosya tooAppVM02 RDP aracılığıyla oturum açmış bir yönetici istekleri</span><span class="sxs-lookup"><span data-stu-id="4b866-497">An administrator logged on tooAppVM02 via RDP requests a file directly from hello IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="4b866-498">arka uç alt ağdaki Hello UDR rota hello güvenlik duvarı hello sonraki atlama yapar</span><span class="sxs-lookup"><span data-stu-id="4b866-498">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
3. <span data-ttu-id="4b866-499">Olduğundan giden hiçbir NSG kuralları hello arka uç alt hello yanıt üzerinde izin verilir</span><span class="sxs-lookup"><span data-stu-id="4b866-499">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
4. <span data-ttu-id="4b866-500">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="4b866-501">FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-501">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="4b866-502">FW kuralı 2-5 (RDP kurallar) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="4b866-503">FW kuralları 6 ve 7 (uygulama kuralları) uygulama, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-503">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="4b866-504">FW kural 8 (tooInternet) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="4b866-504">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="4b866-505">FW kural 9 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-505">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="4b866-506">FW kural 10 (içi alt ağ) geçerli, trafiğe izin verilir, güvenlik duvarı trafiği too10.0.1.4 (IIS01) geçirir</span><span class="sxs-lookup"><span data-stu-id="4b866-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic too10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="4b866-507">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4b866-508">NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-508">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="4b866-509">Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="4b866-509">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="4b866-510">Uygun kimlik doğrulama ve yetkilendirme varsayıldığında, IIS01 hello isteği kabul eder ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="4b866-510">Assuming proper authentication and authorization, IIS01 accepts hello request and responds</span></span>
7. <span data-ttu-id="4b866-511">ön uç alt ağdaki Hello UDR rota hello güvenlik duvarı hello sonraki atlama yapar</span><span class="sxs-lookup"><span data-stu-id="4b866-511">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
8. <span data-ttu-id="4b866-512">Olduğundan giden hiçbir NSG kuralları hello ön uç alt hello yanıt üzerinde izin verilir</span><span class="sxs-lookup"><span data-stu-id="4b866-512">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
9. <span data-ttu-id="4b866-513">Bu hello Güvenlik Duvarı'nda var olan bir oturum olarak bu yanıt izin verilir ve hello güvenlik duvarı hello yanıt tooAppVM02 döndürür</span><span class="sxs-lookup"><span data-stu-id="4b866-513">As this is an existing session on hello firewall this response is allowed and hello firewall returns hello response tooAppVM02</span></span>
10. <span data-ttu-id="4b866-514">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="4b866-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="4b866-515">NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-515">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="4b866-516">Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="4b866-516">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="4b866-517">AppVM02 hello yanıtı alır</span><span class="sxs-lookup"><span data-stu-id="4b866-517">AppVM02 receives hello response</span></span>

#### <a name="denied-internet-direct-tooweb-server"></a><span data-ttu-id="4b866-518">(Reddedildi) Internet doğrudan tooWeb sunucu</span><span class="sxs-lookup"><span data-stu-id="4b866-518">(Denied) Internet direct tooWeb Server</span></span>
1. <span data-ttu-id="4b866-519">Internet kullanıcı tooaccess hello web sunucusu, IIS01, hello FrontEnd001.CloudApp.Net hizmeti ile çalışır</span><span class="sxs-lookup"><span data-stu-id="4b866-519">Internet user tries tooaccess hello web server, IIS01, through hello FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="4b866-520">HTTP trafiği için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="4b866-520">Since there are no endpoints open for HTTP traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="4b866-521">Hello NSG (blok Internet) hello ön uç alt ağdaki Hello uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller</span><span class="sxs-lookup"><span data-stu-id="4b866-521">If hello endpoints were open for some reason, hello NSG (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="4b866-522">Son olarak, hello ön uç alt UDR rota hello sonraki atlama olarak IIS01 toohello Güvenlik Duvarı'ndan tüm giden trafiği gönderebilir ve hello Güvenlik Duvarı'nı bu asimetrik trafiği olarak görebilir ve hello giden yanıt en az üç bağımsız katmanı vardır nedenle bırakma Merhaba arasında yetkisiz/uygunsuz erişimi engelleme kendi bulut hizmeti Internet ve IIS01 yolu.</span><span class="sxs-lookup"><span data-stu-id="4b866-522">Finally, hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toobackend-server"></a><span data-ttu-id="4b866-523">(Reddedildi) Internet tooBackend sunucu</span><span class="sxs-lookup"><span data-stu-id="4b866-523">(Denied) Internet tooBackend Server</span></span>
1. <span data-ttu-id="4b866-524">Internet kullanıcı tooaccess AppVM01 bir dosyada hello BackEnd001.CloudApp.Net hizmeti ile çalışır</span><span class="sxs-lookup"><span data-stu-id="4b866-524">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="4b866-525">Dosya Paylaşımı için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="4b866-525">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="4b866-526">Herhangi bir nedenden dolayı Hello uç noktaları açıksa hello NSG (blok Internet) bu trafiği engeller</span><span class="sxs-lookup"><span data-stu-id="4b866-526">If hello endpoints were open for some reason, hello NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="4b866-527">Son olarak, hello UDR rota hello sonraki atlama olarak AppVM01 toohello Güvenlik Duvarı'ndan tüm giden trafiği gönderebilir ve hello Güvenlik Duvarı'nı bu asimetrik trafiği olarak görebilir ve hello giden yanıt en az üç bağımsız katmanlar arasında savunma vardır nedenle bırakma Internet ve AppVM01 yetkisiz/uygunsuz erişimi engelleme kendi bulut hizmeti ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="4b866-527">Finally, hello UDR route would send any outbound traffic from AppVM01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-toobackend-server"></a><span data-ttu-id="4b866-528">(Reddedildi) Ön uç sunucusu tooBackend sunucu</span><span class="sxs-lookup"><span data-stu-id="4b866-528">(Denied) Frontend server tooBackend Server</span></span>
1. <span data-ttu-id="4b866-529">IIS01 aşılmış ve kötü amaçlı kod tooscan hello arka uç sunucuları alt çalışırken çalıştığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="4b866-529">Assume IIS01 was compromised and is running malicious code trying tooscan hello Backend subnet servers.</span></span>
2. <span data-ttu-id="4b866-530">Merhaba ön uç alt UDR rota tüm giden trafiği IIS01 toohello Güvenlik Duvarı'nı hello sonraki atlama olarak gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-530">hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop.</span></span> <span data-ttu-id="4b866-531">Bu tarafından değiştirilmiş bir şey değil hello tehlikeye VM.</span><span class="sxs-lookup"><span data-stu-id="4b866-531">This is not something that can be altered by hello compromised VM.</span></span>
3. <span data-ttu-id="4b866-532">Hello isteği tooAppVM01 veya trafiği hello Güvenlik Duvarı'nı (son tooFW kuralları 7 ve 9) tarafından izin verilebilir DNS araması için toohello DNS sunucusu olduğunda hello güvenlik duvarı hello trafiği işleme.</span><span class="sxs-lookup"><span data-stu-id="4b866-532">hello firewall would process hello traffic, if hello request was tooAppVM01, or toohello DNS server for DNS lookups that traffic could potentially be allowed by hello firewall (due tooFW Rules 7 and 9).</span></span> <span data-ttu-id="4b866-533">Diğer tüm trafik FW kural 11 göre (tüm reddetme) engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="4b866-534">Tehdit algılama Gelişmiş hello güvenlik duvarı etkinleştirildi (da değil kapsanan bu belgede, Gelişmiş tehdit özellikleri, belirli bir ağ Gereci hello satıcı belgelerine bakın), hatta tarafından hello kuralları iletme temel izin trafiği Bu konuda ele alınan belge engelledi hello trafiği bilinen imzaları ya da bir Gelişmiş tehdit kuralı bayrak desenler içeriyorsa.</span><span class="sxs-lookup"><span data-stu-id="4b866-534">If advanced threat detection was enabled on hello firewall (which is not covered in this document, see hello vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by hello basic forwarding rules discussed in this document could be prevented if hello traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="4b866-535">(Reddedildi) DNS sunucusunda Internet DNS araması</span><span class="sxs-lookup"><span data-stu-id="4b866-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="4b866-536">Internet kullanıcı toolookup DNS01 BackEnd001.CloudApp.Net hizmeti aracılığıyla bir iç DNS kaydını çalışır</span><span class="sxs-lookup"><span data-stu-id="4b866-536">Internet user tries toolookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="4b866-537">DNS trafiği için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello sunucusuna ulaşabilir olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="4b866-537">Since there are no endpoints open for DNS traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="4b866-538">Herhangi bir nedenden dolayı Hello uç noktaları açıksa hello ön uç alt ağdaki hello NSG kuralının (blok Internet) bu trafiği engeller</span><span class="sxs-lookup"><span data-stu-id="4b866-538">If hello endpoints were open for some reason, hello NSG rule (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="4b866-539">Son olarak, hello arka uç alt UDR rota hello sonraki atlama olarak DNS01 toohello Güvenlik Duvarı'ndan tüm giden trafiği gönderebilir ve hello Güvenlik Duvarı'nı bu asimetrik trafiği olarak görebilir ve hello giden yanıt en az üç bağımsız katmanı vardır nedenle bırakma Merhaba arasında yetkisiz/uygunsuz erişimi engelleme kendi bulut hizmeti Internet ve DNS01 yolu.</span><span class="sxs-lookup"><span data-stu-id="4b866-539">Finally, hello Backend subnet UDR route would send any outbound traffic from DNS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toosql-access-through-firewall"></a><span data-ttu-id="4b866-540">(Reddedildi) Güvenlik Duvarı üzerinden Internet tooSQL erişimi</span><span class="sxs-lookup"><span data-stu-id="4b866-540">(Denied) Internet tooSQL access through Firewall</span></span>
1. <span data-ttu-id="4b866-541">Internet kullanıcı SQL verileri SecSvc001.CloudApp.Net (Internet'e yönelik bulut hizmeti) ' ister.</span><span class="sxs-lookup"><span data-stu-id="4b866-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="4b866-542">SQL için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello güvenlik duvarı ulaşmak olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="4b866-542">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="4b866-543">Herhangi bir nedenden dolayı SQL uç noktaları açıksa hello güvenlik duvarı kuralı işlemeye başlamak:</span><span class="sxs-lookup"><span data-stu-id="4b866-543">If SQL endpoints were open for some reason, hello firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="4b866-544">FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-544">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="4b866-545">FW kuralları 2-5 (RDP kurallar) yok, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="4b866-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="4b866-546">FW kural 6 ve 7 (uygulama kuralları) uygulama, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-546">FW Rule 6 & 7 (Application Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="4b866-547">FW kural 8 (tooInternet) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="4b866-547">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="4b866-548">FW kural 9 (DNS) uygulanmaz, taşıma toonext kuralı</span><span class="sxs-lookup"><span data-stu-id="4b866-548">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="4b866-549">FW kural 10 (içi alt ağ) değil, uygulama toonext kuralı Taşı</span><span class="sxs-lookup"><span data-stu-id="4b866-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move toonext rule</span></span>
   7. <span data-ttu-id="4b866-550">FW kural 11 (Tümünü Reddet) geçerli, engellenmiş, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="4b866-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="4b866-551">Başvurular</span><span class="sxs-lookup"><span data-stu-id="4b866-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="4b866-552">Ana komut dosyası ve ağ yapılandırması</span><span class="sxs-lookup"><span data-stu-id="4b866-552">Main Script and Network Config</span></span>
<span data-ttu-id="4b866-553">Merhaba tam komut dosyası bir PowerShell komut dosyası kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4b866-553">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="4b866-554">Merhaba ağ yapılandırma "NetworkConf2.xml" adlı bir dosyaya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4b866-554">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="4b866-555">Merhaba kullanıcı tanımlı değişkenleri gerektiği gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4b866-555">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="4b866-556">Merhaba komut dosyasını çalıştırın, ardından hello güvenlik duvarı kuralı kurulum yönergeleri yukarıdaki izleyin.</span><span class="sxs-lookup"><span data-stu-id="4b866-556">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="4b866-557">Tam komut dosyası</span><span class="sxs-lookup"><span data-stu-id="4b866-557">Full Script</span></span>
<span data-ttu-id="4b866-558">Merhaba kullanıcı tanımlı değişkenleri esas alarak bu betiği olur:</span><span class="sxs-lookup"><span data-stu-id="4b866-558">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="4b866-559">Tooan Azure aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="4b866-559">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="4b866-560">Yeni depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b866-560">Create a new storage account</span></span>
3. <span data-ttu-id="4b866-561">Yeni bir VNet ve hello ağ yapılandırma dosyasında tanımlanan üç alt ağlar oluşturun</span><span class="sxs-lookup"><span data-stu-id="4b866-561">Create a new VNet and three subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="4b866-562">Beş sanal makineler oluşturun; Güvenlik Duvarı'nı 1 ve 4 windows server Vm'leri</span><span class="sxs-lookup"><span data-stu-id="4b866-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="4b866-563">UDR dahil olmak üzere yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="4b866-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="4b866-564">İki yeni yönlendirme tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b866-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="4b866-565">Yollar toohello tabloları ekleyin</span><span class="sxs-lookup"><span data-stu-id="4b866-565">Add routes toohello tables</span></span>
   3. <span data-ttu-id="4b866-566">Tablolar tooappropriate alt ağları bağlama</span><span class="sxs-lookup"><span data-stu-id="4b866-566">Bind tables tooappropriate subnets</span></span>
6. <span data-ttu-id="4b866-567">IP iletimi NVA hello üzerinde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="4b866-567">Enable IP Forwarding on hello NVA</span></span>
7. <span data-ttu-id="4b866-568">NSG dahil olmak üzere yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="4b866-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="4b866-569">Bir NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b866-569">Creating a NSG</span></span>
   2. <span data-ttu-id="4b866-570">Bir kural ekleme</span><span class="sxs-lookup"><span data-stu-id="4b866-570">Adding a rule</span></span>
   3. <span data-ttu-id="4b866-571">Merhaba NSG toohello uygun alt ağları bağlama</span><span class="sxs-lookup"><span data-stu-id="4b866-571">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="4b866-572">Bu PowerShell Betiği, bir bilgisayar veya sunucu, Internet'e yerel olarak çalıştırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4b866-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b866-573">Bu komut dosyasını çalıştırdığınızda, uyarı veya PowerShell'de pop diğer bilgilendirici iletileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="4b866-574">Yalnızca hata iletileri kırmızı sorunu nedeni edilir.</span><span class="sxs-lookup"><span data-stu-id="4b866-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

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
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

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

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

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
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
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
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
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


#### <a name="network-config-file"></a><span data-ttu-id="4b866-575">Ağ yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="4b866-575">Network Config File</span></span>
<span data-ttu-id="4b866-576">Güncelleştirilmiş konumla bu xml dosyasını kaydedin ve hello bağlantı toothis toohello $NetworkConfigFile değişkeni yukarıdaki hello komut dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4b866-576">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
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

#### <a name="sample-application-scripts"></a><span data-ttu-id="4b866-577">Örnek uygulama komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="4b866-577">Sample Application Scripts</span></span>
<span data-ttu-id="4b866-578">Bu ve diğer çevre örnekleri için örnek bir uygulama tooinstall istiyorsanız, bir bağlantı aşağıdaki hello sağlanmış: [örnek uygulama betiği][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="4b866-578">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Çift yönlü DMZ NVA, NSG ve UDR"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Mantıksal görünümünü hello güvenlik duvarı kuralları"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Bir ön uç ağ nesnesi oluşturun"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Bir DNS sunucusu nesnesi oluşturun"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Varsayılan RDP kuralı kopyası"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 kuralı"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Uygulama yeniden yönlendirme simgesi"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Hedef NAT simgesi"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Geçişi simgesi"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Güvenlik Duvarı Yönetimi kuralı"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Güvenlik Duvarı RDP kuralı"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Güvenlik Duvarı Web kuralı"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Güvenlik Duvarı AppVM01 kuralı"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Giden güvenlik duvarı kuralı"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Güvenlik Duvarı DNS kuralı"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Güvenlik Duvarı içi sanal ağ kuralı"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Güvenlik duvarı kuralı Reddet"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Güvenlik duvarı kuralını etkinleştirme"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
