---
title: "URL yönlendirme kullanarak bir uygulama ağ geçidi kuralları aaaCreate | Microsoft Docs"
description: "Bu sayfa yönergeleri toocreate sağlar, URL yönlendirme kurallarını kullanarak bir Azure uygulama ağ geçidi yapılandırma"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="0912e-103">Yol tabanlı yönlendirme kullanarak bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0912e-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0912e-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="0912e-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="0912e-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="0912e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="0912e-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0912e-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="0912e-107">URL yolu tabanlı yönlendirme hello URL yola bir Http isteğinin göre tooassociate yollar sağlar.</span><span class="sxs-lookup"><span data-stu-id="0912e-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="0912e-108">Bu uygulama ağ geçidi hello sunulan hello URL için yapılandırılmış bir rota tooa arka uç havuzu olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="0912e-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway.</span></span> <span data-ttu-id="0912e-109">Ardından, arka uç havuzu hello ağ trafiği toohello tanımlanan gönderir.</span><span class="sxs-lookup"><span data-stu-id="0912e-109">It then sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="0912e-110">Farklı içerik türlerini toodifferent arka uç sunucu havuzu tooload bakiye istekleri URL tabanlı yönlendirme için ortak bir kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0912e-110">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="0912e-111">URL tabanlı yönlendirme yeni bir kural türü tooapplication ağ geçidi sunar.</span><span class="sxs-lookup"><span data-stu-id="0912e-111">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="0912e-112">Uygulama ağ geçidi sahip iki kural türleri: temel ve PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="0912e-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="0912e-113">Temel kural türü hello arka uç için hepsini hizmeti tooround bir kez deneme dağıtımı sırasında PathBasedRouting ayrıca havuzları, ayrıca hello arka uç havuzu seçerken hello istek URL'sinin yol deseni dikkate alır sağlar.</span><span class="sxs-lookup"><span data-stu-id="0912e-113">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="0912e-114">Senaryo</span><span class="sxs-lookup"><span data-stu-id="0912e-114">Scenario</span></span>

<span data-ttu-id="0912e-115">Aşağıdaki örneğine hello iki arka uç sunucu havuzu ile trafiği contoso.com için uygulama ağ geçidi hizmet: video sunucu havuzu ve görüntü sunucu havuzu.</span><span class="sxs-lookup"><span data-stu-id="0912e-115">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="0912e-116">Http://contoso.com/image * yönlendirilir tooimage sunucu havuzuna (pool1) ve http://contoso.com/video * yönlendirilir isteğinin toovideo sunucu havuzuna (pool2).</span><span class="sxs-lookup"><span data-stu-id="0912e-116">Requests for http://contoso.com/image* are routed tooimage server pool (pool1), and http://contoso.com/video* are routed toovideo server pool (pool2).</span></span> <span data-ttu-id="0912e-117">Merhaba yolu desenleri hiçbiri eşleşirse, varsayılan sunucu havuzuna (pool1) seçilidir.</span><span class="sxs-lookup"><span data-stu-id="0912e-117">if none of hello path patterns match, a default server pool (pool1) is selected.</span></span>

![URL rota](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="0912e-119">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="0912e-119">Before you begin</span></span>

1. <span data-ttu-id="0912e-120">Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0912e-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="0912e-121">Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0912e-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="0912e-122">Uygulama ağ geçidi için bir sanal ağ ve alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0912e-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="0912e-123">Hiçbir sanal makine veya Bulut dağıtımları hello alt kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0912e-123">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="0912e-124">Merhaba uygulama ağ geçidi tek başına bir sanal ağ alt ağında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0912e-124">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="0912e-125">Merhaba sunucuları toohello arka uç havuzu toouse hello uygulama ağ geçidi mevcut olmalıdır veya uç noktaları hello sanal ağda veya atanan genel IP/VIP'ye ile oluşturduğunuz eklendi.</span><span class="sxs-lookup"><span data-stu-id="0912e-125">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="0912e-126">Gerekli toocreate bir uygulama ağ geçidi nedir?</span><span class="sxs-lookup"><span data-stu-id="0912e-126">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="0912e-127">**Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="0912e-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="0912e-128">listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0912e-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="0912e-129">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="0912e-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="0912e-130">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="0912e-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="0912e-131">**Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="0912e-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="0912e-132">Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="0912e-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="0912e-133">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="0912e-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="0912e-134">**Kural:** hello kural hello dinleyicisi, hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler.</span><span class="sxs-lookup"><span data-stu-id="0912e-134">**Rule:** hello rule binds hello listener, hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="0912e-135">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0912e-135">Create an application gateway</span></span>

<span data-ttu-id="0912e-136">Azure Klasik ve Azure Resource Manager kullanma arasındaki fark hello hello uygulama ağ geçidi ve yapılandırılmış toobe gereksinim hello öğelerini oluşturmak hello sırasıdır.</span><span class="sxs-lookup"><span data-stu-id="0912e-136">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="0912e-137">Resource Manager ile uygulama ağ geçidini oluşturan öğeler ayrı ayrı yapılandırılır ve toocreate hello uygulama ağ geçidi kaynağı bir araya getirin.</span><span class="sxs-lookup"><span data-stu-id="0912e-137">With Resource Manager, all items that make an application gateway are configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="0912e-138">Gerekli toocreate bir uygulama ağ geçidi hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0912e-138">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="0912e-139">Resource Manager için kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0912e-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="0912e-140">Bir sanal ağ, alt ağ ve hello uygulama ağ geçidi için genel IP oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0912e-140">Create a virtual network, subnet, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="0912e-141">Uygulama ağ geçidi yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0912e-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="0912e-142">Uygulama ağ geçidi kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0912e-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="0912e-143">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="0912e-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="0912e-144">Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0912e-144">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="0912e-145">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="0912e-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="0912e-146">1. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-146">Step 1</span></span>

<span data-ttu-id="0912e-147">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="0912e-147">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="0912e-148">Kimlik bilgilerinizle istendiğinde tooauthenticate var.</span><span class="sxs-lookup"><span data-stu-id="0912e-148">You are prompted tooauthenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="0912e-149">2. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-149">Step 2</span></span>

<span data-ttu-id="0912e-150">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="0912e-150">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="0912e-151">3. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-151">Step 3</span></span>

<span data-ttu-id="0912e-152">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="0912e-152">Choose which of your Azure subscriptions toouse.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="0912e-153">4. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-153">Step 4</span></span>

<span data-ttu-id="0912e-154">Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="0912e-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="0912e-155">Alternatif olarak, uygulama ağ geçidi için bir kaynak grubu için etiketler de oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0912e-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="0912e-156">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0912e-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="0912e-157">Bu kaynak grubu, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0912e-157">This resource group is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="0912e-158">Tüm komutlar, toocreate bir uygulama ağ geçidi kullanım hello emin olun aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="0912e-158">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="0912e-159">Merhaba yukarıdaki örnekte, "appgw-RG adlı" "Batı ABD" konumlu bir kaynak grubu oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="0912e-159">In hello example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="0912e-160">Uygulama ağ geçidiniz için özel bir araştırma tooconfigure gerekirse bkz [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0912e-160">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="0912e-161">Daha fazla bilgi için [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) konusunu inceleyin.</span><span class="sxs-lookup"><span data-stu-id="0912e-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="0912e-162">Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="0912e-162">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="0912e-163">örnekte gösterildiği nasıl aşağıdaki hello toocreate Kaynak Yöneticisi'ni kullanarak bir sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="0912e-163">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="0912e-164">Bu örnek hello uygulama ağ geçidi için bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0912e-164">This example creates a VNET for hello Application Gateway.</span></span> <span data-ttu-id="0912e-165">Uygulama ağ geçidi hello uygulama ağ geçidi için oluşturulan hello alt VNET adres alanı hello küçük olan bu nedenle, kendi alt gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0912e-165">Application Gateway requires its own subnet, for this reason hello subnet created for hello Application Gateway is smaller than hello VNET address space.</span></span> <span data-ttu-id="0912e-166">Bu da dahil olmak üzere için diğer kaynaklar sağlar ancak bunlarla sınırlı tooweb sunucuları toobe yapılandırılmış hello aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="0912e-166">This allows for other resources, including but not limited tooweb servers toobe configured in hello same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="0912e-167">1. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-167">Step 1</span></span>

<span data-ttu-id="0912e-168">Başlangıç adresi aralığı 10.0.0.0/24 toohello alt kullanılan değişken toobe toocreate bir sanal ağ atayın.</span><span class="sxs-lookup"><span data-stu-id="0912e-168">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toocreate a virtual network.</span></span>  <span data-ttu-id="0912e-169">Bu uygulama ağ geçidi hello sonraki örnekte kullanılan hello için hello alt ağ yapılandırma nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0912e-169">This creates hello subnet configuration object for hello Application Gateway, which is used in hello next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="0912e-170">2. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-170">Step 2</span></span>

<span data-ttu-id="0912e-171">Adlı bir sanal ağ oluşturma **appgwvnet** kaynak grubunda **appgw-rg** 10.0.0.0/24 alt ağıyla hello önek 10.0.0.0/16 kullanarak hello Batı ABD bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="0912e-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="0912e-172">Bu hello VNET hello uygulama ağ geçidi tooreside için tek bir alt ağ ile Merhaba yapılandırmasını tamamlar.</span><span class="sxs-lookup"><span data-stu-id="0912e-172">This completes hello configuration of hello VNET with a single subnet for hello Application Gateway tooreside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="0912e-173">3. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-173">Step 3</span></span>

<span data-ttu-id="0912e-174">Sonraki adımlar hello için Hello alt ağ değişkeni atayın, bu toohello geçirilen `New-AzureRMApplicationGateway` bir sonraki adımda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0912e-174">Assign hello subnet variable for hello next steps, this is passed toohello `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="0912e-175">Merhaba ön uç yapılandırma için genel bir IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="0912e-175">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="0912e-176">Genel IP kaynağı oluşturun **Publicıp01** kaynak grubunda **appgw-rg** hello Batı ABD bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="0912e-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="0912e-177">Uygulama ağ geçidi genel bir IP adresi, iç IP adresi veya hem tooreceive istekleri Yük Dengeleme için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0912e-177">Application Gateway can use a public IP address, internal IP address or both tooreceive requests for load balancing.</span></span>  <span data-ttu-id="0912e-178">Bu örnekte yalnızca genel IP adresi kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0912e-178">This example only uses a public IP address.</span></span> <span data-ttu-id="0912e-179">Aşağıdaki örnek hello, DNS adı yok hello genel IP adresi oluşturmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="0912e-179">In hello following example, no DNS name is configured for creating hello Public IP address.</span></span>  <span data-ttu-id="0912e-180">Application Gateway, genel IP adreslerinde özel DNS adlarını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="0912e-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="0912e-181">Merhaba ortak uç nokta için özel bir adı gerekiyorsa, toopoint otomatik olarak oluşturulan toohello DNS adı hello ortak IP adresi için bir CNAME kaydı oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0912e-181">If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="0912e-182">Merhaba hizmeti başladığında toohello uygulama ağ geçidi bir IP adresi atanır.</span><span class="sxs-lookup"><span data-stu-id="0912e-182">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="0912e-183">Uygulama ağ geçidi yapılandırmasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="0912e-183">Create application gateway configuration</span></span>

<span data-ttu-id="0912e-184">Tüm yapılandırma öğeleri hello uygulama ağ geçidi oluşturmadan önce ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0912e-184">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="0912e-185">Merhaba aşağıdaki adımları hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0912e-185">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="0912e-186">1. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-186">Step 1</span></span>

<span data-ttu-id="0912e-187">**gatewayIP01** adlı bir uygulama ağ geçidi IP yapılandırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0912e-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="0912e-188">Application Gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki rota.</span><span class="sxs-lookup"><span data-stu-id="0912e-188">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="0912e-189">Her örneğin bir IP adresi aldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="0912e-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="0912e-190">2. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-190">Step 2</span></span>

<span data-ttu-id="0912e-191">Adlı hello arka uç IP adresi havuzunu yapılandırmak **pool01** ve **pool2** için IP adresleriyle **pool1** ve **pool2**.</span><span class="sxs-lookup"><span data-stu-id="0912e-191">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="0912e-192">Merhaba IP adreslerini hello uygulama ağ geçidi tarafından korunan hello web uygulama toobe barındırma hello kaynakların bu IP adresleridir.</span><span class="sxs-lookup"><span data-stu-id="0912e-192">These IP addresses are hello IP addresses of hello resources that are hosting hello web application toobe protected by hello application gateway.</span></span> <span data-ttu-id="0912e-193">Temel araştırmalar veya özel araştırmalara olup bu arka uç havuzu tarafından araştırmalar sağlıklı tüm doğrulanmış toobe üyeleridir.</span><span class="sxs-lookup"><span data-stu-id="0912e-193">These backend pool members are all validated toobe healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="0912e-194">Trafik sonra yönlendirilir istekleri hello uygulama ağ geçidine geldiğinizde toothem.</span><span class="sxs-lookup"><span data-stu-id="0912e-194">Traffic is then routed toothem when requests come into hello application gateway.</span></span> <span data-ttu-id="0912e-195">Arka uç havuzları, aynı hello üzerinde bulunan birden çok web uygulamaları için bir arka uç havuzu kullanılabilirdi anlamı hello uygulama ağ geçidi içinde birden çok kurallar tarafından kullanılabilir ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="0912e-195">Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="0912e-196">Bu örnekte, iki arka uç havuzları tooroute ağ trafiğini hello URL yola göre vardır.</span><span class="sxs-lookup"><span data-stu-id="0912e-196">In this example, there are two back-end pools tooroute network traffic based on hello URL path.</span></span> <span data-ttu-id="0912e-197">Bir havuz "/video" URL yolundan trafiği alırken, diğer havuz "/image" yolundan trafiği alır.</span><span class="sxs-lookup"><span data-stu-id="0912e-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="0912e-198">Kendi uygulama IP adresi bitiş IP adreslerini tooadd önceki hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0912e-198">Replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="0912e-199">3. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-199">Step 3</span></span>

<span data-ttu-id="0912e-200">Uygulama ağ geçidi ayarlarını yapılandırmanız **poolsetting01** ve **poolsetting02** hello yük dengeli ağ trafiği hello arka uç havuzundaki.</span><span class="sxs-lookup"><span data-stu-id="0912e-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="0912e-201">Bu örnekte, hello arka uç havuzları farklı arka uç havuzu ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0912e-201">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="0912e-202">Her bir arka uç havuzu kendi arka uç havuzu ayarlarına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="0912e-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="0912e-203">Arka uç HTTP ayarları kuralları tooroute trafiği toohello doğru arka uç havuzu üyeleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0912e-203">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="0912e-204">Bu, hello protokolü ve trafik toohello arka uç havuzu üyeleri gönderirken kullanılan bağlantı noktası belirler.</span><span class="sxs-lookup"><span data-stu-id="0912e-204">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="0912e-205">Tanımlama bilgisi tabanlı oturum de hello arka uç HTTP ayarları tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="0912e-205">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="0912e-206">Etkinleştirilirse, tanımlama bilgisi tabanlı oturum benzeşimi trafiği toohello gönderir aynı arka uç her paket için önceki istekleri olarak.</span><span class="sxs-lookup"><span data-stu-id="0912e-206">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="0912e-207">4. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-207">Step 4</span></span>

<span data-ttu-id="0912e-208">Merhaba ön uç IP ile genel IP uç noktasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0912e-208">Configure hello front-end IP with public IP endpoint.</span></span> <span data-ttu-id="0912e-209">Merhaba ön uç IP yapılandırma nesnesi tarafından dinleyici toorelate hello dışa doğru hello dinleyici IP adresiyle karşılıklı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0912e-209">hello front-end IP configuration object is used by a listener toorelate hello outward facing IP address with hello listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="0912e-210">5. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-210">Step 5</span></span>

<span data-ttu-id="0912e-211">Merhaba, bir uygulama ağ geçidi için ön uç bağlantı noktasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0912e-211">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="0912e-212">Merhaba ön uç bağlantı noktası yapılandırma nesnesi tarafından dinleyici toodefine ne hello dinleyicisi trafiğini hello uygulama ağ geçidi dinlediği bağlantı noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0912e-212">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="0912e-213">6. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-213">Step 6</span></span>

<span data-ttu-id="0912e-214">Merhaba dinleyicisini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0912e-214">Configure hello listener.</span></span> <span data-ttu-id="0912e-215">Bu adım hello dinleyici hello genel IP adresi için yapılandırır ve bağlantı noktası tooreceive gelen ağ trafiğini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0912e-215">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="0912e-216">Aşağıdaki örneğine hello önceden yapılandırılmış hello ön uç IP yapılandırmasını, ön uç bağlantı noktası yapılandırması ve bir protokol (http veya https) alır ve hello dinleyicisi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="0912e-216">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="0912e-217">Bu örnekte, hello dinleyici tooHTTP trafiği daha önce oluşturulan hello genel IP adresi üzerinde bağlantı noktası 80 üzerinde dinler.</span><span class="sxs-lookup"><span data-stu-id="0912e-217">In this example, hello listener listens tooHTTP traffic on port 80 on hello public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="0912e-218">7. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-218">Step 7</span></span>

<span data-ttu-id="0912e-219">URL kuralı yolları hello arka uç havuzları için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0912e-219">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="0912e-220">Bu adım, uygulama ağ geçidi tarafından kullanılan hello göreli yolu yapılandırır ve hello URL yolu ile toohandle hello gelen trafiği atanan hello arka uç havuzu arasında hello eşleme tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0912e-220">This step configures hello relative path used by application gateway and defines hello mapping between hello URL path and hello back-end pool that is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0912e-221">Her bir yol ile başlamalıdır / ve hello yalnızca Yerleştir bir "\*" izin verilir, hello sonunda olur.</span><span class="sxs-lookup"><span data-stu-id="0912e-221">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="0912e-222">Geçerli örnekler /xyz, /xyz* veya/xyz / *.</span><span class="sxs-lookup"><span data-stu-id="0912e-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="0912e-223">Merhaba toohello yolu Eşleştirici sat dize herhangi bir metin hello sonra ilk içermiyor "?" veya "#" ve bu karakterleri izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="0912e-223">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="0912e-224">Merhaba aşağıdaki örnekte iki kural oluşturur: biri "/ Görüntü /" yol yönlendirme trafiği tooback uç "pool1" ve başka bir yönlendirme trafiği tooback uç "pool2." "/ video /" yolu için</span><span class="sxs-lookup"><span data-stu-id="0912e-224">hello following example creates two rules: one for "/image/" path routing traffic tooback-end "pool1" and another one for "/video/" path routing traffic tooback-end "pool2."</span></span> <span data-ttu-id="0912e-225">Bu kurallar, trafiği URL'leri her kümesi yönlendirilmiş toohello arka uç olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0912e-225">These rules ensure that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="0912e-226">Örneğin, http://contoso.com/image/figure1.jpg toopool1 gider ve http://contoso.com/video/example.mp4 toopool2 geçer.</span><span class="sxs-lookup"><span data-stu-id="0912e-226">For example, http://contoso.com/image/figure1.jpg goes toopool1 and http://contoso.com/video/example.mp4 goes toopool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="0912e-227">Merhaba yolu hello önceden tanımlanmış bir yol kurallardan herhangi birinin eşleşmiyorsa, hello kuralı yol haritası yapılandırmasını varsayılan arka uç adres havuzu da yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="0912e-227">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="0912e-228">Örneğin, hello eşleşmeyen trafiği için varsayılan havuzu olarak tanımlanan http://contoso.com/shoppingcart/test.html toopool1 gider.</span><span class="sxs-lookup"><span data-stu-id="0912e-228">For example, http://contoso.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="0912e-229">8. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-229">Step 8</span></span>

<span data-ttu-id="0912e-230">Bir kural ayarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0912e-230">Create a rule setting.</span></span> <span data-ttu-id="0912e-231">Bu adım, hello uygulama ağ geçidi toouse URL yolu tabanlı yönlendirme yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="0912e-231">This step configures hello application gateway toouse URL path-based routing.</span></span> <span data-ttu-id="0912e-232">Merhaba `$urlPathMap` tanımlanan değişken hello önceki adımda şimdi kullanılan toocreate hello yol tabanlı kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="0912e-232">hello `$urlPathMap` variable defined in hello earlier step is now used toocreate hello path-based rule.</span></span> <span data-ttu-id="0912e-233">Bu adımda, biz hello kuralı bir dinleyici ve daha önce oluşturduğunuz hello url yolu eşlemesi ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="0912e-233">In this step, we associate hello rule with a listener and hello url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="0912e-234">9. Adım</span><span class="sxs-lookup"><span data-stu-id="0912e-234">Step 9</span></span>

<span data-ttu-id="0912e-235">Merhaba sayısı örnekleri ve boyutu hello uygulama ağ geçidi için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0912e-235">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="0912e-236">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0912e-236">Create Application Gateway</span></span>

<span data-ttu-id="0912e-237">Merhaba adımları önceki tüm yapılandırma nesnelerden ile bir uygulama ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0912e-237">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="0912e-238">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="0912e-238">Get application gateway DNS name</span></span>

<span data-ttu-id="0912e-239">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="0912e-239">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="0912e-240">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="0912e-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="0912e-241">hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="0912e-241">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="0912e-242">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0912e-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="0912e-243">tooconfigure hello ön uç IP CNAME kaydı ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adını alır.</span><span class="sxs-lookup"><span data-stu-id="0912e-243">tooconfigure hello frontend IP CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="0912e-244">kullanılan toocreate bir CNAME kaydı Hello uygulama ağ geçidi DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0912e-244">hello application gateway's DNS name should be used toocreate a CNAME record.</span></span> <span data-ttu-id="0912e-245">Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="0912e-245">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0912e-246">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0912e-246">Next steps</span></span>

<span data-ttu-id="0912e-247">Güvenli Yuva Katmanı (SSL) yük boşaltma toolearn istiyorsanız, bkz: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="0912e-247">If you want toolearn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

