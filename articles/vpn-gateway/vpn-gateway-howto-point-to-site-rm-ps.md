---
title: "Bilgisayar tooan noktası Site kullanarak Azure sanal ağı bağlanmak ve sertifika kimlik doğrulaması: PowerShell | Microsoft Docs"
description: "Sertifika kimlik doğrulaması kullanarak bir noktadan siteye VPN ağ geçidi bağlantısı oluşturarak güvenli bir şekilde bir bilgisayar tooyour sanal ağına bağlayın. Bu makalede toohello Resource Manager dağıtım modeli uygular ve PowerShell kullanır."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="bf852-104">Bir noktadan siteye bağlantı tooa VNet yapılandırma sertifika kimlik doğrulaması kullanarak: PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf852-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="bf852-105">Bu makalede toocreate hello Resource Manager dağıtım noktası Site bağlantısında sahip bir VNet nasıl model PowerShell kullanarak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bf852-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="bf852-106">Bu yapılandırma, sertifikaları tooauthenticate hello istemci bağlanma kullanır.</span><span class="sxs-lookup"><span data-stu-id="bf852-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="bf852-107">Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bf852-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf852-108">Azure portal</span><span class="sxs-lookup"><span data-stu-id="bf852-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="bf852-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf852-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="bf852-110">Azure portal (klasik)</span><span class="sxs-lookup"><span data-stu-id="bf852-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="bf852-111">Bir noktadan siteye (P2S) VPN ağ geçidi tek bir istemci bilgisayardan güvenli bağlantı tooyour sanal ağ oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf852-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="bf852-112">Noktadan siteye VPN bağlantıları tooconnect tooyour VNet uzak bir konumdan, örneğin, evden veya bir Konferanstan telecommuting zaman istediğinizde faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="bf852-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="bf852-113">Tooconnect tooa VNet gereken yalnızca birkaç istemciniz P2S VPN de yararlı çözüm toouse bir siteden siteye VPN yerine durumdur.</span><span class="sxs-lookup"><span data-stu-id="bf852-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span>

<span data-ttu-id="bf852-114">P2S kullanır, Güvenli Yuva Tünel Protokolü (bir SSL tabanlı VPN protokolü, SSTP), hello.</span><span class="sxs-lookup"><span data-stu-id="bf852-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="bf852-115">P2S VPN bağlantısı, hello istemci bilgisayardan başlatılmasıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bf852-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Bilgisayar tooan Azure VNet - noktadan siteye bağlantı diyagramı Bağlan](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="bf852-117">Noktadan siteye sertifika kimlik doğrulaması bağlantıları hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="bf852-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="bf852-118">RouteBased VPN ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="bf852-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="bf852-119">Merhaba karşıya yüklenen tooAzure bir kök sertifikası için ortak anahtarı (.cer dosyası).</span><span class="sxs-lookup"><span data-stu-id="bf852-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="bf852-120">Merhaba sertifika yüklendikten sonra güvenilen bir sertifika olarak kabul edilir ve kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bf852-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="bf852-121">Merhaba kök sertifikasından oluşturulur ve toohello VNet bağlanacak her istemci bilgisayarda yüklü bir istemci sertifikası.</span><span class="sxs-lookup"><span data-stu-id="bf852-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="bf852-122">Bu sertifika, istemci kimlik doğrulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bf852-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="bf852-123">VPN istemcisi yapılandırma paketi.</span><span class="sxs-lookup"><span data-stu-id="bf852-123">A VPN client configuration package.</span></span> <span data-ttu-id="bf852-124">Merhaba VPN istemcisi yapılandırma paketini hello hello istemci tooconnect toohello VNet için gerekli bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="bf852-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="bf852-125">Merhaba paket yerel toohello Windows işletim sistemi hello mevcut VPN istemcisi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bf852-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="bf852-126">Merhaba yapılandırma paketini kullanarak bağlanan her istemci yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf852-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="bf852-127">Noktadan Siteye bağlantılar için bir VPN cihazına veya şirket içi genel kullanıma yönelik bir IP adresine gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="bf852-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="bf852-128">Merhaba VPN bağlantı SSTP (Güvenli Yuva Tünel Protokolü) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bf852-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="bf852-129">Merhaba sunucu tarafında SSTP sürümleri 1.0, 1.1 ve 1.2 destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="bf852-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="bf852-130">Merhaba istemci hangi sürümü toouse karar verir.</span><span class="sxs-lookup"><span data-stu-id="bf852-130">hello client decides which version toouse.</span></span> <span data-ttu-id="bf852-131">Windows 8.1 ve sonraki sürümlerinde, SSTP'de varsayılan olarak 1.2 kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bf852-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="bf852-132">Merhaba noktadan siteye bağlantılar hakkında daha fazla bilgi için bkz: [noktası siteye SSS](#faq) hello bu makalenin sonunda.</span><span class="sxs-lookup"><span data-stu-id="bf852-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="bf852-133">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="bf852-133">Before beginning</span></span>

* <span data-ttu-id="bf852-134">Azure aboneliğiniz olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bf852-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="bf852-135">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="bf852-136">Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bf852-136">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="bf852-137">PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bf852-137">For more information about installing PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="bf852-138"><a name="example"></a>Örnek değerler</span><span class="sxs-lookup"><span data-stu-id="bf852-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="bf852-139">Merhaba örnek değerleri toocreate bir test ortamı kullanın veya toothese değerleri bkz toobetter anlamak bu makaledeki hello örnekler.</span><span class="sxs-lookup"><span data-stu-id="bf852-139">You can use hello example values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article.</span></span> <span data-ttu-id="bf852-140">Merhaba değişkenler bölümünde ayarlarız [1](#declare) hello makalenin.</span><span class="sxs-lookup"><span data-stu-id="bf852-140">We set hello variables in section [1](#declare) of hello article.</span></span> <span data-ttu-id="bf852-141">Merhaba adımları bir kılavuz kullanın ve bunları değiştirmeden hello değerleri kullanın veya tooreflect değiştirmek ortamınızı.</span><span class="sxs-lookup"><span data-stu-id="bf852-141">You can either use hello steps as a walk-through and use hello values without changing them, or change them tooreflect your environment.</span></span> 

* <span data-ttu-id="bf852-142">**Ad: VNet1**</span><span class="sxs-lookup"><span data-stu-id="bf852-142">**Name: VNet1**</span></span>
* <span data-ttu-id="bf852-143">**Adres alanı: 192.168.0.0/16** ve **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="bf852-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="bf852-144">Bu örnekte, bu yapılandırma ile birden çok adres alanları çalışır birden fazla adres alanı tooillustrate kullanırız.</span><span class="sxs-lookup"><span data-stu-id="bf852-144">For this example, we use more than one address space tooillustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="bf852-145">Ancak, bu yapılandırma için birden çok adres alanı gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="bf852-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="bf852-146">**Alt ağ adı: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="bf852-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="bf852-147">**Alt ağ adres aralığı: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="bf852-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="bf852-148">**Alt ağ adı: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="bf852-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="bf852-149">**Alt ağ adres aralığı: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="bf852-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="bf852-150">**Alt ağ adı: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="bf852-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="bf852-151">Merhaba alt ağ adı *GatewaySubnet* hello VPN ağ geçidi toowork için zorunludur.</span><span class="sxs-lookup"><span data-stu-id="bf852-151">hello Subnet name *GatewaySubnet* is mandatory for hello VPN gateway toowork.</span></span>
  * <span data-ttu-id="bf852-152">**Ağ Geçidi Alt Ağ adres aralığı: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="bf852-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="bf852-153">**VPN istemcisi adres havuzu: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="bf852-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="bf852-154">Toohello bu noktadan siteye bağlantıyı kullanarak VNet bağlantı VPN istemcileri, VPN istemci adres havuzu hello bir IP adresi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="bf852-154">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello VPN client address pool.</span></span>
* <span data-ttu-id="bf852-155">**Abonelik:** kullandığınızdan emin olun, birden fazla aboneliğiniz varsa doğru olanı hello.</span><span class="sxs-lookup"><span data-stu-id="bf852-155">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="bf852-156">**Kaynak Grubu: TestRG**</span><span class="sxs-lookup"><span data-stu-id="bf852-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="bf852-157">**Konum: Doğu ABD**</span><span class="sxs-lookup"><span data-stu-id="bf852-157">**Location: East US**</span></span>
* <span data-ttu-id="bf852-158">**DNS sunucusu: IP adresi** hello DNS sunucusunun ad çözümlemesi için toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="bf852-158">**DNS Server: IP address** of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="bf852-159">**Ağ Geçidi Adı: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="bf852-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="bf852-160">**Ortak IP adı: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="bf852-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="bf852-161">**VpnType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="bf852-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="bf852-162"><a name="declare"></a>1. Oturum açma ve değişkenleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="bf852-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="bf852-163">Bu bölümde, oturum açın ve bu yapılandırma için kullanılan hello değerlerini bildirin.</span><span class="sxs-lookup"><span data-stu-id="bf852-163">In this section, you log in and declare hello values used for this configuration.</span></span> <span data-ttu-id="bf852-164">Hello olarak bildirilen değerler hello örnek komut dosyalarını kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bf852-164">hello declared values are used in hello sample scripts.</span></span> <span data-ttu-id="bf852-165">Merhaba değerleri tooreflect kendi ortamınızdaki değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bf852-165">Change hello values tooreflect your own environment.</span></span> <span data-ttu-id="bf852-166">Veya değerleri bildirilen hello kullanın ve hello adımları bir alıştırma olarak gidin.</span><span class="sxs-lookup"><span data-stu-id="bf852-166">Or, you can use hello declared values and go through hello steps as an exercise.</span></span>

1. <span data-ttu-id="bf852-167">PowerShell Konsolunuzu yükseltilmiş ayrıcalıklarla açın ve tooyour Azure hesabı oturum.</span><span class="sxs-lookup"><span data-stu-id="bf852-167">Open your PowerShell console with elevated privileges, and log in tooyour Azure account.</span></span> <span data-ttu-id="bf852-168">Bu cmdlet hello oturum açma kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="bf852-168">This cmdlet prompts you for hello login credentials.</span></span> <span data-ttu-id="bf852-169">Kullanılabilir tooAzure PowerShell; böylece oturum açtıktan sonra hesap ayarlarınızı indirir.</span><span class="sxs-lookup"><span data-stu-id="bf852-169">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="bf852-170">Azure aboneliklerinizin bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="bf852-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="bf852-171">Merhaba abonelik toouse istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="bf852-171">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="bf852-172">Toouse istediğiniz hello değişkenleri bildirin.</span><span class="sxs-lookup"><span data-stu-id="bf852-172">Declare hello variables that you want toouse.</span></span> <span data-ttu-id="bf852-173">Aşağıdaki örnek, hello değerleri gerektiğinde kendi değiştirerek hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="bf852-173">Use hello following sample, substituting hello values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <span data-ttu-id="bf852-174"><a name="ConfigureVNet"></a>2. Sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bf852-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="bf852-175">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bf852-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="bf852-176">Merhaba adlandırarak hello sanal ağ alt ağı yapılandırmaları oluşturmak *ön uç*, *arka uç*, ve *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="bf852-176">Create hello subnet configurations for hello virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="bf852-177">Bu önekleri Merhaba, bildirilen VNet adres alanı bir parçası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf852-177">These prefixes must be part of hello VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="bf852-178">Merhaba sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bf852-178">Create hello virtual network.</span></span>

  <span data-ttu-id="bf852-179">Bu örnekte, hello DNS sunucusu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bf852-179">In this example, hello DNS server is optional.</span></span> <span data-ttu-id="bf852-180">Bir değer belirtildiğinde yeni bir DNS sunucusu oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="bf852-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="bf852-181">Merhaba, belirttiğiniz DNS sunucusu IP adresi, bağlandığınız hello kaynaklar için hello adları çözümlemek için bir DNS sunucusu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bf852-181">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="bf852-182">Bu örnek için özel bir IP adresi kullandık, ancak bu hello IP adresinin DNS sunucunuzun olmadığını olasıdır.</span><span class="sxs-lookup"><span data-stu-id="bf852-182">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="bf852-183">Kendi değerlerinizi toouse emin olun.</span><span class="sxs-lookup"><span data-stu-id="bf852-183">Be sure toouse your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="bf852-184">Oluşturduğunuz hello sanal ağ için Hello değişkenleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="bf852-184">Specify hello variables for hello virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="bf852-185">Bir VPN ağ geçidinin genel bir IP adresi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bf852-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="bf852-186">Başlangıç IP adresi kaynağı ilk isteği ve ardından sanal ağ geçidinizi oluştururken tooit bakın.</span><span class="sxs-lookup"><span data-stu-id="bf852-186">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="bf852-187">Başlangıç IP adresi toohello kaynak Hello VPN ağ geçidi oluşturulup dinamik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="bf852-187">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="bf852-188">VPN Gateway hizmeti şu anda yalnızca *Dinamik* Genel IP adresi ayırmayı desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="bf852-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="bf852-189">Statik bir Genel IP adresi ataması isteğinde bulunamazsınız.</span><span class="sxs-lookup"><span data-stu-id="bf852-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="bf852-190">Ancak, tooyour VPN ağ geçidi atandıktan sonra hello IP adresini değiştirse anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="bf852-190">However, it doesn't mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="bf852-191">ağ geçidi Hello genel IP adresi değişiklikleri hello zaman hello yalnızca zaman silinmiş ve yeniden oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bf852-191">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="bf852-192">VPN ağ geçidiniz üzerinde gerçekleştirilen yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında değişmez.</span><span class="sxs-lookup"><span data-stu-id="bf852-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="bf852-193">Dinamik olarak atanan bir genel IP adresi isteyin.</span><span class="sxs-lookup"><span data-stu-id="bf852-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="bf852-194"><a name="creategateway"></a>3. Merhaba VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bf852-194"><a name="creategateway"></a>3. Create hello VPN gateway</span></span>

<span data-ttu-id="bf852-195">Yapılandırın ve hello sanal ağ geçidi için sanal ağınızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bf852-195">Configure and create hello virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="bf852-196">Merhaba *- GatewayType* olmalıdır **Vpn** ve hello *- VpnType* olmalıdır **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="bf852-196">hello *-GatewayType* must be **Vpn** and hello *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="bf852-197">Bir VPN ağ geçidi hello bağlı olarak too45 dakika toocomplete yukarı sürebilir [ağ geçidi SKU'su](vpn-gateway-about-vpn-gateway-settings.md) seçin.</span><span class="sxs-lookup"><span data-stu-id="bf852-197">A VPN gateway can take up too45 minutes toocomplete, depending on hello [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="bf852-198"><a name="addresspool"></a>4. Merhaba VPN istemci adres havuzu ekleme</span><span class="sxs-lookup"><span data-stu-id="bf852-198"><a name="addresspool"></a>4. Add hello VPN client address pool</span></span>

<span data-ttu-id="bf852-199">Merhaba VPN ağ geçidi oluşturduktan sonra hello VPN istemci adres havuzu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-199">After hello VPN gateway finishes creating, you can add hello VPN client address pool.</span></span> <span data-ttu-id="bf852-200">Merhaba VPN istemci adres havuzu içinden hello VPN istemcileri bir IP adresi bağlanırken alma hello aralıktır.</span><span class="sxs-lookup"><span data-stu-id="bf852-200">hello VPN client address pool is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="bf852-201">Çakışmayan bir özel IP adres aralığı, bağlanması hello şirket içi konumla veya hello tooconnect için istediğiniz VNet ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="bf852-201">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="bf852-202">Bu örnekte, hello VPN istemci adres havuzu olarak bildirilmiş bir [değişkeni](#declare) 1. adımda.</span><span class="sxs-lookup"><span data-stu-id="bf852-202">In this example, hello VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="bf852-203"><a name="Certificates"></a>5. İstemci sertifikaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="bf852-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="bf852-204">Sertifikalar için noktadan siteye VPN Azure tooauthenticate VPN istemcileri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bf852-204">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="bf852-205">Ortak anahtar bilgileri hello kök sertifika tooAzure hello karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bf852-205">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="bf852-206">Merhaba ortak anahtar ardından 'güvenilir' olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="bf852-206">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="bf852-207">İstemci sertifikaları gerekir hello güvenilen kök sertifika oluşturulur ve ardından her bir istemci bilgisayarı hello Sertifikalar-Geçerli kullanıcı/kişisel sertifika deposunda yüklü.</span><span class="sxs-lookup"><span data-stu-id="bf852-207">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="bf852-208">bağlantı toohello VNet başlattığında hello kullanılan tooauthenticate hello istemci sertifikasıdır.</span><span class="sxs-lookup"><span data-stu-id="bf852-208">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="bf852-209">Otomatik olarak imzalanan sertifikalar kullanıyorsanız bu sertifikaların belirli parametreler kullanılarak oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf852-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="bf852-210">Merhaba yönergeleri kullanarak otomatik olarak imzalanan bir sertifika oluşturabilir [PowerShell ve Windows 10](vpn-gateway-certificates-point-to-site.md), veya Windows 10 yoksa, kullanabileceğiniz [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="bf852-210">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="bf852-211">Otomatik olarak imzalanan kök sertifikalar ve istemci sertifikalarını oluştururken hello yönergelerindeki hello adımları izleyin önemlidir.</span><span class="sxs-lookup"><span data-stu-id="bf852-211">It's important that you follow hello steps in hello instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="bf852-212">Aksi takdirde, oluşturduğunuz hello sertifikaları P2S bağlantılarının ile uyumlu değil ve bağlantı hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="bf852-212">Otherwise, hello certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="bf852-213"><a name="cer"></a>1. Merhaba .cer dosyasını hello kök sertifikası için edinin</span><span class="sxs-lookup"><span data-stu-id="bf852-213"><a name="cer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="bf852-214"><a name="generate"></a>2. İstemci sertifikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="bf852-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="bf852-215"><a name="upload"></a>6. Merhaba kök sertifika ortak anahtar bilgileri karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="bf852-215"><a name="upload"></a>6. Upload hello root certificate public key information</span></span>

<span data-ttu-id="bf852-216">VPN ağ geçidini oluşturma işleminin tamamlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bf852-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="bf852-217">Bu tamamlandıktan sonra (Merhaba ortak anahtar bilgileri içeren) hello .cer dosyası için bir güvenilen kök sertifika tooAzure karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-217">Once it has completed, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="bf852-218">Azure a.cer dosya yüklendikten sonra hello güvenilen kök sertifika oluşturulan bir istemci sertifikası yüklemiş tooauthenticate istemcileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-218">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="bf852-219">Gerektiğinde ek güvenilen kök sertifika dosyaları - 20 - daha sonra tooa toplam karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-219">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="bf852-220">Merhaba değerini kendi değerlerinizle değiştirerek sertifika adınızı Hello değişken bildirin.</span><span class="sxs-lookup"><span data-stu-id="bf852-220">Declare hello variable for your certificate name, replacing hello value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="bf852-221">Merhaba dosya yolu kendinizinkilerle değiştirin ve ardından hello cmdlet'lerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bf852-221">Replace hello file path with your own, and then run hello cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="bf852-222">Merhaba ortak anahtar bilgileri tooAzure karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bf852-222">Upload hello public key information tooAzure.</span></span> <span data-ttu-id="bf852-223">Azure Hello sertifika bilgilerini yüklendikten sonra bir güvenilen kök sertifika bu toobe göz önünde bulundurur.</span><span class="sxs-lookup"><span data-stu-id="bf852-223">Once hello certificate information is uploaded, Azure considers this toobe a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="bf852-224"><a name="clientconfig"></a>7. Merhaba VPN istemcisi yapılandırma paketini indirme</span><span class="sxs-lookup"><span data-stu-id="bf852-224"><a name="clientconfig"></a>7. Download hello VPN client configuration package</span></span>

<span data-ttu-id="bf852-225">tooconnect tooa noktadan siteye VPN kullanarak VNet, her istemci hello yerel VPN istemcisi ile hello ayarlarını yapılandıran istemci yapılandırma paketi ve gerekli tooconnect toohello sanal ağ olan dosyaları yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf852-225">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="bf852-226">Merhaba VPN istemcisi yapılandırma paketini hello yerel Windows VPN istemcisi yapılandırır, yeni veya farklı bir VPN istemcisi yükleme yapmaz.</span><span class="sxs-lookup"><span data-stu-id="bf852-226">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="bf852-227">Hello sürüm hello istemci için hello mimarisi eşleştiği sürece, aynı VPN istemcisi yapılandırma paketini her istemci bilgisayarında hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-227">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="bf852-228">Merhaba, desteklenen istemci işletim sistemlerinin Hello listesi için bkz [noktadan siteye bağlantılar hakkında SSS](#faq) hello bu makalenin sonunda.</span><span class="sxs-lookup"><span data-stu-id="bf852-228">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

1. <span data-ttu-id="bf852-229">Merhaba ağ geçidi oluşturulduktan sonra oluşturmak ve hello istemcisi yapılandırma paketini indirin.</span><span class="sxs-lookup"><span data-stu-id="bf852-229">After hello gateway has been created, you can generate and download hello client configuration package.</span></span> <span data-ttu-id="bf852-230">Bu örnek, 64-bit istemciler için hello paketi indirir.</span><span class="sxs-lookup"><span data-stu-id="bf852-230">This example downloads hello package for 64-bit clients.</span></span> <span data-ttu-id="bf852-231">Toodownload hello 32 bit istemci istiyorsanız, 'Amd64' 'x86' ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bf852-231">If you want toodownload hello 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="bf852-232">Merhaba VPN istemcisi hello Azure portal kullanarak da yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-232">You can also download hello VPN client by using hello Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="bf852-233">Alma hello bağlantı çevreleyen tooremove hello teklifleri verdiğiniz tooa web tarayıcı toodownload hello paketi, döndürülen hello bağlantı kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="bf852-233">Copy and paste hello link that is returned tooa web browser toodownload hello package, taking care tooremove hello quotes surrounding hello link.</span></span> 
3. <span data-ttu-id="bf852-234">Paketini indirin ve hello hello istemci bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bf852-234">Download and install hello package on hello client computer.</span></span> <span data-ttu-id="bf852-235">Bir SmartScreen açılır penceresi görürseniz **Daha fazla bilgi**’ye ve ardından **Yine de çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf852-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="bf852-236">Diğer istemci bilgisayarlarda hello paket tooinstall da kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-236">You can also save hello package tooinstall on other client computers.</span></span>
4. <span data-ttu-id="bf852-237">Merhaba istemci bilgisayarda çok gidin**ağ ayarlarını** tıklatıp **VPN**.</span><span class="sxs-lookup"><span data-stu-id="bf852-237">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="bf852-238">Merhaba VPN bağlantısı hello bağlanır hello sanal ağ adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bf852-238">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="bf852-239"><a name="clientcertificate"></a>8. Dışarı aktarılan bir istemci sertifikasını yükleme</span><span class="sxs-lookup"><span data-stu-id="bf852-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="bf852-240">Toocreate bir P2S bağlantısı istiyorsanız hello dışında bir istemci bilgisayardan bir toogenerate hello istemci sertifikalarını kullandığınız, tooinstall bir istemci sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf852-240">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="bf852-241">Bir istemci sertifikası yüklerken hello istemci sertifikası dışarı aktarılırken oluşturduğunuz hello parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf852-241">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="bf852-242">Genellikle, bu hello sertifikayı çift ve bu yükleme yalnızca bir konudur.</span><span class="sxs-lookup"><span data-stu-id="bf852-242">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="bf852-243">Merhaba istemci sertifikası (Merhaba varsayılandır) hello tüm sertifika zinciri ile birlikte bir .pfx olarak aktarılmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bf852-243">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="bf852-244">Aksi takdirde hello kök sertifika bilgilerini hello istemci bilgisayarda mevcut değil ve hello istemci mümkün tooauthenticate düzgün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="bf852-244">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="bf852-245">Daha fazla bilgi için bkz. [Dışarı aktarılan istemci sertifikasını yükleme](vpn-gateway-certificates-point-to-site.md#install).</span><span class="sxs-lookup"><span data-stu-id="bf852-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="bf852-246"><a name="connect"></a>9. TooAzure Bağlan</span><span class="sxs-lookup"><span data-stu-id="bf852-246"><a name="connect"></a>9. Connect tooAzure</span></span>

1. <span data-ttu-id="bf852-247">Merhaba istemci bilgisayarda, tooconnect tooyour Vnet'in tooVPN bağlantıları gidin ve oluşturduğunuz hello VPN bağlantısını bulun.</span><span class="sxs-lookup"><span data-stu-id="bf852-247">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="bf852-248">Aynı sanal ağ olarak ad hello adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="bf852-248">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="bf852-249">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf852-249">Click **Connect**.</span></span> <span data-ttu-id="bf852-250">Bir açılır ileti toousing hello sertifika başvuran görünebilir.</span><span class="sxs-lookup"><span data-stu-id="bf852-250">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="bf852-251">Tıklatın **devam** toouse yükseltilmiş ayrıcalıklar.</span><span class="sxs-lookup"><span data-stu-id="bf852-251">Click **Continue** toouse elevated privileges.</span></span> 
2. <span data-ttu-id="bf852-252">Merhaba üzerinde **bağlantı** durum sayfasında, tıklatın **Bağlan** toostart hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="bf852-252">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="bf852-253">Görürseniz bir **Sertifika Seç** ekranında, hello istemci sertifikası gösteren toouse tooconnect istediğiniz hello biri olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bf852-253">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="bf852-254">Değilse, hello aşağı açılan okunu tooselect hello doğru sertifikayı kullanın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bf852-254">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![VPN istemci tooAzure bağlanır](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="bf852-256">Bağlantınız kurulur.</span><span class="sxs-lookup"><span data-stu-id="bf852-256">Your connection is established.</span></span>

  ![Bağlantı kuruldu](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="bf852-258">P2S bağlantılarının sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="bf852-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="bf852-259"><a name="verify"></a>10. Bağlantınızı doğrulama</span><span class="sxs-lookup"><span data-stu-id="bf852-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="bf852-260">VPN bağlantınızın etkin olduğunu tooverify yükseltilmiş bir komut istemi açın ve çalıştırın *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="bf852-260">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="bf852-261">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="bf852-261">View hello results.</span></span> <span data-ttu-id="bf852-262">Başlangıç IP adresi aldığınız yapılandırmanızda belirtilen hello noktadan siteye VPN istemci adres havuzu içindeki hello adresleri birini olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bf852-262">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="bf852-263">Merhaba, benzer toothis örnek karşılaşılır:</span><span class="sxs-lookup"><span data-stu-id="bf852-263">hello results are similar toothis example:</span></span>

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="bf852-264"><a name="connectVM"></a>Tooa sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="bf852-264"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="bf852-265"><a name="addremovecert"></a>Kök sertifika ekleme veya kaldırma</span><span class="sxs-lookup"><span data-stu-id="bf852-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="bf852-266">Azure’da güvenilen kök sertifikayı ekleyebilir veya kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="bf852-267">Bir kök sertifikası kaldırdığınızda, oluşturulan hello kök sertifikasından bir sertifika olan istemcileri kimlik doğrulaması yapamaz ve tooconnect mümkün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="bf852-267">When you remove a root certificate, clients that have a certificate generated from hello root certificate can't authenticate and won't be able tooconnect.</span></span> <span data-ttu-id="bf852-268">İstemci tooauthenticate ve bağlanmak istiyorsanız, yeni bir istemci sertifikası güvenilen (karşıya yüklenen) tooAzure olan bir kök sertifika oluşturulan tooinstall gerekir.</span><span class="sxs-lookup"><span data-stu-id="bf852-268">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="bf852-269"><a name="addtrustedroot"></a>tooadd güvenilen bir kök sertifikası</span><span class="sxs-lookup"><span data-stu-id="bf852-269"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="bf852-270">Too20 kök sertifika .cer dosyaları tooAzure ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-270">You can add up too20 root certificate .cer files tooAzure.</span></span> <span data-ttu-id="bf852-271">bir kök sertifika Ekle Yardım Hello aşağıdaki adımları:</span><span class="sxs-lookup"><span data-stu-id="bf852-271">hello following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="bf852-272"><a name="certmethod1"></a>1. Yöntem</span><span class="sxs-lookup"><span data-stu-id="bf852-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="bf852-273">Merhaba en verimli yöntemi tooupload bir kök sertifikası budur.</span><span class="sxs-lookup"><span data-stu-id="bf852-273">This is hello most efficient method tooupload a root certificate.</span></span>

1. <span data-ttu-id="bf852-274">Merhaba .cer dosyasını tooupload hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="bf852-274">Prepare hello .cer file tooupload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="bf852-275">Merhaba dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bf852-275">Upload hello file.</span></span> <span data-ttu-id="bf852-276">Aynı anda yalnızca bir dosya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="bf852-277">Sertifika dosyası karşıya hello tooverify:</span><span class="sxs-lookup"><span data-stu-id="bf852-277">tooverify that hello certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="bf852-278"><a name="certmethod2"></a>2. Yöntem</span><span class="sxs-lookup"><span data-stu-id="bf852-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="bf852-279">Bu yöntem yöntemi 1'den daha fazla adım vardır, ancak var olan hello aynı sonucu.</span><span class="sxs-lookup"><span data-stu-id="bf852-279">This method is has more steps than Method 1, but has hello same result.</span></span> <span data-ttu-id="bf852-280">Tooview hello sertifika verilere ihtiyaç durumunda dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="bf852-280">It is included in case you need tooview hello certificate data.</span></span>

1. <span data-ttu-id="bf852-281">Oluşturma ve hello yeni kök sertifika tooadd tooAzure hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="bf852-281">Create and prepare hello new root certificate tooadd tooAzure.</span></span> <span data-ttu-id="bf852-282">Base-64 olarak kodlanmış X.509 gibi hello ortak anahtarı dışarı aktar (. CER) ve bir metin düzenleyicisiyle açın.</span><span class="sxs-lookup"><span data-stu-id="bf852-282">Export hello public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="bf852-283">Hello aşağıdaki örnekte gösterildiği gibi Hello değerleri kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="bf852-283">Copy hello values, as shown in hello following example:</span></span>

  ![sertifika](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="bf852-285">Merhaba sertifika veri kopyalama işlemi sırasında satır başı veya satır beslemelerini olmadan sürekli bir satır olarak hello metin kopyaladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bf852-285">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="bf852-286">Merhaba metin düzenleyicisi too'Show simgesi/tüm karakterleri toosee hello satır döndürür ve satır besleme karakterlerini göster görünümünüzde toomodify gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bf852-286">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="bf852-287">Merhaba sertifika adı ve anahtar bilgileri bir değişken olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="bf852-287">Specify hello certificate name and key information as a variable.</span></span> <span data-ttu-id="bf852-288">Merhaba bilgileri kendi hello gösterildiği gibi aşağıdaki örnekle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bf852-288">Replace hello information with your own, as shown in hello following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="bf852-289">Merhaba yeni kök sertifikasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bf852-289">Add hello new root certificate.</span></span> <span data-ttu-id="bf852-290">Tek seferde yalnızca bir sertifika ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="bf852-291">Bu hello yeni sertifika doğru şekilde aşağıdaki örneğine hello kullanılarak eklenen doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bf852-291">You can verify that hello new certificate was added correctly by using hello following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="bf852-292"><a name="removerootcert"></a>tooremove bir kök sertifikası</span><span class="sxs-lookup"><span data-stu-id="bf852-292"><a name="removerootcert"></a>tooremove a root certificate</span></span>

1. <span data-ttu-id="bf852-293">Merhaba değişkenleri bildirin.</span><span class="sxs-lookup"><span data-stu-id="bf852-293">Declare hello variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="bf852-294">Merhaba sertifika kaldırın.</span><span class="sxs-lookup"><span data-stu-id="bf852-294">Remove hello certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="bf852-295">Sertifika hello örnek tooverify aşağıdaki kullanım hello başarıyla kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="bf852-295">Use hello following example tooverify that hello certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="bf852-296"><a name="revoke"></a>İstemci sertifikasını iptal etme</span><span class="sxs-lookup"><span data-stu-id="bf852-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="bf852-297">İstemci sertifikalarını iptal edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-297">You can revoke client certificates.</span></span> <span data-ttu-id="bf852-298">Merhaba sertifika iptal listesi tooselectively sağlayan tek bir istemci sertifikalarını temel alarak noktadan siteye bağlantı reddedin.</span><span class="sxs-lookup"><span data-stu-id="bf852-298">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="bf852-299">Bu, güvenilen kök sertifika kaldırma işleminden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="bf852-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="bf852-300">Azure'dan bir güvenilen kök sertifika .cer kaldırırsanız, tüm istemci sertifikaları için oluşturulan ve imzalanmış hello iptal edilen kök sertifikası tarafından hello erişimi iptal eder.</span><span class="sxs-lookup"><span data-stu-id="bf852-300">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="bf852-301">Bir istemci sertifikası iptal etmek hello kök sertifika yerine hello kök sertifika toocontinue toobe kimlik doğrulaması için kullanılan gelen oluşturulan diğer sertifikaları hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf852-301">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="bf852-302">Merhaba yaygın toouse hello kök sertifika toomanage erişim düzeyleri, ekip veya kuruluş bireysel kullanıcılar üzerinde ayrıntılı erişim denetimi için İptal edilen istemci sertifikalarını kullanırken bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="bf852-302">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="bf852-303"><a name="revokeclientcert"></a>toorevoke bir istemci sertifikası</span><span class="sxs-lookup"><span data-stu-id="bf852-303"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

1. <span data-ttu-id="bf852-304">Merhaba istemci sertifikası parmak izi alma.</span><span class="sxs-lookup"><span data-stu-id="bf852-304">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="bf852-305">Daha fazla bilgi için bkz: [nasıl tooretrieve hello bir sertifikanın parmak izini](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf852-305">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="bf852-306">Merhaba bilgileri tooa metin düzenleyicisi kopyalayın ve sürekli bir dize olmasını tüm boşlukları Kaldır.</span><span class="sxs-lookup"><span data-stu-id="bf852-306">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="bf852-307">Bu dize bir değişken olarak hello sonraki adımda bildirildi.</span><span class="sxs-lookup"><span data-stu-id="bf852-307">This string is declared as a variable in hello next step.</span></span>
3. <span data-ttu-id="bf852-308">Merhaba değişkenleri bildirin.</span><span class="sxs-lookup"><span data-stu-id="bf852-308">Declare hello variables.</span></span> <span data-ttu-id="bf852-309">Alınan emin toodeclare hello parmak izi hello önceki adımda olun.</span><span class="sxs-lookup"><span data-stu-id="bf852-309">Make sure toodeclare hello thumbprint you retrieved in hello previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="bf852-310">Merhaba parmak izi toohello iptal edilen sertifikaların listesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bf852-310">Add hello thumbprint toohello list of revoked certificates.</span></span> <span data-ttu-id="bf852-311">Merhaba parmak izi eklendiğinde "Başarılı" konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="bf852-311">You see "Succeeded" when hello thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="bf852-312">Bu hello parmak izi toohello sertifika iptal listesi eklenen doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bf852-312">Verify that hello thumbprint was added toohello certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="bf852-313">Merhaba parmak izi eklendikten sonra hello sertifika artık kullanılan tooconnect olabilir.</span><span class="sxs-lookup"><span data-stu-id="bf852-313">After hello thumbprint has been added, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="bf852-314">Bu sertifikayı kullanarak tooconnect deneyin istemcileri bu hello sertifika artık geçerli olduğunu bildiren bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="bf852-314">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

### <span data-ttu-id="bf852-315"><a name="reinstateclientcert"></a>tooreinstate bir istemci sertifikası</span><span class="sxs-lookup"><span data-stu-id="bf852-315"><a name="reinstateclientcert"></a>tooreinstate a client certificate</span></span>

<span data-ttu-id="bf852-316">Bir istemci sertifikası, iptal edilen istemci sertifikalarını hello listeden hello parmak izi kaldırarak yeniden başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-316">You can reinstate a client certificate by removing hello thumbprint from hello list of revoked client certificates.</span></span>

1. <span data-ttu-id="bf852-317">Merhaba değişkenleri bildirin.</span><span class="sxs-lookup"><span data-stu-id="bf852-317">Declare hello variables.</span></span> <span data-ttu-id="bf852-318">Merhaba doğru parmak izi tooreinstate istediğiniz hello sertifika bildirme emin olun.</span><span class="sxs-lookup"><span data-stu-id="bf852-318">Make sure you declare hello correct thumbprint for hello certificate that you want tooreinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="bf852-319">Merhaba sertifika parmak izi hello sertifikayı iptal listesinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="bf852-319">Remove hello certificate thumbprint from hello certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="bf852-320">Merhaba parmak izi hello iptal listesinden kaldırılır, denetleyin.</span><span class="sxs-lookup"><span data-stu-id="bf852-320">Check if hello thumbprint is removed from hello revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="bf852-321"><a name="faq"></a>Noktadan Siteye hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="bf852-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="bf852-322">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bf852-322">Next steps</span></span>
<span data-ttu-id="bf852-323">Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf852-323">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="bf852-324">Daha fazla bilgi için bkz. [Sanal Makineler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="bf852-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="bf852-325">Ağ ve sanal makineler hakkında daha fazla toounderstand bkz [Azure ve Linux VM ağına genel bakış](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf852-325">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
