---
title: "aaaLayered App Service ortamları ile güvenlik mimarisi"
description: "Uygulama hizmeti ortamları katmanlı güvenlik mimarisiyle uygulama."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="aa1a7-103">Uygulama hizmeti ortamları katmanlı güvenlik mimarisiyle uygulama</span><span class="sxs-lookup"><span data-stu-id="aa1a7-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="aa1a7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="aa1a7-104">Overview</span></span>
<span data-ttu-id="aa1a7-105">Uygulama hizmeti ortamları sanal ağınıza dağıtılmış bir yalıtılmış çalışma zamanı ortamı sağlamak için geliştiriciler için her fiziksel uygulama katmanı düzeyleri farklı ağ erişim sağlayan bir katmanlı güvenlik mimarisi oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="aa1a7-106">Ortak desire toohide API'si arka uçları genel Internet erişimine karşı olduğu ve yalnızca Yukarı Akış web uygulamaları tarafından adlı API'leri toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-106">A common desire is toohide API back-ends from general Internet access, and only allow APIs toobe called by upstream web apps.</span></span>  <span data-ttu-id="aa1a7-107">[Ağ güvenlik grupları (Nsg'ler)] [ NetworkSecurityGroups] App Service ortamları toorestrict genel erişim tooAPI uygulamaları içeren alt ağlarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments toorestrict public access tooAPI applications.</span></span>

<span data-ttu-id="aa1a7-108">Hello diyagrama bir uygulama hizmeti ortamı dağıtılan Webapı tabanlı uygulama ile bir örnek mimari gösterilir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-108">hello diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="aa1a7-109">Üç ayrı uygulama hizmeti ortamları üzerinde dağıtılan üç ayrı web app örnekleri olun arka uç çağrıları toohello aynı Webapı uygulama.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls toohello same WebAPI app.</span></span>

![Kavramsal mimarisi][ConceptualArchitecture] 

<span data-ttu-id="aa1a7-111">Merhaba yeşil artı işaretini gösteren bu hello "apiase" içeren hello alt ağındaki ağ güvenlik grubu kendisinden iyi çağrıları Yukarı Akış web uygulamaları hello gelen gelen çağrıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-111">hello green plus signs indicate that hello network security group on hello subnet containing "apiase" allows inbound calls from hello upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="aa1a7-112">Aynı ağ güvenlik grubu açıkça reddeder hello erişim ancak toogeneral gelen hello Internet trafiği.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-112">However hello same network security group explicitly denies access toogeneral inbound traffic from hello Internet.</span></span> 

<span data-ttu-id="aa1a7-113">Bu konunun geri kalanı Hello "apiase" içeren hello alt ağda hello adımları gerekli tooconfigure hello ağ güvenlik grubu anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-113">hello remainder of this topic walks through hello steps needed tooconfigure hello network security group on hello subnet containing "apiase".</span></span>

## <a name="determining-hello-network-behavior"></a><span data-ttu-id="aa1a7-114">Merhaba ağ davranışı belirleme</span><span class="sxs-lookup"><span data-stu-id="aa1a7-114">Determining hello Network Behavior</span></span>
<span data-ttu-id="aa1a7-115">Sipariş tooknow kuralları gereklidir, hangi ağ güvenliği hangi ağ istemcileri tooreach hello uygulama hizmeti ortamı içeren hello API uygulaması ve hangi istemcilerin engellenecek izin verilecek toodetermine gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-115">In order tooknow what network security rules are needed, you need toodetermine which network clients will be allowed tooreach hello App Service Environment containing hello API app, and which clients will be blocked.</span></span>

<span data-ttu-id="aa1a7-116">Bu yana [güvenlik gruplarını (Nsg'ler) ağ] [ NetworkSecurityGroups] uygulanan toosubnets olan ve uygulama hizmeti ortamları dağıtılır, alt hello kuralları bir NSG içinde yer alan çok geçerli**tüm** bir uygulama hizmeti ortamı üzerinde çalıştırılan uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied toosubnets, and App Service Environments are deployed into subnets, hello rules contained in an NSG apply too**all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="aa1a7-117">Bir ağ güvenlik grubu "apiase", "Merhaba apiase uygulama hizmeti ortamı hello tarafından korunur" üzerinde çalışan tüm uygulamaları içeren uygulanan toohello alt olduğunda bu makale için hello örnek mimarisi kullanarak, aynı güvenlik kuralları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-117">Using hello sample architecture for this article, once a network security group is applied toohello subnet containing "apiase", all apps running on hello "apiase" App Service Environment will be protected by hello same set of security rules.</span></span> 

* <span data-ttu-id="aa1a7-118">**Yukarı Akış arayanlar Hello giden IP adresini belirlemek:** hello IP adresini veya adreslerini hello Yukarı Akış arayanlar nedir?</span><span class="sxs-lookup"><span data-stu-id="aa1a7-118">**Determine hello outbound IP address of upstream callers:**  What is hello IP address or addresses of hello upstream callers?</span></span>  <span data-ttu-id="aa1a7-119">Bu adresler erişim hello NSG açıkça izin verilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-119">These addresses will need toobe explicitly allowed access in hello NSG.</span></span>  <span data-ttu-id="aa1a7-120">Uygulama hizmeti ortamları arasında çağrıları "Internet" çağrıları kabul edilen olduğundan, bu hello giden IP adresi atanmış tooeach erişim hello NSG hello "apiase" alt ağı için izin verilen hello üç Yukarı Akış App Service ortamları gereksinimlerini toobe, anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-120">Since calls between App Service Environments are considered "Internet" calls, this means hello outbound IP address assigned tooeach of hello three upstream App Service Environments needs toobe allowed access in hello NSG for hello "apiase" subnet.</span></span>   <span data-ttu-id="aa1a7-121">Uygulama hizmeti ortamı'nda çalışan uygulamalar hello görmek için hello giden IP adresi belirleme hakkında daha fazla bilgi [ağ mimarisi] [ NetworkArchitecture] genel bakış makalesi.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-121">For more details on determining hello outbound IP address for apps running in an App Service Environment see hello [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="aa1a7-122">**Merhaba arka uç API uygulaması toocall kendisini gerekecek mi?**</span><span class="sxs-lookup"><span data-stu-id="aa1a7-122">**Will hello back-end API app need toocall itself?**</span></span>  <span data-ttu-id="aa1a7-123">Bazen gözden kaçan önemli ve zarif noktası nerede toocall kendisini Merhaba arka uç uygulaması gereken hello senaryodur.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-123">A sometimes overlooked and subtle point is hello scenario where hello back-end application needs toocall itself.</span></span>  <span data-ttu-id="aa1a7-124">Bir uygulama hizmeti ortamı üzerinde bir arka uç API uygulamasının toocall kendisini gerekiyorsa, bu da değerlendirilir "Internet" çağrısı olarak.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-124">If a back-end API application on an App Service Environment needs toocall itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="aa1a7-125">Merhaba örnek mimarisinde bu hello "apiase" uygulama hizmeti ortamı de hello giden IP adresinden gelen erişimine gerektirir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-125">In hello sample architecture this requires allowing access from hello outbound IP address of hello "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-hello-network-security-group"></a><span data-ttu-id="aa1a7-126">Ağ güvenlik grubu hello ayarlama</span><span class="sxs-lookup"><span data-stu-id="aa1a7-126">Setting up hello Network Security Group</span></span>
<span data-ttu-id="aa1a7-127">Merhaba, ayarladıktan sonra giden IP adreslerini bilinen, hello sonraki adıma tooconstruct bir ağ güvenlik grubu.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-127">Once hello set of outbound IP addresses are known, hello next step is tooconstruct a network security group.</span></span>  <span data-ttu-id="aa1a7-128">Sanal ağlar olarak Klasik sanal ağlar hem Resource Manager tabanlı için ağ güvenlik grupları oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="aa1a7-129">Aşağıdaki Hello örnekleri oluşturma ve Powershell kullanarak bir Klasik sanal ağda bir NSG yapılandırma gösterir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-129">hello examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="aa1a7-130">Boş bir NSG bu bölgede oluşturulan şekilde hello örnek mimarisi için Orta Güney ABD içinde hello ortamları bulunur:</span><span class="sxs-lookup"><span data-stu-id="aa1a7-130">For hello sample architecture, hello environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="aa1a7-131">İlk açık bir izin üzerinde hello makalesinde belirtildiği gibi hello Azure Yönetimi altyapısı için eklenen kural [gelen trafiği] [ InboundTraffic] App Service ortamları için.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-131">First an explicit allow rule is added for hello Azure management infrastructure as noted in hello article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="aa1a7-132">Ardından, iki kural tooallow HTTP eklenir ve HTTPS çağrılarından hello ilk Yukarı Akış uygulama hizmeti ortamı ("fe1ase").</span><span class="sxs-lookup"><span data-stu-id="aa1a7-132">Next, two rules are added tooallow HTTP and HTTPS calls from hello first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="aa1a7-133">Parlatıcı ve yineleme için ikinci ve üçüncü Yukarı Akış App Service ortamları ("fe2ase" ve "fe3ase") hello.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-133">Rinse and repeat for hello second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="aa1a7-134">Son olarak, böylece kendi içine geri çağırabilirsiniz hello arka uç API'nin uygulama hizmeti ortamı erişim toohello giden IP adresi verin.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-134">Lastly, grant access toohello outbound IP address of hello back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="aa1a7-135">Başka bir ağ güvenlik kuralları her NSG hello Internet'ten gelen erişim engelle varsayılan kuralları kümesi olduğundan, varsayılan olarak yapılandırılan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-135">No other network security rules need toobe configured because every NSG has a set of default rules that block inbound access from hello Internet by default.</span></span>

<span data-ttu-id="aa1a7-136">Merhaba hello ağ güvenlik grubu kuralları tam listesini aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-136">hello full list of rules in hello network security group are shown below.</span></span>  <span data-ttu-id="aa1a7-137">Vurgulanır, hello son kural hangi açık olarak erişim izni olanlar dışındaki tüm arayanlar'ten gelen erişim nasıl engellediği unutmayın.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-137">Note how hello last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![NSG yapılandırma][NSGConfiguration] 

<span data-ttu-id="aa1a7-139">Merhaba son hello "apiase" uygulama hizmeti ortamı içeren tooapply hello NSG toohello alt adımdır.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-139">hello final step is tooapply hello NSG toohello subnet that contains hello "apiase" App Service Environment.</span></span>  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="aa1a7-140">Merhaba NSG uygulanır toohello olan bir alt ağ, yalnızca hello üç Yukarı Akış App Service ortamları ve hello uygulama hizmeti ortamı içeren hello API uç toocall hello "apiase" ortamına izin verilir.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-140">With hello NSG applied toohello subnet, only hello three upstream App Service Environments, and hello App Service Environment containing hello API back-end, are allowed toocall into hello "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="aa1a7-141">Ek bağlantıları ve bilgileri</span><span class="sxs-lookup"><span data-stu-id="aa1a7-141">Additional Links and Information</span></span>
<span data-ttu-id="aa1a7-142">Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="aa1a7-142">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="aa1a7-143">Hakkında bilgi [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="aa1a7-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="aa1a7-144">Anlama [giden IP adreslerini] [ NetworkArchitecture] ve uygulama hizmeti ortamları.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="aa1a7-145">[Ağ bağlantı noktalarını] [ InboundTraffic] App Service ortamları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aa1a7-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
