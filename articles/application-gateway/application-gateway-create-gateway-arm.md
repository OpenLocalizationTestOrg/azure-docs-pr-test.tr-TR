---
title: "aaaCreate ve Azure uygulama ağ geçidi - PowerShell yönetme | Microsoft Docs"
description: "Bu sayfa toocreate, yapılandırmak, başlatmak ve Azure Resource Manager kullanarak bir Azure uygulama ağ geçidini silme yönergelerini sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="e9d18-103">Azure Resource Manager kullanarak bir uygulama ağ geçidi oluşturma, başlatma veya silme</span><span class="sxs-lookup"><span data-stu-id="e9d18-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9d18-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e9d18-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="e9d18-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9d18-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="e9d18-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9d18-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="e9d18-107">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="e9d18-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="e9d18-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e9d18-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="e9d18-109">Azure Application Gateway, bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="e9d18-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="e9d18-110">Merhaba Bulut veya şirket içi olup, yük devretme ve performans yönlendirme HTTP isteklerini, farklı sunucular arasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9d18-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="e9d18-111">Application Gateway; HTTP yük dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) boşaltma, özel sistem durumu araştırmaları, çoklu site desteği gibi birçok uygulama teslim denetleyicisi (ADC) özelliği sunar.</span><span class="sxs-lookup"><span data-stu-id="e9d18-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="e9d18-112">toofind desteklenen özelliklerin tam bir listesi ziyaret [uygulama ağ geçidi'ne genel bakış](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e9d18-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="e9d18-113">Bu makalede hello adımları toocreate anlatılmaktadır, yapılandırmak, başlatmak ve bir uygulama ağ geçidini silin.</span><span class="sxs-lookup"><span data-stu-id="e9d18-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9d18-114">Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="e9d18-114">Before you work with Azure resources, it is important toounderstand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="e9d18-115">Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e9d18-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="e9d18-116">Bu makalenin hello üstünde hello sekmeleri tıklayarak farklı araçlarla ilgili hello belgeleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9d18-116">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="e9d18-117">Bu belge, Azure Resource Manager’ı kullanarak uygulama ağ geçidi oluşturmayı kapsar.</span><span class="sxs-lookup"><span data-stu-id="e9d18-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="e9d18-118">toouse hello Klasik sürümü, çok Git[PowerShell kullanarak bir uygulama ağ geçidi Klasik dağıtımı oluşturma](application-gateway-create-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="e9d18-118">toouse hello classic version, go too[Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e9d18-119">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e9d18-119">Before you begin</span></span>

1. <span data-ttu-id="e9d18-120">Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e9d18-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="e9d18-121">Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e9d18-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="e9d18-122">Varolan bir sanal ağınız varsa, mevcut bir boş alt seçin veya hello uygulama ağ geçidi tarafından varolan sanal ağınızda kullanmak için yalnızca bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e9d18-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="e9d18-123">Merhaba uygulama ağ geçidi tooa farklı sanal ağı dağıtamazsınız hello uygulama ağ geçidi arkasında toodeploy düşündüğünüz daha hello kaynak.</span><span class="sxs-lookup"><span data-stu-id="e9d18-123">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway.</span></span>
1. <span data-ttu-id="e9d18-124">toouse hello uygulama ağ geçidi yapılandırma hello sunucular mevcut olmalıdır veya hello sanal ağ veya genel IP/VIP'ye ile oluşturulan uç noktaları atadınız.</span><span class="sxs-lookup"><span data-stu-id="e9d18-124">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="e9d18-125">Gerekli toocreate bir uygulama ağ geçidi nedir?</span><span class="sxs-lookup"><span data-stu-id="e9d18-125">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="e9d18-126">**Arka uç sunucusu havuzu:** IP adresleri, FQDN'ler ya da NIC'ler hello arka uç sunucularının hello listesi.</span><span class="sxs-lookup"><span data-stu-id="e9d18-126">**Backend server pool:** hello list of IP addresses, FQDNs, or NICs of hello backend servers.</span></span> <span data-ttu-id="e9d18-127">IP adresleri kullanılıyorsa, ya da toohello sanal ağ alt ait olması gerekir veya genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e9d18-127">If IP addresses are used, they should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="e9d18-128">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="e9d18-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="e9d18-129">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="e9d18-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="e9d18-130">**ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="e9d18-130">**frontend port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="e9d18-131">Trafiği, bu bağlantı noktasında trafik ve yeniden yönlendirilen tooone hello arka uç sunucularının alır.</span><span class="sxs-lookup"><span data-stu-id="e9d18-131">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="e9d18-132">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="e9d18-132">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="e9d18-133">**Kural:** hello kural hello dinleyicisi, hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğini olmalıdır belirler.</span><span class="sxs-lookup"><span data-stu-id="e9d18-133">**Rule:** hello rule binds hello listener, hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="e9d18-134">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="e9d18-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="e9d18-135">Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e9d18-135">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="e9d18-136">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="e9d18-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="e9d18-137">İçinde tooAzure oturum ve kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="e9d18-137">Log in tooAzure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="e9d18-138">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="e9d18-138">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="e9d18-139">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="e9d18-139">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="e9d18-140">Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="e9d18-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="e9d18-141">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e9d18-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="e9d18-142">Bu konum, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e9d18-142">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="e9d18-143">Bir uygulama ağ geçidini kullanan tüm komutları toocreate Merhaba, aynı olduğundan emin olun kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="e9d18-143">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="e9d18-144">Adlı bir kaynak grubu oluşturduk Hello yukarıdaki örnekte, **ContosoRG** ve konum **Doğu ABD**.</span><span class="sxs-lookup"><span data-stu-id="e9d18-144">In hello example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="e9d18-145">Uygulama ağ geçidiniz için özel bir araştırma tooconfigure gerekiyorsa, ziyaret edin: [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e9d18-145">If you need tooconfigure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="e9d18-146">Daha fazla bilgi için [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) konusunu inceleyin.</span><span class="sxs-lookup"><span data-stu-id="e9d18-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-hello-application-gateway-configuration-objects"></a><span data-ttu-id="e9d18-147">Merhaba uygulama ağ geçidi yapılandırma nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="e9d18-147">Create hello application gateway configuration objects</span></span>

<span data-ttu-id="e9d18-148">Tüm yapılandırma öğeleri hello uygulama ağ geçidi oluşturmadan önce ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9d18-148">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="e9d18-149">Merhaba aşağıdaki adımları hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e9d18-149">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="e9d18-150">Tamamlandığında, DNS ve VIP hello uygulama ağ geçidi ayrıntılarını hello ortak IP kaynak ekli toohello uygulama ağ geçidi'nden alın.</span><span class="sxs-lookup"><span data-stu-id="e9d18-150">When complete, retrieve DNS and VIP details of hello application gateway from hello public IP resource attached toohello application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="e9d18-151">Merhaba uygulama ağ geçidini Sil</span><span class="sxs-lookup"><span data-stu-id="e9d18-151">Delete hello application gateway</span></span>

<span data-ttu-id="e9d18-152">Merhaba aşağıdaki örnek hello uygulama ağ geçidini siler.</span><span class="sxs-lookup"><span data-stu-id="e9d18-152">hello following example deletes hello application gateway.</span></span>

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="e9d18-153">Merhaba **-force** anahtar kullanılan toosuppress hello kaldırma onayı iletisini olabilir.</span><span class="sxs-lookup"><span data-stu-id="e9d18-153">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="e9d18-154">Hizmet hello tooverify kaldırıldı, hello kullanabilirsiniz `Get-AzureRmApplicationGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="e9d18-154">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="e9d18-155">Bu adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e9d18-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="e9d18-156">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="e9d18-156">Get application gateway DNS name</span></span>

<span data-ttu-id="e9d18-157">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="e9d18-157">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="e9d18-158">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="e9d18-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="e9d18-159">hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="e9d18-159">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="e9d18-160">toodo Bu, alma ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adı.</span><span class="sxs-lookup"><span data-stu-id="e9d18-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="e9d18-161">Bu Azure DNS veya diğer DNS sağlayıcıları tarafından toohello işaret eden bir CNAME kaydı oluşturma yapılabilir [genel IP adresi](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="e9d18-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points toohello [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="e9d18-162">Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="e9d18-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="e9d18-163">Merhaba hizmeti başladığında toohello uygulama ağ geçidi bir IP adresi atanır.</span><span class="sxs-lookup"><span data-stu-id="e9d18-163">An IP address is assigned toohello application gateway when hello service starts.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a><span data-ttu-id="e9d18-164">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="e9d18-164">Delete all resources</span></span>

<span data-ttu-id="e9d18-165">Bu makalede, aşağıdaki tam hello oluşturulan tüm kaynakları adım toodelete:</span><span class="sxs-lookup"><span data-stu-id="e9d18-165">toodelete all resources created in this article, complete hello following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="e9d18-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e9d18-166">Next steps</span></span>

<span data-ttu-id="e9d18-167">SSL boşaltma tooconfigure istiyorsanız, ziyaret edin: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="e9d18-167">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="e9d18-168">Bir iç yük dengeleyici ile bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, ziyaret edin: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="e9d18-168">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="e9d18-169">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.:</span><span class="sxs-lookup"><span data-stu-id="e9d18-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="e9d18-170">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e9d18-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="e9d18-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e9d18-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
