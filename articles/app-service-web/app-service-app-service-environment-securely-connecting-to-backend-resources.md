---
title: "Bir uygulama hizmeti ortamındaki arka uç kaynaklarına güvenli bir şekilde bağlanma"
description: "Bir uygulama hizmeti ortamındaki arka uç kaynaklarına güvenli bir şekilde bağlanma hakkında bilgi edinin."
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
ms.openlocfilehash: 0b6d3a47dc429c469b37c2c74f546cfeca580358
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="2ed01-103">Bir uygulama hizmeti ortamındaki arka uç kaynaklarına güvenli bir şekilde bağlanma</span><span class="sxs-lookup"><span data-stu-id="2ed01-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="2ed01-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2ed01-104">Overview</span></span>
<span data-ttu-id="2ed01-105">Uygulama hizmeti ortamı'nda her zaman oluşturulduğundan **ya da** bir Azure Resource Manager sanal ağ **veya** Klasik dağıtım modeli [sanal ağ] [ virtualnetwork], bir uygulama hizmeti ortamı giden bağlantılar diğer arka uç kaynaklarına yalnızca sanal ağ üzerinden akış.</span><span class="sxs-lookup"><span data-stu-id="2ed01-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="2ed01-106">Haziran 2016'da yapılan son bir değişiklikle ASEs de ortak adres aralıklarını veya RFC1918 adres alanlarını (örn.) kullanan sanal ağlar dağıtılabilir</span><span class="sxs-lookup"><span data-stu-id="2ed01-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="2ed01-107">özel adresler).</span><span class="sxs-lookup"><span data-stu-id="2ed01-107">private addresses).</span></span>  

<span data-ttu-id="2ed01-108">Örneğin, bağlantı noktası 1433 kilitli olan sanal makinelerin bir kümede çalışan bir SQL Server olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-108">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="2ed01-109">Uç nokta yalnızca aynı sanal ağda diğer kaynaklara erişime izin verecek şekilde ACLd olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-109">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="2ed01-110">Başka bir örnek olarak, hassas uç noktaları şirket içinde çalıştırabilir ve Azure'a ya da bağlı [siteden siteye] [ SiteToSite] veya [Azure ExpressRoute] [ ExpressRoute] bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="2ed01-110">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="2ed01-111">Sonuç olarak, siteden siteye veya ExpressRoute tüneller bağlı sanal ağlar kaynaklarında yalnızca şirket içi uç noktaları erişebilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2ed01-111">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="2ed01-112">Tüm bu senaryolar için bir uygulama hizmeti ortamı üzerinde çalışan uygulamalar çeşitli sunuculara ve kaynaklara güvenli bir şekilde bağlanabilmek için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2ed01-112">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="2ed01-113">Uygulama hizmeti ortamı'nda özel uç noktalar aynı sanal ağda çalışan uygulamalardan giden trafik (veya aynı sanal ağa bağlı), sanal ağ üzerinden yalnızca akış olur.</span><span class="sxs-lookup"><span data-stu-id="2ed01-113">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="2ed01-114">Özel uç noktalarına giden trafiği genel Internet üzerinden akar değil.</span><span class="sxs-lookup"><span data-stu-id="2ed01-114">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="2ed01-115">Bir uyarı Uç noktalara bir sanal ağ içindeki bir uygulama hizmeti ortamı'ndan giden trafiği için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-115">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="2ed01-116">Uygulama hizmeti ortamları uç noktaları bulunan sanal makinelerin erişemiyor **aynı** uygulama hizmeti ortamı olarak alt ağ.</span><span class="sxs-lookup"><span data-stu-id="2ed01-116">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="2ed01-117">Uygulama hizmeti ortamları yalnızca uygulama hizmeti ortamı tarafından özel kullanım için ayrılmış bir alt ağ içinde dağıtılan sürece bu normalde bir sorun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="2ed01-117">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="2ed01-118">Giden bağlantısı ve DNS gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="2ed01-118">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="2ed01-119">Bir uygulama hizmeti düzgün şekilde çalışabilmesi ortamı için çeşitli uç noktalarına giden erişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-119">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="2ed01-120">Tam bir ana tarafından kullanılan dış uç noktalar "Ağ bağlantısı gerekli" bölümünde listelenmiştir [ExpressRoute için ağ yapılandırması](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) makalesi.</span><span class="sxs-lookup"><span data-stu-id="2ed01-120">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="2ed01-121">Uygulama hizmeti ortamları sanal ağ için yapılandırılmış geçerli bir DNS altyapısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-121">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="2ed01-122">Bir uygulama hizmeti ortamı oluşturulduktan sonra DNS yapılandırmasını herhangi bir nedenle değiştirilirse, geliştiricilerin yeni DNS yapılandırmasını almak için bir uygulama hizmeti ortamı zorlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ed01-122">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="2ed01-123">Portalı'nda uygulama hizmeti ortamı yönetim dikey pencerenin üstündeki "Yeniden Başlat" simgesini kullanarak çalışırken bir ortamı yeniden başlatma tetikleme yeni DNS yapılandırmasını almak ortam neden olur.</span><span class="sxs-lookup"><span data-stu-id="2ed01-123">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="2ed01-124">Ayrıca, tüm özel DNS sunucuları vnet üzerinde bir uygulama hizmeti ortamı oluşturmadan önce vaktinden Kurulum olması önerilir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-124">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="2ed01-125">Bir uygulama hizmeti ortamı oluşturulurken bir sanal ağın DNS yapılandırması değiştiyse, uygulama hizmeti ortamı oluşturma işlemi başarısız olan neden olur.</span><span class="sxs-lookup"><span data-stu-id="2ed01-125">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="2ed01-126">Benzer bir damarlı içinde özel bir DNS sunucusu bir VPN ağ geçidi diğer ucundaki var ve DNS sunucusu erişilemez veya kullanılamaz, uygulama hizmeti ortamı oluşturma işlemi de başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="2ed01-126">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="2ed01-127">Bir SQL Server'a bağlanma</span><span class="sxs-lookup"><span data-stu-id="2ed01-127">Connecting to a SQL Server</span></span>
<span data-ttu-id="2ed01-128">Yaygın olarak kullanılan SQL Server yapılandırması 1433 bağlantı noktasını dinleyen bir uç nokta vardır:</span><span class="sxs-lookup"><span data-stu-id="2ed01-128">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![SQL sunucusu uç noktası][SqlServerEndpoint]

<span data-ttu-id="2ed01-130">Bu uç noktaya trafiği kısıtlama için iki yaklaşım vardır:</span><span class="sxs-lookup"><span data-stu-id="2ed01-130">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="2ed01-131">[Ağ erişim denetim listeleri] [ NetworkAccessControlLists] (ağ ACL'leri)</span><span class="sxs-lookup"><span data-stu-id="2ed01-131">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="2ed01-132">[Ağ güvenlik grupları][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="2ed01-132">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="2ed01-133">Bir ağ ACL ile erişimi kısıtlama</span><span class="sxs-lookup"><span data-stu-id="2ed01-133">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="2ed01-134">Bağlantı noktası 1433'ü bir ağ erişim denetimi listesi kullanılarak güvenli hale getirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-134">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="2ed01-135">Whitelists istemci aşağıdaki örnekte, bir sanal ağ içinde kaynaklanan adresleri ve diğer tüm istemciler için erişim engellenir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-135">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![Ağ erişim denetim listesi örneği][NetworkAccessControlListExample]

<span data-ttu-id="2ed01-137">SQL Server için SQL Server örneğini kullanarak bağlanmak olarak uygulama hizmeti ortamı'nda aynı sanal ağ içinde çalışan uygulamaların **VNet iç** SQL Server sanal makine için IP adresi.</span><span class="sxs-lookup"><span data-stu-id="2ed01-137">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="2ed01-138">Aşağıdaki örnek bağlantı dizesi, özel IP adresini kullanarak SQL Server başvurur.</span><span class="sxs-lookup"><span data-stu-id="2ed01-138">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="2ed01-139">Sanal makine genel bir uç nokta da olsa da, genel IP adresi kullanılarak yapılan bağlantı girişimleri ACL ağ nedeniyle kabul edilmeyecek.</span><span class="sxs-lookup"><span data-stu-id="2ed01-139">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="2ed01-140">Bir ağ güvenlik grubu ile erişimi kısıtlama</span><span class="sxs-lookup"><span data-stu-id="2ed01-140">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="2ed01-141">Bir ağ güvenlik grubuyla erişim güvenliğini sağlamak için alternatif bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="2ed01-141">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="2ed01-142">Tek tek sanal makineleri veya sanal makine içeren bir alt ağ için ağ güvenlik grupları uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-142">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="2ed01-143">İlk ağ güvenlik grubu oluşturulması gerekir:</span><span class="sxs-lookup"><span data-stu-id="2ed01-143">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="2ed01-144">Yalnızca VNet iç trafiği erişimi kısıtlamak, bir ağ güvenlik grubuyla çok kolaydır.</span><span class="sxs-lookup"><span data-stu-id="2ed01-144">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="2ed01-145">Varsayılan kuralları bir ağ güvenlik grubu sadece erişim aynı sanal ağdaki diğer ağ istemcilerden izin verir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-145">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="2ed01-146">Sonuç olarak SQL Server erişimi kilitleme ya da SQL Server ya da sanal makineleri içeren alt ağ çalışan sanal makineleri için ağ güvenlik grubu, varsayılan kuralları ile uygulama olarak kadar basittir.</span><span class="sxs-lookup"><span data-stu-id="2ed01-146">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="2ed01-147">Aşağıdaki örnek bir ağ güvenlik grubu içeren alt ağ için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="2ed01-147">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="2ed01-148">Nihai sonuç, VNet iç erişim sağlarken dış erişimi engelleme güvenlik kurallar kümesidir:</span><span class="sxs-lookup"><span data-stu-id="2ed01-148">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Varsayılan ağ güvenlik kuralları][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="2ed01-150">Başlarken</span><span class="sxs-lookup"><span data-stu-id="2ed01-150">Getting started</span></span>
<span data-ttu-id="2ed01-151">Tüm makaleler ve nasıl-için uygulama hizmeti ortamları kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="2ed01-151">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="2ed01-152">Uygulama hizmeti ortamları ile çalışmaya başlamak için bkz: [uygulama hizmeti ortamı giriş][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="2ed01-152">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="2ed01-153">Uygulama hizmeti ortamına gelen trafik denetleme geçici daha fazla bilgi için bkz [bir uygulama hizmeti ortamına gelen trafik denetleme][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="2ed01-153">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="2ed01-154">Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="2ed01-154">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
