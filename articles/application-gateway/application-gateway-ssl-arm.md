---
title: "Azure uygulama ağ geçidi - PowerShell SSL boşaltma - yapılandırma | Microsoft Docs"
description: "Bu sayfada Azure Resource Manager kullanarak SSL yük boşaltımıyla uygulama ağ geçidi oluşturmak için yönergeler bulunmaktadır."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="80d3b-103">Azure Resource Manager kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="80d3b-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="80d3b-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="80d3b-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="80d3b-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="80d3b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="80d3b-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="80d3b-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="80d3b-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="80d3b-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="80d3b-108">Azure Application Gateway, web grubunda maliyetli SSL şifre çözme görevlerinin oluşmasından kaçınmak için Güvenli Yuva Katmanı (SSL) oturumunu sonlandırmak amacıyla yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="80d3b-109">SSL yük boşaltımı ön uç sunucusunun kurulumunu ve web uygulamasının yönetimini de basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="80d3b-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="80d3b-110">Before you begin</span></span>

1. <span data-ttu-id="80d3b-111">Web Platformu Yükleyicisi’ni kullanarak Azure PowerShell cmdlet’lerin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="80d3b-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="80d3b-112">**İndirmeler sayfası**’ndaki [Windows PowerShell](https://azure.microsoft.com/downloads/) bölümünden en son sürümü indirip yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80d3b-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="80d3b-113">Uygulama ağ geçidi için bir sanal ağ ve bir alt ağ oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="80d3b-113">You create a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="80d3b-114">Hiçbir sanal makinenin veya bulut dağıtımlarının alt ağı kullanmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="80d3b-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="80d3b-115">Application Gateway tek başına bir sanal ağ alt ağında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="80d3b-116">Uygulama ağ geçidi kullanırken yapılandırdığınız sunucular mevcut olmalıdır veya uç noktaları sanal ağda veya atanan genel bir IP/VIP’de oluşturulmuş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-116">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="80d3b-117">Bir uygulama ağ geçidi oluşturmak için ne gereklidir?</span><span class="sxs-lookup"><span data-stu-id="80d3b-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="80d3b-118">**Arka uç sunucusu havuzu:** Arka uç sunucularının IP adreslerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="80d3b-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="80d3b-119">Listede bulunan IP adresleri sanal ağ alt ağına veya genel IP/VIP’ye ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-119">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="80d3b-120">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="80d3b-121">Bu ayarlar bir havuza bağlıdır ve havuzdaki tüm sunuculara uygulanır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="80d3b-122">**Ön uç bağlantı noktası:** Bu bağlantı noktası uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="80d3b-123">Bu bağlantı noktasında trafik olursa arka uç sunuculardan birine yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="80d3b-124">**Dinleyici:** Dinleyicide bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu ayarlar büyük/küçük harfe duyarlıdır) ve SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa) vardır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="80d3b-125">**Kural:** Kural, dinleyiciyi ve arka uç sunucusu havuzunu bağlar ve belli bir dinleyicide trafik olduğunda trafiğin hangi arka uç sunucu havuzuna yönlendirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="80d3b-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="80d3b-126">Şu anda yalnızca *temel* kural desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="80d3b-127">*Temel* kural hepsini bir kez deneme yöntemiyle yük dağıtımıdır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-127">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="80d3b-128">**Ek yapılandırma notları**</span><span class="sxs-lookup"><span data-stu-id="80d3b-128">**Additional configuration notes**</span></span>

<span data-ttu-id="80d3b-129">SSL sertifikaları yapılandırmada **HttpListener**’daki protokol *Https* (küçük/büyük harf duyarlı) ile değiştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-129">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="80d3b-130">**SslCertificate** öğesi SSL sertifikası için yapılandırılmış değişken değerle **HttpListener**’a eklenir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-130">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="80d3b-131">Ön uç bağlantı noktası 443’e yükseltilmelidir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-131">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="80d3b-132">**Tanımlama bilgisi temelli benzeşimi etkinleştirme:** Bir uygulama ağ geçidi, bir istemci oturumundan gelen isteğin web grubunda hep aynı VM’e yönlendirildiğinden emin olmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-132">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="80d3b-133">Bu senaryo, ağ geçidinin trafiği uygun bir şekilde yönlendirmesini sağlayacak oturum tanımlama bilgisinin eklenmesiyle gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-133">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="80d3b-134">Tanımlama bilgisi temelli benzeşimi etkinleştirmek için, **CookieBasedAffinity**’yi *BackendHttpSetting* öğesindeki **Enabled**’a ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="80d3b-134">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="80d3b-135">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="80d3b-135">Create an application gateway</span></span>

<span data-ttu-id="80d3b-136">Azure Klasik dağıtım modeli ve Azure Resource Manager arasındaki fark, uygulama ağ geçidi oluştururken takip ettiğiniz sıra ve yapılandırılması gereken öğelerdir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-136">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="80d3b-137">Resource Manager'da uygulama ağ geçidini oluşturan tüm öğeler ayrı ayrı yapılandırılır ve ardından bir uygulama ağ geçidi kaynağı oluşturmak üzere bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-137">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span></span>

<span data-ttu-id="80d3b-138">Bir uygulama ağ geçidi oluşturmak için takip etmeniz gereken adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="80d3b-138">Here are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="80d3b-139">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="80d3b-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="80d3b-140">Uygulama ağ geçidi için sanal ağ, alt ağ ve genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="80d3b-140">Create virtual network, subnet, and public IP for the application gateway</span></span>
3. <span data-ttu-id="80d3b-141">Uygulama ağ geçidi yapılandırma nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="80d3b-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="80d3b-142">Bir uygulama ağ geçidi kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80d3b-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="80d3b-143">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="80d3b-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="80d3b-144">Azure Resource Manager cmdlet’lerini kullanmak için PowerShell modunu açtığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="80d3b-144">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="80d3b-145">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="80d3b-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="80d3b-146">1. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="80d3b-147">2. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-147">Step 2</span></span>

<span data-ttu-id="80d3b-148">Hesapla ilişkili abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="80d3b-148">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="80d3b-149">Kimlik bilgilerinizle kimliğinizi doğrulamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-149">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="80d3b-150">3. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-150">Step 3</span></span>

<span data-ttu-id="80d3b-151">Hangi Azure aboneliğinizin kullanılacağını seçin.</span><span class="sxs-lookup"><span data-stu-id="80d3b-151">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="80d3b-152">4. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-152">Step 4</span></span>

<span data-ttu-id="80d3b-153">Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="80d3b-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="80d3b-154">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="80d3b-155">Bu ayar, kaynak grubundaki kaynaklar için varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-155">This setting is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="80d3b-156">Uygulama ağ geçidi oluşturmak için verilen komutların aynı kaynak grubunu kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="80d3b-156">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="80d3b-157">Yukarıdaki örnekte, **appgw-RG** adlı, **Batı ABD** konumlu bir kaynak grubu oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="80d3b-157">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="80d3b-158">Uygulama ağ geçidi için bir sanal ağ ve bir alt ağ oluşturun</span><span class="sxs-lookup"><span data-stu-id="80d3b-158">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="80d3b-159">Aşağıdaki örnek Resource Manager kullanarak nasıl sanal ağ oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="80d3b-159">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="80d3b-160">1. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="80d3b-161">Bu örnek, 10.0.0.0/24 adres aralığını, sanal ağ oluşturmak için kullanılacak bir alt ağ değişkenine atar.</span><span class="sxs-lookup"><span data-stu-id="80d3b-161">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="80d3b-162">2. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="80d3b-163">Bu örnek adlı bir sanal ağ oluşturur **appgwvnet** kaynak grubunda **appgw-rg** 10.0.0.0/24 alt ağıyla önek 10.0.0.0/16 kullanarak Batı ABD bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="80d3b-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="80d3b-164">3. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="80d3b-165">Bu örnek, sonraki adımlar için alt ağ nesnesini bir $subnet değişkenine atar.</span><span class="sxs-lookup"><span data-stu-id="80d3b-165">This sample assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="80d3b-166">Ön uç yapılandırma için genel bir IP adresi oluşturun</span><span class="sxs-lookup"><span data-stu-id="80d3b-166">Create a public IP address for the front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="80d3b-167">Bu örnek bir genel IP kaynağı oluşturur **Publicıp01** kaynak grubunda **appgw-rg** Batı ABD bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="80d3b-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="80d3b-168">Uygulama ağ geçidi yapılandırma nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="80d3b-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="80d3b-169">1. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="80d3b-170">Bu örnek adlı uygulama ağ geçidi IP yapılandırması oluşturur **Gatewayıp01**.</span><span class="sxs-lookup"><span data-stu-id="80d3b-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="80d3b-171">Application Gateway başladığında, yapılandırılan alt ağdan bir IP adresi alır ve ağ trafiğini arka uç IP havuzundaki IP adreslerine yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-171">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="80d3b-172">Her örneğin bir IP adresi aldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="80d3b-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="80d3b-173">2. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="80d3b-174">Bu örnek adlı arka uç IP adresi havuzunu yapılandırır **pool01** IP adresleriyle **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span><span class="sxs-lookup"><span data-stu-id="80d3b-174">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="80d3b-175">Bu değerler, ön uç IP uç noktasından gelen ağ trafiğinin yönlendirildiği IP adresleridir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-175">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="80d3b-176">Önceki örnekte yazılan IP adreslerini, kendi web uygulaması uç noktalarınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="80d3b-176">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="80d3b-177">3. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="80d3b-178">Bu örnek uygulama ağ geçidi ayarı yapılandırır **poolsetting01** arka uç havuzundaki yük dengeli ağ trafiği.</span><span class="sxs-lookup"><span data-stu-id="80d3b-178">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="80d3b-179">4. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="80d3b-180">Bu örnek adlı ön uç IP bağlantı noktasını yapılandırır **frontendport01** genel IP uç noktası için.</span><span class="sxs-lookup"><span data-stu-id="80d3b-180">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="80d3b-181">5. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="80d3b-182">Bu örnek, SSL bağlantısı için kullanılan sertifikayı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-182">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="80d3b-183">Sertifikanın .pfx formatında olması gerekir ve parola 4 ile 12 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="80d3b-184">6. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="80d3b-185">Bu örnek adlı ön uç IP yapılandırmasını oluşturur **fipconfig01** ve genel IP adresi ön uç IP yapılandırmasını ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-185">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="80d3b-186">7. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="80d3b-187">Bu örnek dinleyici adı oluşturur **listener01** ve ön uç bağlantı noktasıyla ön uç IP yapılandırmasını ve sertifikasını ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-187">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="80d3b-188">8. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="80d3b-189">Bu örnek adlı Yük Dengeleyiciyi yönlendirme kuralını oluşturur **rule01** yük dengeleyici davranışını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-189">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="80d3b-190">9. Adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="80d3b-191">Bu örnek, uygulama ağ geçidinin örnek boyutunu yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-191">This sample configures the instance size of the application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="80d3b-192">*InstanceCount* için varsayılan değer 2 ile 10 arasıdır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-192">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="80d3b-193">*GatewaySize* için varsayılan değer Medium’dur.</span><span class="sxs-lookup"><span data-stu-id="80d3b-193">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="80d3b-194">Aynı zamanda Standard_Small, Standard_Medium ve Standard_Large seçenekleri de bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="80d3b-195">10. adım</span><span class="sxs-lookup"><span data-stu-id="80d3b-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="80d3b-196">Bu adım, uygulama ağ geçidinde kullanmak için SSL İlkesi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="80d3b-196">This step defines the SSL policy to use on the application gateway.</span></span> <span data-ttu-id="80d3b-197">Ziyaret [SSL yapılandırma İlkesi sürümlerini ve şifre paketleri uygulama ağ geçidi üzerinde](application-gateway-configure-ssl-policy-powershell.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="80d3b-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="80d3b-198">New-AzureApplicationGateway kullanarak bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="80d3b-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="80d3b-199">Bu örnek, önceki adımlarda geçen tüm yapılandırma öğeleri ile bir uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80d3b-199">This sample creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="80d3b-200">Örnekte uygulama ağ geçidi olarak adlandırılır **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="80d3b-200">In the example, the application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="80d3b-201">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="80d3b-201">Get application gateway DNS name</span></span>

<span data-ttu-id="80d3b-202">Ağ geçidi oluşturulduktan sonraki adım, iletişim için ön uç yapılandırması yapmaktır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-202">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="80d3b-203">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="80d3b-204">Son kullanıcıların uygulama ağ geçidine ulaşmasını sağlamak için uygulama ağ geçidinin genel uç noktasını işaret edecek bir CNAME kaydı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="80d3b-204">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="80d3b-205">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="80d3b-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="80d3b-206">Bunu yapmak için uygulama ağ geçidinin ayrıntılarını ve onunla ilişkilendirilmiş olan IP/DNS adını uygulama ağ geçidine eklenmiş PublicIPAddress öğesini kullanarak alın.</span><span class="sxs-lookup"><span data-stu-id="80d3b-206">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="80d3b-207">Uygulama ağ geçidinin DNS adı, iki web uygulamasını bu DNS adına götüren bir CNAME kaydı oluşturmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="80d3b-207">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="80d3b-208">Uygulama ağ geçidi yeniden başlatıldığında VIP değişebileceğinden A kaydı kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="80d3b-208">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="80d3b-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="80d3b-209">Next steps</span></span>

<span data-ttu-id="80d3b-210">Bir uygulama ağ geçidini bir iç yük dengeleyici (ILB) ile kullanmak için yapılandırmak istiyorsanız, bkz. [İç yük dengeleyiciyle bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="80d3b-210">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="80d3b-211">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="80d3b-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="80d3b-212">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="80d3b-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="80d3b-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="80d3b-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

