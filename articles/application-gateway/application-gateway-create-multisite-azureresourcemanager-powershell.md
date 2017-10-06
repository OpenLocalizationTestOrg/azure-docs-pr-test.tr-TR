---
title: "birden çok sitesi barındırmak için bir uygulama ağ geçidi aaaCreate | Microsoft Docs"
description: "Bu sayfa yönergeleri toocreate sağlar, hello birden çok web uygulamalarını barındırmak için bir Azure uygulama ağ geçidi aynı ağ geçidi."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="47326-103">Birden çok web uygulamalarını barındırmak için bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="47326-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="47326-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="47326-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="47326-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="47326-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="47326-106">Birden çok siteyi barındıran bir web uygulaması'birden fazla toodeploy üzerinde hello sağlar aynı uygulama ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="47326-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="47326-107">Ana bilgisayar üst bilgisi hello gelen HTTP isteği, hangi dinleyicisi trafiği alacağı toodetermine kullanır.</span><span class="sxs-lookup"><span data-stu-id="47326-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="47326-108">Merhaba dinleyicisi sonra hello kuralları tanımı hello ağ geçidi içinde yapılandırıldığı gibi trafik tooappropriate arka uç havuzu yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="47326-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="47326-109">SSL etkin web uygulamaları, uygulama ağ geçidi hello sunucu adı göstergesi (SNI) uzantısı toochoose hello doğru dinleyicisi hello web trafiği için kullanır.</span><span class="sxs-lookup"><span data-stu-id="47326-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="47326-110">Tooload bakiye istekleri farklı web etki alanları toodifferent arka uç sunucu havuzu için birden çok sitesi barındırmak için ortak bir kullanılır.</span><span class="sxs-lookup"><span data-stu-id="47326-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="47326-111">Benzer şekilde aynı kök etki alanı üzerinde de barındırılabilecek hello birden çok alt etki alanları aynı uygulama ağ geçidi hello.</span><span class="sxs-lookup"><span data-stu-id="47326-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="47326-112">Senaryo</span><span class="sxs-lookup"><span data-stu-id="47326-112">Scenario</span></span>

<span data-ttu-id="47326-113">Aşağıdaki örneğine hello iki arka uç sunucu havuzu ile trafiği contoso.com ve fabrikam.com için uygulama ağ geçidi hizmet: contoso sunucu havuzu ve fabrikam sunucu havuzu.</span><span class="sxs-lookup"><span data-stu-id="47326-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="47326-114">Benzer Kurulum app.contoso.com ve blog.contoso.com gibi kullanılan toohost alt etki alanları olabilir.</span><span class="sxs-lookup"><span data-stu-id="47326-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="47326-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="47326-116">Before you begin</span></span>

1. <span data-ttu-id="47326-117">Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="47326-117">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="47326-118">Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="47326-118">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="47326-119">Merhaba sunucuları toohello arka uç havuzu toouse hello uygulama ağ geçidi mevcut olmalıdır veya uç noktaları da hello sanal ağda ayrı bir alt ağ veya atanan genel IP/VIP'ye oluşturduysanız eklendi.</span><span class="sxs-lookup"><span data-stu-id="47326-119">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="47326-120">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="47326-120">Requirements</span></span>

* <span data-ttu-id="47326-121">**Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="47326-121">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="47326-122">listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="47326-122">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="47326-123">FQDN de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="47326-123">FQDN can also be used.</span></span>
* <span data-ttu-id="47326-124">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="47326-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="47326-125">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="47326-125">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="47326-126">**Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="47326-126">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="47326-127">Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="47326-127">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="47326-128">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="47326-128">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="47326-129">Çok siteli kullanan bir uygulama ağ geçitleri için ana bilgisayar adı ve SNI göstergeleri de eklenir.</span><span class="sxs-lookup"><span data-stu-id="47326-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="47326-130">**Kural:** hello kural hello dinleyicisi, hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler.</span><span class="sxs-lookup"><span data-stu-id="47326-130">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="47326-131">Kuralları listelendikleri hello sırada işlenir ve trafik belirginliğe bağımsız olarak eşleşen ilk kural hello aracılığıyla yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="47326-131">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="47326-132">Temel bir dinleyici kullanan bir kural ve çok siteli dinleyicisi hem aynı bağlantı noktası, hello kuralla hello kullanarak bir kuralı varsa, örneğin, hello çok siteli dinleyicisi önce hello kural hello çok siteli kural toofunction sırayla hello temel dinleyicisiyle listelenmiş olması gerekir bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="47326-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="47326-133">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="47326-133">Create an application gateway</span></span>

<span data-ttu-id="47326-134">Merhaba hello adımları toocreate bir uygulama ağ geçidi gerekli şunlardır:</span><span class="sxs-lookup"><span data-stu-id="47326-134">hello following are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="47326-135">Resource Manager için kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47326-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="47326-136">Bir sanal ağ, alt ağlar ve hello uygulama ağ geçidi için genel IP oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47326-136">Create a virtual network, subnets, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="47326-137">Uygulama ağ geçidi yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47326-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="47326-138">Uygulama ağ geçidi kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47326-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="47326-139">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="47326-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="47326-140">Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="47326-140">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="47326-141">Daha fazla bilgi için bkz. [Resource Manager ile Windows PowerShell kullanarak](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="47326-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="47326-142">1. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-142">Step 1</span></span>

<span data-ttu-id="47326-143">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="47326-143">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="47326-144">Kimlik bilgilerinizle istendiğinde tooauthenticate var.</span><span class="sxs-lookup"><span data-stu-id="47326-144">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="47326-145">2. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-145">Step 2</span></span>

<span data-ttu-id="47326-146">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="47326-146">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="47326-147">3. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-147">Step 3</span></span>

<span data-ttu-id="47326-148">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="47326-148">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="47326-149">4. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-149">Step 4</span></span>

<span data-ttu-id="47326-150">Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="47326-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="47326-151">Alternatif olarak, uygulama ağ geçidi için bir kaynak grubu için etiketler de oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="47326-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="47326-152">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="47326-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="47326-153">Bu konum, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="47326-153">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="47326-154">Tüm komutlar, toocreate bir uygulama ağ geçidi kullanım hello emin olun aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="47326-154">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="47326-155">Adlı bir kaynak grubu oluşturduk Hello yukarıdaki örnekte, **appgw-RG** konumunu ile **Batı ABD**.</span><span class="sxs-lookup"><span data-stu-id="47326-155">In hello example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="47326-156">Uygulama ağ geçidiniz için özel bir araştırma tooconfigure gerekirse bkz [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="47326-156">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="47326-157">Ziyaret [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="47326-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="47326-158">Bir sanal ağ ve alt ağlar oluşturun</span><span class="sxs-lookup"><span data-stu-id="47326-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="47326-159">örnekte gösterildiği nasıl aşağıdaki hello toocreate Kaynak Yöneticisi'ni kullanarak bir sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="47326-159">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="47326-160">Bu adımda iki alt ağ oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="47326-160">Two subnets are created in this step.</span></span> <span data-ttu-id="47326-161">Merhaba ilk alt hello uygulama ağ geçidi için kendisini değil.</span><span class="sxs-lookup"><span data-stu-id="47326-161">hello first subnet is for hello application gateway itself.</span></span> <span data-ttu-id="47326-162">Uygulama ağ geçidi, kendi alt toohold örneklerini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="47326-162">Application gateway requires its own subnet toohold its instances.</span></span> <span data-ttu-id="47326-163">Bu alt ağda yalnızca başka uygulama ağ geçitleri dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="47326-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="47326-164">Merhaba ikinci alt kullanılan toohold hello uygulama arka uç sunucuları değil.</span><span class="sxs-lookup"><span data-stu-id="47326-164">hello second subnet is used toohold hello application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="47326-165">1. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-165">Step 1</span></span>

<span data-ttu-id="47326-166">Başlangıç adresi aralığı 10.0.0.0/24 toohello alt değişken toobe kullanılan toohold hello uygulama ağ geçidi atayın.</span><span class="sxs-lookup"><span data-stu-id="47326-166">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toohold hello application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="47326-167">2. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-167">Step 2</span></span>

<span data-ttu-id="47326-168">Başlangıç adresi aralığı 10.0.1.0/24 toohello Altağ2 değişken toobe Hello arka uç havuzları için kullanılan atayın.</span><span class="sxs-lookup"><span data-stu-id="47326-168">Assign hello address range 10.0.1.0/24 toohello subnet2 variable toobe used for hello backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="47326-169">3. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-169">Step 3</span></span>

<span data-ttu-id="47326-170">Adlı bir sanal ağ oluşturma **appgwvnet** kaynak grubunda **appgw-rg** hello önek 10.0.0.0/16 10.0.0.0/24 alt ağıyla hello Batı ABD bölgesi için kullanarak ve 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="47326-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="47326-171">4. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-171">Step 4</span></span>

<span data-ttu-id="47326-172">Bir uygulama ağ geçidi oluşturur hello sonraki adımlar için bir alt ağ değişkeni atayın.</span><span class="sxs-lookup"><span data-stu-id="47326-172">Assign a subnet variable for hello next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="47326-173">Merhaba ön uç yapılandırma için genel bir IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="47326-173">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="47326-174">Genel IP kaynağı oluşturun **Publicıp01** kaynak grubunda **appgw-rg** hello Batı ABD bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="47326-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="47326-175">Merhaba hizmeti başladığında toohello uygulama ağ geçidi bir IP adresi atanır.</span><span class="sxs-lookup"><span data-stu-id="47326-175">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="47326-176">Uygulama ağ geçidi yapılandırmasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="47326-176">Create application gateway configuration</span></span>

<span data-ttu-id="47326-177">Merhaba uygulama ağ geçidi oluşturmadan önce tüm yapılandırma öğeleri yukarı tooset sahip.</span><span class="sxs-lookup"><span data-stu-id="47326-177">You have tooset up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="47326-178">Merhaba aşağıdaki adımları hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47326-178">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="47326-179">1. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-179">Step 1</span></span>

<span data-ttu-id="47326-180">**gatewayIP01** adlı bir uygulama ağ geçidi IP yapılandırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47326-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="47326-181">Application gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki rota.</span><span class="sxs-lookup"><span data-stu-id="47326-181">When application gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="47326-182">Her örneğin bir IP adresi aldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="47326-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="47326-183">2. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-183">Step 2</span></span>

<span data-ttu-id="47326-184">Adlı hello arka uç IP adresi havuzunu yapılandırmak **pool01** ve **pool2** IP adresleriyle **134.170.185.46**, **134.170.188.221**, **134.170.185.50** için **pool1** ve **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  için **pool2**.</span><span class="sxs-lookup"><span data-stu-id="47326-184">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="47326-185">Bu örnekte, iki arka uç havuzları tooroute ağ trafiğini hello istenen sitesinde dayalı vardır.</span><span class="sxs-lookup"><span data-stu-id="47326-185">In this example, there are two back-end pools tooroute network traffic based on hello requested site.</span></span> <span data-ttu-id="47326-186">Bir havuz "contoso.com" sitesinden trafiği alır ve diğer havuzu "fabrikam.com" sitesinden trafiği alır.</span><span class="sxs-lookup"><span data-stu-id="47326-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="47326-187">Kendi uygulama IP adresi bitiş IP adreslerini tooadd önceki tooreplace hello var.</span><span class="sxs-lookup"><span data-stu-id="47326-187">You have tooreplace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> <span data-ttu-id="47326-188">İç IP adresleri yerine, arka uç örnekleri için genel IP adresleri, FQDN veya bir sanal makinenin NIC de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47326-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="47326-189">PowerShell kullanımda toospecify FQDN'ler IP'leri yerine "-BackendFQDNs" parametresi.</span><span class="sxs-lookup"><span data-stu-id="47326-189">toospecify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="47326-190">3. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-190">Step 3</span></span>

<span data-ttu-id="47326-191">Uygulama ağ geçidi ayarlarını yapılandırmanız **poolsetting01** ve **poolsetting02** hello yük dengeli ağ trafiği hello arka uç havuzundaki.</span><span class="sxs-lookup"><span data-stu-id="47326-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="47326-192">Bu örnekte, hello arka uç havuzları farklı arka uç havuzu ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="47326-192">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="47326-193">Her bir arka uç havuzu kendi arka uç havuzu ayarlarına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="47326-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="47326-194">4. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-194">Step 4</span></span>

<span data-ttu-id="47326-195">Merhaba ön uç IP ile genel IP uç noktasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="47326-195">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="47326-196">5. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-196">Step 5</span></span>

<span data-ttu-id="47326-197">Merhaba, bir uygulama ağ geçidi için ön uç bağlantı noktasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="47326-197">Configure hello front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="47326-198">6. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-198">Step 6</span></span>

<span data-ttu-id="47326-199">İki SSL sertifikalarını yapılandırmak için hello iki Web siteleri Biz bu örnekte toosupport adımıdır.</span><span class="sxs-lookup"><span data-stu-id="47326-199">Configure two SSL certificates for hello two websites we are going toosupport in this example.</span></span> <span data-ttu-id="47326-200">Bir sertifika contoso.com trafiği için ve diğer hello fabrikam.com trafiği için.</span><span class="sxs-lookup"><span data-stu-id="47326-200">One certificate is for contoso.com traffic and hello other is for fabrikam.com traffic.</span></span> <span data-ttu-id="47326-201">Bu sertifikalar, Web siteleri için sertifikalar bir sertifika yetkilisi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="47326-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="47326-202">Otomatik olarak imzalanan sertifikalar desteklenir, ancak üretim trafiği için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="47326-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="47326-203">7. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-203">Step 7</span></span>

<span data-ttu-id="47326-204">Bu örnekte, iki dinleyicileri hello iki web sitesi için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="47326-204">Configure two listeners for hello two web sites in this example.</span></span> <span data-ttu-id="47326-205">Ortak IP adresi, bağlantı noktası ve ana bilgisayar tooreceive gelen trafiği kullanılan için bu adımı hello dinleyicileri yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="47326-205">This step configures hello listeners for public IP address, port, and host used tooreceive incoming traffic.</span></span> <span data-ttu-id="47326-206">Ana bilgisayar adı parametresi, çoklu site desteği için gereklidir ve hangi Merhaba trafiğinin alınıp kümesi toohello uygun Web sitesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="47326-206">HostName parameter is required for multiple site support and should be set toohello appropriate website for which hello traffic is received.</span></span> <span data-ttu-id="47326-207">Requireservernameındication parametresi birden çok ana senaryo için SSL desteklenmesi gereken Web siteleri için tootrue ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="47326-207">RequireServerNameIndication parameter should be set tootrue for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="47326-208">SSL desteği gerekiyorsa, toospecify hello SSL ayrıca gereken sertifika, web uygulaması için kullanılan toosecure trafiği.</span><span class="sxs-lookup"><span data-stu-id="47326-208">If SSL support is required, you also need toospecify hello SSL certificate that is used toosecure traffic for that web application.</span></span> <span data-ttu-id="47326-209">Frontendıpconfiguration, FrontendPort ve ana bilgisayar adı Hello birleşimi benzersiz tooa dinleyicisi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="47326-209">hello combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique tooa listener.</span></span> <span data-ttu-id="47326-210">Her dinleyicisi bir sertifikayı destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="47326-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="47326-211">8. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-211">Step 8</span></span>

<span data-ttu-id="47326-212">Bu örnekte, iki web uygulamaları için Hello ayarlama iki kural oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47326-212">Create two rule setting for hello two web applications in this example.</span></span> <span data-ttu-id="47326-213">Bir kural dinleyicileri, arka uç havuzları ve http ayarları birbirine bağlar.</span><span class="sxs-lookup"><span data-stu-id="47326-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="47326-214">Bu adım hello uygulama ağ geçidi toouse temel yönlendirme kuralı, her Web sitesi için bir tane yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="47326-214">This step configures hello application gateway toouse Basic routing rule, one for each website.</span></span> <span data-ttu-id="47326-215">Trafiği tooeach Web sitesi, yapılandırılmış bir dinleyici tarafından alınır ve ardından tooits hello BackendHttpSettings belirtilen hello özelliklerini kullanarak arka uç havuzu yapılandırılmış yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="47326-215">Traffic tooeach website is received by its configured listener, and is then directed tooits configured backend pool, using hello properties specified in hello BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="47326-216">9. Adım</span><span class="sxs-lookup"><span data-stu-id="47326-216">Step 9</span></span>

<span data-ttu-id="47326-217">Merhaba sayısı örnekleri ve boyutu hello uygulama ağ geçidi için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="47326-217">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="47326-218">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="47326-218">Create application gateway</span></span>

<span data-ttu-id="47326-219">Merhaba adımları önceki tüm yapılandırma nesnelerden ile bir uygulama ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="47326-219">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="47326-220">Uygulama ağ geçidi sağlama, uzun süreli bir işlemdir ve bazı zaman toocomplete sürebilir.</span><span class="sxs-lookup"><span data-stu-id="47326-220">Application Gateway provisioning is a long running operation and may take some time toocomplete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="47326-221">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="47326-221">Get application gateway DNS name</span></span>

<span data-ttu-id="47326-222">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="47326-222">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="47326-223">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="47326-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="47326-224">hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="47326-224">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="47326-225">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47326-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="47326-226">toodo Bu, alma ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adı.</span><span class="sxs-lookup"><span data-stu-id="47326-226">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="47326-227">Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="47326-227">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="47326-228">Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="47326-228">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="47326-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="47326-229">Next steps</span></span>

<span data-ttu-id="47326-230">Bilgi nasıl tooprotect ile Web siteleri [uygulama ağ geçidi - Web uygulaması güvenlik duvarı](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="47326-230">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

