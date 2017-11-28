---
title: "Zorlamalı tünel Azure siteden siteye bağlantıları için yapılandırın: Klasik | Microsoft Docs"
description: "Nasıl tooredirect veya 'force' tüm Internet'e bağlı trafik geri tooyour konumu şirket içi."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="8f2c8-103">Zorlamalı tünel kullanarak yapılandırma hello Klasik dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="8f2c8-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="8f2c8-104">Yeniden yönlendirme veya "tüm Internet'e bağlı trafik geri tooyour şirket içi konumu denetleme ve denetim için bir siteden siteye VPN tüneli aracılığıyla zorla" sağlar tünel zorlandı.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="8f2c8-105">Bu, çoğu kurumsal BT için kritik güvenlik gereksinimdir ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="8f2c8-106">Zorlamalı tünel olmadan, Internet'e bağlı trafik, vm'lerden azure'da her zaman toohello Internet hello seçeneği tooallow olmadan çıkışı doğrudan Azure ağ altyapısından, tooinspect ya da Denetim hello trafik dizinlere.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="8f2c8-107">Yetkisiz Internet erişimine olası tooinformation açığa çıkmasına veya diğer tür güvenlik ihlallerini yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="8f2c8-108">Bu makalede zorlamalı tünel hello Klasik dağıtım modeli kullanılarak oluşturulmuş sanal ağlar için nasıl yapılandıracağınız anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="8f2c8-109">Zorlamalı tünel, değil hello Portalı aracılığıyla PowerShell kullanarak yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="8f2c8-110">Zorlanan hello Resource Manager dağıtım modeli için tünel tooconfigure istiyorsanız, Klasik makale açılır listeden aşağıdaki hello seçin:</span><span class="sxs-lookup"><span data-stu-id="8f2c8-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f2c8-111">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="8f2c8-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="8f2c8-112">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f2c8-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="8f2c8-113">Gereksinimleri ve konular</span><span class="sxs-lookup"><span data-stu-id="8f2c8-113">Requirements and considerations</span></span>
<span data-ttu-id="8f2c8-114">Zorlamalı tünel Azure'da sanal ağ kullanıcı tanımlı yolları (UDR) yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="8f2c8-115">Yeniden yönlendirme trafiği tooan site varsayılan yol toohello Azure VPN ağ geçidi olarak ifade edilir şirket içi.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="8f2c8-116">Merhaba aşağıdaki bölümde bir Azure sanal ağı hello yönlendirme tablosuna ve yollar sınırlama geçerli hello listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="8f2c8-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="8f2c8-117">Her sanal ağ alt yerleşik sistem yönlendirme tablosu vardır.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="8f2c8-118">Merhaba sistem yönlendirme tablosu aşağıdaki üç grup yolların hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8f2c8-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="8f2c8-119">**Yerel VNet yollar:** doğrudan toohello hedef VM'ler hello aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="8f2c8-120">**Şirket içi yollar:** toohello Azure VPN ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="8f2c8-121">**Varsayılan yol:** doğrudan toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="8f2c8-122">Merhaba önceki iki yolları tarafından kapsanmayan hedefleyen paketler toohello özel IP adresleri bırakılır.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="8f2c8-123">Kullanıcı tanımlı yolların Hello sürümle birlikte, varsayılan yol yönlendirme tablosu tooadd oluşturun ve bu alt ağlardaki tünel zorunlu hello yönlendirme tablosu tooyour sanal ağ alt ağı tooenable ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="8f2c8-124">Tooset "varsayılan site" Merhaba şirket içi yerel siteleri bağlı toohello sanal ağ arasında gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="8f2c8-125">Zorlamalı tünel dinamik yönlendirme VPN ağ geçidi (olmayan bir statik ağ geçidi) sahip bir sanal ağ ile ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="8f2c8-126">Zorlanan tünel ExpressRoute bu düzenek yapılandırılmamış, ancak bunun yerine, varsayılan rota hello ExpressRoute BGP üzerinden reklam tarafından etkinleştirilmiş eşliği oturumlarını.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="8f2c8-127">Lütfen hello bakın [ExpressRoute belgeleri](https://azure.microsoft.com/documentation/services/expressroute/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="8f2c8-128">Yapılandırmasına genel bakış</span><span class="sxs-lookup"><span data-stu-id="8f2c8-128">Configuration overview</span></span>
<span data-ttu-id="8f2c8-129">Aşağıdaki örneğine hello hello ön uç alt ağı değil zorlamalı tünel.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="8f2c8-130">Merhaba ön uç alt Hello iş yüklerini tooaccept devam et ve toocustomer isteklerini doğrudan Internet hello yanıt.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="8f2c8-131">Merhaba Orta katmanda ve arka uç alt zorlanır tünel.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="8f2c8-132">Bu iki alt toohello Internet tüm giden bağlantılar zorlanmış ya da yeniden yönlendirilen geri tooan şirket içi site S2S VPN tünelleri hello biri aracılığıyla olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="8f2c8-133">Bu toorestrict sağlar ve Internet erişimi, sanal makinelerden inceleme veya çok katmanlı bir hizmet Mimarinizi gerekli tooenable devam ederken, azure'daki hizmetlere bulut.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="8f2c8-134">Sanal ağlarınıza hiçbir Internet'e iş yükleri varsa zorlamalı tünel toohello tüm sanal ağların de uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Zorlamalı Tünel Oluşturma](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="8f2c8-136">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="8f2c8-136">Before you begin</span></span>
<span data-ttu-id="8f2c8-137">Aşağıdaki başlangıç yapılandırması önce öğelerindeki hello sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="8f2c8-138">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-138">An Azure subscription.</span></span> <span data-ttu-id="8f2c8-139">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8f2c8-140">Yapılandırılmış bir sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-140">A configured virtual network.</span></span> 
* <span data-ttu-id="8f2c8-141">en son sürümünü hello Azure PowerShell cmdlet'lerini Hello.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8f2c8-142">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="8f2c8-143">Zorlamalı tünel yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8f2c8-143">Configure forced tunneling</span></span>
<span data-ttu-id="8f2c8-144">Aşağıdaki yordamı hello için bir sanal ağ zorlamalı tünel belirtmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="8f2c8-145">Merhaba yapılandırma adımları toohello VNet ağ yapılandırma dosyası karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="8f2c8-146">Bu örnekte, hello sanal ağ 'MultiTier-VNet' üç alt ağa sahip değil: 'Ön uç', 'Midtier' ve 'Backend' alt ağlar, dört şirket içi ve dışı bağlantılar: 'DefaultSiteHQ' ve üç dalları.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="8f2c8-147">Merhaba adımları hello 'DefaultSiteHQ' hello varsayılan site bağlantısı zorlamalı tünel olarak ayarlayın ve zorlanan tünel hello Midtier ve arka uç alt ağlar toouse yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="8f2c8-148">Bir yönlendirme tablosu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-148">Create a routing table.</span></span> <span data-ttu-id="8f2c8-149">Cmdlet toocreate aşağıdaki hello yol tablosu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="8f2c8-150">Varsayılan rota toohello yönlendirme tablosu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="8f2c8-151">Merhaba aşağıdaki örnek 1. adımda oluşturduğunuz bir varsayılan rota toohello yönlendirme tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="8f2c8-152">Yalnızca desteklenen rota hello Not "0.0.0.0/0" toohello "VPNGateway" NextHop hello hedef öneki ' dir.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="8f2c8-153">Merhaba yönlendirme tablosu toohello alt ağları ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="8f2c8-154">Bir yönlendirme tablosu oluşturulur ve bir yol eklenir sonra örnek tooadd aşağıdaki hello kullanın veya hello rota tablosu tooa sanal ağ alt ağını ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="8f2c8-155">Merhaba örnek hello rota tablosu "MyRouteTable" toohello Midtier ve arka uç alt ağlar VNet MultiTier-VNet ekler.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="8f2c8-156">Varsayılan site zorlanan tünel için atayın.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="8f2c8-157">Adım önceki hello hello örnek cmdlet komutlar yönlendirme tablosunu hello oluşturulan ve hello rota tablosu tootwo hello sanal ağların ilişkili.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="8f2c8-158">Merhaba kalan tooselect bir yerel site hello çok siteli bağlantıları hello varsayılan siteyle veya tünel hello sanal ağ arasında bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="8f2c8-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="8f2c8-159">Ek PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="8f2c8-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="8f2c8-160">toodelete bir yol tablosu</span><span class="sxs-lookup"><span data-stu-id="8f2c8-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="8f2c8-161">toolist bir yol tablosu</span><span class="sxs-lookup"><span data-stu-id="8f2c8-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="8f2c8-162">toodelete giden bir yol tablosu bir yolu</span><span class="sxs-lookup"><span data-stu-id="8f2c8-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="8f2c8-163">tooremove bir alt ağdaki bir yol</span><span class="sxs-lookup"><span data-stu-id="8f2c8-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="8f2c8-164">bir alt ağla ilişkili toolist hello yol tablosu</span><span class="sxs-lookup"><span data-stu-id="8f2c8-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="8f2c8-165">bir sanal ağ VPN ağ geçidi varsayılan sitesinden tooremove</span><span class="sxs-lookup"><span data-stu-id="8f2c8-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```