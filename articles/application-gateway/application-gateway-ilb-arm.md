---
title: "İç yük dengeleyici - PowerShell ile Azure uygulama ağ geçidi aaaUsing | Microsoft Docs"
description: "Bu sayfa toocreate, yapılandırmak, başlatmak ve Azure Resource Manager için iç yük dengeleyiciye (ILB) sahip bir Azure uygulama ağ geçidi silme yönergelerini sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="5b831-103">Azure Resource Manager kullanarak iç yük dengeleyiciye (ILB) sahip bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b831-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b831-104">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b831-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="5b831-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b831-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="5b831-106">Azure uygulama ağ geçidi, bir Internet'e yönelik VIP veya gösterilen toohello Internet, olarak da bilinen bir iç yük dengeleyiciye (ILB) uç noktası olmayan iç uç nokta ile yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5b831-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed toohello Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="5b831-107">Yapılandırma hello ağ geçidini bir ILB ile sunulan toohello Internet olmayan iç iş kolu satır uygulamaları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="5b831-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications that are not exposed toohello Internet.</span></span> <span data-ttu-id="5b831-108">Ayrıca Hizmetleri için faydalı olur ve dağıtım, oturum sürekliliği veya Güvenli Yuva Katmanı (SSL) sonlandırma gösterilen toohello Internet olmayan bir güvenlik sınırı içinde sunulmamış ancak hala hepsini gerektiren çok katmanlı bir uygulama içinde katmanları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5b831-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed toohello Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="5b831-109">Bu makalede, hello adımları tooconfigure bir uygulama ağ geçidini bir ILB ile adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5b831-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5b831-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5b831-110">Before you begin</span></span>

1. <span data-ttu-id="5b831-111">Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5b831-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="5b831-112">Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5b831-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="5b831-113">Application Gateway için bir sanal ağ ve bir alt ağ oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5b831-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="5b831-114">Hiçbir sanal makine veya Bulut dağıtımları hello alt kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5b831-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="5b831-115">Application Gateway tek başına bir sanal ağ alt ağında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5b831-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="5b831-116">toouse hello uygulama ağ geçidi yapılandırma hello sunucular mevcut olmalıdır veya hello sanal ağ veya genel IP/VIP'ye ile oluşturulan uç noktaları atadınız.</span><span class="sxs-lookup"><span data-stu-id="5b831-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="5b831-117">Gerekli toocreate bir uygulama ağ geçidi nedir?</span><span class="sxs-lookup"><span data-stu-id="5b831-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="5b831-118">**Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="5b831-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="5b831-119">Merhaba listede IP adresleri ya da toohello sanal ağ ait olması gerekir, ancak hello uygulama ağ geçidi için farklı bir alt ağ veya genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5b831-119">hello IP addresses listed should either belong toohello virtual network but in a different subnet for hello application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="5b831-120">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="5b831-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="5b831-121">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="5b831-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="5b831-122">**Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="5b831-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="5b831-123">Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="5b831-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="5b831-124">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bunlar büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="5b831-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="5b831-125">**Kural:** hello kural hello dinleyicisi ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler.</span><span class="sxs-lookup"><span data-stu-id="5b831-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="5b831-126">Şu anda yalnızca hello *temel* kural desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b831-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="5b831-127">Merhaba *temel* hepsini bir kez deneme yük dağıtımı kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="5b831-127">hello *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="5b831-128">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b831-128">Create an application gateway</span></span>

<span data-ttu-id="5b831-129">Azure Klasik ve Azure Resource Manager kullanma arasındaki fark hello hello uygulama ağ geçidi ve yapılandırılmış toobe gereksinim hello öğelerini oluşturmak hello sırasıdır.</span><span class="sxs-lookup"><span data-stu-id="5b831-129">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>
<span data-ttu-id="5b831-130">Resource Manager ile uygulama ağ geçidini oluşturan öğeler ayrı ayrı yapılandırılır ve toocreate hello uygulama ağ geçidi kaynağı bir araya getirin.</span><span class="sxs-lookup"><span data-stu-id="5b831-130">With Resource Manager, all items that make an application gateway is configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="5b831-131">Gerekli toocreate bir uygulama ağ geçidi hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5b831-131">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="5b831-132">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="5b831-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="5b831-133">Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b831-133">Create a virtual network and a subnet for hello application gateway</span></span>
3. <span data-ttu-id="5b831-134">Uygulama ağ geçidi yapılandırma nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="5b831-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="5b831-135">Bir uygulama ağ geçidi kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b831-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="5b831-136">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="5b831-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="5b831-137">PowerShell modu toouse hello Azure Resource Manager cmdlet'lerini geçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5b831-137">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="5b831-138">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="5b831-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="5b831-139">1. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="5b831-140">2. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-140">Step 2</span></span>

<span data-ttu-id="5b831-141">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="5b831-141">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="5b831-142">Kimlik bilgilerinizle istendiğinde tooauthenticate var.</span><span class="sxs-lookup"><span data-stu-id="5b831-142">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="5b831-143">3. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-143">Step 3</span></span>

<span data-ttu-id="5b831-144">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="5b831-144">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="5b831-145">4. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-145">Step 4</span></span>

<span data-ttu-id="5b831-146">Yeni bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="5b831-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="5b831-147">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5b831-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="5b831-148">Bu kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5b831-148">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="5b831-149">Bir uygulama ağ geçidini kullanan tüm komutları toocreate Merhaba, aynı olduğundan emin olun kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="5b831-149">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="5b831-150">Örnek önceki hello "Appgw-rg" ve konum "Batı ABD" konumlu bir kaynak grubu oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="5b831-150">In hello preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="5b831-151">Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b831-151">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="5b831-152">örnekte gösterildiği nasıl aşağıdaki hello toocreate Kaynak Yöneticisi'ni kullanarak bir sanal ağ:</span><span class="sxs-lookup"><span data-stu-id="5b831-152">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="5b831-153">1. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="5b831-154">Bu adım, bir sanal ağ başlangıç adresi aralığı 10.0.0.0/24 tooa alt kullanılan değişken toobe toocreate atar.</span><span class="sxs-lookup"><span data-stu-id="5b831-154">This step assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="5b831-155">2. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="5b831-156">Bu adım, "appgw-rg" kaynak grubunda 10.0.0.0/24 alt ağıyla hello önek 10.0.0.0/16 kullanarak hello Batı ABD bölgesi için "appgwvnet" adlı bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5b831-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="5b831-157">3. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="5b831-158">Bu adım hello sonraki adımlar için hello alt ağ nesnesini toovariable $subnet atar.</span><span class="sxs-lookup"><span data-stu-id="5b831-158">This step assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="5b831-159">Uygulama ağ geçidi yapılandırma nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="5b831-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="5b831-160">1. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="5b831-161">Bu adım, "Gatewayıp01" adlı uygulama ağ geçidi IP yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5b831-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="5b831-162">Application Gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki rota.</span><span class="sxs-lookup"><span data-stu-id="5b831-162">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="5b831-163">Her örneğin bir IP adresi aldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5b831-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="5b831-164">2. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

<span data-ttu-id="5b831-165">Bu adım adlı hello arka uç IP adresi havuzunu yapılandırır "pool01" IP adresleri "10.1.1.8, 10.1.1.9, 10.1.1.10".</span><span class="sxs-lookup"><span data-stu-id="5b831-165">This step configures hello back-end IP address pool named "pool01" with IP addresses "10.1.1.8, 10.1.1.9, 10.1.1.10".</span></span> <span data-ttu-id="5b831-166">Bu hello ön uç IP uç noktasından gelen ağ trafiğini hello aldığınız hello IP adresleridir.</span><span class="sxs-lookup"><span data-stu-id="5b831-166">Those are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="5b831-167">Kendi uygulama IP adresi bitiş IP adreslerini tooadd önceki hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5b831-167">You replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="5b831-168">3. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="5b831-169">Bu adım, uygulama "dengeli poolsetting01" ağ geçidi hello yük için ağ trafiğini hello arka uç havuzundaki yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5b831-169">This step configures application gateway setting "poolsetting01" for hello load balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="5b831-170">4. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="5b831-171">Bu adım hello ILB için "frontendport01" adlı hello ön uç IP bağlantı noktasını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5b831-171">This step configures hello front-end IP port named "frontendport01" for hello ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="5b831-172">5. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="5b831-173">Bu adım hello "fipconfig01" adlı ön uç IP yapılandırmasını oluşturur ve hello geçerli sanal ağ alt ağından özel IP ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="5b831-173">This step creates hello front-end IP configuration called "fipconfig01" and associates it with a private IP from hello current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="5b831-174">6. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="5b831-175">Bu adım, "listener01" adlı hello dinleyiciyi oluşturur ve hello ön uç bağlantı noktası toohello ön uç IP yapılandırmasını ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="5b831-175">This step creates hello listener called "listener01" and associates hello front-end port toohello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="5b831-176">7. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="5b831-177">Bu adım hello Yük Dengeleyiciyi yönlendirme kuralını hello yük dengeleyici davranışını yapılandıran "rule01" adlı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5b831-177">This step creates hello load balancer routing rule called "rule01" that configures hello load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="5b831-178">8. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="5b831-179">Bu adım hello uygulama ağ geçidi hello örnek boyutunu yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5b831-179">This step configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="5b831-180">Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir.</span><span class="sxs-lookup"><span data-stu-id="5b831-180">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="5b831-181">Merhaba için varsayılan değer *GatewaySize* Orta'dır.</span><span class="sxs-lookup"><span data-stu-id="5b831-181">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="5b831-182">Aynı zamanda Standard_Small, Standard_Medium ve Standard_Large seçenekleri de bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5b831-182">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="5b831-183">New-AzureApplicationGateway kullanarak bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b831-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="5b831-184">Merhaba adımları önceki tüm yapılandırma öğelerinden bir uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5b831-184">Creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="5b831-185">Bu örnekte, hello uygulama ağ geçidi "appgwtest" olarak adlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5b831-185">In this example, hello application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="5b831-186">Bu adım, önceki adımları hello tüm yapılandırma öğelerinden bir uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5b831-186">This step creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="5b831-187">Merhaba örnekte hello uygulama ağ geçidi "appgwtest" olarak adlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5b831-187">In hello example, hello application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="5b831-188">Uygulama ağ geçidini silme</span><span class="sxs-lookup"><span data-stu-id="5b831-188">Delete an application gateway</span></span>

<span data-ttu-id="5b831-189">bir uygulama ağ geçidi toodelete, aşağıdaki adımları sırayla toodo hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="5b831-189">toodelete an application gateway, you need toodo hello following steps in order:</span></span>

1. <span data-ttu-id="5b831-190">Kullanım hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="5b831-190">Use hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="5b831-191">Kullanım hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="5b831-191">Use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="5b831-192">Bu hello ağ geçidi hello kullanarak kaldırıldı doğrulayın `Get-AzureApplicationGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5b831-192">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="5b831-193">1. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-193">Step 1</span></span>

<span data-ttu-id="5b831-194">Merhaba uygulama ağ geçidi nesnesini alın ve tooa değişkeni "$getgw" ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b831-194">Get hello application gateway object and associate it tooa variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="5b831-195">2. Adım</span><span class="sxs-lookup"><span data-stu-id="5b831-195">Step 2</span></span>

<span data-ttu-id="5b831-196">Kullanım `Stop-AzureRmApplicationGateway` toostop hello uygulama ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="5b831-196">Use `Stop-AzureRmApplicationGateway` toostop hello application gateway.</span></span> <span data-ttu-id="5b831-197">Bu örnek hello gösterir `Stop-AzureRmApplicationGateway` cmdlet hello ilk satırdaki ardından tarafından hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="5b831-197">This sample shows hello `Stop-AzureRmApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="5b831-198">Merhaba uygulama ağ geçidi durdurulmuş durumda olduğunda, hello kullan `Remove-AzureRmApplicationGateway` cmdlet tooremove hello hizmet.</span><span class="sxs-lookup"><span data-stu-id="5b831-198">Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> <span data-ttu-id="5b831-199">Merhaba **-force** anahtar kullanılan toosuppress hello kaldırma onayı iletisini olabilir.</span><span class="sxs-lookup"><span data-stu-id="5b831-199">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="5b831-200">Hizmet hello tooverify kaldırıldı, hello kullanabilirsiniz `Get-AzureRmApplicationGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5b831-200">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="5b831-201">Bu adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="5b831-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="5b831-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b831-202">Next steps</span></span>

<span data-ttu-id="5b831-203">SSL boşaltma tooconfigure istiyorsanız, bkz: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="5b831-203">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="5b831-204">Bir uygulama ağ geçidi toouse bir ILB ile tooconfigure istiyorsanız, bkz: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="5b831-204">If you want tooconfigure an application gateway toouse with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="5b831-205">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="5b831-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="5b831-206">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5b831-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="5b831-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="5b831-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

