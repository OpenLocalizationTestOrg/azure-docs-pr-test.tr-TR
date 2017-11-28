---
title: "Klasik sanal ağlar Azure Resource Manager sanal ağlara bağlanma: PowerShell | Microsoft Docs"
description: "Klasik sanal ağlar ve Resource Manager VPN ağ geçidi ve PowerShell kullanarak sanal ağlar arasında bir VPN bağlantısı oluşturma hakkında bilgi edinin"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 842a32e5304977af92706cdda464286983122247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="fb818-103">PowerShell kullanarak farklı dağıtım modellerindeki sanal ağları birbirine bağlama</span><span class="sxs-lookup"><span data-stu-id="fb818-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="fb818-104">Bu makalede Resource Manager birbirleri ile iletişim kurmak için ayrı bir dağıtım modellerindeki kaynaklara izin vermek için sanal ağlar için Klasik sanal ağlara bağlanma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fb818-104">This article shows you how to connect classic VNets to Resource Manager VNets to allow the resources located in the separate deployment models to communicate with each other.</span></span> <span data-ttu-id="fb818-105">Bu makaledeki adımları PowerShell kullanın, ancak makaleyi bu listeden seçerek Azure Portalı'nı kullanarak bu yapılandırmayı de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb818-105">The steps in this article use PowerShell, but you can also create this configuration using the Azure portal by selecting the article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb818-106">Portal</span><span class="sxs-lookup"><span data-stu-id="fb818-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="fb818-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb818-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="fb818-108">Bir Resource Manager Vnet'i klasik bir VNet bağlama, bir şirket içi site konumuna bir sanal ağa bağlanma benzer.</span><span class="sxs-lookup"><span data-stu-id="fb818-108">Connecting a classic VNet to a Resource Manager VNet is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="fb818-109">Her iki bağlantı türü de IPsec/IKE kullanarak güvenli bir tünel sunmak üzere bir VPN ağ geçidi kullanır.</span><span class="sxs-lookup"><span data-stu-id="fb818-109">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="fb818-110">Farklı Aboneliklerde ve farklı bölgelerdeki sanal ağlar arasında bir bağlantı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb818-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="fb818-111">Dinamik ya da rota tabanlı ağ geçidi ile yapılandırılmamış olduğu sürece şirket içi ağlara bağlantılar zaten sanal ağlar da bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb818-111">You can also connect VNets that already have connections to on-premises networks, as long as the gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="fb818-112">Sanal ağlar arası bağlantılar hakkında daha fazla bilgi için bu makalenin sonunda yer alan [Sanal ağlar arası bağlantılar hakkında SSS](#faq) bölümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="fb818-112">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span> 

<span data-ttu-id="fb818-113">Sanal ağlar aynı bölgede varsa, bunun yerine bunları VNet eşlemesi kullanmanın bağlayarak göz önünde bulundurun isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb818-113">If your VNets are in the same region, you may want to instead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="fb818-114">VNet eşlemesi VPN ağ geçidini kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="fb818-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="fb818-115">Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb818-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="fb818-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="fb818-116">Before beginning</span></span>

<span data-ttu-id="fb818-117">Aşağıdaki adımlar, her sanal ağ için dinamik veya rota tabanlı ağ geçidi yapılandırmak ve ağ geçitleri arasında bir VPN bağlantısı oluşturmak gerekli ayarları size yol.</span><span class="sxs-lookup"><span data-stu-id="fb818-117">The following steps walk you through the settings necessary to configure a dynamic or route-based gateway for each VNet and create a VPN connection between the gateways.</span></span> <span data-ttu-id="fb818-118">Bu yapılandırma, statik veya ilke tabanlı ağ geçitleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="fb818-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fb818-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fb818-119">Prerequisites</span></span>

* <span data-ttu-id="fb818-120">Her iki Vnet'in zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="fb818-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="fb818-121">Sanal ağlar için adres aralıklarını değil birbirleri ile üst üste veya ağ geçitleri bağlı olabilir diğer bağlantılar için aralıklardan herhangi biriyle çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="fb818-121">The address ranges for the VNets do not overlap with each other, or overlap with any of the ranges for other connections that the gateways may be connected to.</span></span>
* <span data-ttu-id="fb818-122">En son PowerShell cmdlet'leri yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="fb818-122">You have installed the latest PowerShell cmdlets.</span></span> <span data-ttu-id="fb818-123">Bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="fb818-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="fb818-124">Hizmet Yönetimi (SM) ve Kaynak Yöneticisi (RM) cmdlet'leri yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="fb818-124">Make sure you install both the Service Management (SM) and the Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="fb818-125"><a name="exampleref"></a>Örnek ayarlar</span><span class="sxs-lookup"><span data-stu-id="fb818-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="fb818-126">Bu değerleri kullanarak bir test ortamı oluşturabilir veya bu makaledeki örnekleri daha iyi anlamak için bunlara bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb818-126">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

<span data-ttu-id="fb818-127">**Klasik VNet ayarları**</span><span class="sxs-lookup"><span data-stu-id="fb818-127">**Classic VNet settings**</span></span>

<span data-ttu-id="fb818-128">Sanal ağ adı ClassicVNet =</span><span class="sxs-lookup"><span data-stu-id="fb818-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="fb818-129">Konum Batı ABD =</span><span class="sxs-lookup"><span data-stu-id="fb818-129">Location = West US</span></span> <br>
<span data-ttu-id="fb818-130">Sanal ağ adres alanları 10.0.0.0/24 =</span><span class="sxs-lookup"><span data-stu-id="fb818-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="fb818-131">Alt ağ 1 10.0.0.0/27 =</span><span class="sxs-lookup"><span data-stu-id="fb818-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="fb818-132">GatewaySubnet 10.0.0.32/29 =</span><span class="sxs-lookup"><span data-stu-id="fb818-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="fb818-133">Yerel ağ adı RMVNetLocal =</span><span class="sxs-lookup"><span data-stu-id="fb818-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="fb818-134">GatewayType DynamicRouting =</span><span class="sxs-lookup"><span data-stu-id="fb818-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="fb818-135">**Resource Manager Vnet'i ayarları**</span><span class="sxs-lookup"><span data-stu-id="fb818-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="fb818-136">Sanal ağ adı RMVNet =</span><span class="sxs-lookup"><span data-stu-id="fb818-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="fb818-137">Kaynak grubu RG1 =</span><span class="sxs-lookup"><span data-stu-id="fb818-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="fb818-138">Sanal ağ IP adresi alanları 192.168.0.0/16 =</span><span class="sxs-lookup"><span data-stu-id="fb818-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="fb818-139">Alt ağ 1 192.168.1.0/24 =</span><span class="sxs-lookup"><span data-stu-id="fb818-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="fb818-140">GatewaySubnet 192.168.0.0/26 =</span><span class="sxs-lookup"><span data-stu-id="fb818-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="fb818-141">Konum Doğu ABD =</span><span class="sxs-lookup"><span data-stu-id="fb818-141">Location = East US</span></span> <br>
<span data-ttu-id="fb818-142">Ağ geçidi genel IP adı gwpip =</span><span class="sxs-lookup"><span data-stu-id="fb818-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="fb818-143">Yerel ağ geçidi ClassicVNetLocal =</span><span class="sxs-lookup"><span data-stu-id="fb818-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="fb818-144">Sanal ağ geçidi adı RMGateway =</span><span class="sxs-lookup"><span data-stu-id="fb818-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="fb818-145">Ağ geçidi IP adresleme yapılandırmasını gwipconfig =</span><span class="sxs-lookup"><span data-stu-id="fb818-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="fb818-146"><a name="createsmgw"></a>1. Bölüm - Klasik VNet yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fb818-146"><a name="createsmgw"></a>Section 1 - Configure the classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="fb818-147">Bölüm 1 - ağ yapılandırma dosyası indirme</span><span class="sxs-lookup"><span data-stu-id="fb818-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="fb818-148">PowerShell konsolunda yükseltilmiş haklara sahip Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fb818-148">Log in to your Azure account in the PowerShell console with elevated rights.</span></span> <span data-ttu-id="fb818-149">Aşağıdaki cmdlet'i Azure hesabınız için oturum açma kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="fb818-149">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="fb818-150">Oturum açtıktan sonra, Azure PowerShell'de kullanabilmeniz için hesap ayarlarınızı indirir.</span><span class="sxs-lookup"><span data-stu-id="fb818-150">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span> <span data-ttu-id="fb818-151">Bu yapılandırmanın parçası tamamlamak için SM PowerShell cmdlet'lerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb818-151">You use the SM PowerShell cmdlets to complete this part of the configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="fb818-152">Azure ağı yapılandırma dosyanızda aşağıdaki komutu çalıştırarak dışa aktarın.</span><span class="sxs-lookup"><span data-stu-id="fb818-152">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="fb818-153">Farklı bir konum gerekirse dışa aktarılacak dosya konumunu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb818-153">You can change the location of the file to export to a different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="fb818-154">İndirilen düzenlemek için .xml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="fb818-154">Open the .xml file that you downloaded to edit it.</span></span> <span data-ttu-id="fb818-155">Ağ yapılandırma dosyası örneği için bkz: [ağ yapılandırma şeması](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb818-155">For an example of the network configuration file, see the [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-the-gateway-subnet"></a><span data-ttu-id="fb818-156">Bölüm 2 - ağ geçidi alt ağını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="fb818-156">Part 2 -Verify the gateway subnet</span></span>
<span data-ttu-id="fb818-157">İçinde **VirtualNetworkSites** öğesi değil zaten oluşturulmuş bir Vnet'inizi için bir ağ geçidi alt ağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fb818-157">In the **VirtualNetworkSites** element, add a gateway subnet to your VNet if one has not already been created.</span></span> <span data-ttu-id="fb818-158">Ağ yapılandırma dosyası ile çalışırken, ağ geçidi alt ağı "GatewaySubnet" adlı gerekir veya Azure algılar ve bir ağ geçidi alt ağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb818-158">When working with the network configuration file, the gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="fb818-159">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="fb818-159">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-the-local-network-site"></a><span data-ttu-id="fb818-160">Bölüm 3 - yerel ağ sitesi ekleme</span><span class="sxs-lookup"><span data-stu-id="fb818-160">Part 3 - Add the local network site</span></span>
<span data-ttu-id="fb818-161">Eklediğiniz yerel ağ sitesine bağlanmak istediğiniz RM VNet temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fb818-161">The local network site you add represents the RM VNet to which you want to connect.</span></span> <span data-ttu-id="fb818-162">Ekleme bir **LocalNetworkSites** zaten yoksa, dosyaya öğesi.</span><span class="sxs-lookup"><span data-stu-id="fb818-162">Add a **LocalNetworkSites** element to the file if one doesn't already exist.</span></span> <span data-ttu-id="fb818-163">Bu noktada biz henüz Resource Manager Vnet'i için ağ geçidi oluşturmadınız çünkü yapılandırmasında VPNGatewayAddress herhangi bir geçerli ortak IP adresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="fb818-163">At this point in the configuration, the VPNGatewayAddress can be any valid public IP address because we haven't yet created the gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="fb818-164">Biz ağ geçidini oluşturduktan sonra Biz bu yer tutucu IP adresi RM ağ geçidine atanmış doğru ortak IP adresi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fb818-164">Once we create the gateway, we replace this placeholder IP address with the correct public IP address that has been assigned to the RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-the-vnet-with-the-local-network-site"></a><span data-ttu-id="fb818-165">Bölüm 4 - VNet yerel ağ sitesi ile ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="fb818-165">Part 4 - Associate the VNet with the local network site</span></span>
<span data-ttu-id="fb818-166">Bu bölümde, Vnet'e bağlanmak istediğiniz yerel ağ sitesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="fb818-166">In this section, we specify the local network site that you want to connect the VNet to.</span></span> <span data-ttu-id="fb818-167">Bu durumda, daha önce başvurulan Resource Manager Vnet'i olur.</span><span class="sxs-lookup"><span data-stu-id="fb818-167">In this case, it is the Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="fb818-168">Eşleşen adları emin olun.</span><span class="sxs-lookup"><span data-stu-id="fb818-168">Make sure the names match.</span></span> <span data-ttu-id="fb818-169">Bu adım, bir ağ geçidi oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="fb818-169">This step does not create a gateway.</span></span> <span data-ttu-id="fb818-170">Ağ geçidi bağlanacağı yerel ağ belirtir.</span><span class="sxs-lookup"><span data-stu-id="fb818-170">It specifies the local network that the gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-the-file-and-upload"></a><span data-ttu-id="fb818-171">Bölüm 5 - karşıya yükleme ve dosyayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="fb818-171">Part 5 - Save the file and upload</span></span>
<span data-ttu-id="fb818-172">Dosyayı kaydedin ve ardından aşağıdaki komutu çalıştırarak Azure'a alın.</span><span class="sxs-lookup"><span data-stu-id="fb818-172">Save the file, then import it to Azure by running the following command.</span></span> <span data-ttu-id="fb818-173">Ortamınız için gerektiği gibi dosya yolu değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="fb818-173">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="fb818-174">İçeri aktarma başarılı olduğunu gösteren benzer bir sonuç görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fb818-174">You will see a similar result showing that the import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-the-gateway"></a><span data-ttu-id="fb818-175">Bölüm 6 - ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb818-175">Part 6 - Create the gateway</span></span>

<span data-ttu-id="fb818-176">Bu örneği çalıştırmadan önce görmek için Azure bekliyor tam adları için indirdiğiniz ağ yapılandırma dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="fb818-176">Before running this example, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="fb818-177">Ağ yapılandırma dosyası, Klasik sanal ağlar için değerleri içerir.</span><span class="sxs-lookup"><span data-stu-id="fb818-177">The network configuration file contains the values for your classic virtual networks.</span></span> <span data-ttu-id="fb818-178">Bazen adları Klasik sanal ağlar için dağıtım modelleri farklılıkları nedeniyle Azure portalında Klasik VNet ayarlarını oluştururken, ağ yapılandırma dosyasında değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="fb818-178">Sometimes the names for classic VNets are changed in the network configuration file when creating classic VNet settings in the Azure portal due to the differences in the deployment models.</span></span> <span data-ttu-id="fb818-179">Örneğin, Klasik VNet 'Klasik VNet' adlı ve 'ClassicRG' adlı bir kaynak grubunda oluşturulan oluşturmak için Azure Portalı'nı kullandıysanız, ağ yapılandırma dosyasında yer alan adı 'Grup ClassicRG Klasik VNet' dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="fb818-179">For example, if you used the Azure portal to create a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', the name that is contained in the network configuration file is converted to 'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="fb818-180">Boşluk içeren bir sanal ağ adı belirtirken, değeri tırnak işaretleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb818-180">When specifying the name of a VNet that contains spaces, use quotation marks around the value.</span></span>


<span data-ttu-id="fb818-181">Dinamik yönlendirme ağ geçidi oluşturmak için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="fb818-181">Use the following example to create a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="fb818-182">Kullanarak ağ geçidi durumunu kontrol edebilirsiniz **Get-AzureVNetGateway** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="fb818-182">You can check the status of the gateway by using the **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="fb818-183"><a name="creatermgw"></a>Bölüm 2: RM VNet ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fb818-183"><a name="creatermgw"></a>Section 2: Configure the RM VNet gateway</span></span>
<span data-ttu-id="fb818-184">RM VNet için VPN ağ geçidi oluşturmak için aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="fb818-184">To create a VPN gateway for the RM VNet, follow the following instructions.</span></span> <span data-ttu-id="fb818-185">Klasik sanal ağınızın ağ geçidi için genel IP adresi aldıktan sonra kadar adımları başlatmayın.</span><span class="sxs-lookup"><span data-stu-id="fb818-185">Don't start the steps until after you have retrieved the public IP address for the classic VNet's gateway.</span></span> 

1. <span data-ttu-id="fb818-186">PowerShell konsolundaki Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fb818-186">Log in to your Azure account in the PowerShell console.</span></span> <span data-ttu-id="fb818-187">Aşağıdaki cmdlet'i Azure hesabınız için oturum açma kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="fb818-187">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="fb818-188">Oturum açtıktan sonra Azure PowerShell kullanılabilir olacak şekilde, hesap ayarlarınızı karşıdan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fb818-188">After logging in, your account settings are downloaded so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="fb818-189">Birden fazla aboneliğiniz varsa, Azure aboneliklerinize listesini alın.</span><span class="sxs-lookup"><span data-stu-id="fb818-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="fb818-190">Kullanmak istediğiniz aboneliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="fb818-190">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="fb818-191">Bir yerel ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fb818-191">Create a local network gateway.</span></span> <span data-ttu-id="fb818-192">Sanal bir ağda, yerel ağ geçidi genellikle şirket içi konumunuz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fb818-192">In a virtual network, the local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="fb818-193">Bu durumda, yerel ağ geçidi Klasik ağınızı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fb818-193">In this case, the local network gateway refers to your Classic VNet.</span></span> <span data-ttu-id="fb818-194">Olarak Azure başvurduğu ve ayrıca adres alanı ön ekini belirtin bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="fb818-194">Give it a name by which Azure can refer to it, and also specify the address space prefix.</span></span> <span data-ttu-id="fb818-195">Azure, belirttiğiniz IP adresi ön ekini kullanarak hangi trafiğin şirket içi konumunuza gönderileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="fb818-195">Azure uses the IP address prefix you specify to identify which traffic to send to your on-premises location.</span></span> <span data-ttu-id="fb818-196">Burada yer alan bilgiler, daha sonra ağ geçidi oluşturmadan önce ayarlamanız gerekip gerekmediğine değerleri değiştirin ve örnek yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fb818-196">If you need to adjust the information here later, before creating your gateway, you can modify the values and run the sample again.</span></span>
   
   <span data-ttu-id="fb818-197">**-Name** yerel ağ geçidine başvurmak için atamak istediğiniz addır.</span><span class="sxs-lookup"><span data-stu-id="fb818-197">**-Name** is the name you want to assign to refer to the local network gateway.</span></span><br><span data-ttu-id="fb818-198">
   **-AddressPrefix** Klasik ağınız için adres alanıdır.</span><span class="sxs-lookup"><span data-stu-id="fb818-198">
   **-AddressPrefix** is the Address Space for your classic VNet.</span></span><br><span data-ttu-id="fb818-199">
**-Gatewayıpaddress** Klasik sanal ağınızın ağ geçidinin genel IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="fb818-199">
**-GatewayIpAddress** is the public IP address of the classic VNet's gateway.</span></span> <span data-ttu-id="fb818-200">Aşağıdaki örnek doğru IP adresini gösterecek şekilde değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="fb818-200">Be sure to change the following sample to reflect the correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="fb818-201">Resource Manager Vnet'i için sanal ağ geçidine ayrılacak genel IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="fb818-201">Request a public IP address to be allocated to the virtual network gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="fb818-202">Kullanmak istediğiniz IP adresini belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb818-202">You can't specify the IP address that you want to use.</span></span> <span data-ttu-id="fb818-203">IP adresi, sanal ağ geçidi olarak dinamik olarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="fb818-203">The IP address is dynamically allocated to the virtual network gateway.</span></span> <span data-ttu-id="fb818-204">Ancak bu, IP adresinin değiştiği anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="fb818-204">However, this does not mean the IP address changes.</span></span> <span data-ttu-id="fb818-205">Yalnızca bir kez sanal ağ geçidi IP adresi değişiklikleri olduğunda ağ geçidi silinip yeniden.</span><span class="sxs-lookup"><span data-stu-id="fb818-205">The only time the virtual network gateway IP address changes is when the gateway is deleted and recreated.</span></span> <span data-ttu-id="fb818-206">Yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında ağ geçidi değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="fb818-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of the gateway.</span></span>

  <span data-ttu-id="fb818-207">Bu adımda, biz de bir sonraki adımda kullanılan bir değişken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fb818-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="fb818-208">Sanal ağınızın ağ geçidi alt ağı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fb818-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="fb818-209">Hiçbir ağ geçidi alt ağı varsa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fb818-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="fb818-210">Ağ geçidi alt ağı adlandırılan emin olun *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="fb818-210">Make sure the gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="fb818-211">Aşağıdaki komutu çalıştırarak ağ geçidi için kullanılan alt ağ alın.</span><span class="sxs-lookup"><span data-stu-id="fb818-211">Retrieve the subnet used for the gateway by running the following command.</span></span> <span data-ttu-id="fb818-212">Bu adımda, biz de sonraki adımda kullanılması için bir değişken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fb818-212">In this step, we also set a variable to be used in the next step.</span></span>
   
   <span data-ttu-id="fb818-213">**-Name** Resource Manager Vnet'i adıdır.</span><span class="sxs-lookup"><span data-stu-id="fb818-213">**-Name** is the name of your Resource Manager VNet.</span></span><br><span data-ttu-id="fb818-214">
   **-ResourceGroupName** VNet ilişkili olduğu kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="fb818-214">
**-ResourceGroupName** is the resource group that the VNet is associated with.</span></span> <span data-ttu-id="fb818-215">Ağ geçidi alt ağı için bu sanal ağ zaten mevcut olmalıdır ve adlandırılmalıdır *GatewaySubnet* düzgün çalışması için.</span><span class="sxs-lookup"><span data-stu-id="fb818-215">The gateway subnet must already exist for this VNet and must be named *GatewaySubnet* to work properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="fb818-216">Ağ geçidi IP adresleme yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fb818-216">Create the gateway IP addressing configuration.</span></span> <span data-ttu-id="fb818-217">Ağ geçidi yapılandırması, kullanılacak alt ağı ve genel IP adresini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fb818-217">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="fb818-218">Ağ geçidi yapılandırmanızı oluşturmak için aşağıdaki örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb818-218">Use the following sample to create your gateway configuration.</span></span>

  <span data-ttu-id="fb818-219">Bu adımda, **- SubnetId** ve **- PublicIpAddressId** parametreleri gerekir bayraklarıdır ID özelliği alt ağ ve IP adresi nesneleri, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="fb818-219">In this step, the **-SubnetId** and **-PublicIpAddressId** parameters must be passed the id property from the subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="fb818-220">Basit bir dize kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="fb818-220">You can't use a simple string.</span></span> <span data-ttu-id="fb818-221">Adımda, bir ortak IP ve adım alt almak için istemek için bu değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fb818-221">These variables are set in the step to request a public IP and the step to retrieve the subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="fb818-222">Aşağıdaki komutu çalıştırarak Resource Manager sanal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fb818-222">Create the Resource Manager virtual network gateway by running the following command.</span></span> <span data-ttu-id="fb818-223">`-VpnType` Olmalıdır *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="fb818-223">The `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="fb818-224">45 dakika veya daha fazla ağ geçidinin oluşturulması alabilir.</span><span class="sxs-lookup"><span data-stu-id="fb818-224">It can take 45 minutes or more for the gateway to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="fb818-225">VPN ağ geçidi oluşturulduktan sonra genel IP adresini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="fb818-225">Copy the public IP address once the VPN gateway has been created.</span></span> <span data-ttu-id="fb818-226">Klasik VNet yerel ağ ayarlarını yapılandırırken kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb818-226">You use it when you configure the local network settings for your Classic VNet.</span></span> <span data-ttu-id="fb818-227">Genel IP adresi almak için aşağıdaki cmdlet'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb818-227">You can use the following cmdlet to retrieve the public IP address.</span></span> <span data-ttu-id="fb818-228">Genel IP adresi, dönüş olarak listelenen *IPADDRESS*.</span><span class="sxs-lookup"><span data-stu-id="fb818-228">The public IP address is listed in the return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-the-classic-vnet-local-site-settings"></a><span data-ttu-id="fb818-229">Bölüm 3: Klasik VNet yerel site ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="fb818-229">Section 3: Modify the classic VNet local site settings</span></span>

<span data-ttu-id="fb818-230">Bu bölümde, Klasik VNet ile birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="fb818-230">In this section, you work with the classic VNet.</span></span> <span data-ttu-id="fb818-231">Resource Manager Vnet'i ağ geçidine bağlanmak için kullanılan yerel site ayarlarını belirtmek için kullanılan yer tutucu IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fb818-231">You replace the placeholder IP address that you used when specifying the local site settings that will be used to connect to the Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="fb818-232">Ağ yapılandırma dosyasını dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="fb818-232">Export the network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="fb818-233">Bir metin düzenleyicisi kullanarak, değer VPNGatewayAddress için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fb818-233">Using a text editor, modify the value for VPNGatewayAddress.</span></span> <span data-ttu-id="fb818-234">Resource Manager ağ geçidi genel IP adresiyle yer tutucu IP adresini değiştirin ve değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fb818-234">Replace the placeholder IP address with the public IP address of the Resource Manager gateway and then save the changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="fb818-235">Değiştirilen ağ yapılandırma dosyasını Azure'a içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="fb818-235">Import the modified network configuration file to Azure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="fb818-236"><a name="connect"></a>4. Bölüm: ağ geçitleri arasında bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb818-236"><a name="connect"></a>Section 4: Create a connection between the gateways</span></span>
<span data-ttu-id="fb818-237">Ağ geçitleri arasında bir bağlantı oluşturmak için PowerShell gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb818-237">Creating a connection between the gateways requires PowerShell.</span></span> <span data-ttu-id="fb818-238">PowerShell cmdlet'leri Klasik sürümü kullanmak için Azure hesabınız eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="fb818-238">You may need to add your Azure Account to use the classic version of the  PowerShell cmdlets.</span></span> <span data-ttu-id="fb818-239">Bunu yapmak için kullanın **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="fb818-239">To do so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="fb818-240">PowerShell konsolunda paylaşılan anahtarınız ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fb818-240">In the PowerShell console, set your shared key.</span></span> <span data-ttu-id="fb818-241">Cmdlet'leri çalıştırmadan önce görmek için Azure bekliyor tam adları için indirdiğiniz ağ yapılandırma dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="fb818-241">Before running the cmdlets, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="fb818-242">Boşluk içeren bir sanal ağ adı belirtirken, değeri tek tırnak işareti kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb818-242">When specifying the name of a VNet that contains spaces, use single quotation marks around the value.</span></span><br><br><span data-ttu-id="fb818-243">Aşağıdaki örnekte, **- vnetname adlı** Klasik VNet adıdır ve **- LocalNetworkSiteName** yerel ağ sitesi için belirtilen ad.</span><span class="sxs-lookup"><span data-stu-id="fb818-243">In following example, **-VNetName** is the name of the classic VNet and **-LocalNetworkSiteName** is the name you specified for the local network site.</span></span> <span data-ttu-id="fb818-244">**- SharedKey** oluşturmak ve belirten bir değer.</span><span class="sxs-lookup"><span data-stu-id="fb818-244">The **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="fb818-245">Örnekte 'abc123' kullandık ancak oluşturabilir ve daha karmaşık bir şey kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb818-245">In the example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="fb818-246">Burada belirttiğiniz değer bağlantınızı oluştururken sonraki adımda belirttiğiniz değerle aynı değere olmalıdır önemli şeydir.</span><span class="sxs-lookup"><span data-stu-id="fb818-246">The important thing is that the value you specify here must be the same value that you specify in the next step when you create your connection.</span></span> <span data-ttu-id="fb818-247">Dönüş göstermelidir **durumu: başarılı**.</span><span class="sxs-lookup"><span data-stu-id="fb818-247">The return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="fb818-248">Aşağıdaki komutları çalıştırarak VPN bağlantısı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fb818-248">Create the VPN connection by running the following commands:</span></span>
   
  <span data-ttu-id="fb818-249">Değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fb818-249">Set the variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="fb818-250">Bağlantıyı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fb818-250">Create the connection.</span></span> <span data-ttu-id="fb818-251">Dikkat **- ConnectionType** IPSec, Vnet2Vnet değil.</span><span class="sxs-lookup"><span data-stu-id="fb818-251">Notice that the **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="fb818-252">Bölüm 5: bağlantılarınızı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="fb818-252">Section 5: Verify your connections</span></span>

### <a name="to-verify-the-connection-from-your-classic-vnet-to-your-resource-manager-vnet"></a><span data-ttu-id="fb818-253">Resource Manager Vnet'i Klasik VNet arasında bağlantı doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="fb818-253">To verify the connection from your classic VNet to your Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="fb818-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb818-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="fb818-255">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="fb818-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="to-verify-the-connection-from-your-resource-manager-vnet-to-your-classic-vnet"></a><span data-ttu-id="fb818-256">Resource Manager Vnet'i bağlantısından Klasik vnet doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="fb818-256">To verify the connection from your Resource Manager VNet to your classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="fb818-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb818-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="fb818-258">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="fb818-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="fb818-259"><a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="fb818-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

