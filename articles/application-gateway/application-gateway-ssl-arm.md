---
title: "aaaConfigure SSL boşaltma - Azure uygulama ağ geçidi - PowerShell | Microsoft Docs"
description: "Bu sayfa bir uygulama ağ geçidi ile SSL boşaltma Azure Kaynak Yöneticisi'ni kullanarak yönergeleri toocreate sağlar"
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
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="d208b-103">Azure Resource Manager kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d208b-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d208b-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="d208b-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="d208b-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="d208b-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="d208b-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="d208b-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="d208b-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d208b-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="d208b-108">Azure uygulama ağ geçidi yapılandırılmış tooterminate hello Güvenli Yuva Katmanı (SSL) hello ağ geçidi tooavoid maliyetli SSL şifre çözme görevleri toohappen hello web grubu adresindeki oturumunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="d208b-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="d208b-109">SSL boşaltma ayrıca hello ön uç sunucusunun kurulumunu ve hello web uygulamasının yönetimini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="d208b-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d208b-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d208b-110">Before you begin</span></span>

1. <span data-ttu-id="d208b-111">Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d208b-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="d208b-112">Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d208b-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d208b-113">Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d208b-113">You create a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="d208b-114">Hiçbir sanal makine veya Bulut dağıtımları hello alt kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d208b-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="d208b-115">Application Gateway tek başına bir sanal ağ alt ağında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d208b-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="d208b-116">toouse hello uygulama ağ geçidi yapılandırma hello sunucular mevcut olmalıdır veya uç noktaları hello sanal ağda veya atanan genel IP/VIP'ye ile oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="d208b-116">hello servers you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="d208b-117">Gerekli toocreate bir uygulama ağ geçidi nedir?</span><span class="sxs-lookup"><span data-stu-id="d208b-117">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="d208b-118">**Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="d208b-118">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="d208b-119">listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d208b-119">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="d208b-120">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="d208b-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="d208b-121">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="d208b-121">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="d208b-122">**Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="d208b-122">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="d208b-123">Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="d208b-123">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="d208b-124">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu ayarları büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="d208b-124">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="d208b-125">**Kural:** hello kural hello dinleyicisi ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler.</span><span class="sxs-lookup"><span data-stu-id="d208b-125">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="d208b-126">Şu anda yalnızca hello *temel* kural desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d208b-126">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="d208b-127">Merhaba *temel* hepsini bir kez deneme yük dağıtımı kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="d208b-127">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="d208b-128">**Ek yapılandırma notları**</span><span class="sxs-lookup"><span data-stu-id="d208b-128">**Additional configuration notes**</span></span>

<span data-ttu-id="d208b-129">SSL sertifikaları yapılandırma, protokolünde hello **HttpListener** çok değiştirmelisiniz*Https* (büyük küçük harf duyarlı).</span><span class="sxs-lookup"><span data-stu-id="d208b-129">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="d208b-130">Merhaba **SslCertificate** öğesi çok eklenen**HttpListener** hello SSL sertifikası için yapılandırılmış hello değişken değeri.</span><span class="sxs-lookup"><span data-stu-id="d208b-130">hello **SslCertificate** element is added too**HttpListener** with hello variable value configured for hello SSL certificate.</span></span> <span data-ttu-id="d208b-131">Merhaba ön uç bağlantı noktası güncelleştirilmiş too443 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d208b-131">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="d208b-132">**tooenable tanımlama bilgisi temelli benzeşimi**: bir uygulama ağ geçidi isteği bir istemci oturumundan her zaman yönlendirilmiş toohello olduğunu yapılandırılmış tooensure olabilir hello web grubundaki aynı VM.</span><span class="sxs-lookup"><span data-stu-id="d208b-132">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="d208b-133">Bu senaryo, uygun şekilde hello ağ geçidi toodirect trafiğe izin veren bir oturum tanımlama bilgisi ekleme işlemi tarafından yapılır.</span><span class="sxs-lookup"><span data-stu-id="d208b-133">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="d208b-134">tanımlama bilgisi temelli benzeşimi tooenable ayarlamak **CookieBasedAffinity** çok*etkin* hello içinde **BackendHttpSettings** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d208b-134">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="d208b-135">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d208b-135">Create an application gateway</span></span>

<span data-ttu-id="d208b-136">hello Azure Klasik dağıtım modeli ve Azure Resource Manager kullanarak arasındaki farkı hello yapılandırılmış toobe gereken bir uygulama ağ geçidi ve hello öğeleri oluşturduğunuz hello sırasıdır.</span><span class="sxs-lookup"><span data-stu-id="d208b-136">hello difference between using hello Azure Classic deployment model and Azure Resource Manager is hello order that you create an application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="d208b-137">Resource Manager ile uygulama ağ geçidi'nın tüm bileşenleri ayrı ayrı yapılandırılır ve sonra birlikte toocreate uygulama ağ geçidi kaynağı.</span><span class="sxs-lookup"><span data-stu-id="d208b-137">With Resource Manager, all components of an application gateway are configured individually and then put together toocreate an application gateway resource.</span></span>

<span data-ttu-id="d208b-138">Bir uygulama ağ geçidi hello adımlar toocreate şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d208b-138">Here are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="d208b-139">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="d208b-139">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="d208b-140">Sanal ağ, alt ağ ve hello uygulama ağ geçidi için genel IP oluşturun</span><span class="sxs-lookup"><span data-stu-id="d208b-140">Create virtual network, subnet, and public IP for hello application gateway</span></span>
3. <span data-ttu-id="d208b-141">Uygulama ağ geçidi yapılandırma nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="d208b-141">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="d208b-142">Bir uygulama ağ geçidi kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d208b-142">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="d208b-143">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="d208b-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="d208b-144">PowerShell modu toouse hello Azure Resource Manager cmdlet'lerini geçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d208b-144">Make sure that you switch PowerShell mode toouse hello Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="d208b-145">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="d208b-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="d208b-146">1. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-146">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="d208b-147">2. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-147">Step 2</span></span>

<span data-ttu-id="d208b-148">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="d208b-148">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="d208b-149">Kimlik bilgilerinizle istendiğinde tooauthenticate var.</span><span class="sxs-lookup"><span data-stu-id="d208b-149">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="d208b-150">3. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-150">Step 3</span></span>

<span data-ttu-id="d208b-151">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="d208b-151">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="d208b-152">4. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-152">Step 4</span></span>

<span data-ttu-id="d208b-153">Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="d208b-153">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="d208b-154">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d208b-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d208b-155">Bu ayar, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d208b-155">This setting is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="d208b-156">Bir uygulama ağ geçidini kullanan tüm komutları toocreate Merhaba, aynı olduğundan emin olun kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="d208b-156">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="d208b-157">Adlı bir kaynak grubu oluşturduk Hello yukarıdaki örnekte, **appgw-RG** ve konum **Batı ABD**.</span><span class="sxs-lookup"><span data-stu-id="d208b-157">In hello example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="d208b-158">Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="d208b-158">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="d208b-159">örnekte gösterildiği nasıl aşağıdaki hello toocreate Kaynak Yöneticisi'ni kullanarak bir sanal ağ:</span><span class="sxs-lookup"><span data-stu-id="d208b-159">hello following example shows how toocreate a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="d208b-160">1. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-160">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="d208b-161">Bu örnek, bir sanal ağ başlangıç adresi aralığı 10.0.0.0/24 tooa alt kullanılan değişken toobe toocreate atar.</span><span class="sxs-lookup"><span data-stu-id="d208b-161">This sample assigns hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="d208b-162">2. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-162">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="d208b-163">Bu örnek adlı bir sanal ağ oluşturur **appgwvnet** kaynak grubunda **appgw-rg** 10.0.0.0/24 alt ağıyla hello önek 10.0.0.0/16 kullanarak hello Batı ABD bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="d208b-163">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="d208b-164">3. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-164">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="d208b-165">Bu örnek hello sonraki adımlar için hello alt ağ nesnesini toovariable $subnet atar.</span><span class="sxs-lookup"><span data-stu-id="d208b-165">This sample assigns hello subnet object toovariable $subnet for hello next steps.</span></span>

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="d208b-166">Merhaba ön uç yapılandırma için genel bir IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="d208b-166">Create a public IP address for hello front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="d208b-167">Bu örnek bir genel IP kaynağı oluşturur **Publicıp01** kaynak grubunda **appgw-rg** hello Batı ABD bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="d208b-167">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="d208b-168">Uygulama ağ geçidi yapılandırma nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="d208b-168">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="d208b-169">1. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-169">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="d208b-170">Bu örnek adlı uygulama ağ geçidi IP yapılandırması oluşturur **Gatewayıp01**.</span><span class="sxs-lookup"><span data-stu-id="d208b-170">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="d208b-171">Application Gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki rota.</span><span class="sxs-lookup"><span data-stu-id="d208b-171">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="d208b-172">Her örneğin bir IP adresi aldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d208b-172">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="d208b-173">2. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-173">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="d208b-174">Bu örnek adlı hello arka uç IP adresi havuzunu yapılandırır **pool01** IP adresleriyle **134.170.185.46**, **134.170.188.221**, **134.170.185.50** .</span><span class="sxs-lookup"><span data-stu-id="d208b-174">This sample configures hello back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="d208b-175">Bu değerleri hello ön uç IP uç noktasından gelen ağ trafiğini hello aldığınız hello IP adresleridir.</span><span class="sxs-lookup"><span data-stu-id="d208b-175">Those values are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="d208b-176">Kendi web uygulama uç hello IP adresleriyle örneği önceki hello Hello IP adreslerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d208b-176">Replace hello IP addresses from hello preceding example with hello IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="d208b-177">3. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-177">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="d208b-178">Bu örnek uygulama ağ geçidi ayarı yapılandırır **poolsetting01** hello arka uç havuzundaki tooload dengeli ağ trafiği.</span><span class="sxs-lookup"><span data-stu-id="d208b-178">This sample configures application gateway setting **poolsetting01** tooload-balanced network traffic in hello back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="d208b-179">4. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-179">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="d208b-180">Bu örnek adlı hello ön uç IP bağlantı noktasını yapılandırır **frontendport01** hello genel IP uç noktası için.</span><span class="sxs-lookup"><span data-stu-id="d208b-180">This sample configures hello front-end IP port named **frontendport01** for hello public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="d208b-181">5. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-181">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="d208b-182">Bu örnek, SSL bağlantısı için kullanılan hello sertifika yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="d208b-182">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="d208b-183">Merhaba sertifikanın .pfx biçiminde toobe gerekir ve hello parola 4 too12 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d208b-183">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="d208b-184">6. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-184">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="d208b-185">Bu örnek hello adlı ön uç IP yapılandırmasını oluşturur **fipconfig01** ve ortak IP adresi hello ön uç IP yapılandırması ile ilişkilendirilmiş bir hello.</span><span class="sxs-lookup"><span data-stu-id="d208b-185">This sample creates hello front-end IP configuration named **fipconfig01** and associates hello public IP address with hello front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="d208b-186">7. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-186">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="d208b-187">Bu örnek hello dinleyici adı oluşturur **listener01** ve hello ön uç bağlantı noktası toohello ön uç IP yapılandırmasını ve sertifikasını ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="d208b-187">This sample creates hello listener name **listener01** and associates hello front-end port toohello front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="d208b-188">8. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-188">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="d208b-189">Bu örnek adlı hello Yük Dengeleyiciyi yönlendirme kuralını oluşturur **rule01** hello yük dengeleyici davranışını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="d208b-189">This sample creates hello load balancer routing rule named **rule01** that configures hello load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="d208b-190">9. Adım</span><span class="sxs-lookup"><span data-stu-id="d208b-190">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="d208b-191">Bu örnek hello uygulama ağ geçidi hello örnek boyutunu yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="d208b-191">This sample configures hello instance size of hello application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="d208b-192">Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir.</span><span class="sxs-lookup"><span data-stu-id="d208b-192">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="d208b-193">Merhaba için varsayılan değer *GatewaySize* Orta'dır.</span><span class="sxs-lookup"><span data-stu-id="d208b-193">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="d208b-194">Aynı zamanda Standard_Small, Standard_Medium ve Standard_Large seçenekleri de bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d208b-194">You can choose between Standard_Small, Standard_Medium, and Standard_Large.</span></span>

### <a name="step-10"></a><span data-ttu-id="d208b-195">10. adım</span><span class="sxs-lookup"><span data-stu-id="d208b-195">Step 10</span></span>

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

<span data-ttu-id="d208b-196">Bu adım hello SSL İlkesi toouse hello uygulama ağ geçidinde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d208b-196">This step defines hello SSL policy toouse on hello application gateway.</span></span> <span data-ttu-id="d208b-197">Ziyaret [SSL yapılandırma İlkesi sürümlerini ve şifre paketleri uygulama ağ geçidi üzerinde](application-gateway-configure-ssl-policy-powershell.md) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="d208b-197">Visit [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn more.</span></span>

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="d208b-198">New-AzureApplicationGateway kullanarak bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d208b-198">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

<span data-ttu-id="d208b-199">Bu örnek hello adımları önceki tüm yapılandırma öğelerinden bir uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d208b-199">This sample creates an application gateway with all configuration items from hello preceding steps.</span></span> <span data-ttu-id="d208b-200">Merhaba örnekte hello uygulama ağ geçidi olarak adlandırılır **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="d208b-200">In hello example, hello application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="d208b-201">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="d208b-201">Get application gateway DNS name</span></span>

<span data-ttu-id="d208b-202">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="d208b-202">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="d208b-203">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="d208b-203">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="d208b-204">hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="d208b-204">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="d208b-205">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d208b-205">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="d208b-206">toodo Bu, alma ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adı.</span><span class="sxs-lookup"><span data-stu-id="d208b-206">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="d208b-207">Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d208b-207">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="d208b-208">Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="d208b-208">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="d208b-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d208b-209">Next steps</span></span>

<span data-ttu-id="d208b-210">Bir iç yük dengeleyiciye (ILB) sahip bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, bkz: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="d208b-210">If you want tooconfigure an application gateway toouse with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="d208b-211">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="d208b-211">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="d208b-212">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="d208b-212">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="d208b-213">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="d208b-213">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

