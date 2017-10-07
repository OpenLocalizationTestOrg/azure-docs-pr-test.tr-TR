---
title: "Sanal ağ uygulama ağ geçidi ile Azure API Management'te aaaHow toouse | Microsoft Docs"
description: "Bilgi nasıl toosetup ve iç sanal ağ ile uygulama ağ geçidi (WAF) ön uç olarak Azure API Management yapılandırın"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="24c68-103">Bir iç sanal ağ API Management'te uygulama ağ geçidi ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="24c68-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="24c68-104"><a name="overview"></a> Genel bakış</span><span class="sxs-lookup"><span data-stu-id="24c68-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="24c68-105">Merhaba API Management hizmeti, bir sanal ağdaki hello sanal ağ içinde yalnızca erişilebilir kılan iç modunda yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="24c68-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="24c68-106">Azure uygulama ağ geçidi bir katman 7 yük dengeleyici sağlayan bir PAAS hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="24c68-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="24c68-107">Ters proxy hizmeti davranır ve onun bir Web uygulaması Güvenlik Duvarı (WAF) sunan arasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="24c68-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="24c68-108">API Management hello uygulama ağ geçidi ön uç ile dahili bir VNET içinde sağlanan birleştirme senaryoları aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="24c68-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="24c68-109">Kullanım hello aynı API Management kaynak tüketimi hem iç tüketiciler hem de dış tüketiciler tarafından.</span><span class="sxs-lookup"><span data-stu-id="24c68-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="24c68-110">Bir alt kümesini API'leri dış Tüketiciler için kullanılabilir API Management tanımladığınız ve tek bir API Management kaynağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="24c68-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="24c68-111">Bir anahtar teslim yolu tooswitch erişim tooAPI yönetim hello gelen sağlayan genel Internet'ı kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24c68-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="24c68-112"><a name="scenario"></a> Senaryosu</span><span class="sxs-lookup"><span data-stu-id="24c68-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="24c68-113">Bu makalede nasıl toouse tek bir API Management hizmet için hem iç hem de dış tüketicileri kapsar ve her iki şirket içi için tek bir ön uç görevi görür ve bulut API'leri yapın.</span><span class="sxs-lookup"><span data-stu-id="24c68-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="24c68-114">Ayrıca görürsünüz nasıl tooexpose Apı'lerinizi (örnekte yeşil vurgulanmış bunlar hello) yalnızca bir kısmı dış uygulama ağ geçidi mevcut hello PathBasedRouting işlevselliğini kullanarak tüketimi için.</span><span class="sxs-lookup"><span data-stu-id="24c68-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="24c68-115">Merhaba ilk kurulum örnekte tüm API'leri yalnızca sanal ağınızın içinde yönetilir.</span><span class="sxs-lookup"><span data-stu-id="24c68-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="24c68-116">İç tüketicileri (vurgulanmış turuncu) tüm iç ve dış API'leri erişebilir.</span><span class="sxs-lookup"><span data-stu-id="24c68-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="24c68-117">Trafik, yüksek performanslı teslim tooInternet Expressroute bağlantı hatları hiçbir zaman gider.</span><span class="sxs-lookup"><span data-stu-id="24c68-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![URL rota](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="24c68-119"><a name="before-you-begin"></a> Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="24c68-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="24c68-120">Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="24c68-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="24c68-121">Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="24c68-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="24c68-122">Bir sanal ağ oluşturma ve API Management ve uygulama ağ geçidi için ayrı alt ağlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="24c68-123">Toocreate hello sanal ağ için özel bir DNS sunucusu düşünüyorsanız, hello dağıtıma başlamadan önce bunu.</span><span class="sxs-lookup"><span data-stu-id="24c68-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="24c68-124">Hello sanal ağ içinde yeni bir alt ağ içinde oluşturulmuş bir sanal makinenin sağlayarak çalıştığını kontrol edin, çözümlemek ve tüm Azure hizmet uç noktalarına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24c68-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="24c68-125">Gerekli toocreate API Management ile uygulama ağ geçidi arasında bir tümleştirme nedir?</span><span class="sxs-lookup"><span data-stu-id="24c68-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="24c68-126">**Arka uç sunucusu havuzu:** hello iç sanal IP adresini hello API Management hizmeti budur.</span><span class="sxs-lookup"><span data-stu-id="24c68-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="24c68-127">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="24c68-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="24c68-128">Bu ayarlar, hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="24c68-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="24c68-129">**Ön uç bağlantı noktası:** bu hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="24c68-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="24c68-130">Bunu basarsa trafiği yeniden yönlendirilen tooone Merhaba, arka uç sunucuları alır.</span><span class="sxs-lookup"><span data-stu-id="24c68-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="24c68-131">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="24c68-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="24c68-132">**Kural:** hello kuralı bir dinleyici tooa arka uç sunucusu havuzunu bağlar.</span><span class="sxs-lookup"><span data-stu-id="24c68-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="24c68-133">**Özel durum araştırması:** uygulama ağ geçidi, varsayılan olarak, hangi sunucuların hello içinde kullanıma BackendAddressPool etkin IP adreslerini göre araştırmalar toofigure kullanır.</span><span class="sxs-lookup"><span data-stu-id="24c68-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="24c68-134">Merhaba API Management hizmeti yalnızca hello doğru ana bilgisayar üstbilgisi olan toorequests yanıtlar, bu nedenle hello varsayılan araştırmalar başarısız.</span><span class="sxs-lookup"><span data-stu-id="24c68-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="24c68-135">Bir özel durum araştırması tanımlanan toobe gereken toohelp uygulama ağ geçidi hello hizmetidir canlı ve isteklerini iletmek belirler.</span><span class="sxs-lookup"><span data-stu-id="24c68-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="24c68-136">**Özel etki alanı sertifikası:** tooaccess API Management hello gelen Internet toocreate CNAME eşlemesi kendi ana bilgisayar adı toohello uygulama ağ geçidi ön uç DNS adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="24c68-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="24c68-137">Bu hello ana bilgisayar üstbilgisi ve gönderilen sertifikayı tooApplication tooAPI iletilen ağ geçidi yönetim bir APIM geçerli olarak tanıyabilmesi olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="24c68-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="24c68-138"><a name="overview-steps"></a> API Management ve uygulama ağ geçidi tümleştirmek için gerekli adımları</span><span class="sxs-lookup"><span data-stu-id="24c68-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="24c68-139">Resource Manager için kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="24c68-140">Bir sanal ağ, alt ağ ve hello uygulama ağ geçidi için genel IP oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="24c68-141">API yönetimi için başka bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="24c68-142">Yukarıda oluşturduğunuz hello sanal alt içinde bir API Management hizmeti oluşturma ve hello iç modu kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="24c68-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="24c68-143">Merhaba API Management hizmeti Hello özel etki alanı adı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="24c68-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="24c68-144">Bir uygulama ağ geçidi yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="24c68-145">Bir uygulama ağ geçidi kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="24c68-146">Merhaba Genel DNS adından hello uygulama ağ geçidi toohello API Management proxy ana bilgisayar adı bir CNAME oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="24c68-147">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="24c68-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="24c68-148">Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="24c68-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="24c68-149">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="24c68-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="24c68-150">1. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-150">Step 1</span></span>

<span data-ttu-id="24c68-151">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="24c68-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="24c68-152">Kimlik bilgilerinizle kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="24c68-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="24c68-153">2. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-153">Step 2</span></span>

<span data-ttu-id="24c68-154">Merhaba hesabının Hello abonelikleri kontrol edin ve seçin.</span><span class="sxs-lookup"><span data-stu-id="24c68-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="24c68-155">3. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-155">Step 3</span></span>

<span data-ttu-id="24c68-156">Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="24c68-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="24c68-157">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="24c68-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="24c68-158">Bu kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="24c68-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="24c68-159">Tüm komutlar, toocreate bir uygulama ağ geçidi kullanım hello emin olun aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="24c68-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="24c68-160">Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="24c68-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="24c68-161">Aşağıdaki örnek hello Kaynak Yöneticisi'ni kullanarak bir sanal ağ toocreate hello nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="24c68-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="24c68-162">1. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-162">Step 1</span></span>

<span data-ttu-id="24c68-163">Başlangıç adresi aralığı 10.0.0.0/24 toohello alt değişken toobe uygulama ağ geçidi için bir sanal ağ oluşturulurken kullanılan atayın.</span><span class="sxs-lookup"><span data-stu-id="24c68-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="24c68-164">2. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-164">Step 2</span></span>

<span data-ttu-id="24c68-165">Başlangıç adresi aralığı 10.0.1.0/24 toohello alt değişken toobe API yönetimi için bir sanal ağ oluşturulurken kullanılan atayın.</span><span class="sxs-lookup"><span data-stu-id="24c68-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="24c68-166">3. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-166">Step 3</span></span>

<span data-ttu-id="24c68-167">Adlı bir sanal ağ oluşturma **appgwvnet** kaynak grubunda **apim-appGw-RG** hello önek 10.0.0.0/16 kullanarak hello Batı ABD bölgesi için 10.0.0.0/24 alt ağları ve 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="24c68-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="24c68-168">4. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-168">Step 4</span></span>

<span data-ttu-id="24c68-169">Merhaba sonraki adımlar için bir alt ağ değişkeni atayın</span><span class="sxs-lookup"><span data-stu-id="24c68-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="24c68-170">İç modunda yapılandırılmış bir sanal ağ içinde bir API Management hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="24c68-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="24c68-171">Merhaba aşağıdaki örnekte toocreate bir VNET içindeki bir API Management hizmeti yalnızca iç erişim için nasıl yapılandırılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="24c68-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="24c68-172">1. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-172">Step 1</span></span>
<span data-ttu-id="24c68-173">Merhaba alt yukarıda oluşturduğunuz $apimsubnetdata kullanarak bir API Yönetim sanal ağ nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="24c68-174">2. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-174">Step 2</span></span>
<span data-ttu-id="24c68-175">Merhaba sanal ağ içinde bir API Management hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="24c68-176">Merhaba komutu yukarıda başarılı olduktan sonra çok başvurmak[DNS yapılandırma gerekli tooaccess iç VNET API Management hizmeti](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess onu.</span><span class="sxs-lookup"><span data-stu-id="24c68-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="24c68-177">Kurulum API Management'te özel etki alanı adı</span><span class="sxs-lookup"><span data-stu-id="24c68-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="24c68-178">1. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-178">Step 1</span></span>
<span data-ttu-id="24c68-179">Merhaba etki alanı için özel anahtara sahip Hello sertifikasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="24c68-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="24c68-180">Bu örnek için olacak `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="24c68-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="24c68-181">2. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-181">Step 2</span></span>
<span data-ttu-id="24c68-182">Merhaba sertifika yüklendikten sonra bir ana bilgisayar adını ile Merhaba proxy için bir ana bilgisayar yapılandırma nesnesi oluşturun `api.contoso.net`hello örnek sertifika yetkilisi Merhaba sağlar gibi `*.contoso.net` etki alanı.</span><span class="sxs-lookup"><span data-stu-id="24c68-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="24c68-183">Merhaba ön uç yapılandırma için genel bir IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="24c68-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="24c68-184">Genel IP kaynağı oluşturun **Publicıp01** kaynak grubunda **apim-appGw-RG** hello Batı ABD bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="24c68-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="24c68-185">Merhaba hizmeti başladığında toohello uygulama ağ geçidi bir IP adresi atanır.</span><span class="sxs-lookup"><span data-stu-id="24c68-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="24c68-186">Uygulama ağ geçidi yapılandırmasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="24c68-186">Create application gateway configuration</span></span>

<span data-ttu-id="24c68-187">Tüm yapılandırma öğeleri hello uygulama ağ geçidi oluşturmadan önce ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="24c68-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="24c68-188">Merhaba aşağıdaki adımları hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="24c68-189">1. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-189">Step 1</span></span>

<span data-ttu-id="24c68-190">**gatewayIP01** adlı bir uygulama ağ geçidi IP yapılandırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="24c68-191">Application Gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki rota.</span><span class="sxs-lookup"><span data-stu-id="24c68-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="24c68-192">Her örneğin bir IP adresi aldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="24c68-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="24c68-193">2. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-193">Step 2</span></span>

<span data-ttu-id="24c68-194">Merhaba ön uç IP bağlantı noktası hello genel IP uç noktası için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="24c68-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="24c68-195">Bu bağlantı noktası, son kullanıcılara bağlanan hello bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="24c68-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="24c68-196">3. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-196">Step 3</span></span>

<span data-ttu-id="24c68-197">Merhaba ön uç IP ile genel IP uç noktasını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="24c68-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="24c68-198">4. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-198">Step 4</span></span>

<span data-ttu-id="24c68-199">Merhaba uygulama ağ geçidi, kullanılan için toodecrypt hello sertifikası yapılandırın ve komut zincirinden geçen hello trafiğini yeniden şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="24c68-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="24c68-200">5. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-200">Step 5</span></span>

<span data-ttu-id="24c68-201">Merhaba HTTP dinleyicisi hello uygulama ağ geçidi için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="24c68-202">Merhaba ön uç IP yapılandırmasını, bağlantı noktası ve ssl sertifika tooit atayın.</span><span class="sxs-lookup"><span data-stu-id="24c68-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="24c68-203">6. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-203">Step 6</span></span>

<span data-ttu-id="24c68-204">Özel araştırma toohello API Management hizmeti oluşturma `ContosoApi` proxy etki alanı uç noktası.</span><span class="sxs-lookup"><span data-stu-id="24c68-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="24c68-205">Merhaba yolu `/status-0123456789abcdef` olan tüm hello API Management services üzerinde barındırılan bir varsayılan durumu uç noktası.</span><span class="sxs-lookup"><span data-stu-id="24c68-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="24c68-206">Ayarlama `api.contoso.net` özel araştırma hostname toosecure olarak SSL sertifikası ile.</span><span class="sxs-lookup"><span data-stu-id="24c68-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="24c68-207">ana bilgisayar adı hello `contosoapi.azure-api.net` adlı bir hizmetin hello varsayılan proxy ana bilgisayar adı yapılandırılır `contosoapi` ortak Azure içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="24c68-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="24c68-208">7. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-208">Step 7</span></span>

<span data-ttu-id="24c68-209">Merhaba SSL etkin arka uç havuzu kaynaklardaki toobe kullanılan hello sertifikasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="24c68-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="24c68-210">Merhaba budur yukarıdaki adım 4'te sağlanan aynı sertifika.</span><span class="sxs-lookup"><span data-stu-id="24c68-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="24c68-211">8. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-211">Step 8</span></span>

<span data-ttu-id="24c68-212">Merhaba uygulama ağ geçidi için HTTP arka uç ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="24c68-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="24c68-213">Bu, daha sonra iptal arka uç istek için zaman aşımı sınırı ayarı içerir.</span><span class="sxs-lookup"><span data-stu-id="24c68-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="24c68-214">Bu değer hello yoklama zaman aşımı farklıdır.</span><span class="sxs-lookup"><span data-stu-id="24c68-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="24c68-215">9. Adım</span><span class="sxs-lookup"><span data-stu-id="24c68-215">Step 9</span></span>

<span data-ttu-id="24c68-216">Adlı bir arka uç IP adresi havuzu yapılandırmak **apimbackend** hello iç sanal IP'ye sahip yukarıda hello API Management hizmeti, bir adres oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="24c68-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="24c68-217">10. adım</span><span class="sxs-lookup"><span data-stu-id="24c68-217">Step 10</span></span>

<span data-ttu-id="24c68-218">Bir kukla (mevcut olmayan) arka uç ayarlarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="24c68-219">İstek tooAPI yollarını biz tooexpose API Management uygulama ağ geçidi aracılığıyla istemiyorsanız bu arka uç isabet ve 404 döndürür.</span><span class="sxs-lookup"><span data-stu-id="24c68-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="24c68-220">Merhaba kukla arka uç HTTP ayarları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="24c68-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="24c68-221">Sahte bir arka uç yapılandırma **dummyBackendPool**, tooa FQDN adresi işaret **dummybackend.com**. Bu FQDN adresi hello sanal ağında yok.</span><span class="sxs-lookup"><span data-stu-id="24c68-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="24c68-222">Uygulama ağ geçidi toohello mevcut olmayan arka uç noktaları varsayılan olarak kullanacağı bu hello ayarını bir kural oluşturmak **dummybackend.com** hello sanal ağ içinde.</span><span class="sxs-lookup"><span data-stu-id="24c68-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="24c68-223">11. adım</span><span class="sxs-lookup"><span data-stu-id="24c68-223">Step 11</span></span>

<span data-ttu-id="24c68-224">URL kuralı yolları hello arka uç havuzları için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="24c68-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="24c68-225">Bu, bazı olması için API Management API'lerinin hello toohello genel kullanıma sunulan yalnızca seçerek sağlar.</span><span class="sxs-lookup"><span data-stu-id="24c68-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="24c68-226">Örneğin, varsa `Echo API` (/ Yankı /) `Calculator API` (/calc/) vb. yapma yalnızca `Echo API` Internet'ten erişilebilir).</span><span class="sxs-lookup"><span data-stu-id="24c68-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="24c68-227">Merhaba aşağıdaki örnek hello "/ Yankı /" yol yönlendirme trafiği toohello arka uç "apimProxyBackendPool" için basit bir kural oluşturur.</span><span class="sxs-lookup"><span data-stu-id="24c68-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="24c68-228">API Management, yol haritası yapılandırması da adlı bir varsayılan arka uç adres havuzu yapılandırır hello kural tooenable istiyoruz hello yolu Hello yolu eşleşmiyorsa kuralları **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="24c68-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="24c68-229">Örneğin, çok http://api.contoso.net/calc/ * gider**dummyBackendPool** beklemediğiniz eşleşen trafiği için varsayılan havuzu hello olarak tanımlanan.</span><span class="sxs-lookup"><span data-stu-id="24c68-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="24c68-230">Yukarıdaki adımı Hello sağlar hello yolu yalnızca istekleri "/ echo" Merhaba uygulama ağ geçidi izin verilir.</span><span class="sxs-lookup"><span data-stu-id="24c68-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="24c68-231">API Management API'leri yapılandırılmış istekleri tooother 404 hataları uygulama Internet hello erişildiğinde ağ geçidi durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="24c68-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="24c68-232">12. adımı</span><span class="sxs-lookup"><span data-stu-id="24c68-232">Step 12</span></span>

<span data-ttu-id="24c68-233">Merhaba uygulama ağ geçidi toouse URL yolu tabanlı yönlendirme kuralı ayarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="24c68-234">13. adım</span><span class="sxs-lookup"><span data-stu-id="24c68-234">Step 13</span></span>

<span data-ttu-id="24c68-235">Merhaba sayısı örnekleri ve boyutu hello uygulama ağ geçidi için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="24c68-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="24c68-236">Merhaba burada kullanıyoruz [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) hello API Management kaynak güvenliği artırmak için.</span><span class="sxs-lookup"><span data-stu-id="24c68-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="24c68-237">14. adım</span><span class="sxs-lookup"><span data-stu-id="24c68-237">Step 14</span></span>

<span data-ttu-id="24c68-238">WAF toobe "Önleme" modunda yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="24c68-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="24c68-239">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="24c68-239">Create Application Gateway</span></span>

<span data-ttu-id="24c68-240">Merhaba yapılandırma adımları önceki hello alt nesnelerden ile bir uygulama ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="24c68-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="24c68-241">CNAME hello API Management proxy ana bilgisayar adı toohello Genel DNS adını hello uygulama ağ geçidi kaynağı</span><span class="sxs-lookup"><span data-stu-id="24c68-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="24c68-242">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="24c68-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="24c68-243">Genel IP kullanırken, uygulama ağ geçidi kolay toouse olmayabilir dinamik olarak atanmış bir DNS adı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="24c68-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="24c68-244">Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate hello APIM proxy ana bilgisayar adını gösteren bir CNAME kaydı olmalıdır (ör `api.contoso.net` yukarıdaki hello örneklerde) toothis DNS adı.</span><span class="sxs-lookup"><span data-stu-id="24c68-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="24c68-245">tooconfigure hello ön uç IP CNAME kaydı hello uygulama ağ geçidi hello ayrıntılarını ve hello Publicıpaddress öğesi kullanarak ilişkili IP/DNS adını alır.</span><span class="sxs-lookup"><span data-stu-id="24c68-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="24c68-246">ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="24c68-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="24c68-247"><a name="summary"></a> Özeti</span><span class="sxs-lookup"><span data-stu-id="24c68-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="24c68-248">Azure API Management sanal ağ içinde yapılandırılmış bir tek ağ geçidi arabirimi barındırılan şirket içi olup olmadıklarını hello bulutta tüm yapılandırılmış API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="24c68-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="24c68-249">Uygulama ağ geçidi API Management ile tümleştirme sağlayan bir Web uygulaması güvenlik duvarı bir ön uç tooyour API Management örneği olarak yanı sıra belirli API'leri toobe hello Internet üzerinde erişilebilir seçmeli olarak etkinleştirme hello esnekliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="24c68-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="24c68-250"><a name="next-steps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="24c68-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="24c68-251">Azure uygulama ağ geçidi hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="24c68-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="24c68-252">Uygulama ağ geçidi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="24c68-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="24c68-253">Uygulama ağ geçidi Web uygulaması güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="24c68-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="24c68-254">Yol tabanlı yönlendirme kullanarak uygulama ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="24c68-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="24c68-255">API Management ve sanal ağlar hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="24c68-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="24c68-256">API Management hello içinde yalnızca VNET kullanılabilir kullanma</span><span class="sxs-lookup"><span data-stu-id="24c68-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="24c68-257">VNET içinde API Management kullanma</span><span class="sxs-lookup"><span data-stu-id="24c68-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
