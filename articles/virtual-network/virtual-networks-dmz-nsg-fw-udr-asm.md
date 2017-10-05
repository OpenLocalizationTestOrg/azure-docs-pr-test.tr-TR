---
title: "DMZ örnek – yapı ağ güvenlik duvarı, UDR ve NSG ile korunacak DMZ | Microsoft Docs"
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
ms.openlocfilehash: fdb3c5cbd3acee90386352c6f180a71aa81f54fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="example-3--build-a-dmz-to-protect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="f6e24-103">Örnek 3 – bir çevre ağ güvenlik duvarı, UDR ve NSG ile korumak için derleme</span><span class="sxs-lookup"><span data-stu-id="f6e24-103">Example 3 – Build a DMZ to Protect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="f6e24-104">[Güvenlik sınırı en iyi yöntemler sayfasına dön][HOME]</span><span class="sxs-lookup"><span data-stu-id="f6e24-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="f6e24-105">Bu örnek, bir güvenlik duvarı, dört windows sunucuları, kullanıcı tanımlı yönlendirme, IP iletimi ve ağ güvenlik grupları ile DMZ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="f6e24-106">Bu da her her adımın daha derin bir anlayış sağlamak için ilgili komutları yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="f6e24-107">Ayrıca bir ayrıntılı sağlamak için bir trafik senaryosu bölümü olan adım adım çevre savunma katmanlar arasında nasıl trafiği devam eder.</span><span class="sxs-lookup"><span data-stu-id="f6e24-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="f6e24-108">Son olarak, içindeki başvuruların sınamak ve çeşitli senaryolarıyla denemeler için bu ortamı oluşturmak için yönerge ve tam bir kod bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="f6e24-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="f6e24-109">![Çift yönlü DMZ NVA, NSG ve UDR][1]</span><span class="sxs-lookup"><span data-stu-id="f6e24-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="f6e24-110">Ortam Kurulumu</span><span class="sxs-lookup"><span data-stu-id="f6e24-110">Environment Setup</span></span>
<span data-ttu-id="f6e24-111">Bu örnekte, aşağıdakileri içeren bir abonelik vardır:</span><span class="sxs-lookup"><span data-stu-id="f6e24-111">In this example there is a subscription that contains the following:</span></span>

* <span data-ttu-id="f6e24-112">Üç bulut hizmetlerini: "SecSvc001", "FrontEnd001" ve "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="f6e24-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="f6e24-113">Bir sanal ağ "CorpNetwork" üç alt ağ ile: "SecNet", "Ön uç" ve "Arka uç"</span><span class="sxs-lookup"><span data-stu-id="f6e24-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="f6e24-114">Bu örnekte bir güvenlik duvarı, bir ağ sanal gereç SecNet alt ağına bağlı</span><span class="sxs-lookup"><span data-stu-id="f6e24-114">A network virtual appliance, in this example a firewall, connected to the SecNet subnet</span></span>
* <span data-ttu-id="f6e24-115">Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="f6e24-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="f6e24-116">Uygulama geri temsil eden iki windows sunucuları sunucuları ("AppVM01", "AppVM02") end</span><span class="sxs-lookup"><span data-stu-id="f6e24-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="f6e24-117">Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu</span><span class="sxs-lookup"><span data-stu-id="f6e24-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="f6e24-118">Başvurular bölümündeki yukarıda açıklanan ortamı çoğunu oluşturacak bir PowerShell komut dosyası yok.</span><span class="sxs-lookup"><span data-stu-id="f6e24-118">In the references section below there is a PowerShell script that will build most of the environment described above.</span></span> <span data-ttu-id="f6e24-119">VM'ler ve sanal ağlar, derleme örnek komut dosyası tarafından yapılır rağmen değil açıklanmıştır bu belgede ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="f6e24-119">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span>

<span data-ttu-id="f6e24-120">Ortamı oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="f6e24-120">To build the environment:</span></span>

1. <span data-ttu-id="f6e24-121">References bölümünde bulunan ağ yapılandırma xml dosyasını kaydedin (adlar, konum ve IP adresleri verilen senaryo eşleşecek şekilde güncelleştirilir)</span><span class="sxs-lookup"><span data-stu-id="f6e24-121">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="f6e24-122">Kullanıcı değişkenleri karşı (Abonelikleri, hizmet adlarını, vb.) çalıştırılacak komut dosyasıdır ortamıyla eşleşecek şekilde güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="f6e24-122">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="f6e24-123">PowerShell komut dosyası yürütme</span><span class="sxs-lookup"><span data-stu-id="f6e24-123">Execute the script in PowerShell</span></span>

<span data-ttu-id="f6e24-124">**Not**: PowerShell Betiği miktarlara bölge ağ yapılandırması xml dosyasında miktarlara bölge ile eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-124">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>

<span data-ttu-id="f6e24-125">Komut dosyası başarıyla çalıştıktan sonra aşağıdaki sonrası betik adımlar izlenebilir:</span><span class="sxs-lookup"><span data-stu-id="f6e24-125">Once the script runs successfully the following post-script steps may be taken:</span></span>

1. <span data-ttu-id="f6e24-126">Güvenlik duvarı kuralları ayarlamak, bu başlıklı bölümde aşağıda ele alınmıştır: güvenlik duvarı kuralı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="f6e24-126">Set up the firewall rules, this is covered in the section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="f6e24-127">İsteğe bağlı olarak web sunucusu ve uygulama sunucusu bu DMZ yapılandırma ile test izin vermek için basit bir web uygulaması ile ayarlamak için iki komut dosyası başvuruları bölümünde bulunur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-127">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="f6e24-128">Komut dosyası kuralları tamamlanması gerekir Güvenlik Duvarı'nı başarıyla çalıştıktan sonra bu başlıklı bölümde ele alınmıştır: güvenlik duvarı kuralları.</span><span class="sxs-lookup"><span data-stu-id="f6e24-128">Once the script runs successfully the firewall rules will need to be completed, this is covered in the section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="f6e24-129">Kullanıcı tanımlı yönlendirme (UDR)</span><span class="sxs-lookup"><span data-stu-id="f6e24-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="f6e24-130">Varsayılan olarak, aşağıdaki sistem yolları gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="f6e24-130">By default, the following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="f6e24-131">Her zaman VNETLocal vnet'in (IE, ağdan Vnet'e her belirli VNet nasıl tanımlandığına bağlı olarak değişir), belirli bir ağ için tanımlanan adres ön ' dir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-131">The VNETLocal is always the defined address prefix(es) of the VNet for that specific network (ie it will change from VNet to VNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="f6e24-132">Kalan sistem yolları statik ve yukarıdaki varsayılan.</span><span class="sxs-lookup"><span data-stu-id="f6e24-132">The remaining system routes are static and default as above.</span></span>

<span data-ttu-id="f6e24-133">Öncelik, ettirilmesi yollar en uzun ön ek eşleşmesi (LPM) yöntemiyle işlenir, böylece en özel bir rota tablosunda belirtilen hedef adresi için geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-133">As for priority, routes are processed via the Longest Prefix Match (LPM) method, thus the most specific route in the table would apply to a given destination address.</span></span>

<span data-ttu-id="f6e24-134">Bu nedenle, yerel ağ (10.0.0.0/16) trafiği (örneğin sunucuya DNS01, 10.0.2.4) 10.0.0.0/16 rota nedeniyle hedefine VNet arasında yönlendirilecektir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-134">Therefore, traffic (for example to the DNS01 server, 10.0.2.4) intended for the local network (10.0.0.0/16) would be routed across the VNet to its destination due to the 10.0.0.0/16 route.</span></span> <span data-ttu-id="f6e24-135">Diğer bir deyişle, 10.0.2.4 için 10.0.0.0/16 en özel bir rota 10.0.0.0/8 ve 0.0.0.0/0 de geçerli olabilir, ancak daha az olduğundan belirli kullanıcılar bu trafiği etkilemez olsa bile yoldur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-135">In other words, for 10.0.2.4, the 10.0.0.0/16 route is the most specific route, even though the 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="f6e24-136">Böylece 10.0.2.4 trafiği, yerel vnet'in sonraki atlama sahip ve yalnızca hedef yol.</span><span class="sxs-lookup"><span data-stu-id="f6e24-136">Thus the traffic to 10.0.2.4 would have a next hop of the local VNet and simply route to the destination.</span></span>

<span data-ttu-id="f6e24-137">Trafik tasarlanmıştır 10.1.1.1 için örneğin, 10.0.0.0/16 rota uygularsanız olmayacaktır, ancak bu 10.0.0.0/8 en belirgin olacaktır ve bu trafiği olacaktır ("siyah holed") sonraki atlama Null olduğundan bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="f6e24-137">If traffic was intended for 10.1.1.1 for example, the 10.0.0.0/16 route wouldn’t apply, but the 10.0.0.0/8 would be the most specific, and this the traffic would be dropped (“black holed”) since the next hop is Null.</span></span> 

<span data-ttu-id="f6e24-138">Hedef herhangi biri Null ön ekler veya VNETLocal önekleri uygulanmadı sonra en az belirli izleyin yönlendirmek, 0.0.0.0/0 ve Internet'e sonraki atlama olarak ve bu nedenle Azure'nın Internet kenar çıkışı yönlendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="f6e24-138">If the destination didn’t apply to any of the Null prefixes or the VNETLocal prefixes, then it would follow the least specific route, 0.0.0.0/0 and be routed out to the Internet as the next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="f6e24-139">Rota tablosunda iki aynı önekleri varsa, yolları "kaynak" özniteliğine dayanarak tercih sırasına göre şudur:</span><span class="sxs-lookup"><span data-stu-id="f6e24-139">If there are two identical prefixes in the route table, the following is the order of preference based on the routes “source” attribute:</span></span>

1. <span data-ttu-id="f6e24-140">"Değerinin VirtualAppliance" el ile tabloya eklenen kullanıcı tanımlanan rota =</span><span class="sxs-lookup"><span data-stu-id="f6e24-140">"VirtualAppliance" = A User Defined Route manually added to the table</span></span>
2. <span data-ttu-id="f6e24-141">"VPNGateway" dinamik rota (BGP), karma ağlarla kullanıldığında = dinamik Protokolü otomatik olarak eşlenmiş ağ değişiklikleri yansıtır gibi dinamik ağ protokolü tarafından eklenen, bu yollar zaman içinde değişebilir</span><span class="sxs-lookup"><span data-stu-id="f6e24-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as the dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="f6e24-142">"Varsayılan" rota yukarıdaki tabloda gösterildiği gibi sistem yolları, yerel VNet ve statik girdilerini =.</span><span class="sxs-lookup"><span data-stu-id="f6e24-142">“Default” = The System Routes, the local VNet and the static entries as shown in the route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="f6e24-143">Giden ve gelen zorlamak için VPN ağ geçitleri trafiği bir ağ sanal gereç (NVA) yönlendirilmeden şirketler arası ve ExpressRoute ile kullanıcı tanımlı yönlendirme (UDR) artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6e24-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways to force outbound and inbound cross-premises traffic to be routed to a network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-the-local-routes"></a><span data-ttu-id="f6e24-144">Yerel yollar oluşturma</span><span class="sxs-lookup"><span data-stu-id="f6e24-144">Creating the local routes</span></span>
<span data-ttu-id="f6e24-145">Bu örnekte, iki yönlendirme tablolarını gereklidir, her biri ön uç ve arka uç alt ağlar için.</span><span class="sxs-lookup"><span data-stu-id="f6e24-145">In this example, two routing tables are needed, one each for the Frontend and Backend subnets.</span></span> <span data-ttu-id="f6e24-146">Her tablo için belirli alt uygun statik yollar ile yüklenir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-146">Each table is loaded with static routes appropriate for the given subnet.</span></span> <span data-ttu-id="f6e24-147">Bu örneğin amacı doğrultusunda, her tablo üç yol vardır:</span><span class="sxs-lookup"><span data-stu-id="f6e24-147">For the purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="f6e24-148">Güvenlik Duvarı atlamak yerel alt ağ trafiğine izin vermek için yerel alt ağ trafiği hiçbir sonraki atlama ile tanımlanan</span><span class="sxs-lookup"><span data-stu-id="f6e24-148">Local subnet traffic with no Next Hop defined to allow local subnet traffic to bypass the firewall</span></span>
2. <span data-ttu-id="f6e24-149">Bir sonraki güvenlik duvarı olarak tanımlanan atlama ile sanal ağ trafiği, bu doğrudan yönlendirmek yerel VNet trafiğe izin veren varsayılan kuralı geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="f6e24-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides the default rule that allows local VNet traffic to route directly</span></span>
3. <span data-ttu-id="f6e24-150">Bir sonraki Güvenlik Duvarı'nı tanımlanan atlama ile tüm kalan trafiği (0/0)</span><span class="sxs-lookup"><span data-stu-id="f6e24-150">All remaining traffic (0/0) with a Next Hop defined as the firewall</span></span>

<span data-ttu-id="f6e24-151">Yönlendirme tabloları oluşturulduktan sonra bunlar için alt ağlarını bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-151">Once the routing tables are created they are bound to their subnets.</span></span> <span data-ttu-id="f6e24-152">Ön uç alt ağ için bir kez oluşturulur ve alt ağına bağlı yönlendirme tablosu aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="f6e24-152">For the Frontend subnet routing table, once created and bound to the subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="f6e24-153">Yol tablosu oluşturmak, bir kullanıcı tanımlı yolu ekleyin ve ardından yol tablosu bir alt ağa bağlamak için kullanılan bu örnek için aşağıdaki komutları (Not; dolar işareti ile başlayan altındaki öğeleri (örn: $BESubnet) kullanıcı tanımlı değişkenler başvuru bölümünde, bu belgenin betikten):</span><span class="sxs-lookup"><span data-stu-id="f6e24-153">For this example, the following commands are used to build the route table, add a user defined route, and then bind the route table to a subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="f6e24-154">Temel yönlendirme tablosu oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-154">First the base routing table must be created.</span></span> <span data-ttu-id="f6e24-155">Bu kod parçacığında arka uç alt ağ için tablo oluşturulmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-155">This snippet shows the creation of the table for the Backend subnet.</span></span> <span data-ttu-id="f6e24-156">Komut dosyasında karşılık gelen bir tablo için ön uç alt da oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-156">In the script, a corresponding table is also created for the Frontend subnet.</span></span>
   
     <span data-ttu-id="f6e24-157">AzureRouteTable yeni-ad $BERouteTableName '</span><span class="sxs-lookup"><span data-stu-id="f6e24-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="f6e24-158">Yol tablosu oluşturulduktan sonra belirli kullanıcı tanımlı yollar eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-158">Once the route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="f6e24-159">Bu konuda kırpılmış, tüm trafik (0.0.0.0/0) (bir değişken $VMIP [0] komut dosyasındaki sanal gereç oluşturulduğunda atanan IP adresi geçirmek için kullanılır) sanal gereç aracılığıyla yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-159">In this snipped, all traffic (0.0.0.0/0) will be routed through the virtual appliance (a variable, $VMIP[0], is used to pass in the IP address assigned when the virtual appliance was created earlier in the script).</span></span> <span data-ttu-id="f6e24-160">Komut dosyasında karşılık gelen kuralı da ön uç tabloda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-160">In the script, a corresponding rule is also created in the Frontend table.</span></span>
   
     <span data-ttu-id="f6e24-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="f6e24-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="f6e24-162">Yukarıdaki rota girişi, doğrudan hedef ve ağ sanal Gerece yönlendirmek için sanal ağ içindeki trafiği izin varsayılan "0.0.0.0/0" yol, ancak hala var olan varsayılan 10.0.0.0/16 kuralı geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-162">The above route entry will override the default "0.0.0.0/0" route, but the default 10.0.0.0/16 rule still existing which would allow traffic within the VNet to route directly to the destination and not to the Network Virtual Appliance.</span></span> <span data-ttu-id="f6e24-163">Doğru Bu davranış izleme kuralı eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-163">To correct this behavior the follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="f6e24-164">Bu noktada yapılacak bir seçenek yoktur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-164">At this point there is a choice to be made.</span></span> <span data-ttu-id="f6e24-165">Yukarıdaki iki yollar değerlendirmesi, tek bir alt ağ içindeki bile trafiği için Güvenlik Duvarı'nda tüm trafik yönlendirilecek.</span><span class="sxs-lookup"><span data-stu-id="f6e24-165">With the above two routes all traffic will route to the firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="f6e24-166">Yerel Güvenlik Duvarı müdahalesi olmadan üçüncü yönlendirmek için bir alt ağ içindeki trafiği izin vermek için çok özel kural eklenebilir ancak bu, istenebilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-166">This may be desired, however to allow traffic within a subnet to route locally without involvement from the firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="f6e24-167">Bu yol var bildiren herhangi bir adresi destine yerel alt ağ yalnızca için rota doğrudan (NextHopType VNETLocal =).</span><span class="sxs-lookup"><span data-stu-id="f6e24-167">This route states that any address destine for the local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="f6e24-168">Son olarak, oluşturulur ve kullanıcı tanımlı yollar ile doldurulur yönlendirme tablosu ile tablonun şimdi bir alt ağa bağlı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-168">Finally, with the routing table created and populated with a user defined routes, the table must now be bound to a subnet.</span></span> <span data-ttu-id="f6e24-169">Komut dosyasında, ön uç yol tablosu ayrıca ön uç alt ağına bağlı.</span><span class="sxs-lookup"><span data-stu-id="f6e24-169">In the script, the front end route table is also bound to the Frontend subnet.</span></span> <span data-ttu-id="f6e24-170">Burada, arka uç alt ağ için bağlama komut verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-170">Here is the binding script for the back end subnet.</span></span>
   
     <span data-ttu-id="f6e24-171">Set-AzureSubnetRouteTable - VirtualNetworkName $VNetName '</span><span class="sxs-lookup"><span data-stu-id="f6e24-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="f6e24-172">IP İletimi</span><span class="sxs-lookup"><span data-stu-id="f6e24-172">IP Forwarding</span></span>
<span data-ttu-id="f6e24-173">Bir yardımcı UDR için özelliktir IP iletimi.</span><span class="sxs-lookup"><span data-stu-id="f6e24-173">A companion feature to UDR, is IP Forwarding.</span></span> <span data-ttu-id="f6e24-174">Gereci özellikle trafiği alabilmesine ve bu trafiğin ultimate hedefine iletmek imkan tanıyan bir sanal gereç bir ayar budur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-174">This is a setting on a Virtual Appliance that allows it to receive traffic not specifically addressed to the appliance and then forward that traffic to its ultimate destination.</span></span>

<span data-ttu-id="f6e24-175">AppVM01 trafiğinden DNS01 sunucusuna bir istek yapıyorsa örnek olarak, UDR bu Güvenlik Duvarı'na rota.</span><span class="sxs-lookup"><span data-stu-id="f6e24-175">As an example, if traffic from AppVM01 makes a request to the DNS01 server, UDR would route this to the firewall.</span></span> <span data-ttu-id="f6e24-176">Etkin IP iletimi ile DNS01 hedef (10.0.2.4) trafiği (10.0.0.4) Gereci tarafından kabul ve olması ultimate hedefine (10.0.2.4) iletilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-176">With IP Forwarding enabled, the traffic for the DNS01 destination (10.0.2.4) will be accepted by the appliance (10.0.0.4) and then forwarded to its ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="f6e24-177">Yol tablosu sonraki atlama olarak bir güvenlik duvarına sahip olsa bile Güvenlik Duvarı'nı etkin IP iletimi, trafiği Gereci tarafından kabul değil.</span><span class="sxs-lookup"><span data-stu-id="f6e24-177">Without IP Forwarding enabled on the Firewall, traffic would not be accepted by the appliance even though the route table has the firewall as the next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f6e24-178">Kullanıcı tanımlı yönlendirme ile birlikte IP iletimi etkinleştirmeyi unutmayın önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-178">It’s critical to remember to enable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="f6e24-179">IP iletimi ayarlama tek bir komut ve VM oluşturma zamanında yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="f6e24-180">Bu örnek akış için kod parçacığında komut dosyasının sonuna doğru olduğundan ve UDR komutları ile gruplandırılır:</span><span class="sxs-lookup"><span data-stu-id="f6e24-180">For the flow of this example the code snippet is towards the end of the script and grouped with the UDR commands:</span></span>

1. <span data-ttu-id="f6e24-181">Bu durumda, bir sanal gereç, güvenlik duvarı olan VM örneği çağırın ve IP iletimini etkinleştirme (Not; dolar işareti kırmızı başlayarak herhangi bir öğeye (örn: $VMName[0]), bu belgenin başvuru bölümdeki komut dosyasından bir kullanıcı tanımlı değişkendir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-181">Call the VM instance that is your virtual appliance, the firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from the script in the reference section of this document.</span></span> <span data-ttu-id="f6e24-182">Köşeli ayraçlar [0], sıfır VM'ler değişiklik yapmadan çalışmak örnek komut dosyası için bir dizi ilk VM'yi temsil eder, Güvenlik Duvarı'nı (VM 0) ilk VM olması gerekir):</span><span class="sxs-lookup"><span data-stu-id="f6e24-182">The zero in brackets, [0], represents the first VM in the array of VMs, for the example script to work without modification, the first VM (VM 0) must be the firewall):</span></span>
   
     <span data-ttu-id="f6e24-183">Get-AzureVM-$ServiceName [0] [0] $VMName - ServiceName adı | \`</span><span class="sxs-lookup"><span data-stu-id="f6e24-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="f6e24-184">Ağ Güvenlik Grupları (NSG)</span><span class="sxs-lookup"><span data-stu-id="f6e24-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="f6e24-185">Bu örnekte, bir NSG grubu yerleşik ve tek bir kural ile yüklenir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="f6e24-186">Bu grup, ardından yalnızca ön uç ve arka uç alt ağlara (SecNet değil) bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-186">This group is then bound only to the Frontend and Backend subnets (not the SecNet).</span></span> <span data-ttu-id="f6e24-187">Aşağıdaki kural oluşturulmakta olan bildirimli olarak:</span><span class="sxs-lookup"><span data-stu-id="f6e24-187">Declaratively the following rule is being built:</span></span>

1. <span data-ttu-id="f6e24-188">Tüm trafiği (tüm bağlantı noktaları) Internet'ten (tüm alt ağlar) tüm sanal ağa reddedildi</span><span class="sxs-lookup"><span data-stu-id="f6e24-188">Any traffic (all ports) from the Internet to the entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="f6e24-189">Nsg'ler Bu örnekte kullanılan cihazın ana amacı el ile yetersizliğini karşı savunma ikincil bir katmanı olarak olsa da.</span><span class="sxs-lookup"><span data-stu-id="f6e24-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="f6e24-190">Ön uç ya da internet'ten gelen tüm trafiği engellemek istiyoruz veya arka uç alt ağlar, trafiği yalnızca SecNet alt ağ güvenlik duvarı aracılığıyla akış (ve ardından IF, alt ağlar ön uç veya arka uç açın gerekli).</span><span class="sxs-lookup"><span data-stu-id="f6e24-190">We want to block all inbound traffic from the internet to either the Frontend or Backend subnets, traffic should only flow through the SecNet subnet to the firewall (and then if appropriate on to the Frontend or Backend subnets).</span></span> <span data-ttu-id="f6e24-191">Ayrıca, bir yerde, UDR kurallarla ön uç veya arka uç alt yaptı tüm trafik çıkışı Güvenlik Duvarı'nda (UDR) sayesinde yönlendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="f6e24-191">Plus, with the UDR rules in place, any traffic that did make it into the Frontend or Backend subnets would be directed out to the firewall (thanks to UDR).</span></span> <span data-ttu-id="f6e24-192">Güvenlik Duvarı'nı bu asimetrik bir akış halinde görür ve giden trafik bırakma.</span><span class="sxs-lookup"><span data-stu-id="f6e24-192">The firewall would see this as an asymmetric flow and would drop the outbound traffic.</span></span> <span data-ttu-id="f6e24-193">Bu nedenle ön uç ve arka uç alt ağ korumaya güvenlik üç katmanı vardır; 1) açık uç nokta yok FrontEnd001 ve BackEnd001 bulut hizmetlerini, 2) Nsg'ler trafiğini Internet'ten, 3) güvenlik duvarı bırakma asimetrik trafiği engelleme.</span><span class="sxs-lookup"><span data-stu-id="f6e24-193">Thus there are three layers of security protecting the Frontend and Backend subnets; 1) no open endpoints on the FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from the Internet, 3) the firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="f6e24-194">Bir ilginç Bu örnekte ağ güvenlik grubu ile ilgili güvenlik alt ağ içerir tüm sanal ağ Internet trafiği engellemek için olan yalnızca bir kural, aşağıda gösterilen içerdiğini noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-194">One interesting point regarding the Network Security Group in this example is that it contains only one rule, shown below, which is to deny internet traffic to the entire virtual network which would include the Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet `
        from the Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="f6e24-195">NSG yalnızca ön uç ve arka uç alt ağa bağlı olduğundan, kuralın trafiğinde ancak işlenen değil gelen güvenlik alt ağ için.</span><span class="sxs-lookup"><span data-stu-id="f6e24-195">However, since the NSG is only bound to the Frontend and Backend subnets, the rule isn’t processed on traffic inbound to the Security subnet.</span></span> <span data-ttu-id="f6e24-196">Sonuç olarak, NSG, hiçbir zaman güvenlik alt ağına bağlı olduğundan NSG kural VNet üzerinde herhangi bir adresi yok Internet trafiğini diyor olsa bile, trafik için güvenlik alt ağ akar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-196">As a result, even though the NSG rule says no Internet traffic to any address on the VNet, because the NSG was never bound to the Security subnet, traffic will flow to the Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="f6e24-197">Güvenlik Duvarı Kuralları</span><span class="sxs-lookup"><span data-stu-id="f6e24-197">Firewall Rules</span></span>
<span data-ttu-id="f6e24-198">Güvenlik Duvarı'nı kuralları iletme oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-198">On the firewall, forwarding rules will need to be created.</span></span> <span data-ttu-id="f6e24-199">Güvenlik duvarı engelleme veya iletme tüm gelen, giden ve içi-VNet trafiği olduğundan birçok güvenlik duvarı kuralları gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-199">Since the firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="f6e24-200">Ayrıca, tüm gelen trafiği güvenlik hizmeti genel IP adresine (farklı bağlantı noktalarını), güvenlik duvarı tarafından işlenmek üzere karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-200">Also, all inbound traffic will hit the Security Service public IP address (on different ports), to be processed by the firewall.</span></span> <span data-ttu-id="f6e24-201">Alt ağlar ayarlamadan önce mantıksal akış diyagramı için en iyi uygulamadır ve daha sonra önlemek için güvenlik duvarı kuralları rework.</span><span class="sxs-lookup"><span data-stu-id="f6e24-201">A best practice is to diagram the logical flows before setting up the subnets and firewall rules to avoid rework later.</span></span> <span data-ttu-id="f6e24-202">Aşağıdaki şekilde, bu örnek için güvenlik duvarı kurallarının mantıksal bir görünümdür:</span><span class="sxs-lookup"><span data-stu-id="f6e24-202">The following figure is a logical view of the firewall rules for this example:</span></span>

<span data-ttu-id="f6e24-203">![Güvenlik duvarı kurallarını mantıksal görünümü][2]</span><span class="sxs-lookup"><span data-stu-id="f6e24-203">![Logical View of the Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="f6e24-204">Ağ sanal kullanılan Gereci bağlı olarak, yönetim bağlantı noktalarını değişir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-204">Based on the Network Virtual Appliance used, the management ports will vary.</span></span> <span data-ttu-id="f6e24-205">Barracuda NextGen Firewall başvurulan Bu örnekte, bağlantı noktası 22, 801 ve 807 kullanır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="f6e24-206">Lütfen kullanılan aygıt yönetimi için kullanılan tam bağlantı noktalarını bulmak için Gereci satıcı belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="f6e24-206">Please consult the appliance vendor documentation to find the exact ports used for management of the device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="f6e24-207">Mantıksal kural açıklaması</span><span class="sxs-lookup"><span data-stu-id="f6e24-207">Logical Rule Description</span></span>
<span data-ttu-id="f6e24-208">Mantıksal Yukarıdaki diyagramda, güvenlik alt ağ güvenlik duvarı o alt ağdaki yalnızca kaynak ve bu diyagramda, güvenlik duvarı kuralları ve nasıl bunlar mantıksal olarak izin verme veya trafiği akışı ve gerçek yönlendirilmiş yol değil reddetme gösteren beri gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="f6e24-208">In the logical diagram above, the security subnet is not shown since the firewall is the only resource on that subnet, and this diagram is showing the firewall rules and how they logically allow or deny traffic flows and not the actual routed path.</span></span> <span data-ttu-id="f6e24-209">Ayrıca, RDP trafiğine için daha yüksek seçilen dış bağlantı noktalarını bağlantı noktaları (8014 – 8026) aralıklı ve biraz daha kolay okunabilir olması için yerel IP adresi son iki sekizlisinin hizalamak için seçildi (örneğin yerel sunucu 10.0.1.4 dış bağlantı noktasıyla ilişkili adresidir 8014), ancak daha yüksek herhangi çakışmayan bağlantı noktaları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-209">Also, the external ports selected for the RDP traffic are higher ranged ports (8014 – 8026) and were selected to somewhat align with the last two octets of the local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="f6e24-210">Bu örnek için 7 tür kuralların ihtiyacımız, bu kural türleri aşağıda açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="f6e24-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="f6e24-211">Dış kuralları (için gelen trafiği):</span><span class="sxs-lookup"><span data-stu-id="f6e24-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="f6e24-212">Güvenlik Duvarı Yönetimi kuralı: Bu uygulama yeniden yönlendirme kuralı ağ sanal gereç yönetim bağlantı noktalarına geçirmek trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-212">Firewall Management Rule: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance.</span></span>
  2. <span data-ttu-id="f6e24-213">RDP kuralları (her windows server için): Bu dört kurallar (her sunucu için bir tane) RDP aracılığıyla tek sunucuların Yönetimi izin verir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of the individual servers via RDP.</span></span> <span data-ttu-id="f6e24-214">Bu ayrıca ağ sanal kullanılan gereç özelliklerine bağlı olarak tek bir kural içine paketlenmiş.</span><span class="sxs-lookup"><span data-stu-id="f6e24-214">This could also be bundled into one rule depending on the capabilities of the Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="f6e24-215">Uygulama trafiği kuralları: Ön uç web trafiği için ilk ve ikinci arka uç trafiği (örn. web sunucusu için veri katmanı) için iki uygulama trafiği kuralları vardır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-215">Application Traffic Rules: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span></span> <span data-ttu-id="f6e24-216">Bu kurallar yapılandırmasını (burada, sunucularınızın yerleştirilir) ağ mimarisi bağımlı ve trafik akışları (hangi yönde trafik akışına ve hangi bağlantı noktaları kullanılır).</span><span class="sxs-lookup"><span data-stu-id="f6e24-216">The configuration of these rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="f6e24-217">İlk kural, uygulama sunucusuna ulaşmaya gerçek uygulama trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-217">The first rule will allow the actual application traffic to reach the application server.</span></span> <span data-ttu-id="f6e24-218">Diğer kurallardan izin verirken, güvenlik, yönetim, vb. için uygulama ne harici kullanıcılar ya da hizmetleri uygulamaları erişmesine izin kurallardır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-218">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span></span> <span data-ttu-id="f6e24-219">Bu örnekte, bağlantı noktası 80 üzerinde tek bir web sunucusu yoktur, böylece bir tek uygulama güvenlik duvarını gelen trafiği web sunucuları iç IP adresi için harici IP yönlendirilecek.</span><span class="sxs-lookup"><span data-stu-id="f6e24-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span></span> <span data-ttu-id="f6e24-220">Yeniden yönlendirilen trafiği oturum NAT iç sunucuya sahip.</span><span class="sxs-lookup"><span data-stu-id="f6e24-220">The redirected traffic session would be NAT’d to the internal server.</span></span>
     * <span data-ttu-id="f6e24-221">İkinci uygulama trafik kuralı AppVM01 sunucu (ancak değil AppVM02) için anlaşmak Web sunucusu herhangi bir bağlantı izin vermek için arka uç kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-221">The second Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="f6e24-222">İç kurallardan (içi-VNet trafiği)</span><span class="sxs-lookup"><span data-stu-id="f6e24-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="f6e24-223">Internet kuralı giden: Bu kural seçilen ağlara geçirmek için herhangi bir ağ trafiğinden izin verir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-223">Outbound to Internet Rule: This rule will allow traffic from any network to pass to the selected networks.</span></span> <span data-ttu-id="f6e24-224">Bu genellikle varsayılan bir kural zaten güvenlik duvarında ancak devre dışı durumdayken kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-224">This rule is usually a default rule already on the firewall, but in a disabled state.</span></span> <span data-ttu-id="f6e24-225">Bu kural, bu örnek için etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="f6e24-226">DNS kuralı: Bu kural DNS sunucusuna iletmek yalnızca DNS (bağlantı noktası 53) trafiği sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-226">DNS Rule: This rule allows only DNS (port 53) traffic to pass to the DNS server.</span></span> <span data-ttu-id="f6e24-227">Çoğu trafiğinden ön uç arka uç için engellenen bu ortam için bu kural tüm yerel alt ağ üzerinden DNS özellikle sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-227">For this environment most traffic from the Frontend to the Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="f6e24-228">Alt ağ için alt kuralı: Bu kural, ön uç alt (ancak tersi) herhangi bir sunucuya bağlanmak için arka uç alt ağda herhangi bir sunucu izin vermektir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-228">Subnet to Subnet Rule: This rule is to allow any server on the back end subnet to connect to any server on the front end subnet (but not the reverse).</span></span>
* <span data-ttu-id="f6e24-229">Yedek operatördür kuralı (yukarıdaki birini karşılamıyor trafiği):</span><span class="sxs-lookup"><span data-stu-id="f6e24-229">Fail-safe Rule (for traffic that doesn’t meet any of the above):</span></span>
  1. <span data-ttu-id="f6e24-230">Tüm trafik kuralı Reddet: Bu her zaman son kural (bakımından öncelik) olmalıdır ve trafik akışlarına bu nedenle bu kural tarafından bırakılacak önceki kurallardan herhangi birinin eşleştirmek başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-230">Deny All Traffic Rule: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="f6e24-231">Bu varsayılan bir kural ve genellikle etkin, değişikliğe genellikle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="f6e24-232">İkinci uygulama trafik kuralı üzerinde herhangi bir bağlantı için en belirli bağlantı noktası gerçek bir senaryoda bu örneğin kolay izin verilir ve adres aralıkları, bu kural, saldırı yüzeyini azaltmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-232">On the second application traffic rule, any port is allowed for easy of this example, in a real scenario the most specific port and address ranges should be used to reduce the attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="f6e24-233">Yukarıdaki kurallarda oluşturulduktan sonra trafiğine izin verilen veya istendiği gibi reddedilen emin olmak için her bir kural önceliğini gözden geçirilmesi önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-233">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="f6e24-234">Bu örnekte, öncelik sırasına göre kurallardır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-234">For this example, the rules are in priority order.</span></span> <span data-ttu-id="f6e24-235">Güvenlik Duvarı'nı yanlış sıralı kuralları nedeniyle dışında kilitlenmesi kolaydır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-235">It's easy to be locked out of the firewall due to mis-ordered rules.</span></span> <span data-ttu-id="f6e24-236">En azından, Yönetim güvenlik duvarı kendisi için her zaman mutlak en yüksek öncelik kuralı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f6e24-236">At a minimum, ensure the management for the firewall itself is always the absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="f6e24-237">Kural önkoşulları</span><span class="sxs-lookup"><span data-stu-id="f6e24-237">Rule Prerequisites</span></span>
<span data-ttu-id="f6e24-238">Bir Güvenlik Duvarı'nı çalıştıran sanal makine için önkoşuldur ortak uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="f6e24-238">One prerequisite for the Virtual Machine running the firewall are public endpoints.</span></span> <span data-ttu-id="f6e24-239">Trafiğini işlemek Güvenlik Duvarı için uygun ortak bitiş noktalarının açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-239">For the firewall to process traffic the appropriate public endpoints must be open.</span></span> <span data-ttu-id="f6e24-240">Bu örnekte trafiğin üç tür vardır; Windows sunucuları ve 3) uygulama trafiğini denetlemek için RDP trafiğine 1) yönetim trafiğinin Güvenlik Duvarı'nı Denetim ve güvenlik duvarı kuralları, 2).</span><span class="sxs-lookup"><span data-stu-id="f6e24-240">There are three types of traffic in this example; 1) Management traffic to control the firewall and firewall rules, 2) RDP traffic to control the windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="f6e24-241">Bu üç sütunlar üst trafik türleri üzerinde güvenlik duvarı kuralları mantıksal görünümünü yarısı'dır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-241">These are the three columns of traffic types in the upper half of logical view of the firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6e24-242">Burada anahtar takeway unutmayın vermektir **tüm** trafiğinin güvenlik duvarı üzerinden gelen.</span><span class="sxs-lookup"><span data-stu-id="f6e24-242">A key takeway here is to remember that **all** traffic will come through the firewall.</span></span> <span data-ttu-id="f6e24-243">Bu nedenle IIS01 sunucuya Uzak Masaüstü için ön uç bulut hizmeti ve ön uç alt olmasına rağmen bu sunucuya erişmek için biz RDP için güvenlik duvarı bağlantı noktası 8014 gerekir ve RDP isteği IIS01 RDP Por için dahili olarak yönlendirmek Güvenlik Duvarı'nı izin ver t.</span><span class="sxs-lookup"><span data-stu-id="f6e24-243">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span></span> <span data-ttu-id="f6e24-244">Azure portal'ın "Bağlan" düğmesi olduğundan IIS01 için doğrudan bir RDP yol yok (portal görebilirsiniz uzaklığa kadar) çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f6e24-244">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span></span> <span data-ttu-id="f6e24-245">Bu, Internet'ten gelen tüm bağlantıları güvenlik hizmeti ve bir bağlantı noktası, örneğin secscv001.cloudapp.net:xxxx (başvuru harici bağlantı noktası, iç IP ve bağlantı noktası eşlemesi için yukarıdaki diyagramda) anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-245">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference the above diagram for the mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="f6e24-246">Bir uç nokta ya da VM oluşturma zamanında açılabilir veya yapı örnek komut dosyasında yapılan ve aşağıda bu kod parçacığında gösterildiği gibi post (Not; herhangi bir dolar işareti öğesi başlayarak (örn: $VMName[$i]) olan bir kullanıcı tanımlı değişken başvuru ntüle komut Bu belgenin n.</span><span class="sxs-lookup"><span data-stu-id="f6e24-246">An endpoint can be opened either at the time of VM creation or post build as is done in the example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from the script in the reference section of this document.</span></span> <span data-ttu-id="f6e24-247">Köşeli ayraçlar "$i" [$i] VM'ler dizisi belirli bir VM'de dizi sayısını temsil eder):</span><span class="sxs-lookup"><span data-stu-id="f6e24-247">The “$i” in brackets, [$i], represents the array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="f6e24-248">Değişkenleri, ancak uç noktalar kullanımını, nedeniyle değil açıkça burada gösterilen ancak **yalnızca** güvenlik bulut Hizmeti'ndeki açılır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-248">Although not clearly shown here due to the use of variables, but endpoints are **only** opened on the Security Cloud Service.</span></span> <span data-ttu-id="f6e24-249">Tüm gelen trafiği yönetildiğinden emin olmak için budur (yönlendirilmiş NAT bırakılan) güvenlik duvarı tarafından.</span><span class="sxs-lookup"><span data-stu-id="f6e24-249">This is to ensure that all inbound traffic is handled (routed, NAT'd, dropped) by the firewall.</span></span>

<span data-ttu-id="f6e24-250">Bir yönetim İstemcisi Güvenlik Duvarı'nı yönetmek ve gerekli yapılandırmaları oluşturmak için bir Bilgisayara yüklü gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-250">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span></span> <span data-ttu-id="f6e24-251">Belge, Güvenlik Duvarı (veya diğer NVA) satıcı cihaz yönetme konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="f6e24-251">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span></span> <span data-ttu-id="f6e24-252">Bu bölümde ve sonraki bölümde, güvenlik duvarı kuralları oluşturma, geri kalan güvenlik duvarı yapılandırmasını kendisini satıcılar Yönetimi istemcisi (yani Azure portal veya PowerShell) aracılığıyla anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-252">The remainder of this section and the next section, Firewall Rules Creation, will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span></span>

<span data-ttu-id="f6e24-253">İstemci Yükleme ve bu örnekte kullanılan Barracuda bağlanmak için yönergeler şurada bulunabilir: [Barracuda NG yönetici](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="f6e24-253">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="f6e24-254">Güvenlik Duvarı üzerine ancak güvenlik duvarı kuralları oluşturmadan önce oturum sonra kuralları daha kolay oluşturma yapabilirsiniz iki önkoşul nesne sınıfları vardır; Ağ & hizmeti nesneleri.</span><span class="sxs-lookup"><span data-stu-id="f6e24-254">Once logged onto the firewall but before creating firewall rules, there are two prerequisite object classes that can make creating the rules easier; Network & Service objects.</span></span>

<span data-ttu-id="f6e24-255">Bu örnekte, üç adlandırılmış ağ nesneleri tanımlı (ön uç alt ağ ve DNS sunucusunun IP adresi için de bir ağ nesnesi Backend alt ağı için bir) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-255">For this example, three named network objects should be defined (one for the Frontend subnet and the Backend subnet, also a network object for the IP address of the DNS server).</span></span> <span data-ttu-id="f6e24-256">Adlandırılmış bir ağ oluşturmak için; Barracuda NG yönetici istemci panodan başlayarak, yapılandırma sekmesine gidin, işletimsel yapılandırma bölümünde Ruleset, ardından "Ağlar" altında güvenlik duvarı nesneleri menüsünü tıklatın, ardından yeni Düzenle ağları menüsünde tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f6e24-256">To create a named network; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Networks” under the Firewall Objects menu, then click New in the Edit Networks menu.</span></span> <span data-ttu-id="f6e24-257">Ağ nesnesi artık, adını ve önekini ekleyerek oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="f6e24-257">The network object can now be created, by adding the name and the prefix:</span></span>

<span data-ttu-id="f6e24-258">![Bir ön uç ağ nesnesi oluşturun][3]</span><span class="sxs-lookup"><span data-stu-id="f6e24-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="f6e24-259">Bu ön uç alt ağ için bir adlandırılmış ağ oluşturur, arka uç alt ağ için de benzer bir nesne oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-259">This will create a named network for the FrontEnd subnet, a similar object should be created for the BackEnd subnet as well.</span></span> <span data-ttu-id="f6e24-260">Şimdi alt ağlar güvenlik duvarı kurallarında ada göre daha kolay başvurulabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-260">Now the subnets can be more easily referenced by name in the firewall rules.</span></span>

<span data-ttu-id="f6e24-261">DNS sunucu nesnesi:</span><span class="sxs-lookup"><span data-stu-id="f6e24-261">For the DNS Server Object:</span></span>

<span data-ttu-id="f6e24-262">![Bir DNS sunucusu nesnesi oluşturun][4]</span><span class="sxs-lookup"><span data-stu-id="f6e24-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="f6e24-263">Bu tek IP adresi başvurusu DNS kuralı belgenin devamındaki kullanılmadan.</span><span class="sxs-lookup"><span data-stu-id="f6e24-263">This single IP address reference will be utilized in a DNS rule later in the document.</span></span>

<span data-ttu-id="f6e24-264">İkinci önkoşul nesneleri Hizmetleri nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-264">The second prerequisite objects are Services objects.</span></span> <span data-ttu-id="f6e24-265">Bunlar, her sunucu için RDP bağlantı noktaları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f6e24-265">These will represent the RDP connection ports for each server.</span></span> <span data-ttu-id="f6e24-266">Varolan RDP hizmeti nesnesi varsayılan RDP bağlantı noktasına bağlı olduğundan, 3389, dış bağlantı noktalarını (8014-8026) trafiğine izin verecek şekilde yeni hizmetler oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-266">Since the existing RDP service object is bound to the default RDP port, 3389, new Services can be created to allow traffic from the external ports (8014-8026).</span></span> <span data-ttu-id="f6e24-267">Yeni bağlantı noktaları, varolan RDP hizmeti eklenemedi, ancak tanıtım kolaylığı için her sunucu için tek bir kuralı oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-267">The new ports could also be added to the existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="f6e24-268">Bir sunucu için yeni bir RDP kuralı oluşturmak için; Barracuda NG yönetici istemci panodan başlayarak, yapılandırma sekmesine gidin, işletimsel yapılandırma bölümünde Ruleset, tıklayın ardından "Hizmetler" altında güvenlik duvarı nesneleri menüsünü tıklatın, hizmetlerin listesini kaydırın ve "RDP" hizmetini seçin.</span><span class="sxs-lookup"><span data-stu-id="f6e24-268">To create a new RDP rule for a server; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Services” under the Firewall Objects menu, scroll down the list of services and select the “RDP” service.</span></span> <span data-ttu-id="f6e24-269">Sağ tıklayın ve kopyalayın, sonra sağ tıklatın ve Yapıştır seçin.</span><span class="sxs-lookup"><span data-stu-id="f6e24-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="f6e24-270">Düzenlenebilir bir RDP Copy1 hizmet nesnesi artık yok.</span><span class="sxs-lookup"><span data-stu-id="f6e24-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="f6e24-271">RDP Copy1 sağ tıklatın ve Düzenle, Düzenle hizmet penceresi aşağıda gösterildiği gibi kadar pop nesnesi seçin:</span><span class="sxs-lookup"><span data-stu-id="f6e24-271">Right-click RDP-Copy1 and select Edit, the Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="f6e24-272">![Varsayılan RDP kuralı kopyası][5]</span><span class="sxs-lookup"><span data-stu-id="f6e24-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="f6e24-273">Değerleri, belirli bir sunucu için RDP hizmeti göstermek için sonra düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-273">The values can then be edited to represent the RDP service for a specific server.</span></span> <span data-ttu-id="f6e24-274">AppVM01 için yukarıdaki varsayılan RDP kural yeni hizmet adı, açıklama ve dış RDP Şekil 8 diyagramda kullanılan bağlantı noktası yansıtacak şekilde değiştirilmesi gerekir (Not: bağlantı noktalarını belirli bu sunucu için kullanılan dış bağlantı noktası 3389 RDP varsayılandan değiştirilir söz konusu olduğunda AppVM01 8025 dış bağlantı noktasıdır) değiştirilmiş hizmeti aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f6e24-274">For AppVM01 the above default RDP rule should be modified to reflect a new Service Name, Description, and external RDP Port used in the Figure 8 diagram (Note: the ports are changed from the RDP default of 3389 to the external port being used for this specific server, in the case of AppVM01 the external Port is 8025) the modified service is shown below:</span></span>

<span data-ttu-id="f6e24-275">![AppVM01 kuralı][6]</span><span class="sxs-lookup"><span data-stu-id="f6e24-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="f6e24-276">Geri kalan sunucular için RDP hizmetleri oluşturmak için bu işlemin yinelenmesi gerekir; AppVM02, DNS01 ve IIS01.</span><span class="sxs-lookup"><span data-stu-id="f6e24-276">This process must be repeated to create RDP Services for the remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="f6e24-277">Bu hizmetler oluşturma kuralı oluşturmayı daha basit ve daha belirgin sonraki bölümde hale getirir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-277">The creation of these Services will make the Rule creation simpler and more obvious in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="f6e24-278">Bir RDP Hizmeti Güvenlik Duvarı için iki nedenden dolayı gerekli değildir; 1) ilk VM Güvenlik Duvarı olduğundan Linux tabanlı görüntü SSH tanesi kullanılacak bağlantı noktası 22 RDP ve 2) bağlantı noktası 22 yerine VM yönetimi ve diğer yönetim bağlantı noktalarına iki Yönetim bağlantısı için aşağıda açıklanan ilk yönetim kuraldaki izin verilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-278">An RDP service for the Firewall is not needed for two reasons; 1) first the firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in the first management rule described below to allow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="f6e24-279">Güvenlik duvarı kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="f6e24-279">Firewall Rules Creation</span></span>
<span data-ttu-id="f6e24-280">Bu örnekte kullanılan güvenlik duvarı kuralları üç tür vardır, hepsinin ayrı simgeler vardır:</span><span class="sxs-lookup"><span data-stu-id="f6e24-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="f6e24-281">Uygulama yeniden yönlendirme kuralı: ![uygulama yeniden yönlendirme simgesi][7]</span><span class="sxs-lookup"><span data-stu-id="f6e24-281">The Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="f6e24-282">Hedef NAT kuralı: ![hedef NAT simgesi][8]</span><span class="sxs-lookup"><span data-stu-id="f6e24-282">The Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="f6e24-283">Geçişi kuralı: ![geçirmek simgesi][9]</span><span class="sxs-lookup"><span data-stu-id="f6e24-283">The Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="f6e24-284">Bu kural hakkında daha fazla bilgi Barracuda web sitesinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-284">More information on these rules can be found at the Barracuda web site.</span></span>

<span data-ttu-id="f6e24-285">Aşağıdaki kuralları oluşturun (veya var olan varsayılan kuralları doğrulamak için), Barracuda NG yönetici istemci panodan başlangıç yapılandırma sekmesine gidin, işletimsel yapılandırmasında bölüm Ruleset tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f6e24-285">To create the following rules (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="f6e24-286">Adlı bir kılavuz "Ana kuralları" varolan etkin ve devre dışı bırakılan kuralları bu Güvenlik Duvarı'nı gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-286">A grid called, “Main Rules” will show the existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="f6e24-287">Bu kılavuz sağ üst köşesindeki olan küçük, yeşil "+" düğmesini tıklatın, yeni bir kural oluşturmak için burayı tıklatın (Not: güvenlik duvarını "değişiklikleri kilitlenebilir", görürseniz bir düğme "Kilit" olarak işaretlenmiş ve oluşturmak veya kuralları düzenlemek için "kural kümesi kilidini açmak için" Bu düğmeye tıklayın sorunu yaşıyor ve  düzenlenmesine izin verilir).</span><span class="sxs-lookup"><span data-stu-id="f6e24-287">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the rule set and allow editing).</span></span> <span data-ttu-id="f6e24-288">Varolan bir kuralı düzenlemek istiyorsanız, o kural seçin, sağ tıklayın ve kuralını Düzenle seçin.</span><span class="sxs-lookup"><span data-stu-id="f6e24-288">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="f6e24-289">Kurallarınızı oluşturulan ve/veya değiştirilmiş, bunlar Güvenlik Duvarı'na gönderilen ve gerekir etkinleştirildiğinden, bu değil yapıldığında kural değişiklikler etkili olmaz.</span><span class="sxs-lookup"><span data-stu-id="f6e24-289">Once your rules are created and/or modified, they must be pushed to the firewall and then activated, if this is not done the rule changes will not take effect.</span></span> <span data-ttu-id="f6e24-290">Anında iletme ve etkinleştirme sürecini ayrıntıları kural açıklamaları açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-290">The push and activation process is described below the details rule descriptions.</span></span>

<span data-ttu-id="f6e24-291">Bu örnek tamamlamak için gereken her bir kural ayrıntılarını aşağıda açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="f6e24-291">The specifics of each rule required to complete this example are described as follows:</span></span>

* <span data-ttu-id="f6e24-292">**Güvenlik Duvarı yönetimi kural**: Bu uygulama yeniden yönlendirme kuralı trafiğin Bu örnekte ağ sanal gerecin yönetim noktalarına Barracuda NextGen Firewall geçmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-292">**Firewall Management Rule**: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="f6e24-293">Yönetim bağlantı noktalarını 801, 807 ve isteğe bağlı olarak 22 ' dir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-293">The management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="f6e24-294">İç ve dış bağlantı noktaları (yani hiçbir bağlantı noktası çevirisi) aynıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-294">The external and internal ports are the same (i.e. no port translation).</span></span> <span data-ttu-id="f6e24-295">Bu kural, Kurulum MGMT erişim, varsayılan bir kural ve varsayılan (olarak Barracuda NextGen Firewall sürüm 6.1) etkinleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="f6e24-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="f6e24-296">![Güvenlik Duvarı Yönetimi kuralı][10]</span><span class="sxs-lookup"><span data-stu-id="f6e24-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="f6e24-297">Bu kuralın kaynak adres alanı, olan Yönetim IP adres aralıklarını biliniyorsa, bu kapsamı azaltma ayrıca yönetim bağlantı noktalarına saldırı yüzeyini azaltmak.</span><span class="sxs-lookup"><span data-stu-id="f6e24-297">The source address space in this rule is Any, if the management IP address ranges are known, reducing this scope would also reduce the attack surface to the management ports.</span></span>
> 
> 

* <span data-ttu-id="f6e24-298">**RDP kuralları**: Bu hedef NAT kuralları izin ver RDP aracılığıyla tek sunucuların yönetimi.</span><span class="sxs-lookup"><span data-stu-id="f6e24-298">**RDP Rules**:  These Destination NAT rules will allow management of the individual servers via RDP.</span></span>
  <span data-ttu-id="f6e24-299">Bu kuralı oluşturmak için gereken dört önemli alanlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f6e24-299">There are four critical fields needed to create this rule:</span></span>
  
  1. <span data-ttu-id="f6e24-300">RDP yerden, başvuru "Herhangi bir" izin vermek için kaynak – kaynak alanında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-300">Source – to allow RDP from anywhere, the reference “Any” is used in the Source field.</span></span>
  2. <span data-ttu-id="f6e24-301">Dış bağlantı noktalarını sunucuları yerel IP adresi ve bağlantı noktası 3386 (varsayılan RDP bağlantı noktası) için yeniden yönlendirme, hizmeti – bu durumda "AppVM01 RDP" daha önce oluşturduğunuz uygun hizmet nesnesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f6e24-301">Service – use the appropriate Service Object created earlier, in this case “AppVM01 RDP”, the external ports redirect to the servers local IP address and to port 3386 (the default RDP port).</span></span> <span data-ttu-id="f6e24-302">Bu belirli AppVM01 RDP erişim kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-302">This specific rule is for RDP access to AppVM01.</span></span>
  3. <span data-ttu-id="f6e24-303">Hedef – olmalıdır *Güvenlik Duvarı'nda yerel bağlantı noktası*, "DCHP 1 yerel IP" ya da statik IP kullanıyorsanız eth0.</span><span class="sxs-lookup"><span data-stu-id="f6e24-303">Destination – should be the *local port on the firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="f6e24-304">Sıra numarasını (eth0, eth1, vb.), ağ Gereci birden çok yerel arabirimi varsa, farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-304">The ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="f6e24-305">Bu güvenlik duvarı olduğundan göndermesinin giden bağlantı noktasıdır (alıcı bağlantı noktası ile aynı olabilir), gerçek yönlendirilmiş hedef hedef listesi alanıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-305">This is the port the firewall is sending out from (may be the same as the receiving port), the actual routed destination is in the Target List field.</span></span>
  4. <span data-ttu-id="f6e24-306">Yeniden yönlendirme – bu bölümün sonunda bu trafiği yönlendirmek nereye sanal gereç bildirir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-306">Redirection – this section tells the virtual appliance where to ultimately redirect this traffic.</span></span> <span data-ttu-id="f6e24-307">En basit yeniden yönlendirme IP ve bağlantı noktası (isteğe bağlı) hedef listesi alanında yerleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-307">The simplest redirection is to place the IP and Port (optional) in the Target List field.</span></span> <span data-ttu-id="f6e24-308">Hiçbir bağlantı noktası kullanılıyorsa, hedef bağlantı noktası gelen istekte olacaktır (IE hiçbir çevirisi), bir bağlantı noktası bağlantı noktası belirlendiyse kullanılan de NAT yanı sıra IP adresi olur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-308">If no port is used the destination port on the inbound request will be used (ie no translation), if a port is designated the port will also be NAT’d along with the IP address.</span></span>
     
     <span data-ttu-id="f6e24-309">![Güvenlik Duvarı RDP kuralı][11]</span><span class="sxs-lookup"><span data-stu-id="f6e24-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="f6e24-310">Dört RDP kuralları toplam oluşturulması gerekecektir:</span><span class="sxs-lookup"><span data-stu-id="f6e24-310">A total of four RDP rules will need to be created:</span></span> 
     
     | <span data-ttu-id="f6e24-311">Kural Adı</span><span class="sxs-lookup"><span data-stu-id="f6e24-311">Rule Name</span></span> | <span data-ttu-id="f6e24-312">Sunucu</span><span class="sxs-lookup"><span data-stu-id="f6e24-312">Server</span></span> | <span data-ttu-id="f6e24-313">Hizmet</span><span class="sxs-lookup"><span data-stu-id="f6e24-313">Service</span></span> | <span data-ttu-id="f6e24-314">Hedef listesi</span><span class="sxs-lookup"><span data-stu-id="f6e24-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="f6e24-315">RDP IIS01</span><span class="sxs-lookup"><span data-stu-id="f6e24-315">RDP-to-IIS01</span></span> |<span data-ttu-id="f6e24-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="f6e24-316">IIS01</span></span> |<span data-ttu-id="f6e24-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="f6e24-317">IIS01 RDP</span></span> |<span data-ttu-id="f6e24-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="f6e24-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="f6e24-319">RDP DNS01</span><span class="sxs-lookup"><span data-stu-id="f6e24-319">RDP-to-DNS01</span></span> |<span data-ttu-id="f6e24-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="f6e24-320">DNS01</span></span> |<span data-ttu-id="f6e24-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="f6e24-321">DNS01 RDP</span></span> |<span data-ttu-id="f6e24-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="f6e24-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="f6e24-323">RDP AppVM01</span><span class="sxs-lookup"><span data-stu-id="f6e24-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="f6e24-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="f6e24-324">AppVM01</span></span> |<span data-ttu-id="f6e24-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="f6e24-325">AppVM01 RDP</span></span> |<span data-ttu-id="f6e24-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="f6e24-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="f6e24-327">RDP AppVM02</span><span class="sxs-lookup"><span data-stu-id="f6e24-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="f6e24-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="f6e24-328">AppVM02</span></span> |<span data-ttu-id="f6e24-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="f6e24-329">AppVm02 RDP</span></span> |<span data-ttu-id="f6e24-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="f6e24-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="f6e24-331">Kaynak ve hizmet alanların kapsamını daraltma saldırı yüzeyini azaltır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-331">Narrowing down the scope of the Source and Service fields will reduce the attack surface.</span></span> <span data-ttu-id="f6e24-332">İşlevselliği sağlayacak en sınırlı kapsam kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-332">The most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="f6e24-333">**Uygulama trafik kurallarını**: ön uç web trafiği için ilk ve ikinci arka uç trafiği (örn. web sunucusu için veri katmanı) için iki uygulama trafiği kuralları vardır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-333">**Application Traffic Rules**: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span></span> <span data-ttu-id="f6e24-334">Bu kurallar (burada, sunucularınızın yerleştirilir) ağ mimarisine göre değişir ve trafik akışları (hangi yönde trafik akışına ve hangi bağlantı noktaları kullanılır).</span><span class="sxs-lookup"><span data-stu-id="f6e24-334">These rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="f6e24-335">Önce ele alınan web trafiği için ön uç kuralı gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f6e24-335">First discussed is the front end rule for web traffic:</span></span>
  
    <span data-ttu-id="f6e24-336">![Güvenlik Duvarı Web kuralı][12]</span><span class="sxs-lookup"><span data-stu-id="f6e24-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="f6e24-337">Bu hedef NAT kuralı uygulama sunucusuna ulaşmaya gerçek uygulama trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-337">This Destination NAT rule allows the actual application traffic to reach the application server.</span></span> <span data-ttu-id="f6e24-338">Diğer kurallardan izin verirken, güvenlik, yönetim, vb. için uygulama ne harici kullanıcılar ya da hizmetleri uygulamaları erişmesine izin kurallardır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-338">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span></span> <span data-ttu-id="f6e24-339">Bu örnekte, bağlantı noktası 80 üzerinde tek bir web sunucusu yok, bu nedenle tek uygulama güvenlik duvarını gelen trafiği web sunucuları iç IP adresi için harici IP yönlendirilecek.</span><span class="sxs-lookup"><span data-stu-id="f6e24-339">For this example, there is a single web server on port 80, thus the single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span></span>
  
    <span data-ttu-id="f6e24-340">**Not**: hedef listesi alanına atanan bağlantı noktası yok, bu nedenle gelen bağlantı noktası 80 (veya seçili hizmeti için 443) web sunucusu yeniden yönlendirilmesini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-340">**Note**: that there is no port assigned in the Target List field, thus the inbound port 80 (or 443 for the Service selected) will be used in the redirection of the web server.</span></span> <span data-ttu-id="f6e24-341">Web sunucusu farklı bir bağlantı noktasında dinleme yapıyorsanız, örneğin 8080 bağlantı noktası, 10.0.1.4:8080 de bağlantı noktası yönlendirmeye izin vermek için hedef liste alanı güncelleştirilemedi.</span><span class="sxs-lookup"><span data-stu-id="f6e24-341">If the web server is listening on a different port, for example port 8080, the Target List field could be updated to 10.0.1.4:8080 to allow for the Port redirection as well.</span></span>
  
    <span data-ttu-id="f6e24-342">Sonraki uygulama trafik kuralı AppVM01 sunucu (ancak değil AppVM02) için anlaşmak Web sunucusu herhangi bir hizmeti izin vermek için arka uç kuralı gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f6e24-342">The next Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="f6e24-343">![Güvenlik Duvarı AppVM01 kuralı][13]</span><span class="sxs-lookup"><span data-stu-id="f6e24-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="f6e24-344">Bu geçiş kuralı herhangi bir IIS sunucusuna AppVM01 ulaşmak için ön uç alt ağda verir (IP adresi 10.0.2.5) herhangi bir bağlantı üzerinde web uygulaması tarafından gerekli verilere erişmek için herhangi bir iletişim kuralı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f6e24-344">This Pass rule allows any IIS server on the Frontend subnet to reach the AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol to access data needed by the web application.</span></span>
  
    <span data-ttu-id="f6e24-345">Bu ekran görüntüsü, bir "\<taşınmaya açık\>" 10.0.2.5 hedef olarak belirtmek için hedef alanındaki değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-345">In this screen shot an "\<explicit-dest\>" is used in the Destination field to signify 10.0.2.5 as the destination.</span></span> <span data-ttu-id="f6e24-346">Bu şunlardan biri olabilir gösterildiği gibi veya açık adlı ağ (DNS sunucusu için Önkoşullar'da yapıldığı gibi) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f6e24-346">This could be either explicit as shown or a named Network Object (as was done in the prerequisites for the DNS server).</span></span> <span data-ttu-id="f6e24-347">Bu toplayıcınızın yöntemi kullanılacak Güvenlik Duvarı'nın kadar yöneticisidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-347">This is up to the administrator of the firewall as to which method will be used.</span></span> <span data-ttu-id="f6e24-348">Altına boş bir ilk satır 10.0.2.5 Explict Desitnation eklemek için çift \<taşınmaya açık\> ve açılır penceresinde adresini girin.</span><span class="sxs-lookup"><span data-stu-id="f6e24-348">To add 10.0.2.5 as an Explict Desitnation, double-click on the first blank row under \<explicit-dest\> and enter the address in the window that pops up.</span></span>
  
    <span data-ttu-id="f6e24-349">Böylece bağlantı yöntemi "No SNAT" ayarlayabilirsiniz bu dahili trafiği olduğundan geçirmek bu kural, NAT gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-349">With this Pass Rule, no NAT is needed since this is internal traffic, so the Connection Method can be set to "No SNAT".</span></span>
  
    <span data-ttu-id="f6e24-350">**Not**: Bu kural kaynak ağında olan herhangi bir kaynak yalnızca olacaksa bir veya web sunucuları, bilinen belirli sayıda ön uç alt ağda, ağ nesnesi kaynak tüm ön uç alt ağa yerine tam bu IP adreslerine daha belirgin oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-350">**Note**: The Source network in this rule is any resource on the FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created to be more specific to those exact IP addresses instead of the entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="f6e24-351">Bu kural hizmet "Herhangi" örnek uygulama kullanması daha kolay hale getirmek için kullanır, bu da Icmpv4 izin verir (ping) tek bir kural.</span><span class="sxs-lookup"><span data-stu-id="f6e24-351">This rule uses the service “Any” to make the sample application easier to setup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="f6e24-352">Ancak, önerilen bir uygulama değildir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="f6e24-353">Bağlantı noktalarını ve protokolleri ("Hizmetler") uygulama işlemi bu sınır saldırı yüzeyini küçültmek sağlayan en olası daraltıldığı.</span><span class="sxs-lookup"><span data-stu-id="f6e24-353">The ports and protocols (“Services”) should be narrowed to the minimum possible that allows application operation to reduce the attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="f6e24-354">Bu kural kullanılan bir hedef açık başvuru gösterir, ancak tutarlı bir yaklaşım güvenlik duvarı yapılandırmasında kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout the firewall configuration.</span></span> <span data-ttu-id="f6e24-355">Adlandırılmış ağ nesnesi boyunca daha kolay okunabilirlik ve desteklenebilirlik için kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-355">It is recommended that the named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="f6e24-356">Açık-taşınmaya burada yalnızca bir alternatif başvuru yöntemi göstermek için kullanılır ve (özellikle karmaşık yapılandırmalar için) genellikle önerilmez.</span><span class="sxs-lookup"><span data-stu-id="f6e24-356">The explicit-dest is used here only to show an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="f6e24-357">**Internet kuralı giden**: Bu geçirmek kuralı izin ver seçili hedef ağlara geçirmek için herhangi bir kaynak ağ trafiği.</span><span class="sxs-lookup"><span data-stu-id="f6e24-357">**Outbound to Internet Rule**: This Pass rule will allow traffic from any Source network to pass to the selected Destination networks.</span></span> <span data-ttu-id="f6e24-358">Bu kural varsayılan bir kural zaten genellikle Barracuda NextGen Güvenlik Duvarı'nda olmakla birlikte, devre dışı durumda.</span><span class="sxs-lookup"><span data-stu-id="f6e24-358">This rule is a default rule usually already on the Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="f6e24-359">Bu kurala sağ etkinleştirme kural komutu erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6e24-359">Right-clicking on this rule can access the Activate Rule command.</span></span> <span data-ttu-id="f6e24-360">Burada gösterilen kural, bu kural kaynak özniteliği için bu belgenin önkoşul bölümüne başvurular olarak oluşturulan iki yerel alt ağlar eklemek için değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="f6e24-360">The rule shown here has been modified to add the two local subnets that were created as references in the prerequisite section of this document to the Source attribute of this rule.</span></span>
  
    <span data-ttu-id="f6e24-361">![Giden güvenlik duvarı kuralı][14]</span><span class="sxs-lookup"><span data-stu-id="f6e24-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="f6e24-362">**DNS kuralı**: Bu geçirmek kural DNS sunucusuna iletmek yalnızca DNS (bağlantı noktası 53) trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic to pass to the DNS server.</span></span> <span data-ttu-id="f6e24-363">Bu kural, çoğu trafiğinden ön uç arka uç için engellenen bu ortam için DNS özellikle sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-363">For this environment most traffic from the FrontEnd to the BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="f6e24-364">![Güvenlik Duvarı DNS kuralı][15]</span><span class="sxs-lookup"><span data-stu-id="f6e24-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="f6e24-365">**Not**: Bu ekran görüntüsü bağlantı yöntemi bulunur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-365">**Note**: In this screen shot the Connection Method is included.</span></span> <span data-ttu-id="f6e24-366">Bu kural, iç IP adresi trafiği iç IP olduğundan, hiçbir NATing gerekli değildir, bu bağlantı yöntemi için bu geçişi kuralı "No SNAT" ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-366">Because this rule is for internal IP to internal IP address traffic, no NATing is required, this the Connection Method is set to “No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="f6e24-367">**Alt ağ için alt kural**: Bu geçirmek etkinleştirildi ve ön uç alt ağda herhangi bir sunucuya bağlanmak için arka uç alt ağda herhangi bir sunucu izin vermek için değiştirilen varsayılan bir kural kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-367">**Subnet to Subnet Rule**: This Pass rule is a default rule that has been activated and modified to allow any server on the back end subnet to connect to any server on the front end subnet.</span></span> <span data-ttu-id="f6e24-368">Bu kural tüm iç trafiği olduğundan, bağlantı yöntemi için Hayır SNAT ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-368">This rule is all internal traffic so the Connection Method can be set to No SNAT.</span></span>
  
    <span data-ttu-id="f6e24-369">![Güvenlik Duvarı içi sanal ağ kuralı][16]</span><span class="sxs-lookup"><span data-stu-id="f6e24-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="f6e24-370">**Not**: çift yönlü onay kutusu işaretli (veya, çoğu kurallarında işaretli değil), bu "tek yönlü" kural sağlar, bu kural için önemli budur, ön uç ağ ancak ters arka uç alt ağından bağlantı başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-370">**Note**: The Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from the back end subnet to the front end network, but not the reverse.</span></span> <span data-ttu-id="f6e24-371">Bu onay kutusu işaretli değilse bu kural bizim mantıksal diyagramdan istenmediği çift yönlü trafiği etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="f6e24-372">**Reddetme tüm trafik kuralı**: Bu her zaman son bir kural (bakımından öncelik) olmalıdır ve trafik herhangi biriyle eşleşen başarısız akışlar, bu nedenle önceki onu bırakılacak bu kural tarafından kuralları.</span><span class="sxs-lookup"><span data-stu-id="f6e24-372">**Deny All Traffic Rule**: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="f6e24-373">Bu varsayılan bir kural ve genellikle etkin, değişikliğe genellikle gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="f6e24-374">![Güvenlik duvarı kuralı Reddet][17]</span><span class="sxs-lookup"><span data-stu-id="f6e24-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6e24-375">Yukarıdaki kurallarda oluşturulduktan sonra trafiğine izin verilen veya istendiği gibi reddedilen emin olmak için her bir kural önceliğini gözden geçirilmesi önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-375">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="f6e24-376">Bu örnekte, Barracuda Management istemcisi kurallarında iletme, ana kılavuzunda görünmesi gereken sırayla kurallardır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-376">For this example, the rules are in the order they should appear in the Main Grid of forwarding rules in the Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="f6e24-377">Kural etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f6e24-377">Rule Activation</span></span>
<span data-ttu-id="f6e24-378">Mantığı diyagramı belirtimi değiştiren ruleset ile ruleset Güvenlik Duvarı'na karşıya ve sonra etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-378">With the ruleset modified to the specification of the logic diagram, the ruleset must be uploaded to the firewall and then activated.</span></span>

<span data-ttu-id="f6e24-379">![Güvenlik duvarı kuralını etkinleştirme][18]</span><span class="sxs-lookup"><span data-stu-id="f6e24-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="f6e24-380">Yönetim istemcisi üst sağ alt köşesindeki düğmeleri oluşan bir küme var.</span><span class="sxs-lookup"><span data-stu-id="f6e24-380">In the upper right hand corner of the management client are a cluster of buttons.</span></span> <span data-ttu-id="f6e24-381">Değiştirilen kuralları Güvenlik Duvarı'na göndermek için "Değişiklikleri Gönder" düğmesini tıklatın, ardından "Etkinleştir" düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f6e24-381">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span></span>

<span data-ttu-id="f6e24-382">Güvenlik Duvarı ruleset etkinleştirme ile bu örnek ortamı yapı tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-382">With the activation of the firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="f6e24-383">Trafik senaryoları</span><span class="sxs-lookup"><span data-stu-id="f6e24-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f6e24-384">Bir anahtar takeway unutmayın vermektir **tüm** trafiğinin güvenlik duvarı üzerinden gelen.</span><span class="sxs-lookup"><span data-stu-id="f6e24-384">A key takeway is to remember that **all** traffic will come through the firewall.</span></span> <span data-ttu-id="f6e24-385">Bu nedenle IIS01 sunucuya Uzak Masaüstü için ön uç bulut hizmeti ve ön uç alt olmasına rağmen bu sunucuya erişmek için biz RDP için güvenlik duvarı bağlantı noktası 8014 gerekir ve RDP isteği IIS01 RDP Por için dahili olarak yönlendirmek Güvenlik Duvarı'nı izin ver t.</span><span class="sxs-lookup"><span data-stu-id="f6e24-385">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span></span> <span data-ttu-id="f6e24-386">Azure portal'ın "Bağlan" düğmesi olduğundan IIS01 için doğrudan bir RDP yol yok (portal görebilirsiniz uzaklığa kadar) çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f6e24-386">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span></span> <span data-ttu-id="f6e24-387">Bu, Internet'ten gelen tüm bağlantıları güvenlik hizmeti ve bağlantı noktası, örneğin secscv001.cloudapp.net:xxxx anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-387">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="f6e24-388">Bu senaryolar için aşağıdaki güvenlik duvarı kuralları yerinde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="f6e24-388">For these scenarios, the following firewall rules should be in place:</span></span>

1. <span data-ttu-id="f6e24-389">Güvenlik Duvarı Yönetimi</span><span class="sxs-lookup"><span data-stu-id="f6e24-389">Firewall Management</span></span>
2. <span data-ttu-id="f6e24-390">RDP IIS01 için</span><span class="sxs-lookup"><span data-stu-id="f6e24-390">RDP to IIS01</span></span>
3. <span data-ttu-id="f6e24-391">RDP DNS01 için</span><span class="sxs-lookup"><span data-stu-id="f6e24-391">RDP to DNS01</span></span>
4. <span data-ttu-id="f6e24-392">RDP AppVM01 için</span><span class="sxs-lookup"><span data-stu-id="f6e24-392">RDP to AppVM01</span></span>
5. <span data-ttu-id="f6e24-393">RDP AppVM02 için</span><span class="sxs-lookup"><span data-stu-id="f6e24-393">RDP to AppVM02</span></span>
6. <span data-ttu-id="f6e24-394">Web uygulaması trafiği</span><span class="sxs-lookup"><span data-stu-id="f6e24-394">App Traffic to the Web</span></span>
7. <span data-ttu-id="f6e24-395">AppVM01 uygulama trafiği</span><span class="sxs-lookup"><span data-stu-id="f6e24-395">App Traffic to AppVM01</span></span>
8. <span data-ttu-id="f6e24-396">Giden internet</span><span class="sxs-lookup"><span data-stu-id="f6e24-396">Outbound to the Internet</span></span>
9. <span data-ttu-id="f6e24-397">DNS01 için ön uç</span><span class="sxs-lookup"><span data-stu-id="f6e24-397">Frontend to DNS01</span></span>
10. <span data-ttu-id="f6e24-398">İçi alt ağ trafiği (yalnızca ön uç için arka uç)</span><span class="sxs-lookup"><span data-stu-id="f6e24-398">Intra-Subnet Traffic (back end to front end only)</span></span>
11. <span data-ttu-id="f6e24-399">Tümünü Reddet</span><span class="sxs-lookup"><span data-stu-id="f6e24-399">Deny All</span></span>

<span data-ttu-id="f6e24-400">Gerçek güvenlik duvarı ruleset büyük olasılıkla bu ek olarak birçok diğer kurallar vardır, belirli bir güvenlik duvarı kurallarında farklı öncelik numaraları burada listelenenlerden daha da sahip olur.</span><span class="sxs-lookup"><span data-stu-id="f6e24-400">The actual firewall ruleset will most likely have many other rules in addition to these, the rules on any given firewall will also have different priority numbers than the ones listed here.</span></span> <span data-ttu-id="f6e24-401">Bu liste ve ilişkili numaralar on bu kurallar ve bunları arasında göreli öncelik arasında uygunluk sağlamak üzeresiniz.</span><span class="sxs-lookup"><span data-stu-id="f6e24-401">This list and associated numbers are to provide relevance between just these eleven rules and the relative priority amongst them.</span></span> <span data-ttu-id="f6e24-402">Diğer bir deyişle; Gerçek Güvenlik Duvarı'nı 5 kural sayısı olabilir, ancak "Güvenlik duvarı Yönetimi" kuralıdır ve "RDP için DNS01" kural amacıyla bu listeyi hizalayın sürece "RDP için IIS01" olabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-402">In other words; on the actual firewall, the “RDP to IIS01” may be rule number 5, but as long as it’s below the “Firewall Management” rule and above the “RDP to DNS01” rule it would align with the intention of this list.</span></span> <span data-ttu-id="f6e24-403">Listenin içinde de yardımcı olur kısaltma; izin verme senaryolar aşağıda Örneğin "FW kuralı 9 (DNS)".</span><span class="sxs-lookup"><span data-stu-id="f6e24-403">The list will also aid in the below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="f6e24-404">Ayrıca okumanızdır dört RDP kuralları topluca çağrılır, "RDP kuralları" trafik senaryo olduğunda için RDP ilgisiz.</span><span class="sxs-lookup"><span data-stu-id="f6e24-404">Also for brevity, the four RDP rules will be collectively called, “the RDP rules” when the traffic scenario is unrelated to RDP.</span></span>

<span data-ttu-id="f6e24-405">Ayrıca ağ güvenlik grupları yerinde geri çağırma ön uç ve arka uç ağlardaki gelen Internet trafiği için.</span><span class="sxs-lookup"><span data-stu-id="f6e24-405">Also recall that Network Security Groups are in-place for inbound internet traffic on the Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="f6e24-406">(İzin verilir) Web sunucusuna Internet</span><span class="sxs-lookup"><span data-stu-id="f6e24-406">(Allowed) Internet to Web Server</span></span>
1. <span data-ttu-id="f6e24-407">Internet kullanıcı istekleri HTTP sayfasına SecSvc001.CloudApp.Net (Internet'e yönelik bulut hizmeti)</span><span class="sxs-lookup"><span data-stu-id="f6e24-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="f6e24-408">Bulut hizmeti geçiş trafiği 80 numaralı bağlantı noktasında güvenlik duvarı arabiriminizi 10.0.0.4:80 üzerinde açık uç noktası aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="f6e24-408">Cloud service passes traffic through open endpoint on port 80 to firewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="f6e24-409">Güvenlik alt ağına atanmış hiçbir NSG bunu sistem NSG kuralları güvenlik duvarı trafiğine izin verecek.</span><span class="sxs-lookup"><span data-stu-id="f6e24-409">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span></span>
4. <span data-ttu-id="f6e24-410">İç IP adresi (10.0.1.4) Güvenlik Duvarı'nın trafik isabetler</span><span class="sxs-lookup"><span data-stu-id="f6e24-410">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="f6e24-411">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="f6e24-412">FW kural 1'i (FW Mgmt) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-412">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="f6e24-413">FW kuralları 2-5 (RDP kurallar) yok, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="f6e24-414">FW kural 6 (uygulama: Web) uygulama trafiğine izin verilir, güvenlik duvarı NAT 10.0.1.4 (IIS01) için</span><span class="sxs-lookup"><span data-stu-id="f6e24-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it to 10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="f6e24-415">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-415">The Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f6e24-416">NSG kural 1'i (blok Internet) olmayan uygulama (Bu trafiği NAT oluştu güvenlik duvarı tarafından gerekir, böylece kaynak adresi şimdi güvenlik alt ağ üzerinde olan güvenlik duvarı ve ön uç alt ağa göre NSG "yerel" trafiği olarak görülen ve böylece izin), sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Frontend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span></span>
   2. <span data-ttu-id="f6e24-417">Varsayılan NSG kuralları alt ağ için alt ağ trafiğine izin verme, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="f6e24-417">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="f6e24-418">IIS01 web trafiği için dinleme, bu isteği alır ve isteği işlemeye başlıyor</span><span class="sxs-lookup"><span data-stu-id="f6e24-418">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
8. <span data-ttu-id="f6e24-419">IIS01 girişimleri AppVM01 arka uç alt ağdaki bir FTP oturumu başlatır</span><span class="sxs-lookup"><span data-stu-id="f6e24-419">IIS01 attempts to initiates an FTP session to AppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="f6e24-420">Ön uç alt ağdaki UDR rota güvenlik duvarı sonraki atlama yapar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-420">The UDR route on Frontend subnet makes the firewall the next hop</span></span>
10. <span data-ttu-id="f6e24-421">Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="f6e24-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="f6e24-422">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="f6e24-423">FW kural 1'i (FW Mgmt) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-423">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="f6e24-424">FW kuralı 2-5 (RDP kurallar) yok, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
    3. <span data-ttu-id="f6e24-425">FW kural 6 (uygulama: Web) geçerli değil, sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-425">FW Rule 6 (App: Web) doesn’t apply, move to next rule</span></span>
    4. <span data-ttu-id="f6e24-426">FW kural 7 ' (uygulama: arka uç) uygulama trafiğine izin verilir, güvenlik duvarı 10.0.2.5 (AppVM01) trafiği iletir</span><span class="sxs-lookup"><span data-stu-id="f6e24-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="f6e24-427">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-427">The Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f6e24-428">NSG kural 1'i (blok Internet) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-428">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="f6e24-429">Varsayılan NSG kuralları alt ağ için alt ağ trafiğine izin verme, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="f6e24-429">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="f6e24-430">AppVM01 isteği alır ve oturumu başlatır ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="f6e24-430">AppVM01 receives the request and initiates the session and responds</span></span>
14. <span data-ttu-id="f6e24-431">Arka uç alt ağdaki UDR rota güvenlik duvarı sonraki atlama yapar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-431">The UDR route on Backend subnet makes the firewall the next hop</span></span>
15. <span data-ttu-id="f6e24-432">Yanıt izin arka uç alt ağda giden hiçbir NSG kuralları olduğundan</span><span class="sxs-lookup"><span data-stu-id="f6e24-432">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span></span>
16. <span data-ttu-id="f6e24-433">Bu yerleşik bir oturum üzerinde trafiği döndürmektir çünkü güvenlik duvarı yanıtı web sunucusu (IIS01) geçirir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-433">Because this is returning traffic on an established session the firewall passes the response back to the web server (IIS01)</span></span>
17. <span data-ttu-id="f6e24-434">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f6e24-435">NSG kural 1'i (blok Internet) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-435">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="f6e24-436">Varsayılan NSG kuralları alt ağ için alt ağ trafiğine izin verme, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="f6e24-436">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="f6e24-437">IIS Sunucu yanıtı alır, AppVM01 işlemle tamamlandıktan ve HTTP yanıtı oluşturma tamamlandıktan, istek sahibine gönderilen bu HTTP yanıtı</span><span class="sxs-lookup"><span data-stu-id="f6e24-437">The IIS server receives the response, completes the transaction with AppVM01, and then completes building the HTTP response, this HTTP response is sent to the requestor</span></span>
19. <span data-ttu-id="f6e24-438">Yanıt izin verilen ön uç alt ağda giden hiçbir NSG kuralları olduğundan</span><span class="sxs-lookup"><span data-stu-id="f6e24-438">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span></span>
20. <span data-ttu-id="f6e24-439">HTTP yanıtı güvenlik duvarı İsabetli ve bu yerleşik bir NAT oturum yanıtı olduğundan güvenlik duvarı tarafından kabul edilir</span><span class="sxs-lookup"><span data-stu-id="f6e24-439">The HTTP response hits the firewall, and because this is the response to an established NAT session is accepted by the firewall</span></span>
21. <span data-ttu-id="f6e24-440">Güvenlik Duvarı yanıtı Internet kullanıcı ardından yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-440">The firewall then redirects the response back to the Internet User</span></span>
22. <span data-ttu-id="f6e24-441">Olduğundan Hayır giden NSG kuralları veya yanıt izin verilen ön uç alt ağdaki UDR atlama ve Internet kullanıcının istenen web sayfasının alır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-441">Since there are no outbound NSG rules or UDR hops on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-internet-rdp-to-backend"></a><span data-ttu-id="f6e24-442">(İzin verilir) Internet arka uç için RDP</span><span class="sxs-lookup"><span data-stu-id="f6e24-442">(Allowed) Internet RDP to Backend</span></span>
1. <span data-ttu-id="f6e24-443">Sunucu Yöneticisi internet üzerindeki AppVM01 8025 "RDP için AppVM01" güvenlik duvarı kuralı kullanıcı tarafından atanan bağlantı noktası numarasını olduğu SecSvc001.CloudApp.Net:8025 üzerinden RDP oturumu istekleri</span><span class="sxs-lookup"><span data-stu-id="f6e24-443">Server Admin on internet requests RDP session to AppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is the user assigned port number for the “RDP to AppVM01” firewall rule</span></span>
2. <span data-ttu-id="f6e24-444">Bulut hizmeti 10.0.0.4:8025 güvenlik duvarı arabirimde 8025 bağlantı noktasında açık uç noktası üzerinden trafiğe geçirir</span><span class="sxs-lookup"><span data-stu-id="f6e24-444">The cloud service passes traffic through the open endpoint on port 8025 to firewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="f6e24-445">Güvenlik alt ağına atanmış hiçbir NSG bunu sistem NSG kuralları güvenlik duvarı trafiğine izin verecek.</span><span class="sxs-lookup"><span data-stu-id="f6e24-445">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span></span>
4. <span data-ttu-id="f6e24-446">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="f6e24-447">FW kural 1'i (FW Mgmt) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-447">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="f6e24-448">FW Kural 2 (RDP IIS) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-448">FW Rule 2 (RDP IIS) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="f6e24-449">FW kural 3 (RDP DNS01) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-449">FW Rule 3 (RDP DNS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="f6e24-450">FW kuralı 4 (RDP AppVM01) uygulamak için trafik verilir, güvenlik duvarı NAT 10.0.2.5:3386 kendisine (AppVM01 üzerinde RDP noktasına)</span><span class="sxs-lookup"><span data-stu-id="f6e24-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it to 10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="f6e24-451">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-451">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f6e24-452">Olmayan NSG kural 1'i (blok Internet) uygulama (Bu trafiği NAT oluştu güvenlik duvarı tarafından gerekir, böylece kaynak adresi şimdi güvenlik alt ağ üzerinde olan güvenlik duvarı ve arka uç alt ağa göre NSG "yerel" trafiği olarak görülen ve böylece izin verilir), sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Backend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span></span>
   2. <span data-ttu-id="f6e24-453">Varsayılan NSG kuralları alt ağ için alt ağ trafiğine izin verme, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="f6e24-453">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="f6e24-454">AppVM01 RDP trafiği için dinleme ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="f6e24-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="f6e24-455">Giden hiçbir NSG kuralları, varsayılan kuralları uygula ve dönüş trafiğine izin verilir</span><span class="sxs-lookup"><span data-stu-id="f6e24-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="f6e24-456">UDR Güvenlik Duvarı'na giden trafik, sonraki atlama olarak yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-456">UDR routes outbound traffic to the firewall as the next hop</span></span>
9. <span data-ttu-id="f6e24-457">Bu yerleşik bir oturum üzerinde trafiği döndürmektir çünkü güvenlik duvarı yanıtı Internet kullanıcı geçirir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-457">Because this is returning traffic on an established session the firewall passes the response back to the internet user</span></span>
10. <span data-ttu-id="f6e24-458">RDP oturumu etkin</span><span class="sxs-lookup"><span data-stu-id="f6e24-458">RDP session is enabled</span></span>
11. <span data-ttu-id="f6e24-459">Kullanıcı adı ve parolasını AppVM01 ister</span><span class="sxs-lookup"><span data-stu-id="f6e24-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="f6e24-460">(İzin verilir) DNS sunucusundaki Web sunucusu DNS araması</span><span class="sxs-lookup"><span data-stu-id="f6e24-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="f6e24-461">Sunucu, IIS01, www.data.gov bir veri akışı gereksinimlerini ancak adresini çözümlemek için gereksinimlerini web.</span><span class="sxs-lookup"><span data-stu-id="f6e24-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="f6e24-462">Ağ yapılandırma için VNet listeleri DNS01 (arka uç alt ağda 10.0.2.4) birincil DNS sunucusu olarak IIS01 DNS isteği için DNS01 gönderir</span><span class="sxs-lookup"><span data-stu-id="f6e24-462">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="f6e24-463">UDR Güvenlik Duvarı'na giden trafik, sonraki atlama olarak yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-463">UDR routes outbound traffic to the firewall as the next hop</span></span>
4. <span data-ttu-id="f6e24-464">Giden hiçbir NSG kuralları ön uç alt ağına bağlı olan, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="f6e24-464">No outbound NSG rules are bound to the Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="f6e24-465">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="f6e24-466">FW kural 1'i (FW Mgmt) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-466">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="f6e24-467">FW kuralı 2-5 (RDP kurallar) yok, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="f6e24-468">FW kuralları 6 ve 7 (uygulama kuralları) verme geçerli, sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-468">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="f6e24-469">FW kural 8 (Internet için) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-469">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="f6e24-470">FW kural 9 (DNS) geçerli, trafiğe izin verilir, güvenlik duvarı 10.0.2.4 (DNS01) trafiğini</span><span class="sxs-lookup"><span data-stu-id="f6e24-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="f6e24-471">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-471">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f6e24-472">NSG kural 1'i (blok Internet) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-472">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="f6e24-473">Varsayılan NSG kuralları alt ağ için alt ağ trafiğine izin verme, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="f6e24-473">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="f6e24-474">DNS sunucusu isteği alır</span><span class="sxs-lookup"><span data-stu-id="f6e24-474">DNS server receives the request</span></span>
8. <span data-ttu-id="f6e24-475">DNS sunucusu önbelleğe adresi yoksa ve bir kök DNS sunucusu internet'te sorar</span><span class="sxs-lookup"><span data-stu-id="f6e24-475">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
9. <span data-ttu-id="f6e24-476">UDR Güvenlik Duvarı'na giden trafik, sonraki atlama olarak yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-476">UDR routes outbound traffic to the firewall as the next hop</span></span>
10. <span data-ttu-id="f6e24-477">Giden hiçbir NSG kuralları arka uç alt ağdaki trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="f6e24-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="f6e24-478">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="f6e24-479">FW kural 1'i (FW Mgmt) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-479">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="f6e24-480">FW kuralı 2-5 (RDP kurallar) yok, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
    3. <span data-ttu-id="f6e24-481">FW kuralları 6 ve 7 (uygulama kuralları) verme geçerli, sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-481">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
    4. <span data-ttu-id="f6e24-482">FW kural 8 (Internet için) geçerlidir, trafiğe izin verilir, çıkışı SNAT Internet üzerindeki kök DNS sunucusuna oturumdur</span><span class="sxs-lookup"><span data-stu-id="f6e24-482">FW Rule 8 (To Internet) does apply, traffic is allowed, session is SNAT out to root DNS server on the Internet</span></span>
12. <span data-ttu-id="f6e24-483">Bu oturumda Güvenlik Duvarı'ndan başlatılan olduğundan, Internet DNS sunucusu yanıt, yanıt güvenlik duvarı tarafından kabul edilir</span><span class="sxs-lookup"><span data-stu-id="f6e24-483">Internet DNS server responds, since this session was initiated from the firewall, the response is accepted by the firewall</span></span>
13. <span data-ttu-id="f6e24-484">Yerleşik bir oturum olarak güvenlik duvarı yanıt DNS01 başlatma sunucusuna iletir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-484">As this is an established session, the firewall forwards the response to the initiating server, DNS01</span></span>
14. <span data-ttu-id="f6e24-485">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-485">The Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f6e24-486">NSG kural 1'i (blok Internet) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-486">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="f6e24-487">Varsayılan NSG kuralları alt ağ için alt ağ trafiğine izin verme, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="f6e24-487">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="f6e24-488">DNS sunucusu alır ve yanıtı önbelleğe alır ve ardından geri IIS01 ilk isteğine yanıt verir</span><span class="sxs-lookup"><span data-stu-id="f6e24-488">The DNS server receives and caches the response, and then responds to the initial request back to IIS01</span></span>
16. <span data-ttu-id="f6e24-489">Arka uç alt ağdaki UDR rota güvenlik duvarı sonraki atlama yapar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-489">The UDR route on backend subnet makes the firewall the next hop</span></span>
17. <span data-ttu-id="f6e24-490">Giden hiçbir NSG kuralları arka uç alt ağda var, trafiğe izin verilir</span><span class="sxs-lookup"><span data-stu-id="f6e24-490">No outbound NSG rules exist on the Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="f6e24-491">Bu Güvenlik Duvarı'nda yerleşik bir oturum, yanıt IIS sunucuya geri güvenlik duvarı tarafından iletilir</span><span class="sxs-lookup"><span data-stu-id="f6e24-491">This is an established session on the firewall, the response is forwarded by the firewall back to the IIS server</span></span>
19. <span data-ttu-id="f6e24-492">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f6e24-493">Gelen için geçerli NSG kural yok NSG hiçbiri uygulama kuralları için ön uç alt ağa, arka uç alt ağından gelen trafik</span><span class="sxs-lookup"><span data-stu-id="f6e24-493">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="f6e24-494">Trafiğe izin için alt ağlar arasında trafiğe izin varsayılan sistem kuralı bu trafiği olanak tanır</span><span class="sxs-lookup"><span data-stu-id="f6e24-494">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
20. <span data-ttu-id="f6e24-495">IIS01 DNS01 yanıtı alır</span><span class="sxs-lookup"><span data-stu-id="f6e24-495">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-backend-server-to-frontend-server"></a><span data-ttu-id="f6e24-496">(İzin verilir) Ön uç sunucusu için arka uç sunucusu</span><span class="sxs-lookup"><span data-stu-id="f6e24-496">(Allowed) Backend server to Frontend server</span></span>
1. <span data-ttu-id="f6e24-497">RDP aracılığıyla AppVM02 için oturum açmış bir yönetici, doğrudan windows dosya Gezgini aracılığıyla IIS01 sunucusundan bir dosya istediğinde</span><span class="sxs-lookup"><span data-stu-id="f6e24-497">An administrator logged on to AppVM02 via RDP requests a file directly from the IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="f6e24-498">Arka uç alt ağdaki UDR rota güvenlik duvarı sonraki atlama yapar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-498">The UDR route on Backend subnet makes the firewall the next hop</span></span>
3. <span data-ttu-id="f6e24-499">Yanıt izin arka uç alt ağda giden hiçbir NSG kuralları olduğundan</span><span class="sxs-lookup"><span data-stu-id="f6e24-499">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span></span>
4. <span data-ttu-id="f6e24-500">Güvenlik duvarı kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="f6e24-501">FW kural 1'i (FW Mgmt) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-501">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="f6e24-502">FW kuralı 2-5 (RDP kurallar) yok, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="f6e24-503">FW kuralları 6 ve 7 (uygulama kuralları) verme geçerli, sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-503">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="f6e24-504">FW kural 8 (Internet için) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-504">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="f6e24-505">FW kural 9 (DNS) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-505">FW Rule 9 (DNS) doesn’t apply, move to next rule</span></span>
   6. <span data-ttu-id="f6e24-506">FW kural 10 (içi alt ağ) geçerli, trafiğe izin verilir, güvenlik duvarı trafiği 10.0.1.4 (IIS01) geçirir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic to 10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="f6e24-507">Ön uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="f6e24-508">NSG kural 1'i (blok Internet) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-508">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="f6e24-509">Varsayılan NSG kuralları alt ağ için alt ağ trafiğine izin verme, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="f6e24-509">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="f6e24-510">Uygun kimlik doğrulama ve yetkilendirme varsayıldığında, IIS01 isteği kabul eder ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="f6e24-510">Assuming proper authentication and authorization, IIS01 accepts the request and responds</span></span>
7. <span data-ttu-id="f6e24-511">Ön uç alt ağdaki UDR rota güvenlik duvarı sonraki atlama yapar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-511">The UDR route on Frontend subnet makes the firewall the next hop</span></span>
8. <span data-ttu-id="f6e24-512">Yanıt izin verilen ön uç alt ağda giden hiçbir NSG kuralları olduğundan</span><span class="sxs-lookup"><span data-stu-id="f6e24-512">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span></span>
9. <span data-ttu-id="f6e24-513">Bu Güvenlik Duvarı'nda var olan bir oturum olarak bu yanıt izin verilir ve güvenlik duvarı AppVM02 yanıtı döndürür</span><span class="sxs-lookup"><span data-stu-id="f6e24-513">As this is an existing session on the firewall this response is allowed and the firewall returns the response to AppVM02</span></span>
10. <span data-ttu-id="f6e24-514">Arka uç alt gelen kuralı işleme başlar:</span><span class="sxs-lookup"><span data-stu-id="f6e24-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="f6e24-515">NSG kural 1'i (blok Internet) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-515">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="f6e24-516">Varsayılan NSG kuralları alt ağ için alt ağ trafiğine izin verme, trafiğe izin verilir, NSG kuralının işlenmesi Durdur</span><span class="sxs-lookup"><span data-stu-id="f6e24-516">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="f6e24-517">AppVM02 yanıtı alır</span><span class="sxs-lookup"><span data-stu-id="f6e24-517">AppVM02 receives the response</span></span>

#### <a name="denied-internet-direct-to-web-server"></a><span data-ttu-id="f6e24-518">(Reddedildi) Web sunucusuna doğrudan Internet</span><span class="sxs-lookup"><span data-stu-id="f6e24-518">(Denied) Internet direct to Web Server</span></span>
1. <span data-ttu-id="f6e24-519">Internet kullanıcı FrontEnd001.CloudApp.Net hizmeti aracılığıyla IIS01, web sunucusu erişmeyi dener</span><span class="sxs-lookup"><span data-stu-id="f6e24-519">Internet user tries to access the web server, IIS01, through the FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="f6e24-520">HTTP trafiği için açık uç nokta yok olduğundan bu bulut hizmeti aracılığıyla geçecek değil ve sunucunun ulaşmak olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="f6e24-520">Since there are no endpoints open for HTTP traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="f6e24-521">Uç noktaları için herhangi bir nedenle açıksa, ön uç alt ağdaki (blok Internet) NSG bu trafiği engeller</span><span class="sxs-lookup"><span data-stu-id="f6e24-521">If the endpoints were open for some reason, the NSG (Block Internet) on the Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="f6e24-522">Son olarak, ön uç alt UDR rota tüm giden trafiği IIS01 Güvenlik Duvarı'nda sonraki atlama olarak gönderir ve Güvenlik Duvarı'nı bu asimetrik trafiği olarak görebilir ve giden yanıt en az üç bağımsız katmanlar arasında savunma vardır nedenle bırakma Internet ve yetkisiz/uygunsuz erişimi engelleme kendi bulut hizmeti aracılığıyla IIS01.</span><span class="sxs-lookup"><span data-stu-id="f6e24-522">Finally, the Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-to-backend-server"></a><span data-ttu-id="f6e24-523">(Reddedildi) Arka uç sunucusuna Internet</span><span class="sxs-lookup"><span data-stu-id="f6e24-523">(Denied) Internet to Backend Server</span></span>
1. <span data-ttu-id="f6e24-524">Internet kullanıcı BackEnd001.CloudApp.Net hizmeti aracılığıyla AppVM01 bir dosyaya erişmeyi dener</span><span class="sxs-lookup"><span data-stu-id="f6e24-524">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="f6e24-525">Dosya Paylaşımı için açık uç nokta yok olduğundan bu bulut hizmeti geçip geçmeyeceğini değil ve tarafından sunucuya ulaşmak olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="f6e24-525">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="f6e24-526">NSG (blok Internet) uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller</span><span class="sxs-lookup"><span data-stu-id="f6e24-526">If the endpoints were open for some reason, the NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="f6e24-527">Son olarak, UDR rota tüm giden trafiği AppVM01 Güvenlik Duvarı'nda sonraki atlama olarak gönderir ve Güvenlik Duvarı'nı bu asimetrik trafiği olarak görebilir ve böylece savunma internet arasında en az üç bağımsız katmanı vardır giden yanıt bırakma ve Yetkisiz/uygunsuz erişimi engelleme kendi bulut hizmeti aracılığıyla AppVM01.</span><span class="sxs-lookup"><span data-stu-id="f6e24-527">Finally, the UDR route would send any outbound traffic from AppVM01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-to-backend-server"></a><span data-ttu-id="f6e24-528">(Reddedildi) Arka uç sunucusuna ön uç sunucusu</span><span class="sxs-lookup"><span data-stu-id="f6e24-528">(Denied) Frontend server to Backend Server</span></span>
1. <span data-ttu-id="f6e24-529">IIS01 aşılmış ve arka uç sunucuları alt için tararken kötü amaçlı kod çalıştığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="f6e24-529">Assume IIS01 was compromised and is running malicious code trying to scan the Backend subnet servers.</span></span>
2. <span data-ttu-id="f6e24-530">Ön uç alt UDR rota tüm giden trafiği IIS01 Güvenlik Duvarı'na sonraki atlama olarak gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-530">The Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop.</span></span> <span data-ttu-id="f6e24-531">Bu, güvenliği aşılan VM tarafından değiştirilebilir bir şey değildir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-531">This is not something that can be altered by the compromised VM.</span></span>
3. <span data-ttu-id="f6e24-532">İstek AppVM01 veya trafiğe Güvenlik Duvarı'nı (nedeniyle FW kuralları 7 ve 9) tarafından izin DNS aramaları için DNS sunucusu olduğunda güvenlik duvarının trafiğini işleyecek.</span><span class="sxs-lookup"><span data-stu-id="f6e24-532">The firewall would process the traffic, if the request was to AppVM01, or to the DNS server for DNS lookups that traffic could potentially be allowed by the firewall (due to FW Rules 7 and 9).</span></span> <span data-ttu-id="f6e24-533">Diğer tüm trafik FW kural 11 göre (tüm reddetme) engellenebilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="f6e24-534">Tehdit algılama Gelişmiş Güvenlik Duvarı'nı etkinleştirildi (da değil kapsanan bu belgede, Gelişmiş tehdit özellikleri, belirli bir ağ Gereci satıcı belgelerine bakın), hatta temel iletme kuralları tarafından izin trafiği Bu konuda ele alınan belge engelledi trafiği bilinen imzaları ya da bir Gelişmiş tehdit kuralı bayrak desenler içeriyorsa.</span><span class="sxs-lookup"><span data-stu-id="f6e24-534">If advanced threat detection was enabled on the firewall (which is not covered in this document, see the vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by the basic forwarding rules discussed in this document could be prevented if the traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="f6e24-535">(Reddedildi) DNS sunucusunda Internet DNS araması</span><span class="sxs-lookup"><span data-stu-id="f6e24-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="f6e24-536">Internet kullanıcı DNS01 BackEnd001.CloudApp.Net hizmeti aracılığıyla bir iç DNS kaydını arama dener</span><span class="sxs-lookup"><span data-stu-id="f6e24-536">Internet user tries to lookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="f6e24-537">DNS trafiği için açık uç nokta yok olduğundan bu bulut hizmeti aracılığıyla geçip geçmeyeceğini değil ve sunucunun ulaşmak olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="f6e24-537">Since there are no endpoints open for DNS traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="f6e24-538">Uç noktaları için herhangi bir nedenle açıksa, ön uç alt ağda NSG kuralının (blok Internet) bu trafiği engeller</span><span class="sxs-lookup"><span data-stu-id="f6e24-538">If the endpoints were open for some reason, the NSG rule (Block Internet) on the Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="f6e24-539">Son olarak, arka uç alt UDR rota tüm giden trafiği DNS01 Güvenlik Duvarı'nda sonraki atlama olarak gönderir ve Güvenlik Duvarı'nı bu asimetrik trafiği olarak görebilir ve giden yanıt en az üç bağımsız katmanlar arasında savunma vardır nedenle bırakma Internet ve yetkisiz/uygunsuz erişimi engelleme kendi bulut hizmeti aracılığıyla DNS01.</span><span class="sxs-lookup"><span data-stu-id="f6e24-539">Finally, the Backend subnet UDR route would send any outbound traffic from DNS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-to-sql-access-through-firewall"></a><span data-ttu-id="f6e24-540">(Reddedildi) SQL erişimi güvenlik duvarı üzerinden İnternete</span><span class="sxs-lookup"><span data-stu-id="f6e24-540">(Denied) Internet to SQL access through Firewall</span></span>
1. <span data-ttu-id="f6e24-541">Internet kullanıcı SQL verileri SecSvc001.CloudApp.Net (Internet'e yönelik bulut hizmeti) ' ister.</span><span class="sxs-lookup"><span data-stu-id="f6e24-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="f6e24-542">SQL için açık uç nokta yok olduğundan bu bulut hizmeti geçip geçmeyeceğini değil ve güvenlik duvarı ulaşmak olmayacaktır</span><span class="sxs-lookup"><span data-stu-id="f6e24-542">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="f6e24-543">SQL uç noktaları için herhangi bir nedenle açıksa, güvenlik duvarı kuralı işlemeye başlamak:</span><span class="sxs-lookup"><span data-stu-id="f6e24-543">If SQL endpoints were open for some reason, the firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="f6e24-544">FW kural 1'i (FW Mgmt) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-544">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="f6e24-545">FW kuralları 2-5 (RDP kurallar) yok, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="f6e24-546">FW kural 6 ve 7 (uygulama kuralları) verme geçerli, sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-546">FW Rule 6 & 7 (Application Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="f6e24-547">FW kural 8 (Internet için) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-547">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="f6e24-548">FW kural 9 (DNS) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-548">FW Rule 9 (DNS) doesn’t apply, move to next rule</span></span>
   6. <span data-ttu-id="f6e24-549">FW kural 10 (içi alt ağ) değil, uygulamak için sonraki kural taşıma</span><span class="sxs-lookup"><span data-stu-id="f6e24-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move to next rule</span></span>
   7. <span data-ttu-id="f6e24-550">FW kural 11 (Tümünü Reddet) geçerli, engellenmiş, Dur kural işlenirken trafiğidir</span><span class="sxs-lookup"><span data-stu-id="f6e24-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="f6e24-551">Başvurular</span><span class="sxs-lookup"><span data-stu-id="f6e24-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="f6e24-552">Ana komut dosyası ve ağ yapılandırması</span><span class="sxs-lookup"><span data-stu-id="f6e24-552">Main Script and Network Config</span></span>
<span data-ttu-id="f6e24-553">Tam komut dosyasını bir PowerShell komut dosyası kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f6e24-553">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="f6e24-554">Ağ Yapılandırma "NetworkConf2.xml" adlı bir dosyaya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f6e24-554">Save the Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="f6e24-555">Kullanıcı tanımlı değişkenleri gerektiği gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f6e24-555">Modify the user defined variables as needed.</span></span> <span data-ttu-id="f6e24-556">Komut dosyasını çalıştırın, ardından yukarıdaki güvenlik duvarı kuralı kurulum yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="f6e24-556">Run the script, then follow the Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="f6e24-557">Tam komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f6e24-557">Full Script</span></span>
<span data-ttu-id="f6e24-558">Kullanıcı tanımlı değişkenleri esas alarak bu betiği olur:</span><span class="sxs-lookup"><span data-stu-id="f6e24-558">This script will, based on the user defined variables:</span></span>

1. <span data-ttu-id="f6e24-559">Bir Azure aboneliğine Bağlanma</span><span class="sxs-lookup"><span data-stu-id="f6e24-559">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="f6e24-560">Yeni depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f6e24-560">Create a new storage account</span></span>
3. <span data-ttu-id="f6e24-561">Yeni bir VNet ve ağ yapılandırma dosyasında tanımlanan üç alt ağlar oluşturun</span><span class="sxs-lookup"><span data-stu-id="f6e24-561">Create a new VNet and three subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="f6e24-562">Beş sanal makineler oluşturun; Güvenlik Duvarı'nı 1 ve 4 windows server Vm'leri</span><span class="sxs-lookup"><span data-stu-id="f6e24-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="f6e24-563">UDR dahil olmak üzere yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f6e24-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="f6e24-564">İki yeni yönlendirme tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="f6e24-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="f6e24-565">Yollar tablolarına ekleme</span><span class="sxs-lookup"><span data-stu-id="f6e24-565">Add routes to the tables</span></span>
   3. <span data-ttu-id="f6e24-566">Tablolar için uygun alt ağları bağlama</span><span class="sxs-lookup"><span data-stu-id="f6e24-566">Bind tables to appropriate subnets</span></span>
6. <span data-ttu-id="f6e24-567">NVA üstünde IP iletimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f6e24-567">Enable IP Forwarding on the NVA</span></span>
7. <span data-ttu-id="f6e24-568">NSG dahil olmak üzere yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f6e24-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="f6e24-569">Bir NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="f6e24-569">Creating a NSG</span></span>
   2. <span data-ttu-id="f6e24-570">Bir kural ekleme</span><span class="sxs-lookup"><span data-stu-id="f6e24-570">Adding a rule</span></span>
   3. <span data-ttu-id="f6e24-571">NSG için uygun alt ağları bağlama</span><span class="sxs-lookup"><span data-stu-id="f6e24-571">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="f6e24-572">Bu PowerShell Betiği, bir bilgisayar veya sunucu, Internet'e yerel olarak çalıştırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e24-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6e24-573">Bu komut dosyasını çalıştırdığınızda, uyarı veya PowerShell'de pop diğer bilgilendirici iletileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="f6e24-574">Yalnızca hata iletileri kırmızı sorunu nedeni edilir.</span><span class="sxs-lookup"><span data-stu-id="f6e24-574">Only error messages in red are cause for concern.</span></span>
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
       - One server on the FrontEnd Subnet
       - Three Servers on the BackEnd Subnet
       - IP Forwading from the FireWall out to the internet
       - User Defined Routing FrontEnd and BackEnd Subnets to the NVA

      Before running script, ensure the network configuration file is created in
      the directory referenced by $NetworkConfigFile variable (or update the
      variable to reflect the path and file name of the config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind the appropriate
      layer(s) of protection. This script serves as an example of some of the techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and the appropriate protections needed, and then effectively
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
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes to reflect your subscription and services
      # Invalid options will fail in the validation section

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
        # Note: To ensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be the NVA.

        # VM 0 - The Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - The Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - The First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - The Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - The DNS Server
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

      # Update Subscription Pointer to New Storage Account
        Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "The SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation varible is correct and the netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see the above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

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
                # Set up all the EndPoints we'll need once we're up and running
                # Note: All traffic goes through the firewall, so we'll need to set up all ports here.
                #       Also, the firewall will be redirecting traffic to a new IP and Port in a forwarding
                #       rule, so all of these endpoint have the same public and local port and the firewall
                #       will do the mapping, NATing, and/or redirection as declared in the firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when the appliance is created.
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

      # Create the Route Tables
        Write-Host "Creating the Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes to Route Tables
        Write-Host "Adding Routes to the Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate the Route Tables with the Subnets
        Write-Host "Binding Route Tables to the Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on the Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

      # Build the NSG
        Write-Host "Building the NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign the NSG to two Subnets
        # The NSG is *not* bound to the Security Subnet. The result
        # is that internet traffic flows only to the Security subnet
        # since the NSG bound to the Frontend and Backback subnets
        # will Deny internet traffic to those subnets.
        Write-Host "Binding the NSG to two subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on the IIS Server)
      # Install Backend resource (Run Post-Build Script on the AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="f6e24-575">Ağ yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="f6e24-575">Network Config File</span></span>
<span data-ttu-id="f6e24-576">Güncelleştirilmiş konumla bu xml dosyasını kaydedin ve bu dosyaya yukarıdaki komut $NetworkConfigFile değişken bağlantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6e24-576">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="f6e24-577">Örnek uygulama komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="f6e24-577">Sample Application Scripts</span></span>
<span data-ttu-id="f6e24-578">Bu ve diğer çevre örnekleri için örnek bir uygulama yüklemek isterseniz, bir aşağıdaki bağlantıda sağlanmış: [örnek uygulama betiği][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="f6e24-578">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
<span data-ttu-id="f6e24-579">[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Çift yönlü DMZ NVA, NSG ve UDR"</span><span class="sxs-lookup"><span data-stu-id="f6e24-579">[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Bi-directional DMZ with NVA, NSG, and UDR"</span></span>
<span data-ttu-id="f6e24-580">[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Güvenlik duvarı kurallarını mantıksal görünümü"</span><span class="sxs-lookup"><span data-stu-id="f6e24-580">[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Logical View of the Firewall Rules"</span></span>
<span data-ttu-id="f6e24-581">[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Bir ön uç ağ nesnesi oluşturun"</span><span class="sxs-lookup"><span data-stu-id="f6e24-581">[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Create a FrontEnd Network Object"</span></span>
<span data-ttu-id="f6e24-582">[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Bir DNS sunucusu nesnesi oluşturun"</span><span class="sxs-lookup"><span data-stu-id="f6e24-582">[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Create a DNS Server Object"</span></span>
<span data-ttu-id="f6e24-583">[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Varsayılan RDP kuralı kopyası"</span><span class="sxs-lookup"><span data-stu-id="f6e24-583">[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copy of Default RDP Rule"</span></span>
<span data-ttu-id="f6e24-584">[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 kuralı"</span><span class="sxs-lookup"><span data-stu-id="f6e24-584">[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 Rule"</span></span>
<span data-ttu-id="f6e24-585">[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Uygulama yeniden yönlendirme simgesi"</span><span class="sxs-lookup"><span data-stu-id="f6e24-585">[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Application Redirect Icon"</span></span>
<span data-ttu-id="f6e24-586">[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Hedef NAT simgesi"</span><span class="sxs-lookup"><span data-stu-id="f6e24-586">[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Destination NAT Icon"</span></span>
<span data-ttu-id="f6e24-587">[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Geçişi simgesi"</span><span class="sxs-lookup"><span data-stu-id="f6e24-587">[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Pass Icon"</span></span>
<span data-ttu-id="f6e24-588">[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Güvenlik Duvarı Yönetimi kuralı"</span><span class="sxs-lookup"><span data-stu-id="f6e24-588">[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Firewall Management Rule"</span></span>
<span data-ttu-id="f6e24-589">[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Güvenlik Duvarı RDP kuralı"</span><span class="sxs-lookup"><span data-stu-id="f6e24-589">[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Firewall RDP Rule"</span></span>
<span data-ttu-id="f6e24-590">[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Güvenlik Duvarı Web kuralı"</span><span class="sxs-lookup"><span data-stu-id="f6e24-590">[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Firewall Web Rule"</span></span>
<span data-ttu-id="f6e24-591">[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Güvenlik Duvarı AppVM01 kuralı"</span><span class="sxs-lookup"><span data-stu-id="f6e24-591">[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Firewall AppVM01 Rule"</span></span>
<span data-ttu-id="f6e24-592">[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Giden güvenlik duvarı kuralı"</span><span class="sxs-lookup"><span data-stu-id="f6e24-592">[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Firewall Outbound Rule"</span></span>
<span data-ttu-id="f6e24-593">[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Güvenlik Duvarı DNS kuralı"</span><span class="sxs-lookup"><span data-stu-id="f6e24-593">[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Firewall DNS Rule"</span></span>
<span data-ttu-id="f6e24-594">[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Güvenlik Duvarı içi sanal ağ kuralı"</span><span class="sxs-lookup"><span data-stu-id="f6e24-594">[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Firewall Intra-VNet Rule"</span></span>
<span data-ttu-id="f6e24-595">[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Güvenlik duvarı kuralı Reddet"</span><span class="sxs-lookup"><span data-stu-id="f6e24-595">[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Firewall Deny Rule"</span></span>
<span data-ttu-id="f6e24-596">[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Güvenlik duvarı kuralını etkinleştirme"</span><span class="sxs-lookup"><span data-stu-id="f6e24-596">[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Firewall Rule Activation"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
