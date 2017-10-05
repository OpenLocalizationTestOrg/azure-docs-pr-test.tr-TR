---
title: "Web uygulaması güvenlik duvarı - Azure uygulama ağ geçidi yapılandırma | Microsoft Docs"
description: "Bu makalede bir mevcut veya yeni uygulama ağ geçidi üzerinde web uygulaması Güvenlik Duvarı'nı kullanmaya başlamak hakkında yönergeler açıklanmaktadır."
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
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="82c33-103">Web uygulaması güvenlik duvarı bir yeni veya var olan uygulama ağ geçidi üzerinde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82c33-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="82c33-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="82c33-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="82c33-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82c33-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="82c33-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="82c33-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="82c33-107">Bir web uygulaması oluşturmayı öğrenin Güvenlik Duvarı etkin uygulama ağ geçidi veya var olan bir uygulama ağ geçidi için web uygulaması güvenlik duvarı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="82c33-107">Learn how to create a web application firewall enabled Application Gateway or add web application firewall to an existing Application Gateway.</span></span>

<span data-ttu-id="82c33-108">Azure uygulama ağ geçidi, web uygulaması Güvenlik Duvarı (WAF), SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini web uygulamaları korur.</span><span class="sxs-lookup"><span data-stu-id="82c33-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="82c33-109">Azure Application Gateway, bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="82c33-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="82c33-110">Bulutta veya şirket içinde olmalarından bağımsız olarak, farklı sunucular arasında yük devretme ile HTTP istekleri için performans amaçlı yönlendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="82c33-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="82c33-111">Uygulama ağ geçidi HTTP dahil olmak üzere pek çok uygulama teslim denetleyici (ADC) özelliklerini Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının, çoklu site desteği ve diğer birçok sağlar.</span><span class="sxs-lookup"><span data-stu-id="82c33-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="82c33-112">Desteklenen özelliklerin tam listesi için ziyaret edin: [genel bakış, uygulama ağ geçidi](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82c33-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="82c33-113">Aşağıdaki makale gösterir nasıl [var olan bir uygulama ağ geçidi için web uygulaması güvenlik duvarı ekleme](#add-web-application-firewall-to-an-existing-application-gateway) ve [web uygulaması Güvenlik Duvarı'nı kullanan uygulama ağ geçidi oluşturma](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="82c33-113">The following article shows how to [add web application firewall to an existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![Senaryo görüntüsü][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="82c33-115">WAF yapılandırma farklılıkları</span><span class="sxs-lookup"><span data-stu-id="82c33-115">WAF configuration differences</span></span>

<span data-ttu-id="82c33-116">Okuma [PowerShell ile bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-arm.md), bir uygulama ağ geçidi oluştururken yapılandırmak için SKU ayarları anlayın.</span><span class="sxs-lookup"><span data-stu-id="82c33-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an Application Gateway.</span></span> <span data-ttu-id="82c33-117">WAF SKU üzerinde bir uygulama ağ geçidini yapılandırırken tanımlamak için ek ayarlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="82c33-117">WAF provides additional settings to define when configuring the SKU on an Application Gateway.</span></span> <span data-ttu-id="82c33-118">Uygulama ağ geçidinde kendisini oluşturan ek değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="82c33-118">There are no additional changes that you make on the Application Gateway itself.</span></span>

| <span data-ttu-id="82c33-119">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="82c33-119">**Setting**</span></span> | <span data-ttu-id="82c33-120">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="82c33-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="82c33-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="82c33-121">**SKU**</span></span> |<span data-ttu-id="82c33-122">WAF destekler olmadan normal bir uygulama ağ geçidi **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**boyutları.</span><span class="sxs-lookup"><span data-stu-id="82c33-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="82c33-123">WAF başlanmasıyla, iki ek SKU vardır **WAF\_orta** ve **WAF\_büyük**.</span><span class="sxs-lookup"><span data-stu-id="82c33-123">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="82c33-124">WAF küçük uygulama ağ geçitleri üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="82c33-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="82c33-125">**Katmanı**</span><span class="sxs-lookup"><span data-stu-id="82c33-125">**Tier**</span></span> | <span data-ttu-id="82c33-126">Kullanılabilir değerler **standart** veya **WAF**.</span><span class="sxs-lookup"><span data-stu-id="82c33-126">The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="82c33-127">Web uygulaması güvenlik duvarı, kullanırken **WAF** seçilmelidir.</span><span class="sxs-lookup"><span data-stu-id="82c33-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="82c33-128">**Modu**</span><span class="sxs-lookup"><span data-stu-id="82c33-128">**Mode**</span></span> | <span data-ttu-id="82c33-129">Bu ayar WAF modudur.</span><span class="sxs-lookup"><span data-stu-id="82c33-129">This setting is the mode of WAF.</span></span> <span data-ttu-id="82c33-130">izin verilen değerler **algılama** ve **önleme**.</span><span class="sxs-lookup"><span data-stu-id="82c33-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="82c33-131">WAF algılama modunda ayarlandığında, tüm tehditler bir günlük dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="82c33-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="82c33-132">Önleme modda olayları yine kaydedilir ancak saldırgan 403 yetkisiz yanıt uygulama ağ geçidi'nden alır.</span><span class="sxs-lookup"><span data-stu-id="82c33-132">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the Application Gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="82c33-133">Web uygulaması güvenlik duvarı için var olan bir uygulama ağ geçidi Ekle</span><span class="sxs-lookup"><span data-stu-id="82c33-133">Add web application firewall to an existing Application Gateway</span></span>

<span data-ttu-id="82c33-134">Azure PowerShell’in en yeni sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="82c33-134">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="82c33-135">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="82c33-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="82c33-136">Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="82c33-136">Log in to your Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="82c33-137">Bu senaryo için kullanılacak aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="82c33-137">Select the subscription to use for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="82c33-138">Web uygulaması Güvenlik Duvarı'nda eklemekte olduğunuz ağ geçidi alın.</span><span class="sxs-lookup"><span data-stu-id="82c33-138">Retrieve the gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="82c33-139">Web uygulaması güvenlik duvarı sku yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="82c33-139">Configure the web application firewall sku.</span></span> <span data-ttu-id="82c33-140">Kullanılabilir boyutları: **WAF\_büyük** ve **WAF\_orta**.</span><span class="sxs-lookup"><span data-stu-id="82c33-140">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="82c33-141">Web uygulaması güvenlik duvarı kullanıldığında katmanı olmalıdır **WAF**, kapasite sku ayarlarken onaylanması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="82c33-141">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="82c33-142">Aşağıdaki örnekte tanımlandığı gibi WAF ayarları yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="82c33-142">Configure the WAF settings as defined in the following example:</span></span>

   <span data-ttu-id="82c33-143">İçin **FirewallMode**, önleme ve algılama değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="82c33-143">For **FirewallMode**, the available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="82c33-144">Uygulama ağ geçidi önceki adımda tanımlanan ayarlarıyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="82c33-144">Update the Application Gateway with the settings defined in the preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="82c33-145">Bu komut, uygulama ağ geçidi web uygulaması güvenlik duvarı ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="82c33-145">This command updates the Application Gateway with web application firewall.</span></span> <span data-ttu-id="82c33-146">Ziyaret [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md) uygulama ağ geçidiniz için günlükleri görüntülemek nasıl anlamak için.</span><span class="sxs-lookup"><span data-stu-id="82c33-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your Application Gateway.</span></span> <span data-ttu-id="82c33-147">WAF güvenlik yapısı nedeniyle, günlükleri, web uygulamalarınızı güvenlik yaklaşımı anlamak için düzenli olarak gözden geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="82c33-147">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="82c33-148">Web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="82c33-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="82c33-149">Aşağıdaki adımları web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturmak için bitiş başından tüm süreci izleyin.</span><span class="sxs-lookup"><span data-stu-id="82c33-149">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="82c33-150">Azure PowerShell’in en yeni sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="82c33-150">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="82c33-151">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="82c33-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="82c33-152">Azure'a çalıştırarak oturum açma `Login-AzureRmAccount`, kimlik bilgilerinizle kimliğinizi isteyip istemediğiniz sorulur.</span><span class="sxs-lookup"><span data-stu-id="82c33-152">Log in to Azure by running `Login-AzureRmAccount`, you are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="82c33-153">Hesap için abonelikler denetleyin`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="82c33-153">Check the subscriptions for the account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="82c33-154">Hangi Azure aboneliğinizin kullanılacağını seçin.</span><span class="sxs-lookup"><span data-stu-id="82c33-154">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="82c33-155">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="82c33-155">Create a resource group</span></span>

<span data-ttu-id="82c33-156">Uygulama ağ geçidi için bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82c33-156">Create a resource group for the Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="82c33-157">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="82c33-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="82c33-158">Bu konum, kaynak grubundaki kaynaklar için varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="82c33-158">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="82c33-159">Bir uygulama ağ geçidi oluşturmak için verilecek komutların aynı kaynak grubunu kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="82c33-159">Make sure that all commands to create an Application Gateway uses the same resource group.</span></span>

<span data-ttu-id="82c33-160">Önceki örnekte, "appgw-RG adlı" "Batı ABD." konumlu bir kaynak grubu oluşturduk</span><span class="sxs-lookup"><span data-stu-id="82c33-160">In the preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="82c33-161">Uygulama ağ geçidiniz için özel bir araştırma yapılandırmanız gerekiyorsa, bkz: [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="82c33-161">If you need to configure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="82c33-162">Daha fazla bilgi için [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) konusunu inceleyin.</span><span class="sxs-lookup"><span data-stu-id="82c33-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="82c33-163">Sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82c33-163">Configure virtual network</span></span>

<span data-ttu-id="82c33-164">Uygulama ağ geçidi alt ağı için kendi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="82c33-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="82c33-165">Bu adımda, bir sanal ağ adres alanı 10.0.0.0/16 ve iki alt ağ, uygulama ağ geçidi için bir tane ve arka uç havuzu üyeleri için bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82c33-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for the Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="82c33-166">Genel IP adresi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="82c33-166">Configure public IP address</span></span>

<span data-ttu-id="82c33-167">Dış isteklerini işlemek için uygulama ağ geçidi genel bir IP adresi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="82c33-167">In order to handle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="82c33-168">Bu genel IP adresi değil olmalıdır bir `DomainNameLabel` uygulama ağ geçidi tarafından kullanılması için tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="82c33-168">This public IP address must not have a `DomainNameLabel` defined to be used by the Application Gateway.</span></span>

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a><span data-ttu-id="82c33-169">Uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="82c33-169">Configure the Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="82c33-170">Temel web uygulaması güvenlik duvarı yapılandırması ile oluşturulmuş uygulama ağ geçitleri için koruma CRS 3.0 ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="82c33-170">Application Gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="82c33-171">Uygulama ağ geçidi DNS adını Al</span><span class="sxs-lookup"><span data-stu-id="82c33-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="82c33-172">Ağ geçidi oluşturulduktan sonraki adım, iletişim için ön uç yapılandırması yapmaktır.</span><span class="sxs-lookup"><span data-stu-id="82c33-172">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="82c33-173">Genel IP kullanırken, uygulama ağ geçidi kolay olmayan dinamik olarak atanmış bir DNS adı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="82c33-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="82c33-174">Son kullanıcıların uygulama ağ geçidi isabet emin olmak için bir CNAME kaydı uygulama ağ geçidi ortak uç noktasına işaret etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="82c33-174">To ensure end users can hit the Application Gateway, a CNAME record can be used to point to the public endpoint of the Application Gateway.</span></span> <span data-ttu-id="82c33-175">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="82c33-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="82c33-176">Bir diğer ad yapılandırmak için uygulama ağ geçidi ve ilişkili IP/DNS adını kullanarak uygulama ağ geçidine bağlı Publicıpaddress öğesi ayrıntılarını alamadı.</span><span class="sxs-lookup"><span data-stu-id="82c33-176">To configure an alias, retrieve details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element attached to the Application Gateway.</span></span> <span data-ttu-id="82c33-177">Uygulama ağ geçidi DNS adı, iki web uygulamaları bu DNS adına işaret eden bir CNAME kaydı oluşturmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="82c33-177">The Application Gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="82c33-178">Uygulama ağ geçidi başlatmada VIP değişebileceği A kayıtlarını kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="82c33-178">The use of A-records is not recommended since the VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="82c33-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82c33-179">Next steps</span></span>

<span data-ttu-id="82c33-180">Algılanan ya da engelledi ile web uygulaması güvenlik duvarı adresini ziyaret ederek günlük olaylarıyla tanılama günlük yapılandırmayı öğrenin [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="82c33-180">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
