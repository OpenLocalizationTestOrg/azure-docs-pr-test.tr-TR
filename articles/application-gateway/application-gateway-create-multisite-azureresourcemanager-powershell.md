---
title: "Birden çok sitesi barındırmak için bir uygulama ağ geçidi oluşturma | Microsoft Docs"
description: "Bu sayfa oluşturma, aynı ağ geçidinde birden çok web uygulamalarını barındırmak için bir Azure uygulama ağ geçidi yapılandırmak için yönergeler sağlar."
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
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="663b3-103">Birden çok web uygulamalarını barındırmak için bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="663b3-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="663b3-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="663b3-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="663b3-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="663b3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="663b3-106">Birden çok siteyi barındıran aynı uygulama ağ geçidi birden çok web uygulamasına dağıtmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="663b3-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="663b3-107">Hangi dinleyicisi trafiği alacağını belirlemek için gelen HTTP isteği, ana bilgisayar üst bilgisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="663b3-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="663b3-108">Dinleyici sonra ağ geçidi kuralları tanımı içinde yapılandırıldığı gibi uygun arka uç havuzu trafiğini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="663b3-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="663b3-109">SSL etkin web uygulamaları, uygulama ağ geçidi web trafiği için doğru dinleyici seçmek için sunucu adı göstergesi (SNI) uzantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="663b3-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="663b3-110">Birden çok sitesi barındırmak için bir genel Yük Dengeleme isteklerini farklı web etki alanları için farklı bir arka uç sunucu havuzları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="663b3-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="663b3-111">Benzer şekilde aynı kök etki alanının birden çok alt de aynı uygulama ağ geçidinde barındırılan.</span><span class="sxs-lookup"><span data-stu-id="663b3-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="663b3-112">Senaryo</span><span class="sxs-lookup"><span data-stu-id="663b3-112">Scenario</span></span>

<span data-ttu-id="663b3-113">Aşağıdaki örnekte, iki arka uç sunucu havuzu ile trafiği contoso.com ve fabrikam.com için uygulama ağ geçidi hizmet: contoso sunucu havuzu ve fabrikam sunucu havuzu.</span><span class="sxs-lookup"><span data-stu-id="663b3-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="663b3-114">Benzer Kurulum app.contoso.com ve blog.contoso.com gibi ana bilgisayar alt etki alanları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="663b3-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="663b3-116">Before you begin</span></span>

1. <span data-ttu-id="663b3-117">Web Platformu Yükleyicisi’ni kullanarak Azure PowerShell cmdlet’lerin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="663b3-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="663b3-118">**İndirmeler sayfası**’ndaki [Windows PowerShell](https://azure.microsoft.com/downloads/) bölümünden en son sürümü indirip yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="663b3-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="663b3-119">Uygulama ağ geçidi kullanmak için arka uç havuzuna eklediğiniz sunucular mevcut olmalıdır veya uç noktaları ya da sanal ağda ayrı bir alt ağ veya atanan genel IP/VIP'ye oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="663b3-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="663b3-120">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="663b3-120">Requirements</span></span>

* <span data-ttu-id="663b3-121">**Arka uç sunucusu havuzu:** Arka uç sunucularının IP adreslerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="663b3-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="663b3-122">Listede bulunan IP adresleri sanal ağ alt ağına veya genel IP/VIP’ye ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="663b3-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="663b3-123">FQDN de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-123">FQDN can also be used.</span></span>
* <span data-ttu-id="663b3-124">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="663b3-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="663b3-125">Bu ayarlar bir havuza bağlıdır ve havuzdaki tüm sunuculara uygulanır.</span><span class="sxs-lookup"><span data-stu-id="663b3-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="663b3-126">**Ön uç bağlantı noktası:** Bu bağlantı noktası uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="663b3-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="663b3-127">Bu bağlantı noktasında trafik olursa arka uç sunuculardan birine yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="663b3-128">**Dinleyici:** Dinleyicide bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerler büyük/küçük harfe duyarlıdır) ve SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa) vardır.</span><span class="sxs-lookup"><span data-stu-id="663b3-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="663b3-129">Çok siteli kullanan bir uygulama ağ geçitleri için ana bilgisayar adı ve SNI göstergeleri de eklenir.</span><span class="sxs-lookup"><span data-stu-id="663b3-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="663b3-130">**Kural:** kural dinleyiciyi arka uç sunucusu havuzunu bağlar ve trafiği için belli bir Dinleyicide trafik olduğunda hangi arka uç sunucu havuzuna yönlendirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="663b3-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="663b3-131">Kuralları listelendikleri sırada işlenir ve trafik belirginliğe bağımsız olarak eşleşen ilk kural üzerinden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="663b3-132">Temel bir dinleyici ve çok siteli dinleyicisi hem aynı bağlantı noktasında kullanan bir kural kullanarak bir kuralı varsa, örneğin, çok siteli dinleyicisi kuralla beklendiği şekilde çalışması için temel dinleyicisi çok siteli kuralı için sırada olan kural önce listelenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="663b3-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="663b3-133">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="663b3-133">Create an application gateway</span></span>

<span data-ttu-id="663b3-134">Bir uygulama ağ geçidi oluşturmak için gereken adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="663b3-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="663b3-135">Resource Manager için kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="663b3-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="663b3-136">Bir sanal ağ, alt ağlar ve uygulama ağ geçidi için genel IP oluşturun.</span><span class="sxs-lookup"><span data-stu-id="663b3-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="663b3-137">Uygulama ağ geçidi yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="663b3-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="663b3-138">Uygulama ağ geçidi kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="663b3-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="663b3-139">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="663b3-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="663b3-140">Azure PowerShell’in en yeni sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="663b3-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="663b3-141">Daha fazla bilgi için bkz. [Resource Manager ile Windows PowerShell kullanarak](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="663b3-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="663b3-142">1. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-142">Step 1</span></span>

<span data-ttu-id="663b3-143">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="663b3-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="663b3-144">Kimlik bilgilerinizle kimliğinizi doğrulamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="663b3-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="663b3-145">2. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-145">Step 2</span></span>

<span data-ttu-id="663b3-146">Hesapla ilişkili abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="663b3-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="663b3-147">3. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-147">Step 3</span></span>

<span data-ttu-id="663b3-148">Hangi Azure aboneliğinizin kullanılacağını seçin.</span><span class="sxs-lookup"><span data-stu-id="663b3-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="663b3-149">4. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-149">Step 4</span></span>

<span data-ttu-id="663b3-150">Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="663b3-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="663b3-151">Alternatif olarak, uygulama ağ geçidi için bir kaynak grubu için etiketler de oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="663b3-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="663b3-152">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="663b3-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="663b3-153">Bu konum, kaynak grubundaki kaynaklar için varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="663b3-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="663b3-154">Bir uygulama ağ geçidi oluşturmak için verilecek komutların aynı kaynak grubunda kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="663b3-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="663b3-155">Yukarıdaki örnekte adlı bir kaynak grubu oluşturduk **appgw-RG** konumunu ile **Batı ABD**.</span><span class="sxs-lookup"><span data-stu-id="663b3-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="663b3-156">Uygulama ağ geçidiniz için özel bir araştırma yapılandırmanız gerekiyorsa, bkz. [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="663b3-156">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="663b3-157">Ziyaret [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="663b3-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="663b3-158">Bir sanal ağ ve alt ağlar oluşturun</span><span class="sxs-lookup"><span data-stu-id="663b3-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="663b3-159">Aşağıdaki örnek Resource Manager kullanarak nasıl sanal ağ oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="663b3-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="663b3-160">Bu adımda iki alt ağ oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="663b3-160">Two subnets are created in this step.</span></span> <span data-ttu-id="663b3-161">İlk alt uygulama ağ geçidi için kendisini değil.</span><span class="sxs-lookup"><span data-stu-id="663b3-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="663b3-162">Uygulama ağ geçidi örneklerini tutmak için kendi alt gerektirir.</span><span class="sxs-lookup"><span data-stu-id="663b3-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="663b3-163">Bu alt ağda yalnızca başka uygulama ağ geçitleri dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="663b3-164">İkinci alt ağ, uygulama arka uç sunucuları tutmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="663b3-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="663b3-165">1. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-165">Step 1</span></span>

<span data-ttu-id="663b3-166">10.0.0.0/24 adres aralığını uygulama ağ geçidi tutmak için kullanılan alt ağ değişkenine atayın.</span><span class="sxs-lookup"><span data-stu-id="663b3-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="663b3-167">2. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-167">Step 2</span></span>

<span data-ttu-id="663b3-168">Adres aralığı 10.0.1.0/24 arka uç havuzları için kullanılacak Altağ2 değişkenine atayın.</span><span class="sxs-lookup"><span data-stu-id="663b3-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="663b3-169">3. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-169">Step 3</span></span>

<span data-ttu-id="663b3-170">Adlı bir sanal ağ oluşturma **appgwvnet** kaynak grubunda **appgw-rg** 10.0.0.0/24 alt ağıyla önek 10.0.0.0/16 kullanarak Batı ABD bölgesi için ve 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="663b3-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="663b3-171">4. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-171">Step 4</span></span>

<span data-ttu-id="663b3-172">Bir uygulama ağ geçidi oluşturur sonraki adımlar için bir alt ağ değişkeni atayın.</span><span class="sxs-lookup"><span data-stu-id="663b3-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="663b3-173">Ön uç yapılandırma için genel bir IP adresi oluşturun</span><span class="sxs-lookup"><span data-stu-id="663b3-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="663b3-174">Batı ABD bölgesi için **appgw-rg** kaynak grubunda **publicIP01** genel bir IP kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="663b3-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="663b3-175">Hizmet başlatıldığında uygulama ağ geçidine bir IP adresi atanır.</span><span class="sxs-lookup"><span data-stu-id="663b3-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="663b3-176">Uygulama ağ geçidi yapılandırmasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="663b3-176">Create application gateway configuration</span></span>

<span data-ttu-id="663b3-177">Uygulama ağ geçidini oluşturmadan önce tüm yapılandırma öğelerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="663b3-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="663b3-178">Aşağıdaki adımlar uygulama ağ geçidi kaynağı için gerekli yapılandırma öğelerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="663b3-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="663b3-179">1. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-179">Step 1</span></span>

<span data-ttu-id="663b3-180">**gatewayIP01** adlı bir uygulama ağ geçidi IP yapılandırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="663b3-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="663b3-181">Uygulama ağ geçidi başladığında, yapılandırılan alt ağdan bir IP adresi seçer ve arka uç IP havuzundaki IP adresleri için ağ trafiğini yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="663b3-182">Her örneğin bir IP adresi aldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="663b3-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="663b3-183">2. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-183">Step 2</span></span>

<span data-ttu-id="663b3-184">Adlı arka uç IP adresi havuzu yapılandırmak **pool01** ve **pool2** IP adresleriyle **134.170.185.46**, **134.170.188.221**, **134.170.185.50** için **pool1** ve **134.170.186.46**, **134.170.189.221**, **134.170.186.50** için **pool2**.</span><span class="sxs-lookup"><span data-stu-id="663b3-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="663b3-185">Bu örnekte, istenen sitesinde göre ağ trafiği yönlendirmek için iki arka uç havuzu yok.</span><span class="sxs-lookup"><span data-stu-id="663b3-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="663b3-186">Bir havuz "contoso.com" sitesinden trafiği alır ve diğer havuzu "fabrikam.com" sitesinden trafiği alır.</span><span class="sxs-lookup"><span data-stu-id="663b3-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="663b3-187">Kendi uygulama IP adresi uç noktalarını eklemek için yukarıdaki IP adreslerini değiştirmek zorunda.</span><span class="sxs-lookup"><span data-stu-id="663b3-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="663b3-188">İç IP adresleri yerine, arka uç örnekleri için genel IP adresleri, FQDN veya bir sanal makinenin NIC de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="663b3-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="663b3-189">PowerShell kullanmak yerine FQDN'ler yerine IP'leri belirtmek için "-BackendFQDNs" parametresi.</span><span class="sxs-lookup"><span data-stu-id="663b3-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="663b3-190">3. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-190">Step 3</span></span>

<span data-ttu-id="663b3-191">Uygulama ağ geçidi ayarlarını yapılandırmanız **poolsetting01** ve **poolsetting02** arka uç havuzundaki yük dengeli ağ trafiği için.</span><span class="sxs-lookup"><span data-stu-id="663b3-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="663b3-192">Bu örnekte, arka uç havuzları farklı arka uç havuzu ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="663b3-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="663b3-193">Her bir arka uç havuzu kendi arka uç havuzu ayarlarına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="663b3-194">4. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-194">Step 4</span></span>

<span data-ttu-id="663b3-195">Ön uç IP’sini genel IP uç noktası ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="663b3-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="663b3-196">5. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-196">Step 5</span></span>

<span data-ttu-id="663b3-197">Bir uygulama ağ geçidi için ön uç bağlantı noktasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="663b3-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="663b3-198">6. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-198">Step 6</span></span>

<span data-ttu-id="663b3-199">Biz bu örnekte destekleyeceğinizi iki SSL sertifikaları iki Web siteleri için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="663b3-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="663b3-200">Bir sertifika contoso.com trafiği için ve diğer fabrikam.com trafiği için.</span><span class="sxs-lookup"><span data-stu-id="663b3-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="663b3-201">Bu sertifikalar, Web siteleri için sertifikalar bir sertifika yetkilisi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="663b3-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="663b3-202">Otomatik olarak imzalanan sertifikalar desteklenir, ancak üretim trafiği için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="663b3-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="663b3-203">7. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-203">Step 7</span></span>

<span data-ttu-id="663b3-204">Bu örnekte, iki dinleyicileri iki web sitesi için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="663b3-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="663b3-205">Bu adım dinleyicileri ortak IP adresi, bağlantı noktası ve gelen trafiği almak için kullanılan ana bilgisayarı için yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="663b3-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="663b3-206">Ana bilgisayar adı parametresi, çoklu site desteği için gereklidir ve trafiği alınan uygun Web sitesine ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="663b3-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="663b3-207">Requireservernameındication parametresi ayarlanmalıdır SSL için birden çok ana senaryo desteği gerektiren Web siteleri için true.</span><span class="sxs-lookup"><span data-stu-id="663b3-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="663b3-208">SSL desteği gerekiyorsa, ayrıca, web uygulaması için trafiğinin güvenliğini sağlamak için kullanılan SSL sertifikası belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="663b3-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="663b3-209">Frontendıpconfiguration, FrontendPort ve ana bilgisayar adı bileşimi için bir dinleyici benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="663b3-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="663b3-210">Her dinleyicisi bir sertifikayı destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="663b3-211">8. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-211">Step 8</span></span>

<span data-ttu-id="663b3-212">Bu örnekte, iki web uygulamaları için iki kural ayarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="663b3-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="663b3-213">Bir kural dinleyicileri, arka uç havuzları ve http ayarları birbirine bağlar.</span><span class="sxs-lookup"><span data-stu-id="663b3-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="663b3-214">Bu adım, uygulama ağ geçidi her Web sitesi için bir tane temel yönlendirme kuralı kullanmak üzere yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="663b3-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="663b3-215">Her Web sitesi trafiğini kendi yapılandırılmış dinleyicisi tarafından alınır ve BackendHttpSettings belirtilen özellikleri kullanarak kendi yapılandırılmış arka uç havuzu yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="663b3-216">9. Adım</span><span class="sxs-lookup"><span data-stu-id="663b3-216">Step 9</span></span>

<span data-ttu-id="663b3-217">Uygulama ağ geçidi için örnek sayısını ve boyutu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="663b3-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="663b3-218">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="663b3-218">Create application gateway</span></span>

<span data-ttu-id="663b3-219">Yukarıdaki adımlarda geçen tüm yapılandırma nesnelerle bir uygulama ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="663b3-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="663b3-220">Uygulama ağ geçidi sağlama, uzun süreli bir işlemdir ve tamamlanması biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-220">Application Gateway provisioning is a long running operation and may take some time to complete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="663b3-221">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="663b3-221">Get application gateway DNS name</span></span>

<span data-ttu-id="663b3-222">Ağ geçidi oluşturulduktan sonraki adım, iletişim için ön uç yapılandırması yapmaktır.</span><span class="sxs-lookup"><span data-stu-id="663b3-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="663b3-223">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="663b3-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="663b3-224">Son kullanıcıların uygulama ağ geçidine ulaşmasını sağlamak için uygulama ağ geçidinin genel uç noktasını işaret edecek bir CNAME kaydı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="663b3-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="663b3-225">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="663b3-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="663b3-226">Bunu yapmak için uygulama ağ geçidinin ayrıntılarını ve onunla ilişkilendirilmiş olan IP/DNS adını uygulama ağ geçidine eklenmiş PublicIPAddress öğesini kullanarak alın.</span><span class="sxs-lookup"><span data-stu-id="663b3-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="663b3-227">Uygulama ağ geçidinin DNS adı, iki web uygulamasını bu DNS adına götüren bir CNAME kaydı oluşturmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="663b3-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="663b3-228">Uygulama ağ geçidi yeniden başlatıldığında VIP değişebileceğinden A kaydı kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="663b3-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="663b3-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="663b3-229">Next steps</span></span>

<span data-ttu-id="663b3-230">İle Web siteleri korumayı öğrenin [uygulama ağ geçidi - Web uygulaması güvenlik duvarı](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="663b3-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

