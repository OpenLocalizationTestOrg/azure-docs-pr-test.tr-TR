---
title: "VPN ağ geçidi ve PowerShell kullanarak bir sanal ağ toomultiple siteleri bağlamak: Klasik | Microsoft Docs"
description: "Bu makalede hello Klasik dağıtım modeli için bir VPN ağ geçidi kullanarak birden çok yerel şirket içi siteler tooa sanal ağ konusunda size yol gösterir."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="ee69a-103">Mevcut bir VPN ağ geçidi bağlantısı olan (Klasik) bir siteden siteye bağlantı tooa VNet ekleme</span><span class="sxs-lookup"><span data-stu-id="ee69a-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee69a-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="ee69a-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="ee69a-105">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="ee69a-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="ee69a-106">Bu makalede, varolan bir bağlantıyı sahip PowerShell tooadd siteden siteye (S2S) bağlantıları tooa VPN ağ geçidi kullanılarak üzerinden açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ee69a-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="ee69a-107">Bu tür bir bağlantı başvurulan tooas "çok siteli" yapılandırma görülür.</span><span class="sxs-lookup"><span data-stu-id="ee69a-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="ee69a-108">Merhaba bu makaledeki adımları hello Klasik dağıtım modeli (Hizmet Yönetimi olarak da bilinir) kullanılarak oluşturulmuş toovirtual ağlara uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ee69a-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="ee69a-109">Bu adımları tooExpressRoute /-siteye eşzamanlı bağlantı yapılandırmaları geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="ee69a-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="ee69a-110">Dağıtım modelleri ve yöntemleri</span><span class="sxs-lookup"><span data-stu-id="ee69a-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="ee69a-111">Bu tabloda yeni makaleler olarak güncelleştiriyoruz ve ek araçlar bu yapılandırma için kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="ee69a-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="ee69a-112">Bir makale kullanılabilir olduğunda sizi doğrudan bu tablodan tooit bağlayın.</span><span class="sxs-lookup"><span data-stu-id="ee69a-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="ee69a-113">Bağlama hakkında</span><span class="sxs-lookup"><span data-stu-id="ee69a-113">About connecting</span></span>

<span data-ttu-id="ee69a-114">Birden çok şirket içi siteler tooa tek bir sanal ağ bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ee69a-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="ee69a-115">Karma bulut çözümleri oluşturmak için özellikle çekici budur.</span><span class="sxs-lookup"><span data-stu-id="ee69a-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="ee69a-116">Çok siteli bağlantı tooyour Azure sanal ağ geçidi oluşturma benzer toocreating diğer siteden siteye bağlantı sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="ee69a-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="ee69a-117">Aslında, Hello ağ geçidi dinamik olduğu sürece, mevcut bir Azure VPN ağ geçidi kullanabilirsiniz (rota tabanlı).</span><span class="sxs-lookup"><span data-stu-id="ee69a-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="ee69a-118">Bir statik ağ geçidi bağlı tooyour sanal ağınız zaten varsa, sipariş tooaccommodate birden çok sitede toorebuild hello sanal ağ gerek kalmadan hello ağ geçidi türü toodynamic değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee69a-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="ee69a-119">Merhaba yönlendirme türü değiştirmeden önce şirket içi VPN ağ geçidinizi rota tabanlı VPN yapılandırmaları desteklediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ee69a-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="ee69a-120">![çok siteli diyagramı](./media/vpn-gateway-multi-site/multisite.png "çok siteli")</span><span class="sxs-lookup"><span data-stu-id="ee69a-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="ee69a-121">Noktaları tooconsider</span><span class="sxs-lookup"><span data-stu-id="ee69a-121">Points tooconsider</span></span>

<span data-ttu-id="ee69a-122">**Mümkün toouse hello portal toomake değişiklikleri toothis sanal ağ olmayacaktır.**</span><span class="sxs-lookup"><span data-stu-id="ee69a-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="ee69a-123">Merhaba portal kullanmak yerine toomake değişiklikleri toohello ağ yapılandırma dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee69a-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="ee69a-124">Merhaba Portalı'nda değişiklik yaparsanız, bu sanal ağ için çok siteli başvuru ayarlarınızı üzerine.</span><span class="sxs-lookup"><span data-stu-id="ee69a-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="ee69a-125">Rahat geliyor olmalıdır hello zamanına göre hello ağ yapılandırma dosyası kullanarak hello çok siteli yordamı tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="ee69a-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="ee69a-126">Ancak, ağ yapılandırmanızı üzerinde çalışan birden çok kişi varsa toomake herkes bu sınırlama hakkında bilir emin ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="ee69a-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="ee69a-127">Bu, hello portal hiç kullanamazsınız anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="ee69a-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="ee69a-128">Başka yapılandırma değişiklikleri toothis belirli sanal ağ oluşturma dışında her şey için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee69a-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ee69a-129">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ee69a-129">Before you begin</span></span>

<span data-ttu-id="ee69a-130">Yapılandırmaya başlamadan önce hello aşağıdaki sahip olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="ee69a-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="ee69a-131">Uyumlu VPN donanım her konum şirket içi.</span><span class="sxs-lookup"><span data-stu-id="ee69a-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="ee69a-132">Denetleme [sanal ağ bağlantısı için VPN aygıtları hakkında](vpn-gateway-about-vpn-devices.md) toobe uyumlu bilinen hello aygıt toouse istediğiniz bir şey ise tooverify.</span><span class="sxs-lookup"><span data-stu-id="ee69a-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="ee69a-133">Bir dışarıya dönük IPv4 için genel IP adresi her VPN cihazı.</span><span class="sxs-lookup"><span data-stu-id="ee69a-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="ee69a-134">Başlangıç IP adresi bir NAT'nin arkasında olamaz</span><span class="sxs-lookup"><span data-stu-id="ee69a-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="ee69a-135">Bu gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="ee69a-135">This is requirement.</span></span>
* <span data-ttu-id="ee69a-136">Tooinstall hello en son sürümünü hello Azure PowerShell cmdlet'lerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee69a-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ee69a-137">Toplama toohello Resource Manager sürümünde hello Hizmet Yönetimi (SM) sürümü yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ee69a-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="ee69a-138">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ee69a-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="ee69a-139">Birisinden VPN donanımınızın yapılandırma sırasında yeterli.</span><span class="sxs-lookup"><span data-stu-id="ee69a-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="ee69a-140">Toohave nasıl güçlü bir anlayış gerekir tooconfigure VPN cihazı veya mu birisi birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="ee69a-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="ee69a-141">hello IP adresi aralığı (sizin zaten bir oluşturmadıysanız), sanal ağınızda toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="ee69a-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="ee69a-142">Başlangıç IP adresi aralıkları için bağlanma hello yerel ağ sitelerinin her biri için.</span><span class="sxs-lookup"><span data-stu-id="ee69a-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="ee69a-143">Toomake başlangıç IP adresi her tooconnect toodo olmayan çakışma istediğiniz hello yerel ağ sitesi için aralıkları emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee69a-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="ee69a-144">Aksi takdirde hello portalı veya REST API hello karşıya yüklenen hello yapılandırma reddeder.</span><span class="sxs-lookup"><span data-stu-id="ee69a-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="ee69a-145">Her ikisi de başlangıç IP adresi aralığı 10.2.3.0/24 içerir ve hedef adres 10.2.3.3 ile bir pakete sahip iki yerel ağ sitesi varsa, Azure toosend hello paket toobecause hello adres aralıkları istediğiniz hangi site Örneğin, bilmeniz olmayacaktır Çakışan.</span><span class="sxs-lookup"><span data-stu-id="ee69a-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="ee69a-146">tooprevent yönlendirme sorunları, Azure tooupload örtüşen aralıklarına sahip bir yapılandırma dosyası izin vermez.</span><span class="sxs-lookup"><span data-stu-id="ee69a-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="ee69a-147">1. Siteden Siteye VPN oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee69a-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="ee69a-148">Zaten bir dinamik yönlendirme ağ geçidi ile siteden siteye VPN harika varsa!</span><span class="sxs-lookup"><span data-stu-id="ee69a-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="ee69a-149">Çok geçebilmeniz[hello sanal ağ yapılandırma ayarlarını dışarı aktar](#export).</span><span class="sxs-lookup"><span data-stu-id="ee69a-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="ee69a-150">Aksi durumda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="ee69a-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="ee69a-151">Siteden siteye sanal ağ zaten var, ancak statik (ilke tabanlı) yönlendirme ağ geçidi varsa:</span><span class="sxs-lookup"><span data-stu-id="ee69a-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="ee69a-152">Ağ geçidi türü toodynamic yönlendirme değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ee69a-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="ee69a-153">Çok siteli VPN dinamik (olarak da bilinen rota tabanlı) yönlendirme ağ geçidi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ee69a-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="ee69a-154">Ağ geçidiniz toochange yazın, toofirst delete hello mevcut ağ geçidine gereksinimi sonra yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee69a-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="ee69a-155">Yönergeler için bkz: [nasıl toochange hello ağ geçidiniz için VPN yönlendirme türü](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="ee69a-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="ee69a-156">Yeni ağ geçidiniz yapılandırın ve VPN tüneli oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ee69a-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="ee69a-157">Yönergeler için bkz: [hello Klasik Azure portalı bir VPN ağ geçidi yapılandırma](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="ee69a-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="ee69a-158">İlk olarak, ağ geçidi türü toodynamic yönlendirme değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ee69a-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="ee69a-159">Siteden siteye sanal ağınız yoksa:</span><span class="sxs-lookup"><span data-stu-id="ee69a-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="ee69a-160">Bu yönergeleri kullanarak, siteden siteye sanal ağ oluşturma: [bir siteden siteye VPN bağlantısının hello Klasik Azure portalı ile bir sanal ağ oluşturma](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="ee69a-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="ee69a-161">Bu yönergeleri kullanarak dinamik yönlendirme ağ geçidi yapılandırma: [bir VPN ağ geçidi yapılandırma](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="ee69a-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="ee69a-162">Emin tooselect olması **dinamik yönlendirme** , ağ geçidi türü.</span><span class="sxs-lookup"><span data-stu-id="ee69a-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="ee69a-163"><a name="export"></a>2. Dışa aktarma hello ağ yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="ee69a-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="ee69a-164">Azure ağı yapılandırma dosyanızı hello aşağıdaki komutu çalıştırarak dışa aktarın.</span><span class="sxs-lookup"><span data-stu-id="ee69a-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="ee69a-165">Merhaba dosya tooexport tooa farklı konumu gerekirse hello konumunu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee69a-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="ee69a-166">3. Açık hello ağ yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="ee69a-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="ee69a-167">Merhaba son adımda indirdiğiniz hello ağ yapılandırma dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="ee69a-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="ee69a-168">İstediğiniz herhangi bir xml düzenleyicisi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ee69a-168">Use any xml editor that you like.</span></span> <span data-ttu-id="ee69a-169">Merhaba dosya benzer toohello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="ee69a-169">hello file should look similar toohello following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="ee69a-170">4. Birden çok sitesi başvuruları ekleme</span><span class="sxs-lookup"><span data-stu-id="ee69a-170">4. Add multiple site references</span></span>
<span data-ttu-id="ee69a-171">Site başvuru bilgileri ekleyip, yapılandırma değişikliklerini hale getireceğiz toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="ee69a-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="ee69a-172">Yeni bir yerel site başvurusu ekleme Azure toocreate yeni tünel tetikler.</span><span class="sxs-lookup"><span data-stu-id="ee69a-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="ee69a-173">Merhaba aşağıdaki örnekte, tek siteli bağlantı için hello ağ yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="ee69a-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="ee69a-174">Yaptığınız değişiklikleri yaptıktan sonra hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ee69a-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="ee69a-175">(çok siteli yapılandırma Oluştur) tooadd ek sitesi başvuruları eklemeniz yeterlidir ek "LocalNetworkSiteRef" satırları hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="ee69a-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="ee69a-176">5. İçeri aktarma hello ağ yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="ee69a-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="ee69a-177">Merhaba ağ yapılandırma dosyasını içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="ee69a-177">Import hello network configuration file.</span></span> <span data-ttu-id="ee69a-178">Merhaba değişikliklerle bu dosyayı içeri aktardığınızda hello yeni tüneller eklenir.</span><span class="sxs-lookup"><span data-stu-id="ee69a-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="ee69a-179">Merhaba tünelleri, daha önce oluşturduğunuz hello dinamik ağ geçidi kullanır.</span><span class="sxs-lookup"><span data-stu-id="ee69a-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="ee69a-180">Merhaba Klasik portal veya PowerShell tooimport hello dosyası ya da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee69a-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="ee69a-181">6. Anahtarları indirin</span><span class="sxs-lookup"><span data-stu-id="ee69a-181">6. Download keys</span></span>
<span data-ttu-id="ee69a-182">Yeni tüneller eklendikten sonra hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPSec/IKE önceden paylaşılan anahtarlar için her tünel kullanın.</span><span class="sxs-lookup"><span data-stu-id="ee69a-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="ee69a-183">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ee69a-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="ee69a-184">İsterseniz, hello de kullanabilirsiniz *alma sanal ağ geçidi paylaşılan anahtarı* REST API tooget hello önceden paylaşılan anahtarlar.</span><span class="sxs-lookup"><span data-stu-id="ee69a-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="ee69a-185">7. Bağlantılarınızı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="ee69a-185">7. Verify your connections</span></span>
<span data-ttu-id="ee69a-186">Merhaba çok siteli tünel durumunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="ee69a-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="ee69a-187">Her tünel Hello tuşları indirdikten sonra tooverify bağlantıları isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ee69a-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="ee69a-188">Sanal ağ listesi tünelleri, 'Get-AzureVnetConnection' tooget hello aşağıdaki örnekte gösterildiği gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ee69a-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="ee69a-189">VNet1 hello VNet hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="ee69a-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="ee69a-190">Örnek dönüş:</span><span class="sxs-lookup"><span data-stu-id="ee69a-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="ee69a-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee69a-191">Next steps</span></span>

<span data-ttu-id="ee69a-192">toolearn, VPN ağ geçitleri hakkında daha fazla bilgi görmek [VPN ağ geçitleri hakkında](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="ee69a-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
