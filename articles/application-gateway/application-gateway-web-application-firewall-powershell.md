---
title: "aaaConfigure web uygulaması güvenlik duvarı - Azure uygulama ağ geçidi | Microsoft Docs"
description: "Bu makalede, nasıl toostart kullanarak izin ver web uygulaması Güvenlik Duvarı'nı varolan veya yeni uygulama ağ geçidi hakkında yönergeleri sunar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="229b5-103">Web uygulaması güvenlik duvarı bir yeni veya var olan uygulama ağ geçidi üzerinde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="229b5-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="229b5-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="229b5-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="229b5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="229b5-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="229b5-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="229b5-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="229b5-107">Uygulama ağ geçidi mevcut web uygulaması güvenlik duvarı tooan ekleyin veya nasıl uygulama ağ geçidi toocreate bir web uygulaması Güvenlik Duvarı etkin öğrenin.</span><span class="sxs-lookup"><span data-stu-id="229b5-107">Learn how toocreate a web application firewall enabled Application Gateway or add web application firewall tooan existing Application Gateway.</span></span>

<span data-ttu-id="229b5-108">Hello web uygulaması Güvenlik Duvarı (WAF) Azure uygulama ağ geçidi, web uygulamaları, SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini korur.</span><span class="sxs-lookup"><span data-stu-id="229b5-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="229b5-109">Azure Application Gateway, bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="229b5-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="229b5-110">Merhaba Bulut veya şirket içinde olmalarından bağımsız yük devretme, HTTP isteklerini, farklı sunucular arasında performans amaçlı yönlendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="229b5-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="229b5-111">Uygulama ağ geçidi HTTP dahil olmak üzere pek çok uygulama teslim denetleyici (ADC) özelliklerini Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının, çoklu site desteği ve diğer birçok sağlar.</span><span class="sxs-lookup"><span data-stu-id="229b5-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="229b5-112">toofind desteklenen özelliklerin tam bir listesi ziyaret edin: [genel bakış, uygulama ağ geçidi](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="229b5-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="229b5-113">Merhaba aşağıdaki makalede nasıl çok gösterilmektedir[uygulama ağ geçidi mevcut web uygulaması güvenlik duvarı tooan ekleme](#add-web-application-firewall-to-an-existing-application-gateway) ve [web uygulaması Güvenlik Duvarı'nı kullanan uygulama ağ geçidi oluşturma](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="229b5-113">hello following article shows how too[add web application firewall tooan existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![Senaryo görüntüsü][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="229b5-115">WAF yapılandırma farklılıkları</span><span class="sxs-lookup"><span data-stu-id="229b5-115">WAF configuration differences</span></span>

<span data-ttu-id="229b5-116">Okuma [PowerShell ile bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-arm.md), bir uygulama ağ geçidi oluştururken hello SKU ayarları tooconfigure anlayın.</span><span class="sxs-lookup"><span data-stu-id="229b5-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand hello SKU settings tooconfigure when creating an Application Gateway.</span></span> <span data-ttu-id="229b5-117">WAF ek ayarlar toodefine hello SKU üzerinde bir uygulama ağ geçidini yapılandırırken sağlar.</span><span class="sxs-lookup"><span data-stu-id="229b5-117">WAF provides additional settings toodefine when configuring hello SKU on an Application Gateway.</span></span> <span data-ttu-id="229b5-118">Uygulama ağ geçidi kendisini hello üzerinde yaptığınız ek değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="229b5-118">There are no additional changes that you make on hello Application Gateway itself.</span></span>

| <span data-ttu-id="229b5-119">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="229b5-119">**Setting**</span></span> | <span data-ttu-id="229b5-120">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="229b5-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="229b5-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="229b5-121">**SKU**</span></span> |<span data-ttu-id="229b5-122">WAF destekler olmadan normal bir uygulama ağ geçidi **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**boyutları.</span><span class="sxs-lookup"><span data-stu-id="229b5-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="229b5-123">WAF Hello başlanmasıyla, iki ek SKU vardır **WAF\_orta** ve **WAF\_büyük**.</span><span class="sxs-lookup"><span data-stu-id="229b5-123">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="229b5-124">WAF küçük uygulama ağ geçitleri üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="229b5-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="229b5-125">**Katmanı**</span><span class="sxs-lookup"><span data-stu-id="229b5-125">**Tier**</span></span> | <span data-ttu-id="229b5-126">Merhaba kullanılabilir değerler **standart** veya **WAF**.</span><span class="sxs-lookup"><span data-stu-id="229b5-126">hello available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="229b5-127">Web uygulaması güvenlik duvarı, kullanırken **WAF** seçilmelidir.</span><span class="sxs-lookup"><span data-stu-id="229b5-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="229b5-128">**Modu**</span><span class="sxs-lookup"><span data-stu-id="229b5-128">**Mode**</span></span> | <span data-ttu-id="229b5-129">Bu ayar, WAF, hello modudur.</span><span class="sxs-lookup"><span data-stu-id="229b5-129">This setting is hello mode of WAF.</span></span> <span data-ttu-id="229b5-130">izin verilen değerler **algılama** ve **önleme**.</span><span class="sxs-lookup"><span data-stu-id="229b5-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="229b5-131">WAF algılama modunda ayarlandığında, tüm tehditler bir günlük dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="229b5-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="229b5-132">Önleme modda olayları yine kaydedilir ancak hello saldırgan 403 yetkisiz yanıt hello uygulama ağ geçidi ' alır.</span><span class="sxs-lookup"><span data-stu-id="229b5-132">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello Application Gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="229b5-133">Uygulama ağ geçidi mevcut web uygulaması güvenlik duvarı tooan Ekle</span><span class="sxs-lookup"><span data-stu-id="229b5-133">Add web application firewall tooan existing Application Gateway</span></span>

<span data-ttu-id="229b5-134">Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="229b5-134">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="229b5-135">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="229b5-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="229b5-136">Tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="229b5-136">Log in tooyour Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="229b5-137">Bu senaryo için Hello abonelik toouse seçin.</span><span class="sxs-lookup"><span data-stu-id="229b5-137">Select hello subscription toouse for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="229b5-138">Web uygulaması Güvenlik Duvarı'na eklediğiniz hello ağ geçidi alın.</span><span class="sxs-lookup"><span data-stu-id="229b5-138">Retrieve hello gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="229b5-139">Merhaba web uygulaması güvenlik duvarı sku yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="229b5-139">Configure hello web application firewall sku.</span></span> <span data-ttu-id="229b5-140">Merhaba kullanılabilir boyutları: **WAF\_büyük** ve **WAF\_orta**.</span><span class="sxs-lookup"><span data-stu-id="229b5-140">hello available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="229b5-141">Web uygulaması güvenlik duvarı kullanıldığında hello katmanı olmalıdır **WAF**, hello kapasite gerekir onaylanıp hello sku ayarlarken.</span><span class="sxs-lookup"><span data-stu-id="229b5-141">When web application firewall is used hello tier must be **WAF**, hello capacity must be confirmed when setting hello sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="229b5-142">Merhaba WAF ayarları aşağıdaki örneğine hello tanımlandığı şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="229b5-142">Configure hello WAF settings as defined in hello following example:</span></span>

   <span data-ttu-id="229b5-143">İçin **FirewallMode**, önleme ve algılama hello değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="229b5-143">For **FirewallMode**, hello available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="229b5-144">Adım önceki hello tanımlanan hello ayarları ile Merhaba uygulama ağ geçidini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="229b5-144">Update hello Application Gateway with hello settings defined in hello preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="229b5-145">Bu komut hello uygulama ağ geçidi web uygulaması güvenlik duvarı ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="229b5-145">This command updates hello Application Gateway with web application firewall.</span></span> <span data-ttu-id="229b5-146">Ziyaret [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md) toounderstand tooview uygulama ağ geçidiniz için nasıl günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="229b5-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your Application Gateway.</span></span> <span data-ttu-id="229b5-147">Güvenlik yapısı toohello WAF, günlükleri gerek toobe toounderstand hello güvenlik yaklaşımı, web uygulamalarınızı, düzenli olarak gözden.</span><span class="sxs-lookup"><span data-stu-id="229b5-147">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="229b5-148">Web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="229b5-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="229b5-149">Merhaba aşağıdaki adımları hello tüm web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturmak için başlangıç tooend işleminden değerli.</span><span class="sxs-lookup"><span data-stu-id="229b5-149">hello following steps take you through hello entire process from beginning tooend for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="229b5-150">Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="229b5-150">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="229b5-151">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="229b5-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="229b5-152">İçinde tooAzure çalıştırarak oturum `Login-AzureRmAccount`, kimlik bilgilerinizle istendiğinde tooauthenticate olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="229b5-152">Log in tooAzure by running `Login-AzureRmAccount`, you are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="229b5-153">Çalıştırarak hello hesabının Hello abonelikleri kontrol edin`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="229b5-153">Check hello subscriptions for hello account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="229b5-154">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="229b5-154">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="229b5-155">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="229b5-155">Create a resource group</span></span>

<span data-ttu-id="229b5-156">Merhaba uygulama ağ geçidi için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="229b5-156">Create a resource group for hello Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="229b5-157">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="229b5-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="229b5-158">Bu konum, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="229b5-158">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="229b5-159">Bir uygulama ağ geçidi toocreate kullanan tüm komutları ile aynı kaynak grubunda hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="229b5-159">Make sure that all commands toocreate an Application Gateway uses hello same resource group.</span></span>

<span data-ttu-id="229b5-160">Örnek önceki hello "Appgw-RG" ve konum "Batı ABD." adlı bir kaynak grubu oluşturduk</span><span class="sxs-lookup"><span data-stu-id="229b5-160">In hello preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="229b5-161">Uygulama ağ geçidiniz için özel bir araştırma tooconfigure gerekirse bkz [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="229b5-161">If you need tooconfigure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="229b5-162">Daha fazla bilgi için [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) konusunu inceleyin.</span><span class="sxs-lookup"><span data-stu-id="229b5-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="229b5-163">Sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="229b5-163">Configure virtual network</span></span>

<span data-ttu-id="229b5-164">Uygulama ağ geçidi alt ağı için kendi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="229b5-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="229b5-165">Bu adımda, bir sanal ağ adres alanı 10.0.0.0/16 ve iki alt ağ, hello uygulama ağ geçidi için bir tane ve arka uç havuzu üyeleri için bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="229b5-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for hello Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="229b5-166">Genel IP adresi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="229b5-166">Configure public IP address</span></span>

<span data-ttu-id="229b5-167">Sipariş toohandle dış isteklerinde, uygulama ağ geçidi genel bir IP adresi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="229b5-167">In order toohandle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="229b5-168">Bu genel IP adresi değil olmalıdır bir `DomainNameLabel` hello uygulama ağ geçidi tarafından kullanılan toobe tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="229b5-168">This public IP address must not have a `DomainNameLabel` defined toobe used by hello Application Gateway.</span></span>

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a><span data-ttu-id="229b5-169">Merhaba uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="229b5-169">Configure hello Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="229b5-170">Merhaba temel web uygulaması güvenlik duvarı yapılandırması ile oluşturulmuş uygulama ağ geçitleri için koruma CRS 3.0 ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="229b5-170">Application Gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="229b5-171">Uygulama ağ geçidi DNS adını Al</span><span class="sxs-lookup"><span data-stu-id="229b5-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="229b5-172">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="229b5-172">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="229b5-173">Genel IP kullanırken, uygulama ağ geçidi kolay olmayan dinamik olarak atanmış bir DNS adı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="229b5-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="229b5-174">Merhaba uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello ortak uç noktasını hello uygulama ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="229b5-174">tooensure end users can hit hello Application Gateway, a CNAME record can be used toopoint toohello public endpoint of hello Application Gateway.</span></span> <span data-ttu-id="229b5-175">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="229b5-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="229b5-176">tooconfigure bir diğer ad ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress bağlı öğesi toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adını alır.</span><span class="sxs-lookup"><span data-stu-id="229b5-176">tooconfigure an alias, retrieve details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello Application Gateway.</span></span> <span data-ttu-id="229b5-177">Merhaba uygulama ağ geçidi'nin DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="229b5-177">hello Application Gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="229b5-178">Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="229b5-178">hello use of A-records is not recommended since hello VIP may change on restart of Application Gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="229b5-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="229b5-179">Next steps</span></span>

<span data-ttu-id="229b5-180">Bilgi nasıl tooconfigure tanılama günlük kaydını, algılanan veya web uygulaması güvenlik duvarı ile ziyaret ederek engelledi toolog hello olayları [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="229b5-180">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
