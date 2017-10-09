---
title: "aaaConfigure son tooend SSL Azure uygulama ağ geçidi ile | Microsoft Docs"
description: "Bu makalede nasıl tooconfigure sona tooend SSL Azure Resource Manager PowerShell kullanarak uygulama ağ geçidi ile açıklanır"
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
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="8c0b7-103">Uygulama ağ geçidi PowerShell kullanarak ile son tooend SSL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8c0b7-103">Configure end tooend SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="8c0b7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8c0b7-104">Overview</span></span>

<span data-ttu-id="8c0b7-105">Uygulama ağ geçidi destekler tooend şifreleme trafik sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-105">Application Gateway supports end tooend encryption of traffic.</span></span> <span data-ttu-id="8c0b7-106">Uygulama ağ geçidi bunu hello uygulama ağ geçidi hello SSL bağlantısını sonlandırarak yapar.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-106">Application Gateway does this by terminating hello SSL connection at hello application gateway.</span></span> <span data-ttu-id="8c0b7-107">Hello ağ geçidi sonra toohello trafiği hello paket yeniden şifreler ve tanımlanan hello yönlendirme kurallarına göre hello paket toohello uygun arka uç iletir hello yönlendirme kuralları uygular.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-107">hello gateway then applies hello routing rules toohello traffic, re-encrypts hello packet, and forwards hello packet toohello appropriate backend based on hello routing rules defined.</span></span> <span data-ttu-id="8c0b7-108">Merhaba web sunucusundan herhangi bir yanıt hello gider aynı işlemi geri toohello son kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-108">Any response from hello web server goes through hello same process back toohello end user.</span></span>

<span data-ttu-id="8c0b7-109">Başka bir özellik, bu uygulama ağ geçidi özel SSL seçenekleri tanımlama destekler.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-109">Another feature that application gateway supports defining custom SSL options.</span></span> <span data-ttu-id="8c0b7-110">Uygulama Ağ Geçidi Protokolü sürüm aşağıdaki devre dışı bırakma hello destekler; **TLSv1.0**, **TLSv1.1**, ve **TLSv1.2** de şifre paketleri toouse ve hello tercih sırasına göre hello tanımlama.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-110">Application Gateway supports disabling hello following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2** as well defining hello which cipher suites toouse and hello order of preference.</span></span>  <span data-ttu-id="8c0b7-111">yapılandırılabilir SSL seçenekleri hakkında daha fazla toolearn ziyaret [SSL ilkesine genel bakış](application-gateway-SSL-policy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8c0b7-111">toolearn more about configurable SSL options, visit [SSL Policy overview](application-gateway-SSL-policy-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8c0b7-112">SSL 2.0 ve SSL 3.0 varsayılan olarak devre dışıdır ve etkinleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-112">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="8c0b7-113">Bunlar Güvensiz olarak kabul edilir ve uygulama ağ geçidi ile kullanılan mümkün toobe değildir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-113">They are considered unsecure and are not able toobe used with Application Gateway.</span></span>

![Senaryo görüntüsü][scenario]

## <a name="scenario"></a><span data-ttu-id="8c0b7-115">Senaryo</span><span class="sxs-lookup"><span data-stu-id="8c0b7-115">Scenario</span></span>

<span data-ttu-id="8c0b7-116">Bu senaryoda, nasıl kullanarak bir uygulama ağ geçidi toocreate sona tooend SSL öğrenin PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-116">In this scenario, you learn how toocreate an application gateway using end tooend SSL using PowerShell.</span></span>

<span data-ttu-id="8c0b7-117">Bu senaryo aşağıdakileri yapar:</span><span class="sxs-lookup"><span data-stu-id="8c0b7-117">This scenario will:</span></span>

* <span data-ttu-id="8c0b7-118">Adlı bir kaynak grubu oluşturmak **appgw-rg**</span><span class="sxs-lookup"><span data-stu-id="8c0b7-118">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="8c0b7-119">Adlı bir sanal ağ oluşturma **appgwvnet** 10.0.0.0/16 bir adres alanı ile.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-119">Create a virtual network named **appgwvnet** with an address space of 10.0.0.0/16.</span></span>
* <span data-ttu-id="8c0b7-120">Adlı iki alt ağ oluşturmak **appgwsubnet** ve **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-120">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="8c0b7-121">Bir küçük uygulama ağ geçidi destek bitiş tooend SSL şifrelemesi bu sınırları SSL protokolleri sürümlerini ve şifre paketleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-121">Create a small application gateway supporting end tooend SSL encryption that limits SSL protocols versions and cipher suites.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8c0b7-122">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="8c0b7-122">Before you begin</span></span>

<span data-ttu-id="8c0b7-123">bir uygulama ağ geçidi ile tooconfigure son tooend SSL, bir sertifika hello ağ geçidi için gereklidir ve sertifikaları hello arka uç sunucuları için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-123">tooconfigure end tooend SSL with an application gateway, a certificate is required for hello gateway and certificates are required for hello backend servers.</span></span> <span data-ttu-id="8c0b7-124">SSL ile kullanılan tooencrypt ve şifre çözme hello gönderilen trafiğin tooit Hello ağ geçidi sertifikasıdır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-124">hello gateway certificate is used tooencrypt and decrypt hello traffic sent tooit using SSL.</span></span> <span data-ttu-id="8c0b7-125">Merhaba ağ geçidi sertifikası kişisel bilgi değişimi (pfx) biçiminde toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-125">hello gateway certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="8c0b7-126">Bu dosya biçimi, hangi hello uygulama ağ geçidi tooperform hello şifreleme ve şifre çözme trafik tarafından gerekli anahtar toobe dışarı Merhaba özel sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-126">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

<span data-ttu-id="8c0b7-127">End tooend SSL şifreleme hello arka uç uygulama ağ geçidi ile Güvenilenler listesine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-127">For end tooend SSL encryption hello backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="8c0b7-128">Bu, hello arka uçlarını toohello uygulama ağ geçidi hello ortak sertifikasını karşıya yükleyerek gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-128">This is done by uploading hello public certificate of hello backends toohello application gateway.</span></span> <span data-ttu-id="8c0b7-129">Bu, o hello uygulama ağ geçidi yalnızca bilinen arka uç örnekleri ile iletişim kurar sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-129">This ensures that hello application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="8c0b7-130">Bu daha fazla hello son tooend iletişimin güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-130">This further secures hello end tooend communication.</span></span>

<span data-ttu-id="8c0b7-131">Bu işlem aşağıdaki adımları hello açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="8c0b7-131">This process is described in hello following steps:</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="8c0b7-132">Merhaba kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="8c0b7-132">Create hello Resource Group</span></span>

<span data-ttu-id="8c0b7-133">Bu bölümde hello uygulama ağ geçidi içeren bir kaynak grubu oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-133">This section walks you through creating a resource group, that contains hello application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c0b7-134">1. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-134">Step 1</span></span>

<span data-ttu-id="8c0b7-135">Tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-135">Log in tooyour Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="8c0b7-136">2. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-136">Step 2</span></span>

<span data-ttu-id="8c0b7-137">Bu senaryo için Hello abonelik toouse seçin.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-137">Select hello subscription toouse for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="8c0b7-138">3. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-138">Step 3</span></span>

<span data-ttu-id="8c0b7-139">Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).</span><span class="sxs-lookup"><span data-stu-id="8c0b7-139">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="8c0b7-140">Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c0b7-140">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="8c0b7-141">Merhaba aşağıdaki örnek bir sanal ağ ve iki alt ağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-141">hello following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="8c0b7-142">Bir alt ağda kullanılan toohold hello uygulama ağ geçidi ' dir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-142">One subnet is used toohold hello application gateway.</span></span> <span data-ttu-id="8c0b7-143">Merhaba diğer alt hello arka uçlarını barındırma hello web uygulaması için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-143">hello other subnet is used for hello backends hosting hello web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c0b7-144">1. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-144">Step 1</span></span>

<span data-ttu-id="8c0b7-145">Merhaba alt hello uygulama ağ geçidi kendisi için kullanılması için bir adres aralığı atayın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-145">Assign an address range for hello subnet be used for hello Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="8c0b7-146">Uygulama ağ geçidi için yapılandırılmış alt ağlar doğru boyutta olması.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-146">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="8c0b7-147">Bir uygulama ağ geçidi too10 örneği için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-147">An application gateway can be configured for up too10 instances.</span></span> <span data-ttu-id="8c0b7-148">Her bir örnek hello alt ağdan bir IP adresi alır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-148">Each instance takes one IP address from hello subnet.</span></span> <span data-ttu-id="8c0b7-149">Çok küçük bir alt ağın, bir uygulama ağ geçidi ölçeklendirme olumsuz yönde etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-149">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="8c0b7-150">2. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-150">Step 2</span></span>

<span data-ttu-id="8c0b7-151">Merhaba arka uç adres havuzu için kullanılan bir adres aralığı toobe atayın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-151">Assign an address range toobe used for hello Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="8c0b7-152">3. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-152">Step 3</span></span>

<span data-ttu-id="8c0b7-153">Önceki adımları hello tanımlanan hello alt ağlar ile bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-153">Create a virtual network with hello subnets defined in hello preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="8c0b7-154">4. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-154">Step 4</span></span>

<span data-ttu-id="8c0b7-155">Aşağıdaki adımları hello kullanılan hello sanal ağ kaynak ve alt ağ kaynakları toobe Al:</span><span class="sxs-lookup"><span data-stu-id="8c0b7-155">Retrieve hello virtual network resource and subnet resources toobe used in hello following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="8c0b7-156">Merhaba ön uç yapılandırma için genel bir IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="8c0b7-156">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="8c0b7-157">Merhaba uygulama ağ geçidi için kullanılan bir ortak IP kaynak toobe oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-157">Create a public IP resource toobe used for hello application gateway.</span></span> <span data-ttu-id="8c0b7-158">Bu genel IP adresi kullanılır aşağıdaki adımı.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-158">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="8c0b7-159">Uygulama ağ geçidi hello tanımlı bir etki alanı etiketi ile oluşturulan bir ortak IP adresi kullanımını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-159">Application Gateway does not support hello use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="8c0b7-160">Yalnızca bir ortak IP adresi dinamik olarak oluşturulan etki alanı etiketi ile desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-160">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="8c0b7-161">Merhaba uygulama ağ geçidi için bir kolay dns adı gerekiyorsa, önerilen toouse bir CNAME kaydı bir diğer ad olarak.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-161">If you require a friendly dns name for hello application gateway, it is recommended toouse a CNAME record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="8c0b7-162">Uygulama ağ geçidi yapılandırma nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="8c0b7-162">Create an application gateway configuration object</span></span>

<span data-ttu-id="8c0b7-163">Tüm yapılandırma öğeleri hello uygulama ağ geçidi oluşturmadan önce ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-163">All configuration items are set before creating hello application gateway.</span></span> <span data-ttu-id="8c0b7-164">Merhaba aşağıdaki adımları hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-164">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c0b7-165">1. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-165">Step 1</span></span>

<span data-ttu-id="8c0b7-166">Uygulama ağ geçidi IP yapılandırması oluşturun, bu ayarı, hangi alt hello uygulama ağ geçidi kullanan yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-166">Create an application gateway IP configuration, this setting configures what subnet hello application gateway uses.</span></span> <span data-ttu-id="8c0b7-167">Application gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-167">When application gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="8c0b7-168">Her örneğin bir IP adresi aldığını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-168">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="8c0b7-169">2. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-169">Step 2</span></span>

<span data-ttu-id="8c0b7-170">Bu ayar hello uygulama ağ geçidi bir özel veya genel IP adresi toohello ön ucu eşlemeleri, ön uç IP yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-170">Create a front-end IP configuration, this setting maps a private or public ip address toohello front end of hello application gateway.</span></span> <span data-ttu-id="8c0b7-171">adımı aşağıdaki hello hello ön uç IP yapılandırmasını adımıyla önceki hello hello genel IP adresi ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-171">hello following step associates hello public IP address in hello preceding step with hello front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="8c0b7-172">3. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-172">Step 3</span></span>

<span data-ttu-id="8c0b7-173">Merhaba arka uç IP adresi havuzu ile Merhaba arka uç web sunucularının hello IP adreslerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-173">Configure hello back-end IP address pool with hello IP addresses of hello backend web servers.</span></span> <span data-ttu-id="8c0b7-174">Bu IP adreslerine hello ön uç IP uç noktasından gelen ağ trafiğini hello aldığınız hello IP adresleridir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-174">These IP addresses are hello IP addresses that receive hello network traffic that comes from hello front-end IP endpoint.</span></span> <span data-ttu-id="8c0b7-175">Kendi uygulama IP adresi bitiş IP adreslerini tooadd aşağıdaki hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-175">You replace hello following IP addresses tooadd your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="8c0b7-176">Bir tam etki alanı adı (FQDN) da geçerli bir değer hello arka uç sunucuları için bir IP adresi yerine hello - BackendFqdns anahtar kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-176">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for hello backend servers by using hello -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="8c0b7-177">4. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-177">Step 4</span></span>

<span data-ttu-id="8c0b7-178">Merhaba ön uç IP bağlantı noktası hello genel IP uç noktası için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-178">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="8c0b7-179">Bu bağlantı noktası, son kullanıcılara bağlanan hello bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-179">This port is hello port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="8c0b7-180">5. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-180">Step 5</span></span>

<span data-ttu-id="8c0b7-181">Merhaba hello uygulama ağ geçidi için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-181">Configure hello certificate for hello application gateway.</span></span> <span data-ttu-id="8c0b7-182">Bu sertifika kullanılan toodecrypt ve hello uygulama ağ geçidi üzerinde hello trafiğini yeniden şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-182">This certificate is used toodecrypt and re-encrypt hello traffic on hello application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="8c0b7-183">Bu örnek, SSL bağlantısı için kullanılan hello sertifika yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-183">This sample configures hello certificate used for SSL connection.</span></span> <span data-ttu-id="8c0b7-184">Merhaba sertifikanın .pfx biçiminde toobe gerekir ve hello parola 4 too12 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-184">hello certificate needs toobe in .pfx format, and hello password must be between 4 too12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="8c0b7-185">6. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-185">Step 6</span></span>

<span data-ttu-id="8c0b7-186">Merhaba HTTP dinleyicisi hello uygulama ağ geçidi için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-186">Create hello HTTP listener for hello application gateway.</span></span> <span data-ttu-id="8c0b7-187">Merhaba ön uç IP yapılandırması, bağlantı noktası ve SSL sertifika toouse atayın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-187">Assign hello front-end ip configuration, port, and SSL certificate toouse.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="8c0b7-188">7. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-188">Step 7</span></span>

<span data-ttu-id="8c0b7-189">Arka uç havuzu kaynaklarına SSL Hello üzerinde kullanılan toobe etkin hello sertifikasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-189">Upload hello certificate toobe used on hello SSL enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="8c0b7-190">Merhaba varsayılan araştırmasını alır hello ortak anahtar hello **varsayılan** SSL bağlaması hello arka uç bilgisayarın IP adresi ve toohello ortak anahtar değeri burada aldığı karşılaştırır hello ortak anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-190">hello default probe gets hello public key from hello **default** SSL binding on hello back-end's IP address and compares hello public key value it receives toohello public key value you provide here.</span></span> <span data-ttu-id="8c0b7-191">Merhaba alınan ortak anahtar mutlaka hedeflenen hello site toowhich trafik akışına olabilir **varsa** ana bilgisayar üstbilgilerinin ve SNI hello arka uçta kullanma.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-191">hello retrieved public key may not necessarily be hello intended site toowhich traffic flows **if** you are using host headers and SNI on hello back-end.</span></span> <span data-ttu-id="8c0b7-192">Emin değilseniz, hangi sertifikanın hello için kullanılan hello arka uçları tooconfirm https://127.0.0.1/ ziyaret **varsayılan** SSL bağlaması.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-192">If in doubt, visit https://127.0.0.1/ on hello back-ends tooconfirm which certificate is used for hello **default** SSL binding.</span></span> <span data-ttu-id="8c0b7-193">Bu bölümde bu istek Hello ortak anahtar kullanın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-193">Use hello public key from that request in this section.</span></span> <span data-ttu-id="8c0b7-194">Ana bilgisayar üstbilgilerinin ve SNI HTTPS bağlantılarına kullanıyorsanız ve, yanıt ve sertifikayı el ile tarayıcı istek toohttps://127.0.0.1/ hello arka ucunda alırsınız olmayan bir varsayılan SSL bağlaması hello arka ucunda ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-194">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request toohttps://127.0.0.1/ on hello back-ends, you must set up a default SSL binding on hello back-ends.</span></span> <span data-ttu-id="8c0b7-195">Bunu yaparsanız, araştırmalar başarısız ve hello arka uç izin verilenler listesinde değil.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-195">If you do not do so, probes fail and hello back-end is not whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="8c0b7-196">Bu adımda sağlanan hello sertifika hello ortak anahtarı hello pfx sertifika hello arka uç üzerinde mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-196">hello certificate provided in this step should be hello public key of hello pfx cert present on hello backend.</span></span> <span data-ttu-id="8c0b7-197">Merhaba arka uç sunucusunda yüklü hello sertifika (Merhaba kök sertifikanın değil) verin. CER biçimlendirin ve bu adımda kullanın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-197">Export hello certificate (not hello root certificate) installed on hello backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="8c0b7-198">Bu adım whitelists hello uygulama ağ geçidi ile arka uç hello.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-198">This step whitelists hello backend with hello application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="8c0b7-199">8. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-199">Step 8</span></span>

<span data-ttu-id="8c0b7-200">Merhaba uygulama ağ geçidi arka uç http ayarları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-200">Configure hello application gateway back-end http settings.</span></span> <span data-ttu-id="8c0b7-201">Adım toohello http ayarları önceki hello karşıya hello sertifika atayın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-201">Assign hello certificate uploaded in hello preceding step toohello http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="8c0b7-202">9. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-202">Step 9</span></span>

<span data-ttu-id="8c0b7-203">Merhaba yük dengeleyici davranışını yapılandıran Yük Dengeleyiciyi yönlendirme kuralını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-203">Create a load balancer routing rule that configures hello load balancer behavior.</span></span> <span data-ttu-id="8c0b7-204">Bu örnekte, bir temel hepsini bir kural oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-204">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="8c0b7-205">10. adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-205">Step 10</span></span>

<span data-ttu-id="8c0b7-206">Merhaba uygulama ağ geçidi Hello örnek boyutunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-206">Configure hello instance size of hello application gateway.</span></span>  <span data-ttu-id="8c0b7-207">Merhaba kullanılabilir boyutları: **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-207">hello available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="8c0b7-208">Kapasite için 1 ile 10 hello değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-208">For capacity, hello available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="8c0b7-209">Test amacıyla örnek sayısını 1 seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-209">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="8c0b7-210">Herhangi bir örneğine altında iki örnek sayısı tooknow hello tarafından SLA kapsamında değildir ve bu nedenle önerilmez önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-210">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="8c0b7-211">Küçük ağ geçitleri geliştirme test ve üretim amaçları için kullanılan toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-211">Small gateways are toobe used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="8c0b7-212">11. adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-212">Step 11</span></span>

<span data-ttu-id="8c0b7-213">Uygulama ağ geçidi Hello üzerinde kullanılan hello SSL İlkesi toobe yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-213">Configure hello SSL policy toobe used on hello Application Gateway.</span></span> <span data-ttu-id="8c0b7-214">Uygulama ağ geçidi hello özelliği tooset en düşük sürüm SSL protokol sürümleri için destekler.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-214">Application Gateway supports hello ability tooset a minimum version for SSL protocol versions.</span></span>

<span data-ttu-id="8c0b7-215">Merhaba aşağıdaki değerleri tanımlanabilir protokol sürümleri listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-215">hello following values are a list of protocol versions that can be defined.</span></span>

* <span data-ttu-id="8c0b7-216">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="8c0b7-216">**TLSv1_0**</span></span>
* <span data-ttu-id="8c0b7-217">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="8c0b7-217">**TLSv1_1**</span></span>
* <span data-ttu-id="8c0b7-218">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="8c0b7-218">**TLSv1_2**</span></span>

<span data-ttu-id="8c0b7-219">Ayarlar hello en düşük protokol sürümü çok**TLSv1_2** ve sağlar **TLS\_ECDHE\_ECDSA\_ile\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_ile\_AES\_256\_GCM\_SHA384**ve **TLS\_RSA\_ile\_AES\_128\_GCM\_SHA256** yalnızca.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-219">Sets hello minimum protocol version too**TLSv1_2** and enables **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** only.</span></span>

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="8c0b7-220">Merhaba uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8c0b7-220">Create hello Application Gateway</span></span>

<span data-ttu-id="8c0b7-221">Adımları önceki tüm hello kullanarak hello uygulama ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-221">Using all hello preceding steps, create hello Application Gateway.</span></span> <span data-ttu-id="8c0b7-222">Merhaba ağ geçidi Hello oluşturulmasını uzun süren bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-222">hello creation of hello gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="8c0b7-223">Mevcut bir uygulama ağ geçidi SSL protokolü sürümlerinde sınırla</span><span class="sxs-lookup"><span data-stu-id="8c0b7-223">Limit SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="8c0b7-224">Merhaba önceki son tooend SSL ile uygulama oluşturma ve belirli SSL protokol sürümleri devre dışı bırakma adımlar.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-224">hello preceding steps take you through creating an application with end tooend SSL and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="8c0b7-225">Merhaba aşağıdaki örnekte belirli SSL ilkeleri var olan bir uygulama ağ geçidi üzerinde devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-225">hello following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c0b7-226">1. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-226">Step 1</span></span>

<span data-ttu-id="8c0b7-227">Merhaba uygulama ağ geçidi tooupdate alın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-227">Retrieve hello application gateway tooupdate.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="8c0b7-228">2. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-228">Step 2</span></span>

<span data-ttu-id="8c0b7-229">SSL ilke tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-229">Define an SSL policy.</span></span> <span data-ttu-id="8c0b7-230">Merhaba, aşağıdaki örneğine TLSv1.0 ve TLSv1.1 devre dışı bırakılır ve şifre paketleri hello **TLS\_ECDHE\_ECDSA\_ile\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_ile\_AES\_256\_GCM\_SHA384**, ve  **TLS\_RSA\_ile\_AES\_128\_GCM\_SHA256** hello izin yalnızca olanlardır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-230">In hello following example, TLSv1.0 and TLSv1.1 are disabled and hello cipher suites **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, and **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** are hello only ones allowed.</span></span>

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a><span data-ttu-id="8c0b7-231">3. Adım</span><span class="sxs-lookup"><span data-stu-id="8c0b7-231">Step 3</span></span>

<span data-ttu-id="8c0b7-232">Son olarak, hello ağ geçidini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-232">Finally, update hello gateway.</span></span> <span data-ttu-id="8c0b7-233">Önemli toonote bu son adım uzun çalışan bir görev olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-233">It is important toonote that this last step is a long running task.</span></span> <span data-ttu-id="8c0b7-234">Tamamlandığında, son tooend SSL hello uygulama ağ geçidinde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-234">When it is done, end tooend SSL is configured on hello application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="8c0b7-235">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="8c0b7-235">Get application gateway DNS name</span></span>

<span data-ttu-id="8c0b7-236">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-236">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="8c0b7-237">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-237">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="8c0b7-238">hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-238">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="8c0b7-239">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8c0b7-239">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="8c0b7-240">toodo Bu, alma ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adı.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-240">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="8c0b7-241">Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-241">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="8c0b7-242">Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="8c0b7-242">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8c0b7-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8c0b7-243">Next steps</span></span>

<span data-ttu-id="8c0b7-244">Web uygulamalarınızın uygulama ağ geçidi üzerinden Web uygulaması güvenlik duvarı ile Merhaba güvenlik ziyaret ederek artırma hakkında bilgi edinin [Web uygulaması güvenlik duvarı genel bakış](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8c0b7-244">Learn about hardening hello security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
