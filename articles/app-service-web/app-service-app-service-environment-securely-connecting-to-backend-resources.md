---
title: "aaaSecurely bağlanma tooBackEnd bir uygulama hizmeti ortamı kaynaklardan"
description: "Nasıl toosecurely toobackend kaynaklar bağlantı bir uygulama hizmeti ortamındaki hakkında bilgi edinin."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a><span data-ttu-id="6403d-103">Güvenli bir şekilde bağlanma tooBackend bir uygulama hizmeti ortamı kaynaklardan</span><span class="sxs-lookup"><span data-stu-id="6403d-103">Securely Connecting tooBackend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="6403d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6403d-104">Overview</span></span>
<span data-ttu-id="6403d-105">Uygulama hizmeti ortamı'nda her zaman oluşturulduğundan **ya da** bir Azure Resource Manager sanal ağ **veya** Klasik dağıtım modeli [sanal ağ] [ virtualnetwork], bir uygulama hizmeti ortamı tooother arka uç kaynaklarına giden bağlantılar yalnızca hello sanal ağ üzerinden akış.</span><span class="sxs-lookup"><span data-stu-id="6403d-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment tooother backend resources can flow exclusively over hello virtual network.</span></span>  <span data-ttu-id="6403d-106">Haziran 2016'da yapılan son bir değişiklikle ASEs ortak adres aralıkları veya RFC1918 adres alanları (özel adresleri) kullanan sanal ağları içinde dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="6403d-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="6403d-107">Örneğin, bağlantı noktası 1433 kilitli olan sanal makinelerin bir kümede çalışan bir SQL Server olabilir.</span><span class="sxs-lookup"><span data-stu-id="6403d-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="6403d-108">Merhaba endpoint tooonly üzerindeki diğer kaynaklardan erişime izin ACLd olabilir hello aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="6403d-108">hello endpoint may be ACLd tooonly allow access from other resources on hello same virtual network.</span></span>  

<span data-ttu-id="6403d-109">Başka bir örnek olarak, hassas uç noktaları şirket içi ve çalıştıran ya da aracılığıyla bağlı tooAzure [siteden siteye] [ SiteToSite] veya [Azure ExpressRoute] [ ExpressRoute] bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="6403d-109">As another example, sensitive endpoints may run on-premises and be connected tooAzure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="6403d-110">Sonuç olarak, sanal ağlar yalnızca kaynaklarında toohello siteden siteye bağlı veya ExpressRoute tüneller mümkün tooaccess şirket içi uç noktaları olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6403d-110">As a result, only resources in virtual networks connected toohello Site-to-Site or ExpressRoute tunnels will be able tooaccess on-premises endpoints.</span></span>

<span data-ttu-id="6403d-111">Tüm bu senaryolar için bir uygulama hizmeti ortamı üzerinde çalışan uygulamalar olması mümkün toosecurely bağlanan toohello çeşitli sunucuları ve kaynakları.</span><span class="sxs-lookup"><span data-stu-id="6403d-111">For all of these scenarios, apps running on an App Service Environment will be able toosecurely connect toohello various servers and resources.</span></span>  <span data-ttu-id="6403d-112">Bir uygulama hizmeti ortamı tooprivate uç noktaları hello içinde çalışan uygulamalardan giden trafiği aynı sanal ağ (veya bağlı toohello aynı sanal ağ), yalnızca akış hello sanal ağ üzerinden olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6403d-112">Outbound traffic from apps running in an App Service Environment tooprivate endpoints in hello same virtual network (or connected toohello same virtual network), will only flow over hello virtual network.</span></span>  <span data-ttu-id="6403d-113">Uç noktaları üzerinden akar değil giden trafiği tooprivate genel Internet hello.</span><span class="sxs-lookup"><span data-stu-id="6403d-113">Outbound traffic tooprivate endpoints will not flow over hello public Internet.</span></span>

<span data-ttu-id="6403d-114">Bir uyarı toooutbound trafiği sanal ağ içindeki bir uygulama hizmeti ortamı tooendpoints gelen geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="6403d-114">One caveat applies toooutbound traffic from an App Service Environment tooendpoints within a virtual network.</span></span>  <span data-ttu-id="6403d-115">Uygulama hizmeti ortamları uç noktaları hello bulunan sanal makinelerin erişemiyor **aynı** uygulama hizmeti ortamı hello gibi bir alt ağ.</span><span class="sxs-lookup"><span data-stu-id="6403d-115">App Service Environments cannot reach endpoints of virtual machines located in hello **same** subnet as hello App Service Environment.</span></span>  <span data-ttu-id="6403d-116">Uygulama hizmeti ortamları yalnızca hello uygulama hizmeti ortamı'tarafından özel kullanım için ayrılmış bir alt ağ içinde dağıtılan sürece bu normalde bir sorun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="6403d-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only hello App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="6403d-117">Giden bağlantısı ve DNS gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="6403d-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="6403d-118">Bir uygulama hizmeti ortamı toofunction için düzgün şekilde giden erişim toovarious uç noktaları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6403d-118">For an App Service Environment toofunction properly, it requires outbound access toovarious endpoints.</span></span> <span data-ttu-id="6403d-119">Tam bir ana tarafından kullanılan hello dış uç noktalar hello hello "Ağ bağlantısı gerekli" bölümünde listelenmiştir [ExpressRoute için ağ yapılandırması](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) makalesi.</span><span class="sxs-lookup"><span data-stu-id="6403d-119">A full list of hello external endpoints used by an ASE is in hello "Required Network Connectivity" section of hello [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="6403d-120">Uygulama hizmeti ortamları hello sanal ağ için yapılandırılmış geçerli bir DNS altyapısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6403d-120">App Service Environments require a valid DNS infrastructure configured for hello virtual network.</span></span>  <span data-ttu-id="6403d-121">Bir uygulama hizmeti ortamı oluşturulduktan sonra herhangi bir nedenle hello için DNS yapılandırması değiştirildiğinde, geliştiricilerin bir uygulama hizmeti ortamı toopick hello yeni DNS yapılandırması zorlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6403d-121">If for any reason hello DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment toopick up hello new DNS configuration.</span></span>  <span data-ttu-id="6403d-122">Merhaba uygulama hizmeti ortamı Hello üstünde bulunan hello "Yeniden Başlat" simgesini kullanarak çalışırken bir ortamı yeniden başlatma tetikleyen yönetim dikey penceresinde hello portal hello ortamı toopick hello yeni DNS yapılandırması neden olur.</span><span class="sxs-lookup"><span data-stu-id="6403d-122">Triggering a rolling environment reboot using hello "Restart" icon located at hello top of hello App Service Environment management blade in hello portal will cause hello environment toopick up hello new DNS configuration.</span></span>

<span data-ttu-id="6403d-123">Merhaba vnet hiçbir özel DNS sunucularında Kurulum zaman önceki toocreating bir uygulama hizmeti ortamı öncesinde olması önerilir.</span><span class="sxs-lookup"><span data-stu-id="6403d-123">It is also recommended that any custom DNS servers on hello vnet be setup ahead of time prior toocreating an App Service Environment.</span></span>  <span data-ttu-id="6403d-124">Bir uygulama hizmeti ortamı oluşturulurken bir sanal ağın DNS yapılandırması değiştiyse, hello uygulama hizmeti ortamı oluşturma işlemi başarısız neden olur.</span><span class="sxs-lookup"><span data-stu-id="6403d-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in hello App Service Environment creation process failing.</span></span>  <span data-ttu-id="6403d-125">Özel bir DNS sunucusu üzerinde hello varsa, benzer bir damarlı içinde başka bir VPN ağ geçidi ve hello DNS sunucusu erişilemez veya kullanılamaz hello uygulama hizmeti ortamı oluşturma işlemi de başarısız olacak sonudur.</span><span class="sxs-lookup"><span data-stu-id="6403d-125">In a similar vein, if a custom DNS server exists on hello other end of a VPN gateway, and hello DNS server is unreachable or unavailable, hello App Service Environment creation process will also fail.</span></span>

## <a name="connecting-tooa-sql-server"></a><span data-ttu-id="6403d-126">SQL Server tooa bağlanma</span><span class="sxs-lookup"><span data-stu-id="6403d-126">Connecting tooa SQL Server</span></span>
<span data-ttu-id="6403d-127">Yaygın olarak kullanılan SQL Server yapılandırması 1433 bağlantı noktasını dinleyen bir uç nokta vardır:</span><span class="sxs-lookup"><span data-stu-id="6403d-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![SQL sunucusu uç noktası][SqlServerEndpoint]

<span data-ttu-id="6403d-129">Trafik toothis endpoint kısıtlama için iki yaklaşım vardır:</span><span class="sxs-lookup"><span data-stu-id="6403d-129">There are two approaches for restricting traffic toothis endpoint:</span></span>

* <span data-ttu-id="6403d-130">[Ağ erişim denetim listeleri] [ NetworkAccessControlLists] (ağ ACL'leri)</span><span class="sxs-lookup"><span data-stu-id="6403d-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="6403d-131">[Ağ güvenlik grupları][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="6403d-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="6403d-132">Bir ağ ACL ile erişimi kısıtlama</span><span class="sxs-lookup"><span data-stu-id="6403d-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="6403d-133">Bağlantı noktası 1433'ü bir ağ erişim denetimi listesi kullanılarak güvenli hale getirilebilir.</span><span class="sxs-lookup"><span data-stu-id="6403d-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="6403d-134">bir sanal ağ içinde kaynaklanan whitelists istemci aşağıdaki Hello örnekte adresleri ve diğer istemciler tooall erişimi.</span><span class="sxs-lookup"><span data-stu-id="6403d-134">hello example below whitelists client addresses originating from inside of a virtual network, and blocks access tooall other clients.</span></span>

![Ağ erişim denetim listesi örneği][NetworkAccessControlListExample]

<span data-ttu-id="6403d-136">Uygulama hizmeti ortamı'nda çalışan tüm uygulamaların aynı sanal ağ hello SQL Server hello kullanarak mümkün tooconnect toohello SQL Server örneği olarak hello **VNet iç** hello SQL Server sanal makine için IP adresi.</span><span class="sxs-lookup"><span data-stu-id="6403d-136">Any applications running in App Service Environment in hello same virtual network as hello SQL Server will be able tooconnect toohello SQL Server instance using hello **VNet internal** IP address for hello SQL Server virtual machine.</span></span>  

<span data-ttu-id="6403d-137">Merhaba örnek bağlantı dizesi başvuruları aşağıda özel IP adresini kullanarak SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="6403d-137">hello example connection string below references hello SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="6403d-138">Merhaba sanal makine genel bir uç nokta da olsa da, hello genel IP adresi kullanılarak yapılan bağlantı girişimleri hello ağ ACL nedeniyle kabul edilmeyecek.</span><span class="sxs-lookup"><span data-stu-id="6403d-138">Although hello virtual machine has a public endpoint as well, connection attempts using hello public IP address will be rejected because of hello network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="6403d-139">Bir ağ güvenlik grubu ile erişimi kısıtlama</span><span class="sxs-lookup"><span data-stu-id="6403d-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="6403d-140">Bir ağ güvenlik grubuyla erişim güvenliğini sağlamak için alternatif bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="6403d-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="6403d-141">Ağ güvenlik grupları uygulanan tooindividual sanal makine ya da sanal makineleri içeren tooa alt olabilir.</span><span class="sxs-lookup"><span data-stu-id="6403d-141">Network security groups can be applied tooindividual virtual machines, or tooa subnet containing virtual machines.</span></span>

<span data-ttu-id="6403d-142">İlk ağ güvenlik grubu oluşturulan toobe gerekir:</span><span class="sxs-lookup"><span data-stu-id="6403d-142">First a network security group needs toobe created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="6403d-143">Erişim tooonly VNet iç trafiği kısıtlama, bir ağ güvenlik grubuyla çok kolaydır.</span><span class="sxs-lookup"><span data-stu-id="6403d-143">Restricting access tooonly VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="6403d-144">bir ağ güvenlik grubundaki Hello varsayılan kuralları yalnızca erişime izin hello'diğer ağ istemcilerden aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="6403d-144">hello default rules in a network security group only allow access from other network clients in hello same virtual network.</span></span>

<span data-ttu-id="6403d-145">Sonuç olarak erişim tooSQL kilitleme sunucu bir ağ güvenlik grubu, varsayılan kuralları tooeither hello SQL Server ya da hello sanal makineleri içeren hello alt çalışan sanal makineler ile uygulama olarak kadar basittir.</span><span class="sxs-lookup"><span data-stu-id="6403d-145">As a result locking down access tooSQL Server is as simple as applying a network security group with its default rules tooeither hello virtual machines running SQL Server, or hello subnet containing hello virtual machines.</span></span>

<span data-ttu-id="6403d-146">Aşağıdaki Hello örneği bir ağ güvenlik grubu toohello içeren alt geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="6403d-146">hello sample below applies a network security group toohello containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="6403d-147">Merhaba Nihai sonuç, VNet iç erişim sağlarken dış erişimi engelleme güvenlik kurallar kümesidir:</span><span class="sxs-lookup"><span data-stu-id="6403d-147">hello end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Varsayılan ağ güvenlik kuralları][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="6403d-149">Başlarken</span><span class="sxs-lookup"><span data-stu-id="6403d-149">Getting started</span></span>
<span data-ttu-id="6403d-150">Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="6403d-150">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="6403d-151">Uygulama hizmeti ortamları ile çalışmaya tooget bakın [giriş tooApp hizmeti ortamı][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="6403d-151">tooget started with App Service Environments, see [Introduction tooApp Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="6403d-152">Denetleme gelen trafiği tooyour uygulama hizmeti ortamı geçici daha fazla bilgi için bkz [gelen trafik tooan uygulama hizmeti ortamı denetleme][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="6403d-152">For details around controlling inbound traffic tooyour App Service Environment, see [Controlling inbound traffic tooan App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="6403d-153">Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="6403d-153">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
