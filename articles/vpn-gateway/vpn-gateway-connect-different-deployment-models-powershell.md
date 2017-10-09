---
title: "Klasik sanal ağlar tooAzure Resource Manager sanal ağlara bağlanma: PowerShell | Microsoft Docs"
description: "Bilgi nasıl toocreate Klasik sanal ağlar ve Resource Manager VPN ağ geçidi ve PowerShell kullanarak sanal ağlar arasında bir VPN bağlantısı"
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
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="8986f-103">PowerShell kullanarak farklı dağıtım modellerindeki sanal ağları birbirine bağlama</span><span class="sxs-lookup"><span data-stu-id="8986f-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="8986f-104">Bu makale size nasıl tooconnect Klasik sanal ağlar tooResource Yöneticisi sanal ağlar tooallow hello hello ayrı dağıtım modelleri toocommunicate birbirleriyle bulunan kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="8986f-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="8986f-105">Hello adımları bu makalede PowerShell kullanın ancak bu listeden hello makale seçerek hello Azure portal kullanarak bu yapılandırmayı da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8986f-105">hello steps in this article use PowerShell, but you can also create this configuration using hello Azure portal by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8986f-106">Portal</span><span class="sxs-lookup"><span data-stu-id="8986f-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="8986f-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8986f-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="8986f-108">Resource Manager Vnet'i klasik bir VNet tooa bağlanma benzer tooconnecting bir VNet tooan şirket içi site konumu değil.</span><span class="sxs-lookup"><span data-stu-id="8986f-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="8986f-109">Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın.</span><span class="sxs-lookup"><span data-stu-id="8986f-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="8986f-110">Farklı Aboneliklerde ve farklı bölgelerdeki sanal ağlar arasında bir bağlantı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8986f-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="8986f-111">Dinamik ya da rota tabanlı ile yapılandırıldığını hello ağ geçidi olduğu sürece bağlantıları tooon içi ağlar, zaten sanal ağlar da bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8986f-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="8986f-112">VNet-VNet bağlantıları hakkında daha fazla bilgi için bkz: Merhaba [VNet-VNet ile ilgili SSS](#faq) hello bu makalenin sonunda.</span><span class="sxs-lookup"><span data-stu-id="8986f-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="8986f-113">Sanal ağlar hello varsa aynı bölgede isteyebilir tooinstead VNet eşlemesi kullanarak bunları bağlanma göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="8986f-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="8986f-114">VNet eşlemesi VPN ağ geçidini kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="8986f-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="8986f-115">Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8986f-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="8986f-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="8986f-116">Before beginning</span></span>

<span data-ttu-id="8986f-117">Merhaba aşağıdaki adımları hello ayarları gerekli tooconfigure, dinamik ya da rota tabanlı ağ geçidi her sanal ağ için yol ve hello ağ geçitleri arasında bir VPN bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8986f-117">hello following steps walk you through hello settings necessary tooconfigure a dynamic or route-based gateway for each VNet and create a VPN connection between hello gateways.</span></span> <span data-ttu-id="8986f-118">Bu yapılandırma, statik veya ilke tabanlı ağ geçitleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="8986f-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8986f-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8986f-119">Prerequisites</span></span>

* <span data-ttu-id="8986f-120">Her iki Vnet'in zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="8986f-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="8986f-121">hello ağ geçitleri bağlı olabilir diğer bağlantılar için hello aralıklardan herhangi biriyle başlangıç adresi aralığı sanal ağlar değil birbirleri ile üst üste veya üst üste hello için.</span><span class="sxs-lookup"><span data-stu-id="8986f-121">hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="8986f-122">Merhaba son PowerShell cmdlet'leri yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="8986f-122">You have installed hello latest PowerShell cmdlets.</span></span> <span data-ttu-id="8986f-123">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="8986f-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="8986f-124">Merhaba Hizmet Yönetimi (SM) ve Kaynak Yöneticisi (RM) cmdlet'leri hello yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="8986f-124">Make sure you install both hello Service Management (SM) and hello Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="8986f-125"><a name="exampleref"></a>Örnek ayarlar</span><span class="sxs-lookup"><span data-stu-id="8986f-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="8986f-126">Bu değerleri toocreate bir test ortamı kullanın veya toothem başvurun toobetter anlamak bu makaledeki hello örnekler.</span><span class="sxs-lookup"><span data-stu-id="8986f-126">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="8986f-127">**Klasik VNet ayarları**</span><span class="sxs-lookup"><span data-stu-id="8986f-127">**Classic VNet settings**</span></span>

<span data-ttu-id="8986f-128">Sanal ağ adı ClassicVNet =</span><span class="sxs-lookup"><span data-stu-id="8986f-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="8986f-129">Konum Batı ABD =</span><span class="sxs-lookup"><span data-stu-id="8986f-129">Location = West US</span></span> <br>
<span data-ttu-id="8986f-130">Sanal ağ adres alanları 10.0.0.0/24 =</span><span class="sxs-lookup"><span data-stu-id="8986f-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="8986f-131">Alt ağ 1 10.0.0.0/27 =</span><span class="sxs-lookup"><span data-stu-id="8986f-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="8986f-132">GatewaySubnet 10.0.0.32/29 =</span><span class="sxs-lookup"><span data-stu-id="8986f-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="8986f-133">Yerel ağ adı RMVNetLocal =</span><span class="sxs-lookup"><span data-stu-id="8986f-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="8986f-134">GatewayType DynamicRouting =</span><span class="sxs-lookup"><span data-stu-id="8986f-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="8986f-135">**Resource Manager Vnet'i ayarları**</span><span class="sxs-lookup"><span data-stu-id="8986f-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="8986f-136">Sanal ağ adı RMVNet =</span><span class="sxs-lookup"><span data-stu-id="8986f-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="8986f-137">Kaynak grubu RG1 =</span><span class="sxs-lookup"><span data-stu-id="8986f-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="8986f-138">Sanal ağ IP adresi alanları 192.168.0.0/16 =</span><span class="sxs-lookup"><span data-stu-id="8986f-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="8986f-139">Alt ağ 1 192.168.1.0/24 =</span><span class="sxs-lookup"><span data-stu-id="8986f-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="8986f-140">GatewaySubnet 192.168.0.0/26 =</span><span class="sxs-lookup"><span data-stu-id="8986f-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="8986f-141">Konum Doğu ABD =</span><span class="sxs-lookup"><span data-stu-id="8986f-141">Location = East US</span></span> <br>
<span data-ttu-id="8986f-142">Ağ geçidi genel IP adı gwpip =</span><span class="sxs-lookup"><span data-stu-id="8986f-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="8986f-143">Yerel ağ geçidi ClassicVNetLocal =</span><span class="sxs-lookup"><span data-stu-id="8986f-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="8986f-144">Sanal ağ geçidi adı RMGateway =</span><span class="sxs-lookup"><span data-stu-id="8986f-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="8986f-145">Ağ geçidi IP adresleme yapılandırmasını gwipconfig =</span><span class="sxs-lookup"><span data-stu-id="8986f-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="8986f-146"><a name="createsmgw"></a>1. bölüm - yapılandırma Klasik VNet hello</span><span class="sxs-lookup"><span data-stu-id="8986f-146"><a name="createsmgw"></a>Section 1 - Configure hello classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="8986f-147">Bölüm 1 - ağ yapılandırma dosyası indirme</span><span class="sxs-lookup"><span data-stu-id="8986f-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="8986f-148">İçinde tooyour yükseltilmiş haklara sahip Azure hesabı hello PowerShell konsolunda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8986f-148">Log in tooyour Azure account in hello PowerShell console with elevated rights.</span></span> <span data-ttu-id="8986f-149">Merhaba aşağıdaki cmdlet'i, hello oturum açma kimlik bilgilerini Azure hesabınız için ister.</span><span class="sxs-lookup"><span data-stu-id="8986f-149">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="8986f-150">Kullanılabilir tooAzure PowerShell; böylece oturum açtıktan sonra hesap ayarlarınızı indirir.</span><span class="sxs-lookup"><span data-stu-id="8986f-150">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span> <span data-ttu-id="8986f-151">Merhaba SM PowerShell cmdlet'leri toocomplete hello yapılandırmasının bu bölümü kullanın.</span><span class="sxs-lookup"><span data-stu-id="8986f-151">You use hello SM PowerShell cmdlets toocomplete this part of hello configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="8986f-152">Azure ağı yapılandırma dosyanızı hello aşağıdaki komutu çalıştırarak dışa aktarın.</span><span class="sxs-lookup"><span data-stu-id="8986f-152">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="8986f-153">Merhaba dosya tooexport tooa farklı konumu gerekirse hello konumunu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8986f-153">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="8986f-154">Açık hello .xml dosyası tooedit indirilen bu.</span><span class="sxs-lookup"><span data-stu-id="8986f-154">Open hello .xml file that you downloaded tooedit it.</span></span> <span data-ttu-id="8986f-155">Merhaba hello ağ yapılandırma dosyası örneği için bkz: [ağ yapılandırma şeması](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="8986f-155">For an example of hello network configuration file, see hello [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-hello-gateway-subnet"></a><span data-ttu-id="8986f-156">Bölüm 2 - hello ağ geçidi alt ağını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8986f-156">Part 2 -Verify hello gateway subnet</span></span>
<span data-ttu-id="8986f-157">Merhaba, **VirtualNetworkSites** öğesi değil zaten oluşturulmuş bir ağ geçidi alt ağı tooyour VNet ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8986f-157">In hello **VirtualNetworkSites** element, add a gateway subnet tooyour VNet if one has not already been created.</span></span> <span data-ttu-id="8986f-158">Merhaba ağ yapılandırma dosyası ile çalışırken, "GatewaySubnet" Merhaba ağ geçidi alt ağı adlı gerekir veya Azure algılar ve bir ağ geçidi alt ağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8986f-158">When working with hello network configuration file, hello gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="8986f-159">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="8986f-159">**Example:**</span></span>

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

### <a name="part-3---add-hello-local-network-site"></a><span data-ttu-id="8986f-160">Bölüm 3 - hello yerel ağ sitesi ekleme</span><span class="sxs-lookup"><span data-stu-id="8986f-160">Part 3 - Add hello local network site</span></span>
<span data-ttu-id="8986f-161">eklediğiniz hello yerel ağ sitesine hello tooconnect istediğiniz RM VNet toowhich temsil eder.</span><span class="sxs-lookup"><span data-stu-id="8986f-161">hello local network site you add represents hello RM VNet toowhich you want tooconnect.</span></span> <span data-ttu-id="8986f-162">Ekleme bir **LocalNetworkSites** zaten yoksa öğe toohello dosyası.</span><span class="sxs-lookup"><span data-stu-id="8986f-162">Add a **LocalNetworkSites** element toohello file if one doesn't already exist.</span></span> <span data-ttu-id="8986f-163">Bu noktada hello ağ geçidi hello Resource Manager Vnet'i için oluşturduğumuz henüz yapmadıysanız için hello yapılandırmasında hello VPNGatewayAddress herhangi bir geçerli ortak IP adresi olabilir.</span><span class="sxs-lookup"><span data-stu-id="8986f-163">At this point in hello configuration, hello VPNGatewayAddress can be any valid public IP address because we haven't yet created hello gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="8986f-164">Biz hello ağ geçidi oluşturduktan sonra Biz bu yer tutucu IP adresi toohello RM ağ geçidi atanmış hello doğru ortak IP adresiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8986f-164">Once we create hello gateway, we replace this placeholder IP address with hello correct public IP address that has been assigned toohello RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a><span data-ttu-id="8986f-165">Bölüm 4 - hello yerel ağ sitesi ile ilişkilendirme hello VNet</span><span class="sxs-lookup"><span data-stu-id="8986f-165">Part 4 - Associate hello VNet with hello local network site</span></span>
<span data-ttu-id="8986f-166">Bu bölümde, tooconnect istediğiniz hello yerel ağ sitesine belirttiğimiz Vnet'e hello.</span><span class="sxs-lookup"><span data-stu-id="8986f-166">In this section, we specify hello local network site that you want tooconnect hello VNet to.</span></span> <span data-ttu-id="8986f-167">Bu durumda, hello daha önce başvurulan Resource Manager Vnet'i olur.</span><span class="sxs-lookup"><span data-stu-id="8986f-167">In this case, it is hello Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="8986f-168">Eşleşen emin hello adlar kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="8986f-168">Make sure hello names match.</span></span> <span data-ttu-id="8986f-169">Bu adım, bir ağ geçidi oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="8986f-169">This step does not create a gateway.</span></span> <span data-ttu-id="8986f-170">Ağ geçidi hello hello yerel ağ bağlanacağı belirtir.</span><span class="sxs-lookup"><span data-stu-id="8986f-170">It specifies hello local network that hello gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a><span data-ttu-id="8986f-171">5 Kısım - hello dosyasını kaydedin ve karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="8986f-171">Part 5 - Save hello file and upload</span></span>
<span data-ttu-id="8986f-172">Merhaba dosyasını kaydedin ve ardından hello aşağıdaki komutu çalıştırarak tooAzure alma.</span><span class="sxs-lookup"><span data-stu-id="8986f-172">Save hello file, then import it tooAzure by running hello following command.</span></span> <span data-ttu-id="8986f-173">Ortamınız için gerektiği gibi hello dosya yolu değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="8986f-173">Make sure you change hello file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="8986f-174">Merhaba içeri aktarma başarılı olduğunu gösteren benzer bir sonuç görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8986f-174">You will see a similar result showing that hello import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a><span data-ttu-id="8986f-175">Bölüm 6 - hello ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8986f-175">Part 6 - Create hello gateway</span></span>

<span data-ttu-id="8986f-176">Bu örneği çalıştırmadan önce toohello başvurmak bu Azure hello tam adları için yüklediğiniz ağ yapılandırma dosyası toosee bekliyor.</span><span class="sxs-lookup"><span data-stu-id="8986f-176">Before running this example, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="8986f-177">Hello ağ yapılandırma dosyası, Klasik sanal ağlar için hello değerler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8986f-177">hello network configuration file contains hello values for your classic virtual networks.</span></span> <span data-ttu-id="8986f-178">Bazen hello adları Klasik sanal ağlar hello ağ yapılandırma dosyasında Klasik VNet ayarlarında oluştururken değişmesi için Azure portal hello dağıtım modellerini toohello farklılıkları nedeniyle hello.</span><span class="sxs-lookup"><span data-stu-id="8986f-178">Sometimes hello names for classic VNets are changed in hello network configuration file when creating classic VNet settings in hello Azure portal due toohello differences in hello deployment models.</span></span> <span data-ttu-id="8986f-179">Örneğin, hello Klasik VNet 'Klasik VNet' adlı ve 'ClassicRG' adlı bir kaynak grubunda oluşturduğunuz Azure portal toocreate kullandıysanız, dönüştürülmüş too'Group ClassicRG Klasik VNet hello ağ yapılandırma dosyasında yer alan hello adı. '.</span><span class="sxs-lookup"><span data-stu-id="8986f-179">For example, if you used hello Azure portal toocreate a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', hello name that is contained in hello network configuration file is converted too'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="8986f-180">Boşluk içeren bir VNet Hello adı belirtirken, hello değeri tırnak işaretleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="8986f-180">When specifying hello name of a VNet that contains spaces, use quotation marks around hello value.</span></span>


<span data-ttu-id="8986f-181">Aşağıdaki örnek toocreate dinamik yönlendirme ağ geçidi hello kullan:</span><span class="sxs-lookup"><span data-stu-id="8986f-181">Use hello following example toocreate a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="8986f-182">Hello kullanarak hello hello ağ geçidi durumunu kontrol edebilirsiniz **Get-AzureVNetGateway** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8986f-182">You can check hello status of hello gateway by using hello **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="8986f-183"><a name="creatermgw"></a>2. Bölüm: Merhaba RM VNet ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8986f-183"><a name="creatermgw"></a>Section 2: Configure hello RM VNet gateway</span></span>
<span data-ttu-id="8986f-184">toocreate hello RM VNet için VPN ağ geçidi hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="8986f-184">toocreate a VPN gateway for hello RM VNet, follow hello following instructions.</span></span> <span data-ttu-id="8986f-185">Merhaba Klasik sanal ağınızın ağ geçidi için genel IP adresi hello aldıktan sonra hello adımları kadar başlatmayın.</span><span class="sxs-lookup"><span data-stu-id="8986f-185">Don't start hello steps until after you have retrieved hello public IP address for hello classic VNet's gateway.</span></span> 

1. <span data-ttu-id="8986f-186">İçinde tooyour Azure hesabı hello PowerShell konsolunda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8986f-186">Log in tooyour Azure account in hello PowerShell console.</span></span> <span data-ttu-id="8986f-187">Merhaba aşağıdaki cmdlet'i, hello oturum açma kimlik bilgilerini Azure hesabınız için ister.</span><span class="sxs-lookup"><span data-stu-id="8986f-187">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="8986f-188">Kullanılabilir tooAzure PowerShell; böylece oturum açtıktan sonra hesap ayarlarınızı indirilir.</span><span class="sxs-lookup"><span data-stu-id="8986f-188">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="8986f-189">Birden fazla aboneliğiniz varsa, Azure aboneliklerinize listesini alın.</span><span class="sxs-lookup"><span data-stu-id="8986f-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="8986f-190">Merhaba abonelik toouse istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="8986f-190">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="8986f-191">Bir yerel ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8986f-191">Create a local network gateway.</span></span> <span data-ttu-id="8986f-192">Bir sanal ağ hello yerel ağ geçidi genellikle tooyour içi konumunuz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8986f-192">In a virtual network, hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="8986f-193">Bu durumda, hello yerel ağ geçidi tooyour Klasik VNet anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8986f-193">In this case, hello local network gateway refers tooyour Classic VNet.</span></span> <span data-ttu-id="8986f-194">Olarak Azure tooit başvurun ve ayrıca hello adres alanı ön ekini belirtin bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="8986f-194">Give it a name by which Azure can refer tooit, and also specify hello address space prefix.</span></span> <span data-ttu-id="8986f-195">Azure başlangıç IP adresi ön eki hangi trafik toosend tooyour içi konumu tooidentify belirttiğiniz kullanır.</span><span class="sxs-lookup"><span data-stu-id="8986f-195">Azure uses hello IP address prefix you specify tooidentify which traffic toosend tooyour on-premises location.</span></span> <span data-ttu-id="8986f-196">Tooadjust hello buradaki bilgiler daha sonra ağ geçidiniz, oluşturmadan önce gerekirse hello değerleri ve çalışma hello örnek yeniden değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8986f-196">If you need tooadjust hello information here later, before creating your gateway, you can modify hello values and run hello sample again.</span></span>
   
   <span data-ttu-id="8986f-197">**-Ad** tooassign toorefer toohello yerel ağ geçidi istediğiniz hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="8986f-197">**-Name** is hello name you want tooassign toorefer toohello local network gateway.</span></span><br><span data-ttu-id="8986f-198">
   **-AddressPrefix** hello Klasik VNet adres alanı değil.</span><span class="sxs-lookup"><span data-stu-id="8986f-198">
   **-AddressPrefix** is hello Address Space for your classic VNet.</span></span><br><span data-ttu-id="8986f-199">
**-Gatewayıpaddress** hello hello Klasik sanal ağınızın ağ geçidinin genel IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="8986f-199">
**-GatewayIpAddress** is hello public IP address of hello classic VNet's gateway.</span></span> <span data-ttu-id="8986f-200">Tooreflect hello doğru IP adresi toochange hello aşağıdaki örnek emin olun.</span><span class="sxs-lookup"><span data-stu-id="8986f-200">Be sure toochange hello following sample tooreflect hello correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="8986f-201">Bir ortak IP adresi toobe ayrılmış toohello sanal ağ geçidi hello Resource Manager Vnet'i için istek.</span><span class="sxs-lookup"><span data-stu-id="8986f-201">Request a public IP address toobe allocated toohello virtual network gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="8986f-202">Başlangıç IP adresi toouse istediğiniz belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="8986f-202">You can't specify hello IP address that you want toouse.</span></span> <span data-ttu-id="8986f-203">Başlangıç IP adresi toohello sanal ağ geçidi dinamik olarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="8986f-203">hello IP address is dynamically allocated toohello virtual network gateway.</span></span> <span data-ttu-id="8986f-204">Ancak, bu başlangıç IP adresi değişiklikleri gelmez.</span><span class="sxs-lookup"><span data-stu-id="8986f-204">However, this does not mean hello IP address changes.</span></span> <span data-ttu-id="8986f-205">ağ geçidi Hello sanal ağ geçidi IP adresi değişiklikleri hello zaman hello yalnızca zaman silindiğinde ve yeniden.</span><span class="sxs-lookup"><span data-stu-id="8986f-205">hello only time hello virtual network gateway IP address changes is when hello gateway is deleted and recreated.</span></span> <span data-ttu-id="8986f-206">Yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında hello ağ geçidi değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="8986f-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of hello gateway.</span></span>

  <span data-ttu-id="8986f-207">Bu adımda, biz de bir sonraki adımda kullanılan bir değişken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8986f-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="8986f-208">Sanal ağınızın ağ geçidi alt ağı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8986f-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="8986f-209">Hiçbir ağ geçidi alt ağı varsa ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8986f-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="8986f-210">Merhaba ağ geçidi alt ağı adlandırılan emin olun *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="8986f-210">Make sure hello gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="8986f-211">Merhaba aşağıdaki komutu çalıştırarak Hello ağ geçidi için kullanılan hello alt alın.</span><span class="sxs-lookup"><span data-stu-id="8986f-211">Retrieve hello subnet used for hello gateway by running hello following command.</span></span> <span data-ttu-id="8986f-212">Bu adımda, biz de hello sonraki adımda kullanılan bir değişken toobe ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8986f-212">In this step, we also set a variable toobe used in hello next step.</span></span>
   
   <span data-ttu-id="8986f-213">**-Name** Resource Manager Vnet'i hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="8986f-213">**-Name** is hello name of your Resource Manager VNet.</span></span><br><span data-ttu-id="8986f-214">
   **-ResourceGroupName** hello kaynak grubudur VNet ile ilişkili o hello.</span><span class="sxs-lookup"><span data-stu-id="8986f-214">
**-ResourceGroupName** is hello resource group that hello VNet is associated with.</span></span> <span data-ttu-id="8986f-215">Merhaba ağ geçidi alt ağı için bu sanal ağ zaten mevcut olmalıdır ve adlandırılmalıdır *GatewaySubnet* toowork düzgün.</span><span class="sxs-lookup"><span data-stu-id="8986f-215">hello gateway subnet must already exist for this VNet and must be named *GatewaySubnet* toowork properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="8986f-216">Merhaba ağ geçidi IP adresleme yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8986f-216">Create hello gateway IP addressing configuration.</span></span> <span data-ttu-id="8986f-217">Merhaba ağ geçidi yapılandırmasını hello alt ağı ve hello ortak IP adresi toouse tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8986f-217">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="8986f-218">Aşağıdaki örnek toocreate hello ağ geçidi yapılandırmanızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8986f-218">Use hello following sample toocreate your gateway configuration.</span></span>

  <span data-ttu-id="8986f-219">Bu adımda, hello **- SubnetId** ve **- PublicIpAddressId** parametreleri gerekir bayraklarıdır hello ID özelliği hello alt ağ ve IP adresi nesneleri, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="8986f-219">In this step, hello **-SubnetId** and **-PublicIpAddressId** parameters must be passed hello id property from hello subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="8986f-220">Basit bir dize kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="8986f-220">You can't use a simple string.</span></span> <span data-ttu-id="8986f-221">Bu değişkenler hello adım toorequest bir ortak IP ayarlanır ve adım tooretrieve hello alt hello.</span><span class="sxs-lookup"><span data-stu-id="8986f-221">These variables are set in hello step toorequest a public IP and hello step tooretrieve hello subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="8986f-222">Merhaba aşağıdaki komutu çalıştırarak Hello Resource Manager sanal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8986f-222">Create hello Resource Manager virtual network gateway by running hello following command.</span></span> <span data-ttu-id="8986f-223">Merhaba `-VpnType` olmalıdır *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="8986f-223">hello `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="8986f-224">45 dakika veya daha fazla hello ağ geçidi toocreate alabilir.</span><span class="sxs-lookup"><span data-stu-id="8986f-224">It can take 45 minutes or more for hello gateway toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="8986f-225">Merhaba VPN ağ geçidi oluşturulduktan sonra hello genel IP adresi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8986f-225">Copy hello public IP address once hello VPN gateway has been created.</span></span> <span data-ttu-id="8986f-226">Klasik sanal ağınızı hello yerel ağ ayarlarını yapılandırırken kullanın.</span><span class="sxs-lookup"><span data-stu-id="8986f-226">You use it when you configure hello local network settings for your Classic VNet.</span></span> <span data-ttu-id="8986f-227">Cmdlet tooretrieve hello genel IP adresi aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8986f-227">You can use hello following cmdlet tooretrieve hello public IP address.</span></span> <span data-ttu-id="8986f-228">Merhaba genel IP adresi hello dönüş olarak listelenen *IPADDRESS*.</span><span class="sxs-lookup"><span data-stu-id="8986f-228">hello public IP address is listed in hello return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a><span data-ttu-id="8986f-229">3. Bölüm: Merhaba Klasik VNet yerel site ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="8986f-229">Section 3: Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="8986f-230">Bu bölümde, hello ile iş Klasik VNet.</span><span class="sxs-lookup"><span data-stu-id="8986f-230">In this section, you work with hello classic VNet.</span></span> <span data-ttu-id="8986f-231">Kullanılan tooconnect toohello Resource Manager Vnet'i ağ geçidi olacaktır hello yerel site ayarlarını belirtmek için kullanılan hello yer tutucu IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8986f-231">You replace hello placeholder IP address that you used when specifying hello local site settings that will be used tooconnect toohello Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="8986f-232">Merhaba ağ yapılandırma dosyasını dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="8986f-232">Export hello network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="8986f-233">Bir metin düzenleyicisi kullanarak VPNGatewayAddress için başlangıç değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8986f-233">Using a text editor, modify hello value for VPNGatewayAddress.</span></span> <span data-ttu-id="8986f-234">Hello ortak IP adresini hello Resource Manager ağ geçidi ile Merhaba yer tutucu IP adresini değiştirin ve ardından hello değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8986f-234">Replace hello placeholder IP address with hello public IP address of hello Resource Manager gateway and then save hello changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="8986f-235">İçeri aktarma hello ağ yapılandırma dosyası tooAzure değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="8986f-235">Import hello modified network configuration file tooAzure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="8986f-236"><a name="connect"></a>4. Bölüm: Merhaba ağ geçitleri arasında bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8986f-236"><a name="connect"></a>Section 4: Create a connection between hello gateways</span></span>
<span data-ttu-id="8986f-237">Merhaba ağ geçitleri arasında bir bağlantı oluşturmak için PowerShell gerekir.</span><span class="sxs-lookup"><span data-stu-id="8986f-237">Creating a connection between hello gateways requires PowerShell.</span></span> <span data-ttu-id="8986f-238">Azure hesabı toouse hello Klasik sürümünüz hello PowerShell cmdlet'leri tooadd gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8986f-238">You may need tooadd your Azure Account toouse hello classic version of hello  PowerShell cmdlets.</span></span> <span data-ttu-id="8986f-239">Bu nedenle, toodo kullanmak **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="8986f-239">toodo so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="8986f-240">Merhaba PowerShell konsolunda paylaşılan anahtarınız ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8986f-240">In hello PowerShell console, set your shared key.</span></span> <span data-ttu-id="8986f-241">Toohello başvurmak Hello cmdlet'leri çalıştırmadan önce bu Azure hello tam adları için yüklediğiniz ağ yapılandırma dosyası toosee bekliyor.</span><span class="sxs-lookup"><span data-stu-id="8986f-241">Before running hello cmdlets, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="8986f-242">Boşluk içeren bir VNet Hello adı belirtirken, hello değeri tek tırnak işareti kullanın.</span><span class="sxs-lookup"><span data-stu-id="8986f-242">When specifying hello name of a VNet that contains spaces, use single quotation marks around hello value.</span></span><br><br><span data-ttu-id="8986f-243">Aşağıdaki örnekte, **- vnetname adlı** hello hello adıdır Klasik VNet ve **- LocalNetworkSiteName** hello yerel ağ sitesi için belirtilen hello adı.</span><span class="sxs-lookup"><span data-stu-id="8986f-243">In following example, **-VNetName** is hello name of hello classic VNet and **-LocalNetworkSiteName** is hello name you specified for hello local network site.</span></span> <span data-ttu-id="8986f-244">Merhaba **- SharedKey** oluşturmak ve belirten bir değer.</span><span class="sxs-lookup"><span data-stu-id="8986f-244">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="8986f-245">Merhaba örnekte 'abc123' kullandık ancak oluşturabilir ve daha karmaşık bir şey kullanın.</span><span class="sxs-lookup"><span data-stu-id="8986f-245">In hello example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="8986f-246">Burada belirttiğiniz başlangıç değeri şeydir önemli Hello hello aynı bağlantınızı oluştururken hello sonraki adımda belirttiğiniz değeri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8986f-246">hello important thing is that hello value you specify here must be hello same value that you specify in hello next step when you create your connection.</span></span> <span data-ttu-id="8986f-247">Hello dönüş Göster **durumu: başarılı**.</span><span class="sxs-lookup"><span data-stu-id="8986f-247">hello return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="8986f-248">Merhaba aşağıdaki komutları çalıştırarak Hello VPN bağlantısı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="8986f-248">Create hello VPN connection by running hello following commands:</span></span>
   
  <span data-ttu-id="8986f-249">Merhaba değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8986f-249">Set hello variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="8986f-250">Merhaba bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8986f-250">Create hello connection.</span></span> <span data-ttu-id="8986f-251">Bu hello fark **- ConnectionType** IPSec, Vnet2Vnet değil.</span><span class="sxs-lookup"><span data-stu-id="8986f-251">Notice that hello **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="8986f-252">Bölüm 5: bağlantılarınızı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8986f-252">Section 5: Verify your connections</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="8986f-253">Klasik VNet tooyour Resource Manager Vnet'i tooverify hello bağlantısından</span><span class="sxs-lookup"><span data-stu-id="8986f-253">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="8986f-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8986f-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="8986f-255">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="8986f-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="8986f-256">Resource Manager Vnet'i tooyour tooverify hello bağlantısından Klasik VNet</span><span class="sxs-lookup"><span data-stu-id="8986f-256">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="8986f-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8986f-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="8986f-258">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="8986f-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="8986f-259"><a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="8986f-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

