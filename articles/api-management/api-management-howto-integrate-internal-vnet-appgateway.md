---
title: "Uygulama ağ geçidi ile sanal ağındaki Azure API Management kullanma | Microsoft Docs"
description: "Kurulum ve iç sanal ağ ile uygulama ağ geçidi (WAF) ön uç olarak Azure API Management yapılandırmak hakkında bilgi edinin"
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
ms.openlocfilehash: 8131ded6b74e9c544bf70b1a4659ed07e5def04d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="88758-103">Bir iç sanal ağ API Management'te uygulama ağ geçidi ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="88758-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="88758-104"><a name="overview"></a> Genel bakış</span><span class="sxs-lookup"><span data-stu-id="88758-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="88758-105">API Management hizmeti, bir sanal ağdaki sanal ağda yalnızca erişilebilir kılan iç modunda yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="88758-105">The API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within the Virtual Network.</span></span> <span data-ttu-id="88758-106">Azure uygulama ağ geçidi bir katman 7 yük dengeleyici sağlayan bir PAAS hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="88758-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="88758-107">Ters proxy hizmeti davranır ve onun bir Web uygulaması Güvenlik Duvarı (WAF) sunan arasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="88758-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="88758-108">API uygulama ağ geçidi ön uç ile dahili bir VNET içinde sağlanan yönetim birleştirme, aşağıdaki senaryolarda sağlar:</span><span class="sxs-lookup"><span data-stu-id="88758-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span></span>

* <span data-ttu-id="88758-109">Hem iç tüketiciler hem de dış tüketiciler tarafından tüketimi için aynı API Management kaynağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="88758-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="88758-110">Bir alt kümesini API'leri dış Tüketiciler için kullanılabilir API Management tanımladığınız ve tek bir API Management kaynağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="88758-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="88758-111">API Management genel Internet'ten açma ve kapatma anahtar erişimi için bir anahtar teslim yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="88758-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span></span> 

##<span data-ttu-id="88758-112"><a name="scenario"></a> Senaryosu</span><span class="sxs-lookup"><span data-stu-id="88758-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="88758-113">Bu makalede, iç ve dış tüketicilerin tek bir API Management hizmetini kullanın ve her iki şirket içi için tek bir ön uç görevi görür ve bulut API'leri sağlamak nasıl ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="88758-113">This article will cover how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="88758-114">Ayrıca dış uygulama ağ geçidi mevcut PathBasedRouting işlevselliğini kullanarak tüketimi için yalnızca bir alt kümesini Apı'lerinizi (yeşil renkte vurgulanır örnekte) kullanıma sunmak nasıl görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="88758-114">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using the PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="88758-115">İlk kurulum örnekte tüm API'leri yalnızca sanal ağınızın içinde yönetilir.</span><span class="sxs-lookup"><span data-stu-id="88758-115">In the first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="88758-116">İç tüketicileri (vurgulanmış turuncu) tüm iç ve dış API'leri erişebilir.</span><span class="sxs-lookup"><span data-stu-id="88758-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="88758-117">Trafik hiçbir zaman yüksek performanslı teslim Internet'e Expressroute bağlantı hatları gider.</span><span class="sxs-lookup"><span data-stu-id="88758-117">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span></span>

![URL rota](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="88758-119"><a name="before-you-begin"></a> Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="88758-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="88758-120">Web Platformu Yükleyicisi’ni kullanarak Azure PowerShell cmdlet’lerin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="88758-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="88758-121">**İndirmeler sayfası**’ndaki [Windows PowerShell](https://azure.microsoft.com/downloads/) bölümünden en son sürümü indirip yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88758-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="88758-122">Bir sanal ağ oluşturma ve API Management ve uygulama ağ geçidi için ayrı alt ağlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="88758-123">Sanal ağ için özel bir DNS sunucusu oluşturmak istiyorsanız, dağıtıma başlamadan önce bunu.</span><span class="sxs-lookup"><span data-stu-id="88758-123">If you intend to create a custom DNS server for the Virtual Network, do so before starting the deployment.</span></span> <span data-ttu-id="88758-124">Sanal ağda yeni bir alt ağ içinde oluşturulmuş bir sanal makinenin sağlayarak çalıştığını kontrol edin, çözümlemek ve tüm Azure hizmet uç noktalarına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88758-124">Double check it works by ensuring a virtual machine created in a new subnet in the Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-to-create-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="88758-125">API Management ile uygulama ağ geçidi arasında bir tümleştirme oluşturmak için gerekli nedir?</span><span class="sxs-lookup"><span data-stu-id="88758-125">What is required to create an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="88758-126">**Arka uç sunucusu havuzu:** API Management hizmeti iç sanal IP adresine budur.</span><span class="sxs-lookup"><span data-stu-id="88758-126">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span></span>
* <span data-ttu-id="88758-127">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="88758-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="88758-128">Bu ayarlar, havuzdaki tüm sunuculara uygulanır.</span><span class="sxs-lookup"><span data-stu-id="88758-128">These settings are applied to all servers within the pool.</span></span>
* <span data-ttu-id="88758-129">**Ön uç bağlantı noktası:** bu uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="88758-129">**Front-end port:** This is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="88758-130">Bunu basarsa trafiği arka uç sunuculardan birine yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="88758-130">Traffic hitting it gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="88758-131">**Dinleyici:** Dinleyicide bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerler büyük/küçük harfe duyarlıdır) ve SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa) vardır.</span><span class="sxs-lookup"><span data-stu-id="88758-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="88758-132">**Kural:** kural dinleyici bir arka uç sunucu havuzuna bağlar.</span><span class="sxs-lookup"><span data-stu-id="88758-132">**Rule:** The rule binds a listener to a back-end server pool.</span></span>
* <span data-ttu-id="88758-133">**Özel durum araştırması:** uygulama ağ geçidi, varsayılan olarak, kullanan IP adreslerini göre araştırmalar BackendAddressPool hangi sunucuları etkin olduğunu anlamak için.</span><span class="sxs-lookup"><span data-stu-id="88758-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span></span> <span data-ttu-id="88758-134">API Management hizmeti yalnızca doğru ana bilgisayar üstbilgisi olan isteklerine yanıt verir, bu nedenle varsayılan araştırmalar başarısız.</span><span class="sxs-lookup"><span data-stu-id="88758-134">The API Management service only responds to requests which have the correct host header, hence the default probes fail.</span></span> <span data-ttu-id="88758-135">Bir özel durum araştırması uygulama ağ geçidi hizmeti kullanımda ve isteklerini iletmek belirlemek amacıyla tanımlanması gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="88758-135">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span></span>
* <span data-ttu-id="88758-136">**Özel etki alanı sertifikası:** API Management kendi ana bilgisayar adı uygulama ağ geçidi ön uç DNS adına CNAME eşlemesi oluşturmanız internet'ten erişmek için.</span><span class="sxs-lookup"><span data-stu-id="88758-136">**Custom domain certificate:** To access API Management from the internet you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span></span> <span data-ttu-id="88758-137">Bu uygulama için API Management ileten ağ geçidi için gönderilen sertifikayı ve ana bilgisayar üstbilgisi bir APIM geçerli olarak tanıyabilmesi için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="88758-137">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="88758-138"><a name="overview-steps"></a> API Management ve uygulama ağ geçidi tümleştirmek için gerekli adımları</span><span class="sxs-lookup"><span data-stu-id="88758-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="88758-139">Resource Manager için kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="88758-140">Uygulama ağ geçidi için bir sanal ağ alt ağı ve genel IP oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-140">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span></span> <span data-ttu-id="88758-141">API yönetimi için başka bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="88758-142">Yukarıda oluşturduğunuz sanal alt ağ içinde bir API Management hizmeti oluşturma ve iç modu kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="88758-142">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span></span>
4. <span data-ttu-id="88758-143">API Management hizmetinde özel etki alanı adı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="88758-143">Setup the custom domain name in the API Management service.</span></span>
5. <span data-ttu-id="88758-144">Bir uygulama ağ geçidi yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="88758-145">Bir uygulama ağ geçidi kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="88758-146">Uygulama ağ geçidi API Management proxy ana bilgisayar adı için Genel DNS adından bir CNAME oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-146">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="88758-147">Resource Manager için kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="88758-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="88758-148">Azure PowerShell’in en yeni sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="88758-148">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="88758-149">Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="88758-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="88758-150">1. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-150">Step 1</span></span>

<span data-ttu-id="88758-151">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="88758-151">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="88758-152">Kimlik bilgilerinizle kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="88758-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="88758-153">2. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-153">Step 2</span></span>

<span data-ttu-id="88758-154">Hesap için abonelikleri kontrol edin ve seçin.</span><span class="sxs-lookup"><span data-stu-id="88758-154">Check the subscriptions for the account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="88758-155">3. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-155">Step 3</span></span>

<span data-ttu-id="88758-156">Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="88758-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="88758-157">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="88758-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="88758-158">Bu, kaynak grubunda kaynaklar için varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="88758-158">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="88758-159">Bir uygulama ağ geçidi oluşturmak için verilecek komutların aynı kaynak grubunda kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="88758-159">Make sure that all commands to create an application gateway use the same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="88758-160">Bir sanal ağ ve uygulama ağ geçidi için bir alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="88758-160">Create a Virtual Network and a subnet for the application gateway</span></span>

<span data-ttu-id="88758-161">Aşağıdaki örnek Yöneticisi kaynağı kullanan bir sanal ağ oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="88758-161">The following example shows how to create a Virtual Network using the resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="88758-162">1. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-162">Step 1</span></span>

<span data-ttu-id="88758-163">10.0.0.0/24 adres aralığını, sanal ağ oluşturulurken uygulama ağ geçidi için kullanılacak bir alt ağ değişkenine atayın.</span><span class="sxs-lookup"><span data-stu-id="88758-163">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="88758-164">2. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-164">Step 2</span></span>

<span data-ttu-id="88758-165">Adres aralığı 10.0.1.0/24 bir sanal ağ oluşturulurken API yönetimi için kullanılacak bir alt ağ değişkenine atayın.</span><span class="sxs-lookup"><span data-stu-id="88758-165">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="88758-166">3. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-166">Step 3</span></span>

<span data-ttu-id="88758-167">Adlı bir sanal ağ oluşturma **appgwvnet** kaynak grubunda **apim-appGw-RG** önek 10.0.0.0/16 kullanarak Batı ABD bölgesi için 10.0.0.0/24 alt ağları ve 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="88758-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region using the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="88758-168">4. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-168">Step 4</span></span>

<span data-ttu-id="88758-169">Sonraki adımlar için bir alt ağ değişkeni atayın</span><span class="sxs-lookup"><span data-stu-id="88758-169">Assign a subnet variable for the next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="88758-170">İç modunda yapılandırılmış bir sanal ağ içinde bir API Management hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="88758-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="88758-171">Aşağıdaki örnekte nasıl bir API Management hizmeti yalnızca iç erişimi için yapılandırılmış bir sanal ağ oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="88758-171">The following example shows how to create an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="88758-172">1. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-172">Step 1</span></span>
<span data-ttu-id="88758-173">Yukarıda oluşturduğunuz $apimsubnetdata alt ağı kullanarak bir API Yönetim sanal ağ nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-173">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="88758-174">2. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-174">Step 2</span></span>
<span data-ttu-id="88758-175">Sanal ağ içindeki bir API Management hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-175">Create an API Management service inside the Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="88758-176">Yukarıdaki komut başarılı olduktan sonra başvurmak [DNS yapılandırma gerekli iç VNET API Management hizmetine erişmek için](api-management-using-with-internal-vnet.md#apim-dns-configuration) erişmek için.</span><span class="sxs-lookup"><span data-stu-id="88758-176">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="88758-177">Kurulum API Management'te özel etki alanı adı</span><span class="sxs-lookup"><span data-stu-id="88758-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="88758-178">1. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-178">Step 1</span></span>
<span data-ttu-id="88758-179">Etki alanı için özel anahtara sahip sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="88758-179">Upload the certificate with private key for the domain.</span></span> <span data-ttu-id="88758-180">Bu örnek için olacak `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="88758-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path to .pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="88758-181">2. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-181">Step 2</span></span>
<span data-ttu-id="88758-182">Sertifika yüklendikten sonra ana bilgisayar adını proxy'si için ana bilgisayar yapılandırma nesnesi oluşturun `api.contoso.net`, örnek sertifika yetkilisi için sağladığından `*.contoso.net` etki alanı.</span><span class="sxs-lookup"><span data-stu-id="88758-182">Once the certificate is uploaded, create a hostname configuration object for the proxy with a hostname of `api.contoso.net`, as the example certificate provides authority for the  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="88758-183">Ön uç yapılandırma için genel bir IP adresi oluşturun</span><span class="sxs-lookup"><span data-stu-id="88758-183">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="88758-184">Genel IP kaynağı oluşturun **Publicıp01** kaynak grubunda **apim-appGw-RG** Batı ABD bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="88758-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="88758-185">Hizmet başlatıldığında uygulama ağ geçidine bir IP adresi atanır.</span><span class="sxs-lookup"><span data-stu-id="88758-185">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="88758-186">Uygulama ağ geçidi yapılandırmasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="88758-186">Create application gateway configuration</span></span>

<span data-ttu-id="88758-187">Tüm yapılandırma öğeleri, uygulama ağ geçidi oluşturulmadan önce ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="88758-187">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="88758-188">Aşağıdaki adımlar uygulama ağ geçidi kaynağı için gerekli yapılandırma öğelerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="88758-188">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="88758-189">1. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-189">Step 1</span></span>

<span data-ttu-id="88758-190">**gatewayIP01** adlı bir uygulama ağ geçidi IP yapılandırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="88758-191">Application Gateway başladığında, yapılandırılan alt ağdan bir IP adresi alır ve ağ trafiğini arka uç IP havuzundaki IP adreslerine yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="88758-191">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="88758-192">Her örneğin bir IP adresi aldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="88758-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="88758-193">2. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-193">Step 2</span></span>

<span data-ttu-id="88758-194">Genel IP uç noktası için ön uç IP bağlantı noktası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88758-194">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="88758-195">Bu bağlantı noktası, son kullanıcılara bağlanan bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="88758-195">This port is the port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="88758-196">3. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-196">Step 3</span></span>

<span data-ttu-id="88758-197">Ön uç IP’sini genel IP uç noktası ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88758-197">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="88758-198">4. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-198">Step 4</span></span>

<span data-ttu-id="88758-199">Komut zincirinden geçen trafik yeniden şifrelemek ve şifresini çözmek için kullanılan uygulama ağ geçidi için sertifika yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88758-199">Configure the certificate for the Application Gateway, used to decrypt and re-encrypt the traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="88758-200">5. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-200">Step 5</span></span>

<span data-ttu-id="88758-201">HTTP dinleyicisi için uygulama ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-201">Create the HTTP listener for the Application Gateway.</span></span> <span data-ttu-id="88758-202">Ön uç IP yapılandırması, bağlantı noktası ve ssl sertifika atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88758-202">Assign the front-end IP configuration, port, and ssl certificate to it.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="88758-203">6. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-203">Step 6</span></span>

<span data-ttu-id="88758-204">API Management hizmeti için özel bir araştırma oluşturmak `ContosoApi` proxy etki alanı uç noktası.</span><span class="sxs-lookup"><span data-stu-id="88758-204">Create a custom probe to the API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="88758-205">Yolun `/status-0123456789abcdef` olan varsayılan, tüm API Management services üzerinde barındırılan bir sistem durumu uç.</span><span class="sxs-lookup"><span data-stu-id="88758-205">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span></span> <span data-ttu-id="88758-206">Ayarlama `api.contoso.net` SSL sertifikası ile güvenli hale getirmek için bir özel araştırma ana bilgisayar adı olarak.</span><span class="sxs-lookup"><span data-stu-id="88758-206">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="88758-207">Ana bilgisayar adı `contosoapi.azure-api.net` olan adlı bir hizmette, yapılandırılan varsayılan proxy ana bilgisayar adı `contosoapi` ortak Azure içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="88758-207">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="88758-208">7. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-208">Step 7</span></span>

<span data-ttu-id="88758-209">SSL etkin arka uç havuzu kaynaklardaki kullanılan sertifikayı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="88758-209">Upload the certificate to be used on the SSL-enabled backend pool resources.</span></span> <span data-ttu-id="88758-210">Bu, adım 4'te sağlanan aynı sertifikadır.</span><span class="sxs-lookup"><span data-stu-id="88758-210">This is the same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path to .cer file>
```

### <a name="step-8"></a><span data-ttu-id="88758-211">8. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-211">Step 8</span></span>

<span data-ttu-id="88758-212">Uygulama ağ geçidi için HTTP arka uç ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88758-212">Configure HTTP backend settings for the Application Gateway.</span></span> <span data-ttu-id="88758-213">Bu, daha sonra iptal arka uç istek için zaman aşımı sınırı ayarı içerir.</span><span class="sxs-lookup"><span data-stu-id="88758-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="88758-214">Bu değer, yoklama zaman aşımı farklıdır.</span><span class="sxs-lookup"><span data-stu-id="88758-214">This value is different from the probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="88758-215">9. Adım</span><span class="sxs-lookup"><span data-stu-id="88758-215">Step 9</span></span>

<span data-ttu-id="88758-216">Adlı bir arka uç IP adresi havuzu yapılandırmak **apimbackend** yukarıda iç sanal IP adresi API Management hizmeti, oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="88758-216">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="88758-217">10. adım</span><span class="sxs-lookup"><span data-stu-id="88758-217">Step 10</span></span>

<span data-ttu-id="88758-218">Bir kukla (mevcut olmayan) arka uç ayarlarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="88758-219">API Management uygulama ağ geçidi aracılığıyla kullanıma sunmak için istiyoruz değil API yolları isteklerine bu arka uç isabet ve 404 döndürür.</span><span class="sxs-lookup"><span data-stu-id="88758-219">Requests to API paths that we do not want to expose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="88758-220">Sahte arka uç HTTP ayarları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88758-220">Configure HTTP settings for the dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="88758-221">Sahte bir arka uç yapılandırma **dummyBackendPool**, bir FQDN adresine işaret eden **dummybackend.com**. Bu FQDN adresi sanal ağında yok.</span><span class="sxs-lookup"><span data-stu-id="88758-221">Configure a dummy backend **dummyBackendPool**, which points to a FQDN address **dummybackend.com**. This FQDN address does not exist in the virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="88758-222">Uygulama ağ geçidi için mevcut olmayan arka uç noktaları varsayılan olarak kullanacağı bir kural ayarı oluşturma **dummybackend.com** sanal ağda.</span><span class="sxs-lookup"><span data-stu-id="88758-222">Create a rule setting that the Application Gateway will use by default which points to the non-existent backend **dummybackend.com** in the Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="88758-223">11. adım</span><span class="sxs-lookup"><span data-stu-id="88758-223">Step 11</span></span>

<span data-ttu-id="88758-224">URL kuralı yolları arka uç havuzları için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88758-224">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="88758-225">Bu API'ları yalnızca bir kısmını herkese açık için API Yönetimi'nden seçerek sağlar.</span><span class="sxs-lookup"><span data-stu-id="88758-225">This enables selecting only some of the APIs from API Management for being exposed to the public.</span></span> <span data-ttu-id="88758-226">Örneğin, varsa `Echo API` (/ Yankı /) `Calculator API` (/calc/) vb. yapma yalnızca `Echo API` Internet'ten erişilebilir).</span><span class="sxs-lookup"><span data-stu-id="88758-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="88758-227">Aşağıdaki örnek, "/ Yankı /" yol yönlendirme trafiği için arka uç "apimProxyBackendPool" basit bir kural oluşturur.</span><span class="sxs-lookup"><span data-stu-id="88758-227">The following example creates a simple rule for the "/echo/" path routing traffic to the back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="88758-228">Yolun istiyoruz API Yönetimi'nden etkinleştirmek için yol kuralları eşleşmiyorsa, kural yol haritası yapılandırmasını da adlı bir varsayılan arka uç adres havuzu yapılandırır **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="88758-228">If the path doesn't match the path rules we want to enable from API Management, the rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="88758-229">Örneğin, http://api.contoso.net/calc/ * gider **dummyBackendPool** beklemediğiniz eşleşen trafik için varsayılan havuzu olarak tanımlanan.</span><span class="sxs-lookup"><span data-stu-id="88758-229">For example, http://api.contoso.net/calc/* goes to **dummyBackendPool** as it is defined as the default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="88758-230">Yukarıdaki adımı yolu yalnızca istekleri sağlar "/ echo" uygulama ağ geçidi üzerinden izin verilir.</span><span class="sxs-lookup"><span data-stu-id="88758-230">The above step ensures that only requests for the path "/echo" are allowed through the Application Gateway.</span></span> <span data-ttu-id="88758-231">API Yönetimi'nde yapılandırılmış diğer API'leri isteklerine Internet'ten erişilen uygulama geçidinden 404 hataları atar.</span><span class="sxs-lookup"><span data-stu-id="88758-231">Requests to other APIs configured in API Management will throw 404 errors from Application Gateway when accessed from the Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="88758-232">12. adımı</span><span class="sxs-lookup"><span data-stu-id="88758-232">Step 12</span></span>

<span data-ttu-id="88758-233">Yol tabanlı URL yönlendirmeyi kullanmak uygulama ağ geçidi için bir kuralı ayarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-233">Create a rule setting for the Application Gateway to use URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="88758-234">13. adım</span><span class="sxs-lookup"><span data-stu-id="88758-234">Step 13</span></span>

<span data-ttu-id="88758-235">Uygulama ağ geçidi için örnekleri ve boyutu sayısını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88758-235">Configure the number of instances and size for the Application Gateway.</span></span> <span data-ttu-id="88758-236">Burada kullanıyoruz [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) API Management kaynağının güvenliği artırmak için.</span><span class="sxs-lookup"><span data-stu-id="88758-236">Here we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="88758-237">14. adım</span><span class="sxs-lookup"><span data-stu-id="88758-237">Step 14</span></span>

<span data-ttu-id="88758-238">WAF "Önleme" modunda olacak şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="88758-238">Configure WAF to be in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="88758-239">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="88758-239">Create Application Gateway</span></span>

<span data-ttu-id="88758-240">Yukarıdaki adımlarda geçen tüm yapılandırma nesne içeren bir uygulama ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="88758-240">Create an Application Gateway with all the configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-the-api-management-proxy-hostname-to-the-public-dns-name-of-the-application-gateway-resource"></a><span data-ttu-id="88758-241">CNAME uygulama ağ geçidi kaynak ortak DNS adına API Management proxy konak adı</span><span class="sxs-lookup"><span data-stu-id="88758-241">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span></span>

<span data-ttu-id="88758-242">Ağ geçidi oluşturulduktan sonraki adım, iletişim için ön uç yapılandırması yapmaktır.</span><span class="sxs-lookup"><span data-stu-id="88758-242">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="88758-243">Genel IP kullanırken, uygulama ağ geçidi kullanımı kolay olmayabilir dinamik olarak atanmış bir DNS adı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="88758-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span></span> 

<span data-ttu-id="88758-244">Uygulama ağ geçidi DNS adı APIM proxy ana bilgisayar adını gösteren bir CNAME kaydı oluşturmak için kullanılması gereken (örneğin `api.contoso.net` Yukarıdaki örneklerde) bu DNS adı.</span><span class="sxs-lookup"><span data-stu-id="88758-244">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span></span> <span data-ttu-id="88758-245">Ön uç IP CNAME kaydını yapılandırmak için uygulama ağ geçidi ve Publicıpaddress öğesini kullanarak ilişkili IP/DNS adı ayrıntılarını alamadı.</span><span class="sxs-lookup"><span data-stu-id="88758-245">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span></span> <span data-ttu-id="88758-246">Ağ geçidi başlatmada VIP değişebileceği A kayıtlarını kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="88758-246">The use of A-records is not recommended since the VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="88758-247"><a name="summary"></a> Özeti</span><span class="sxs-lookup"><span data-stu-id="88758-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="88758-248">Azure API Management sanal ağ içinde yapılandırılmış bir tek ağ geçidi arabirimi barındırılan şirket içi olmalarından bağımsız veya bulutta tüm yapılandırılmış API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="88758-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span></span> <span data-ttu-id="88758-249">Uygulama ağ geçidi API Management ile tümleştirme, API Management örneği için bir ön olarak bir Web uygulaması güvenlik duvarı sağlama yanı sıra seçmeli olarak Internet üzerinden erişilebilir olması için belirli API'ler etkinleştirme esnekliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="88758-249">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span></span>

##<span data-ttu-id="88758-250"><a name="next-steps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="88758-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="88758-251">Azure uygulama ağ geçidi hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="88758-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="88758-252">Uygulama ağ geçidi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="88758-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="88758-253">Uygulama ağ geçidi Web uygulaması güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="88758-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="88758-254">Yol tabanlı yönlendirme kullanarak uygulama ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="88758-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="88758-255">API Management ve sanal ağlar hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="88758-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="88758-256">Yalnızca sanal ağ içinde kullanılabilir API Management kullanma</span><span class="sxs-lookup"><span data-stu-id="88758-256">Using API Management available only within the VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="88758-257">VNET içinde API Management kullanma</span><span class="sxs-lookup"><span data-stu-id="88758-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
