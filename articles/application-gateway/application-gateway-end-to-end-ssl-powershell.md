---
title: "Azure uygulama ağ geçidi ile uçtan uca SSL'yi yapılandırma | Microsoft Docs"
description: "Bu makalede uçtan uca SSL uygulama ağ geçidi kullanarak Azure Resource Manager PowerShell ile nasıl yapılandırılacağı açıklanmaktadır"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="17166-103">Uygulama ağ geçidi PowerShell kullanarak ile uçtan uca SSL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="17166-103">Configure end to end SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="17166-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="17166-104">Overview</span></span>

<span data-ttu-id="17166-105">Uygulama ağ geçidi uçtan uca şifreleme trafiği destekler.</span><span class="sxs-lookup"><span data-stu-id="17166-105">Application Gateway supports end to end encryption of traffic.</span></span> <span data-ttu-id="17166-106">Application Gateway bu işlemi uygulama ağ geçidindeki SSL bağlantısını sonlandırarak yapar.</span><span class="sxs-lookup"><span data-stu-id="17166-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span></span> <span data-ttu-id="17166-107">Ağ geçidi bundan sonra yönlendirme kurallarını trafiğe uygular, paketi yeniden şifreler ve tanımlanan yönlendirme kurallarına göre paketi uygun arka uca iletir.</span><span class="sxs-lookup"><span data-stu-id="17166-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span></span> <span data-ttu-id="17166-108">Web sunucusundan alınan herhangi bir yanıt, son kullanıcıya dönerken aynı süreci izler.</span><span class="sxs-lookup"><span data-stu-id="17166-108">Any response from the web server goes through the same process back to the end user.</span></span>

<span data-ttu-id="17166-109">Başka bir özellik, bu uygulama ağ geçidi özel SSL seçenekleri tanımlama destekler.</span><span class="sxs-lookup"><span data-stu-id="17166-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="17166-110">Uygulama ağ geçidi, aşağıdaki iletişim kuralı sürüm devre dışı bırakma destekler; **TLSv1.0**, **TLSv1.1**, ve **TLSv1.2** iyi tanımlayıcı olarak hangi şifre paketleri ve tercih sırasına göre.</span><span class="sxs-lookup"><span data-stu-id="17166-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining the which cipher suites to use and the order of preference.</span></span>  <span data-ttu-id="17166-111">Yapılandırılabilir SSL seçenekler hakkında daha fazla bilgi için [SSL ilkesine genel bakış](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="17166-111">To learn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="17166-112">SSL 2.0 ve SSL 3.0 varsayılan olarak devre dışıdır ve etkinleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="17166-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="17166-113">Bunlar Güvensiz olarak kabul edilir ve uygulama ağ geçidi ile kullanılması mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="17166-113">They are considered unsecure and are not able to be used with Application Gateway.</span></span>

![Senaryo görüntüsü][scenario]

## <a name="scenario"></a><span data-ttu-id="17166-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="17166-115">Scenario</span></span>

<span data-ttu-id="17166-116">Bu senaryoda, PowerShell kullanarak uçtan uca SSL kullanan bir uygulama ağ geçidi oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="17166-116">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span></span>

<span data-ttu-id="17166-117">Bu senaryo aşağıdakileri yapar:</span><span class="sxs-lookup"><span data-stu-id="17166-117">This scenario will:</span></span>

* <span data-ttu-id="17166-118">Adlı bir kaynak grubu oluşturmak **appgw-rg**</span><span class="sxs-lookup"><span data-stu-id="17166-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="17166-119">Adlı bir sanal ağ oluşturma **appgwvnet** 10.0.0.0/16 bir adres alanı ile.</span><span class="sxs-lookup"><span data-stu-id="17166-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="17166-120">Adlı iki alt ağ oluşturmak **appgwsubnet** ve **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="17166-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="17166-121">Uçtan uca SSL şifrelemesini destekleyen bir küçük uygulama ağ geçidi, o sınırlar SSL protokolleri sürümlerini ve şifre paketleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="17166-121">Create a small application gateway supporting end to end SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="17166-122">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="17166-122">Before you begin</span></span>

<span data-ttu-id="17166-123">Bir uygulama ağ geçidi ile uçtan uca SSL'yi yapılandırmak için bir sertifika ağ geçidi için gereklidir ve sertifikaları arka uç sunucuları için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="17166-123">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span></span> <span data-ttu-id="17166-124">Ağ geçidi sertifikası şifrelemek ve SSL ile gönderilen trafiğin şifresini çözmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="17166-124">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span></span> <span data-ttu-id="17166-125">Ağ geçidi sertifikası kişisel bilgi değişimi (pfx) biçiminde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="17166-125">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="17166-126">Bu dosya biçimi, uygulama ağ geçidi tarafından şifreleme ve şifre çözme trafik gerçekleştirmek için gereken özel anahtar verilebilsin sağlar.</span><span class="sxs-lookup"><span data-stu-id="17166-126">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

<span data-ttu-id="17166-127">Uçtan uca SSL şifrelemesi için arka uç uygulama ağ geçidi ile güvenilir listesinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="17166-127">For end to end SSL encryption the backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="17166-128">Bu uygulama ağ geçidi arka uçlarını ortak sertifikasını karşıya yükleyerek gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="17166-128">This is done by uploading the public certificate of the backends to the application gateway.</span></span> <span data-ttu-id="17166-129">Bu uygulama ağ geçidi ile bilinen arka uç örnekleri yalnızca iletişim kurar sağlar.</span><span class="sxs-lookup"><span data-stu-id="17166-129">This ensures that the application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="17166-130">Bu ek uçtan uca iletişimin güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="17166-130">This further secures the end to end communication.</span></span>

<span data-ttu-id="17166-131">Bu işlem aşağıdaki adımlarda açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="17166-131">This process is described in the following steps:</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="17166-132">Kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="17166-132">Create the Resource Group</span></span>

<span data-ttu-id="17166-133">Bu bölümde uygulama ağ geçidi içeren bir kaynak grubu oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="17166-133">This section walks you through creating a resource group, that contains the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="17166-134">1. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-134">Step 1</span></span>

<span data-ttu-id="17166-135">Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="17166-135">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="17166-136">2. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-136">Step 2</span></span>

<span data-ttu-id="17166-137">Bu senaryo için kullanılacak aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="17166-137">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="17166-138">3. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-138">Step 3</span></span>

<span data-ttu-id="17166-139">Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="17166-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="17166-140">Uygulama ağ geçidi için bir sanal ağ ve bir alt ağ oluşturun</span><span class="sxs-lookup"><span data-stu-id="17166-140">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="17166-141">Aşağıdaki örnek, bir sanal ağ ve iki alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="17166-141">The following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="17166-142">Bir alt ağ, uygulama ağ geçidi tutmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="17166-142">One subnet is used to hold the application gateway.</span></span> <span data-ttu-id="17166-143">Diğer alt web uygulamasını barındıran arka uçlarını için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="17166-143">The other subnet is used for the backends hosting the web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="17166-144">1. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-144">Step 1</span></span>

<span data-ttu-id="17166-145">Alt ağ uygulama ağ geçidi için kendisini kullanılması için bir adres aralığı atayın.</span><span class="sxs-lookup"><span data-stu-id="17166-145">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="17166-146">Uygulama ağ geçidi için yapılandırılmış alt ağlar doğru boyutta olması.</span><span class="sxs-lookup"><span data-stu-id="17166-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="17166-147">Bir uygulama ağ geçidi için en fazla 10 örneğini yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="17166-147">An application gateway can be configured for up to 10 instances.</span></span> <span data-ttu-id="17166-148">Her örneğin bir IP adresi alt ağdan alır.</span><span class="sxs-lookup"><span data-stu-id="17166-148">Each instance takes one IP address from the subnet.</span></span> <span data-ttu-id="17166-149">Çok küçük bir alt ağın, bir uygulama ağ geçidi ölçeklendirme olumsuz yönde etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="17166-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="17166-150">2. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-150">Step 2</span></span>

<span data-ttu-id="17166-151">Arka uç adres havuzu için kullanılacak bir adres aralığı atayın.</span><span class="sxs-lookup"><span data-stu-id="17166-151">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="17166-152">3. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-152">Step 3</span></span>

<span data-ttu-id="17166-153">Önceki adımlarda tanımlanan alt ağları ile bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="17166-153">Create a virtual network with the subnets defined in the preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="17166-154">4. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-154">Step 4</span></span>

<span data-ttu-id="17166-155">Aşağıdaki adımlarda kullanılacak alt ağ kaynaklarının ve sanal ağ kaynak Al:</span><span class="sxs-lookup"><span data-stu-id="17166-155">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="17166-156">Ön uç yapılandırma için genel bir IP adresi oluşturun</span><span class="sxs-lookup"><span data-stu-id="17166-156">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="17166-157">Uygulama ağ geçidi için kullanılacak genel bir IP kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="17166-157">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="17166-158">Bu genel IP adresi kullanılır aşağıdaki adımı.</span><span class="sxs-lookup"><span data-stu-id="17166-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="17166-159">Uygulama ağ geçidi, tanımlı bir etki alanı etiketi ile oluşturulan bir ortak IP adresi kullanımını desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="17166-159">Application Gateway does not support the use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="17166-160">Yalnızca bir ortak IP adresi dinamik olarak oluşturulan etki alanı etiketi ile desteklenir.</span><span class="sxs-lookup"><span data-stu-id="17166-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="17166-161">Uygulama ağ geçidi için bir kolay dns adı gerekiyorsa, bir CNAME kaydı bir diğer ad olarak kullanmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="17166-161">If you require a friendly dns name for the application gateway, it is recommended to use a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="17166-162">Uygulama ağ geçidi yapılandırma nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="17166-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="17166-163">Tüm yapılandırma öğeleri, uygulama ağ geçidi oluşturmadan önce ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="17166-163">All configuration items are set before creating the application gateway.</span></span> <span data-ttu-id="17166-164">Aşağıdaki adımlar uygulama ağ geçidi kaynağı için gerekli yapılandırma öğelerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="17166-164">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="17166-165">1. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-165">Step 1</span></span>

<span data-ttu-id="17166-166">Uygulama ağ geçidi IP yapılandırması oluşturun, bu ayarı, uygulama ağ geçidini kullanır hangi alt yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="17166-166">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span></span> <span data-ttu-id="17166-167">Uygulama ağ geçidi başladığında, yapılandırılan alt ağdan bir IP adresi seçer ve arka uç IP havuzundaki IP adresleri için ağ trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="17166-167">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="17166-168">Her örneğin bir IP adresi aldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="17166-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="17166-169">2. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-169">Step 2</span></span>

<span data-ttu-id="17166-170">Bir ön uç IP yapılandırmasını oluşturur, bu ayar, uygulama ağ geçidi ön ucu bir özel veya genel IP adresi eşler.</span><span class="sxs-lookup"><span data-stu-id="17166-170">Create a front-end IP configuration, this setting maps a private or public ip address to the front end of the application gateway.</span></span> <span data-ttu-id="17166-171">Aşağıdaki adım önceki adımda genel IP adresi ön uç IP yapılandırmasını ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="17166-171">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="17166-172">3. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-172">Step 3</span></span>

<span data-ttu-id="17166-173">Arka uç IP adresi havuzu ile arka uç web sunucularının IP adreslerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="17166-173">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="17166-174">Bu IP adresleri ön uç IP uç noktasından gelen ağ trafiğinin yönlendirildiği IP adresleridir.</span><span class="sxs-lookup"><span data-stu-id="17166-174">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="17166-175">Kendi uygulama IP adresi uç noktalarını eklemek için aşağıdaki IP adreslerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="17166-175">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="17166-176">Bir tam etki alanı adı (FQDN) aynı zamanda arka uç sunucuları için bir IP adresi yerine geçerli bir değer - BackendFqdns anahtar kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="17166-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="17166-177">4. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-177">Step 4</span></span>

<span data-ttu-id="17166-178">Genel IP uç noktası için ön uç IP bağlantı noktası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="17166-178">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="17166-179">Bu bağlantı noktası, son kullanıcılara bağlanan bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="17166-179">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="17166-180">5. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-180">Step 5</span></span>

<span data-ttu-id="17166-181">Uygulama ağ geçidi için sertifika yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="17166-181">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="17166-182">Bu sertifika, uygulama ağ geçidi trafiğinde yeniden şifrelemek ve şifresini çözmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="17166-182">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="17166-183">Bu örnek, SSL bağlantısı için kullanılan sertifikayı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="17166-183">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="17166-184">Sertifikanın .pfx formatında olması gerekir ve parola 4 ile 12 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="17166-184">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="17166-185">6. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-185">Step 6</span></span>

<span data-ttu-id="17166-186">HTTP dinleyicisi için uygulama ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="17166-186">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="17166-187">Ön uç IP yapılandırması, bağlantı noktası ve kullanmak için SSL sertifikası atayın.</span><span class="sxs-lookup"><span data-stu-id="17166-187">Assign the front-end ip configuration, port, and SSL certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="17166-188">7. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-188">Step 7</span></span>

<span data-ttu-id="17166-189">SSL etkin arka uç havuzu kaynaklardaki kullanılan sertifikayı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="17166-189">Upload the certificate to be used on the SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="17166-190">Ortak anahtarı ile varsayılan araştırmasını alır **varsayılan** SSL bağlaması arka uç bilgisayarın IP adresi ve aldığı ortak anahtar değeri, ortak anahtar değeri sağlamak burada karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="17166-190">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span></span> <span data-ttu-id="17166-191">Alınan ortak anahtar hangi trafik akışları hedeflenen siteye mutlaka olmayabilir **varsa** ana bilgisayar üstbilgilerinin ve SNI uç kullanma.</span><span class="sxs-lookup"><span data-stu-id="17166-191">The retrieved public key may not necessarily be the intended site to which traffic flows **if** you are using host headers and SNI on the back-end.</span></span> <span data-ttu-id="17166-192">Emin değilseniz, hangi sertifika için kullanılan onaylamak için arka uç https://127.0.0.1/ ziyaret **varsayılan** SSL bağlaması.</span><span class="sxs-lookup"><span data-stu-id="17166-192">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span></span> <span data-ttu-id="17166-193">Bu bölümde bu istek ortak anahtarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="17166-193">Use the public key from that request in this section.</span></span> <span data-ttu-id="17166-194">Ana bilgisayar üstbilgilerinin ve SNI HTTPS bağlantılarına kullanıyorsanız ve bir yanıt ve sertifika el ile tarayıcı isteğinden arka ucunda https://127.0.0.1/ için aldığınız olmayan bir varsayılan SSL bağlaması arka ucunda ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="17166-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span></span> <span data-ttu-id="17166-195">Bunu yaparsanız, araştırmalar başarısız ve arka uç izin verilenler listesinde değil.</span><span class="sxs-lookup"><span data-stu-id="17166-195">If you do not do so, probes fail and the back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="17166-196">Bu adımda sağlanan sertifikanın arka uç mevcut pfx sertifika ortak anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="17166-196">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span></span> <span data-ttu-id="17166-197">Arka uç sunucuda yüklü sertifikayı (kök sertifikanın değil) verin. CER biçimlendirin ve bu adımda kullanın.</span><span class="sxs-lookup"><span data-stu-id="17166-197">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="17166-198">Bu adım whitelists arka uç uygulama ağ geçidi ile.</span><span class="sxs-lookup"><span data-stu-id="17166-198">This step whitelists the backend with the application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="17166-199">8. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-199">Step 8</span></span>

<span data-ttu-id="17166-200">Uygulama ağ geçidi arka uç http ayarları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="17166-200">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="17166-201">Http ayarları için önceki adımda yüklediğiniz sertifikayı atayın.</span><span class="sxs-lookup"><span data-stu-id="17166-201">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="17166-202">9. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-202">Step 9</span></span>

<span data-ttu-id="17166-203">Yük Dengeleyici davranışını yapılandıran Yük Dengeleyiciyi yönlendirme kuralını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="17166-203">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="17166-204">Bu örnekte, bir temel hepsini bir kural oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="17166-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="17166-205">10. adım</span><span class="sxs-lookup"><span data-stu-id="17166-205">Step 10</span></span>

<span data-ttu-id="17166-206">Uygulama ağ geçidinin örnek boyutunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="17166-206">Configure the instance size of the application gateway.</span></span>  <span data-ttu-id="17166-207">Kullanılabilir boyutları: **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**.</span><span class="sxs-lookup"><span data-stu-id="17166-207">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="17166-208">Kapasite için 1 ile 10 değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="17166-208">For capacity, the available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="17166-209">Test amacıyla örnek sayısını 1 seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="17166-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="17166-210">Tüm örnek sayısı iki örneği altında SLA kapsamında değildir ve bu nedenle önerilmez bilmeniz önemlidir.</span><span class="sxs-lookup"><span data-stu-id="17166-210">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="17166-211">Küçük ağ geçitleri geliştirme test ve üretim amaçları için kullanılacak olan.</span><span class="sxs-lookup"><span data-stu-id="17166-211">Small gateways are to be used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="17166-212">11. adım</span><span class="sxs-lookup"><span data-stu-id="17166-212">Step 11</span></span>

<span data-ttu-id="17166-213">Uygulama ağ geçidinde kullanılacak SSL ilkesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="17166-213">Configure the SSL policy to be used on the Application Gateway.</span></span> <span data-ttu-id="17166-214">Uygulama ağ geçidi SSL protokol sürümleri için en düşük sürüm ayarlama özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="17166-214">Application Gateway supports the ability to set a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="17166-215">Aşağıdaki değerleri tanımlanabilir protokol sürümleri listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="17166-215">The following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="17166-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="17166-216">**TLSv1_0**</span></span>
* <span data-ttu-id="17166-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="17166-217">**TLSv1_1**</span></span>
* <span data-ttu-id="17166-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="17166-218">**TLSv1_2**</span></span>

<span data-ttu-id="17166-219">En düşük protokol sürümü ayarlar **TLSv1_2** ve sağlar **TLS\_ECDHE\_ECDSA\_ile\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_ile\_AES\_256\_GCM\_SHA384**ve  **TLS\_RSA\_ile\_AES\_128\_GCM\_SHA256** yalnızca.</span><span class="sxs-lookup"><span data-stu-id="17166-219">Sets the minimum protocol version to **TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="17166-220">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="17166-220">Create the Application Gateway</span></span>

<span data-ttu-id="17166-221">Yukarıdaki adımları kullanarak uygulama ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="17166-221">Using all the preceding steps, create the Application Gateway.</span></span> <span data-ttu-id="17166-222">Ağ geçidi oluşturma uzun süren bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="17166-222">The creation of the gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="17166-223">Mevcut bir uygulama ağ geçidi SSL protokolü sürümlerinde sınırla</span><span class="sxs-lookup"><span data-stu-id="17166-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="17166-224">Önceki adımlar, uçtan uca SSL ile uygulama oluşturma ve belirli SSL protokol sürümleri devre dışı bırakma uygulayın.</span><span class="sxs-lookup"><span data-stu-id="17166-224">The preceding steps take you through creating an application with end to end SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="17166-225">Aşağıdaki örnekte belirli SSL ilkeleri var olan bir uygulama ağ geçidi üzerinde devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="17166-225">The following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="17166-226">1. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-226">Step 1</span></span>

<span data-ttu-id="17166-227">Uygulama ağ geçidi güncelleştirilecek alın.</span><span class="sxs-lookup"><span data-stu-id="17166-227">Retrieve the application gateway to update.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="17166-228">2. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-228">Step 2</span></span>

<span data-ttu-id="17166-229">SSL ilke tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="17166-229">Define an SSL policy.</span></span> <span data-ttu-id="17166-230">Aşağıdaki örnekte, TLSv1.0 ve TLSv1.1 devre dışı bırakıldı ve şifre paketleri olduğundan **TLS\_ECDHE\_ECDSA\_ile\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_ile\_AES\_256\_GCM\_SHA384**, ve  **TLS\_RSA\_ile\_AES\_128\_GCM\_SHA256** olan izin verilen yalnızca bu çalışanların.</span><span class="sxs-lookup"><span data-stu-id="17166-230">In the following example, TLSv1.0 and TLSv1.1 are disabled and the cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are the only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="17166-231">3. Adım</span><span class="sxs-lookup"><span data-stu-id="17166-231">Step 3</span></span>

<span data-ttu-id="17166-232">Son olarak, ağ geçidini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="17166-232">Finally, update the gateway.</span></span> <span data-ttu-id="17166-233">Bu son adım uzun çalışan bir görev olduğunu dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="17166-233">It is important to note that this last step is a long running task.</span></span> <span data-ttu-id="17166-234">Tamamlandığında, uçtan uca SSL uygulama ağ geçidinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="17166-234">When it is done, end to end SSL is configured on the application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="17166-235">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="17166-235">Get application gateway DNS name</span></span>

<span data-ttu-id="17166-236">Ağ geçidi oluşturulduktan sonraki adım, iletişim için ön uç yapılandırması yapmaktır.</span><span class="sxs-lookup"><span data-stu-id="17166-236">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="17166-237">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="17166-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="17166-238">Son kullanıcıların uygulama ağ geçidine ulaşmasını sağlamak için uygulama ağ geçidinin genel uç noktasını işaret edecek bir CNAME kaydı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="17166-238">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="17166-239">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="17166-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="17166-240">Bunu yapmak için uygulama ağ geçidinin ayrıntılarını ve onunla ilişkilendirilmiş olan IP/DNS adını uygulama ağ geçidine eklenmiş PublicIPAddress öğesini kullanarak alın.</span><span class="sxs-lookup"><span data-stu-id="17166-240">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="17166-241">Uygulama ağ geçidinin DNS adı, iki web uygulamasını bu DNS adına götüren bir CNAME kaydı oluşturmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="17166-241">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="17166-242">Uygulama ağ geçidi yeniden başlatıldığında VIP değişebileceğinden A kaydı kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="17166-242">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="17166-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="17166-243">Next steps</span></span>

<span data-ttu-id="17166-244">Uygulama ağ geçidi üzerinden Web uygulaması güvenlik duvarı ile web uygulamalarınızın güvenliğini ziyaret ederek artırma hakkında bilgi edinin [Web uygulaması güvenlik duvarı genel bakış](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="17166-244">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
