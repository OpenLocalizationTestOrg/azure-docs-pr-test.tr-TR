---
title: "Zorlamalı tünel Azure siteden siteye bağlantıları için yapılandırın: Klasik | Microsoft Docs"
description: "Yeniden yönlendirme veya 'force' tüm Internet'e bağlı trafik, şirket içi konumuna geri nasıl."
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
ms.openlocfilehash: 79bf6892c823da282c3e763921e830f986419854
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-forced-tunneling-using-the-classic-deployment-model"></a><span data-ttu-id="997da-103">Klasik dağıtım modelini kullanarak zorlamalı tünel yapılandırma</span><span class="sxs-lookup"><span data-stu-id="997da-103">Configure forced tunneling using the classic deployment model</span></span>

<span data-ttu-id="997da-104">Zorlamalı tünel yeniden yönlendirme veya "tüm Internet'e bağlı trafik, denetleme ve denetim için bir siteden siteye VPN tüneli aracılığıyla şirket içi konumunuza geri zorla" olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="997da-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="997da-105">Bu, çoğu kurumsal BT için kritik güvenlik gereksinimdir ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="997da-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="997da-106">Zorlamalı tünel olmadan, Internet'e bağlı trafik, vm'lerden azure'da her zaman Azure ağ altyapısından doğrudan inceleme veya trafiği denetlemek için izin verme seçeneği olmadan Internet'e dizinlere.</span><span class="sxs-lookup"><span data-stu-id="997da-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="997da-107">Yetkisiz Internet erişimine potansiyel olarak bilgilerin açığa çıkmasına veya diğer tür güvenlik ihlallerini yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="997da-107">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="997da-108">Bu makalede Klasik dağıtım modeli kullanılarak oluşturulan sanal ağlar için tünel zorlanmış'ı yapılandıracağınız anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="997da-108">This article walks you through configuring forced tunneling for virtual networks created using the classic deployment model.</span></span> <span data-ttu-id="997da-109">Zorlamalı tünel, Portalı aracılığıyla değil, PowerShell kullanarak yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="997da-109">Forced tunneling can be configured by using PowerShell, not through the portal.</span></span> <span data-ttu-id="997da-110">Resource Manager dağıtım modeli için zorlamalı tünel yapılandırmak istiyorsanız, Klasik makale aşağıdaki açılan listeden seçin:</span><span class="sxs-lookup"><span data-stu-id="997da-110">If you want to configure forced tunneling for the Resource Manager deployment model, select classic article from the following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="997da-111">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="997da-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="997da-112">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="997da-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="997da-113">Gereksinimleri ve konular</span><span class="sxs-lookup"><span data-stu-id="997da-113">Requirements and considerations</span></span>
<span data-ttu-id="997da-114">Zorlamalı tünel Azure'da sanal ağ kullanıcı tanımlı yolları (UDR) yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="997da-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="997da-115">Bir şirket içi siteye trafiği yönlendirerek Azure VPN ağ geçidi için varsayılan bir yol olarak ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="997da-115">Redirecting traffic to an on-premises site is expressed as a Default Route to the Azure VPN gateway.</span></span> <span data-ttu-id="997da-116">Aşağıdaki bölümde, bir Azure sanal ağı için yönlendirme tablosunu ve yollar geçerli sınırlaması listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="997da-116">The following section lists the current limitation of the routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="997da-117">Her sanal ağ alt yerleşik sistem yönlendirme tablosu vardır.</span><span class="sxs-lookup"><span data-stu-id="997da-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="997da-118">Sistem yönlendirme tablosu yolların aşağıdaki üç grup vardır:</span><span class="sxs-lookup"><span data-stu-id="997da-118">The system routing table has the following three groups of routes:</span></span>

  * <span data-ttu-id="997da-119">**Yerel VNet yollar:** doğrudan hedefe Vm'leri aynı sanal ağda.</span><span class="sxs-lookup"><span data-stu-id="997da-119">**Local VNet routes:** Directly to the destination VMs in the same virtual network.</span></span>
  * <span data-ttu-id="997da-120">**Şirket içi yollar:** için Azure VPN ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="997da-120">**On-premises routes:** To the Azure VPN gateway.</span></span>
  * <span data-ttu-id="997da-121">**Varsayılan yol:** doğrudan Internet'e.</span><span class="sxs-lookup"><span data-stu-id="997da-121">**Default route:** Directly to the Internet.</span></span> <span data-ttu-id="997da-122">Önceki iki yoldan tarafından kapsanmayan özel IP adresleri giden paketler düşürülür.</span><span class="sxs-lookup"><span data-stu-id="997da-122">Packets destined to the private IP addresses not covered by the previous two routes will be dropped.</span></span>
* <span data-ttu-id="997da-123">Kullanıcı tanımlı yollar sürümle birlikte, varsayılan yol eklemek üzere bir yönlendirme tablosu oluşturun ve ardından bu alt ağlardaki zorlamalı tüneli etkinleştirmek için sanal ağ alt ağı için yönlendirme tablosunu ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="997da-123">With the release of user-defined routes, you can create a routing table to add a default route, and then associate the routing table to your VNet subnet(s) to enable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="997da-124">"Sanal ağa bağlı bir varsayılan site" şirket içi yerel siteleri arasında ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="997da-124">You need to set a "default site" among the cross-premises local sites connected to the virtual network.</span></span>
* <span data-ttu-id="997da-125">Zorlamalı tünel dinamik yönlendirme VPN ağ geçidi (olmayan bir statik ağ geçidi) sahip bir sanal ağ ile ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="997da-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="997da-126">Zorlanan tünel ExpressRoute bu düzenek yapılandırılmamış, ancak bunun yerine, varsayılan rota ExpressRoute BGP eşliği oturumlarını üzerinden reklam tarafından etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="997da-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via the ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="997da-127">Lütfen bakın [ExpressRoute belgeleri](https://azure.microsoft.com/documentation/services/expressroute/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="997da-127">Please see the [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="997da-128">Yapılandırmasına genel bakış</span><span class="sxs-lookup"><span data-stu-id="997da-128">Configuration overview</span></span>
<span data-ttu-id="997da-129">Aşağıdaki örnekte, ön uç alt ağı değil zorlamalı tünel.</span><span class="sxs-lookup"><span data-stu-id="997da-129">In the following example, the Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="997da-130">Ön uç alt iş yükleri kabul etmek ve doğrudan Internet'ten müşteri isteklerine yanıt vermek devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="997da-130">The workloads in the Frontend subnet can continue to accept and respond to customer requests from the Internet directly.</span></span> <span data-ttu-id="997da-131">Orta katman ve arka uç alt zorlamalı tünel.</span><span class="sxs-lookup"><span data-stu-id="997da-131">The Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="997da-132">Bu iki alt internet tüm giden bağlantılar zorlanmış veya siteye bir şirket içi S2S VPN tünelleri biri aracılığıyla yeniden yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="997da-132">Any outbound connections from these two subnets to the Internet will be forced or redirected back to an on-premises site via one of the S2S VPN tunnels.</span></span>

<span data-ttu-id="997da-133">Bu kısıtlama ve Internet erişimi, sanal makinelerden inceleme veya Bulut Hizmetleri, azure'da çok katmanlı bir hizmet Mimarinizi gerekli etkinleştirmek devam ederken olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="997da-133">This allows you to restrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing to enable your multi-tier service architecture required.</span></span> <span data-ttu-id="997da-134">Ayrıca, sanal ağlarınız hiçbir Internet'e iş yükleri varsa tüm sanal ağların zorlamalı tünel uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="997da-134">You also can apply forced tunneling to the entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Zorlamalı Tünel Oluşturma](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="997da-136">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="997da-136">Before you begin</span></span>
<span data-ttu-id="997da-137">Yapılandırmaya başlamadan önce aşağıdaki öğelerin bulunduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="997da-137">Verify that you have the following items before beginning configuration.</span></span>

* <span data-ttu-id="997da-138">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="997da-138">An Azure subscription.</span></span> <span data-ttu-id="997da-139">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="997da-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="997da-140">Yapılandırılmış bir sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="997da-140">A configured virtual network.</span></span> 
* <span data-ttu-id="997da-141">Azure PowerShell cmdlet'lerinin en son sürümü.</span><span class="sxs-lookup"><span data-stu-id="997da-141">The latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="997da-142">PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz. [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="997da-142">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="997da-143">Zorlamalı tünel yapılandırma</span><span class="sxs-lookup"><span data-stu-id="997da-143">Configure forced tunneling</span></span>
<span data-ttu-id="997da-144">Aşağıdaki yordam için bir sanal ağ zorlamalı tünel belirtmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="997da-144">The following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="997da-145">Yapılandırma adımları sanal ağ yapılandırma dosyasına karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="997da-145">The configuration steps correspond to the VNet network configuration file.</span></span>

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

<span data-ttu-id="997da-146">Bu örnekte, sanal ağ 'MultiTier-VNet' üç alt ağa sahip değil: 'Ön uç', 'Midtier' ve 'Backend' alt ağlar, dört şirket içi ve dışı bağlantılar: 'DefaultSiteHQ' ve üç dalları.</span><span class="sxs-lookup"><span data-stu-id="997da-146">In this example, the virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="997da-147">Adımları zorlanan tünel 'DefaultSiteHQ' varsayılan site bağlantısı olarak ayarlayın ve Midtier yapılandırmak ve kullanmak için arka uç alt ağlar zorlanan tünel.</span><span class="sxs-lookup"><span data-stu-id="997da-147">The steps will set the 'DefaultSiteHQ' as the default site connection for forced tunneling, and configure the Midtier and Backend subnets to use forced tunneling.</span></span>

1. <span data-ttu-id="997da-148">Bir yönlendirme tablosu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="997da-148">Create a routing table.</span></span> <span data-ttu-id="997da-149">Yol tablosu oluşturmak için aşağıdaki cmdlet'i kullanın.</span><span class="sxs-lookup"><span data-stu-id="997da-149">Use the following cmdlet to create your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="997da-150">Varsayılan rota yönlendirme tablosuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="997da-150">Add a default route to the routing table.</span></span> 

  <span data-ttu-id="997da-151">Aşağıdaki örnek varsayılan yolun 1. adımda oluşturduğunuz yönlendirme tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="997da-151">The following example adds a default route to the routing table created in Step 1.</span></span> <span data-ttu-id="997da-152">Yalnızca rota desteklenen Not "VPNGateway" NextHop için "0.0.0.0/0" hedef önekidir.</span><span class="sxs-lookup"><span data-stu-id="997da-152">Note that the only route supported is the destination prefix of "0.0.0.0/0" to the "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="997da-153">Alt ağlar için yönlendirme tablosunu ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="997da-153">Associate the routing table to the subnets.</span></span> 

  <span data-ttu-id="997da-154">Bir yönlendirme tablosu oluşturulur ve bir yol eklenir sonra eklemek veya bir sanal ağ alt ağı için yol tablosu ilişkilendirmek için aşağıdaki örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="997da-154">After a routing table is created and a route added, use the following example to add or associate the route table to a VNet subnet.</span></span> <span data-ttu-id="997da-155">Örnek Midtier ve arka uç alt ağlar VNet MultiTier-VNet için yol tablosu "MyRouteTable" ekler.</span><span class="sxs-lookup"><span data-stu-id="997da-155">The example adds the route table "MyRouteTable" to the Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="997da-156">Varsayılan site zorlanan tünel için atayın.</span><span class="sxs-lookup"><span data-stu-id="997da-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="997da-157">Önceki adımda, örnek cmdlet komutlar yönlendirme tablosu oluşturulur ve iki sanal ağ alt ağ için yol tablosu ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="997da-157">In the preceding step, the sample cmdlet scripts created the routing table and associated the route table to two of the VNet subnets.</span></span> <span data-ttu-id="997da-158">Kalan sanal ağın çok siteli bağlantıları arasında yerel bir site varsayılan site veya tünel seçmek için bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="997da-158">The remaining step is to select a local site among the multi-site connections of the virtual network as the default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="997da-159">Ek PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="997da-159">Additional PowerShell cmdlets</span></span>
### <a name="to-delete-a-route-table"></a><span data-ttu-id="997da-160">Bir yol tablosu silmek için</span><span class="sxs-lookup"><span data-stu-id="997da-160">To delete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="to-list-a-route-table"></a><span data-ttu-id="997da-161">Bir yol tablosu listelemek için</span><span class="sxs-lookup"><span data-stu-id="997da-161">To list a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="to-delete-a-route-from-a-route-table"></a><span data-ttu-id="997da-162">Bir rota tablosundan bir yolu silmek için</span><span class="sxs-lookup"><span data-stu-id="997da-162">To delete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="to-remove-a-route-from-a-subnet"></a><span data-ttu-id="997da-163">Bir alt ağdan bir rota kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="997da-163">To remove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="to-list-the-route-table-associated-with-a-subnet"></a><span data-ttu-id="997da-164">Bir alt ağ ile ilişkili yol tablosu listelemek için</span><span class="sxs-lookup"><span data-stu-id="997da-164">To list the route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="to-remove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="997da-165">Sanal ağ VPN ağ geçidi'nden bir varsayılan siteyi kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="997da-165">To remove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```