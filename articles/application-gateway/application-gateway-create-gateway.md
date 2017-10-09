---
title: "aaaCreate, başlatma veya bir uygulama ağ geçidini silme | Microsoft Docs"
description: "Bu sayfa toocreate, yapılandırmak, başlatın ve bir Azure uygulama ağ geçidini silme yönergelerini sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="62dd4-103">PowerShell ile bir uygulama ağ geçidi oluşturma, başlatma veya silme</span><span class="sxs-lookup"><span data-stu-id="62dd4-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="62dd4-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="62dd4-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="62dd4-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="62dd4-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="62dd4-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="62dd4-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="62dd4-107">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="62dd4-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="62dd4-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="62dd4-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="62dd4-109">Azure Application Gateway, bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="62dd4-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="62dd4-110">Merhaba Bulut veya şirket içinde olmalarından bağımsız yük devretme, HTTP isteklerini, farklı sunucular arasında performans amaçlı yönlendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="62dd4-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="62dd4-111">Application Gateway; HTTP yük dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) boşaltma, özel sistem durumu araştırmaları, çoklu site desteği gibi birçok Application Delivery Controller (ADC) özelliği sunar.</span><span class="sxs-lookup"><span data-stu-id="62dd4-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="62dd4-112">toofind desteklenen özelliklerin tam bir listesi ziyaret [uygulama ağ geçidi'ne genel bakış](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="62dd4-112">toofind a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="62dd4-113">Bu makalede hello adımları toocreate anlatılmaktadır, yapılandırmak, başlatmak ve bir uygulama ağ geçidini silin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="62dd4-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="62dd4-114">Before you begin</span></span>

1. <span data-ttu-id="62dd4-115">Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-115">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="62dd4-116">Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="62dd4-116">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="62dd4-117">Varolan bir sanal ağınız varsa, mevcut bir boş alt seçin veya hello uygulama ağ geçidi tarafından kullanılmak üzere yalnızca varolan sanal ağınızda yeni bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="62dd4-118">Merhaba uygulama ağ geçidi tooa farklı sanal ağı dağıtamazsınız daha hello kaynak vnet eşlemesi kullanılmadığı sürece hello uygulama ağ geçidi arkasında toodeploy düşündüğünüz.</span><span class="sxs-lookup"><span data-stu-id="62dd4-118">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway unless vnet peering is used.</span></span> <span data-ttu-id="62dd4-119">toolearn daha ziyaret [Vnet eşlemesi](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="62dd4-119">toolearn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="62dd4-120">Geçerli bir alt ağla çalışan bir sanal ağa sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="62dd4-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="62dd4-121">Hiçbir sanal makine veya Bulut dağıtımları hello alt kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-121">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="62dd4-122">Merhaba uygulama ağ geçidi tek başına bir sanal ağ alt ağında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="62dd4-122">hello application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="62dd4-123">toouse hello uygulama ağ geçidi yapılandırma hello sunucular mevcut olmalıdır veya hello sanal ağ veya genel IP/VIP'ye ile oluşturulan uç noktaları atadınız.</span><span class="sxs-lookup"><span data-stu-id="62dd4-123">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="62dd4-124">Gerekli toocreate bir uygulama ağ geçidi nedir?</span><span class="sxs-lookup"><span data-stu-id="62dd4-124">What is required toocreate an application gateway?</span></span>

<span data-ttu-id="62dd4-125">Merhaba kullandığınızda `New-AzureApplicationGateway` komutu toocreate hello uygulama ağ geçidi, herhangi bir yapılandırma bu noktada ayarlanır ve yeni oluşturulan hello kaynak yapılandırılmış XML veya bir yapılandırma nesnesi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="62dd4-125">When you use hello `New-AzureApplicationGateway` command toocreate hello application gateway, no configuration is set at this point and hello newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="62dd4-126">Merhaba değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="62dd4-126">hello values are:</span></span>

* <span data-ttu-id="62dd4-127">**Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="62dd4-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="62dd4-128">listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="62dd4-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="62dd4-129">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="62dd4-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="62dd4-130">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="62dd4-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="62dd4-131">**Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="62dd4-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="62dd4-132">Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="62dd4-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="62dd4-133">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="62dd4-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="62dd4-134">**Kural:** hello kural hello dinleyicisi ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler.</span><span class="sxs-lookup"><span data-stu-id="62dd4-134">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="62dd4-135">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="62dd4-135">Create an application gateway</span></span>

<span data-ttu-id="62dd4-136">bir uygulama ağ geçidi toocreate:</span><span class="sxs-lookup"><span data-stu-id="62dd4-136">toocreate an application gateway:</span></span>

1. <span data-ttu-id="62dd4-137">Uygulama ağ geçidi kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="62dd4-138">Bir XML yapılandırma dosyası veya yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="62dd4-139">Hello yapılandırma toohello yeni oluşturulmuş uygulama ağ geçidi kaynağına uygulayın.</span><span class="sxs-lookup"><span data-stu-id="62dd4-139">Commit hello configuration toohello newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="62dd4-140">Uygulama ağ geçidiniz için özel bir araştırma tooconfigure gerekirse bkz [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="62dd4-140">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="62dd4-141">Daha fazla bilgi için [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) konusunu inceleyin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Senaryo örneği][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="62dd4-143">Bir uygulama ağ geçidi kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="62dd4-143">Create an application gateway resource</span></span>

<span data-ttu-id="62dd4-144">toocreate hello ağ geçidi, kullanım hello `New-AzureApplicationGateway` hello değerleri kendi değerlerinizle değiştirerek cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="62dd4-144">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="62dd4-145">Merhaba ağ geçidi için fatura bu noktada başlatılmaz.</span><span class="sxs-lookup"><span data-stu-id="62dd4-145">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="62dd4-146">Merhaba ağ geçidi başarıyla başlatıldığında faturalama bir sonraki adımda başlar.</span><span class="sxs-lookup"><span data-stu-id="62dd4-146">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="62dd4-147">Merhaba aşağıdaki örnek bir uygulama ağ geçidi "testvnet1" ve "subnet-1" adlı bir alt ağ olarak adlandırılan bir sanal ağ kullanarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="62dd4-147">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="62dd4-148">*Description*, *InstanceCount* ve *GatewaySize* tercihe bağlı parametrelerdir.</span><span class="sxs-lookup"><span data-stu-id="62dd4-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="62dd4-149">ağ geçidi hello toovalidate oluşturuldu, hello kullanabilirsiniz `Get-AzureApplicationGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="62dd4-149">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="62dd4-150">Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir.</span><span class="sxs-lookup"><span data-stu-id="62dd4-150">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="62dd4-151">Merhaba için varsayılan değer *GatewaySize* Orta'dır.</span><span class="sxs-lookup"><span data-stu-id="62dd4-151">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="62dd4-152">Small, Medium ve Large seçenekleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="62dd4-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="62dd4-153">*VirtualIPs* ve *DnsName* hello ağ geçidi henüz başlatılmamış olduğundan boş olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="62dd4-153">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="62dd4-154">Merhaba ağ geçidi çalışır durumda hello olduğunda bunlar oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="62dd4-154">These are created once hello gateway is in hello running state.</span></span>

## <a name="configure-hello-application-gateway"></a><span data-ttu-id="62dd4-155">Merhaba uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="62dd4-155">Configure hello application gateway</span></span>

<span data-ttu-id="62dd4-156">XML veya bir yapılandırma nesnesi kullanarak hello uygulama ağ geçidini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62dd4-156">You can configure hello application gateway by using XML or a configuration object.</span></span>

### <a name="configure-hello-application-gateway-by-using-xml"></a><span data-ttu-id="62dd4-157">XML kullanarak Hello uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="62dd4-157">Configure hello application gateway by using XML</span></span>

<span data-ttu-id="62dd4-158">Aşağıdaki örneğine hello, tüm uygulama ağ geçidi ayarları bir XML dosyası tooconfigure kullanın ve toohello uygulama ağ geçidi kaynağına uygulayın.</span><span class="sxs-lookup"><span data-stu-id="62dd4-158">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="62dd4-159">1. Adım</span><span class="sxs-lookup"><span data-stu-id="62dd4-159">Step 1</span></span>

<span data-ttu-id="62dd4-160">Metin tooNotepad aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="62dd4-160">Copy hello following text tooNotepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="62dd4-161">Merhaba yapılandırma öğeleri için hello parantez Hello değerlerini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-161">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="62dd4-162">Merhaba dosyası .xml. uzantısıyla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-162">Save hello file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62dd4-163">Http veya Https Hello protokol öğesi büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="62dd4-163">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="62dd4-164">Aşağıdaki örneğine hello nasıl toouse bir yapılandırma dosyası hello uygulama ağ geçidi yukarı tooset gösterir.</span><span class="sxs-lookup"><span data-stu-id="62dd4-164">hello following example shows how toouse a configuration file tooset up hello application gateway.</span></span> <span data-ttu-id="62dd4-165">Merhaba örnek yük ortak bağlantı noktası 80 üzerinde HTTP trafiği dengeler ve ağ trafiğini iki IP adresi arasında tooback uç bağlantı noktası 80 gönderir.</span><span class="sxs-lookup"><span data-stu-id="62dd4-165">hello example load balances HTTP traffic on public port 80 and sends network traffic tooback-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a><span data-ttu-id="62dd4-166">2. Adım</span><span class="sxs-lookup"><span data-stu-id="62dd4-166">Step 2</span></span>

<span data-ttu-id="62dd4-167">Ardından, hello uygulama ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="62dd4-167">Next, set hello application gateway.</span></span> <span data-ttu-id="62dd4-168">Kullanım hello `Set-AzureApplicationGatewayConfig` cmdlet'ini bir XML yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="62dd4-168">Use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="62dd4-169">Bir yapılandırma nesnesi kullanarak Hello uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="62dd4-169">Configure hello application gateway by using a configuration object</span></span>

<span data-ttu-id="62dd4-170">Aşağıdaki örnek hello nasıl tooconfigure hello uygulama ağ geçidi yapılandırma nesnesi kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="62dd4-170">hello following example shows how tooconfigure hello application gateway by using configuration objects.</span></span> <span data-ttu-id="62dd4-171">Tüm yapılandırma öğeleri ayrı ayrı yapılandırılır ve daha sonra eklenen tooan uygulama ağ geçidi yapılandırma nesnesi.</span><span class="sxs-lookup"><span data-stu-id="62dd4-171">All configuration items must be configured individually and then added tooan application gateway configuration object.</span></span> <span data-ttu-id="62dd4-172">Merhaba Yapılandırma nesnesini oluşturduktan sonra hello kullan `Set-AzureApplicationGateway` komutu toocommit hello yapılandırma toohello daha önce oluşturduğunuz uygulama ağ geçidi kaynağı.</span><span class="sxs-lookup"><span data-stu-id="62dd4-172">After creating hello configuration object, you use hello `Set-AzureApplicationGateway` command toocommit hello configuration toohello previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="62dd4-173">Bir değer tooeach yapılandırma nesnesi atamadan önce depolama için PowerShell ne tür bir nesneyi kullanan toodeclare gerekir.</span><span class="sxs-lookup"><span data-stu-id="62dd4-173">Before assigning a value tooeach configuration object, you need toodeclare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="62dd4-174">Merhaba ilk satırı toocreate hello ayrı ayrı öğeler tanımlar ne `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="62dd4-174">hello first line toocreate hello individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="62dd4-175">1. Adım</span><span class="sxs-lookup"><span data-stu-id="62dd4-175">Step 1</span></span>

<span data-ttu-id="62dd4-176">Tüm bireysel yapılandırma öğelerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-176">Create all individual configuration items.</span></span>

<span data-ttu-id="62dd4-177">Merhaba ön uç IP hello aşağıdaki örnekte gösterildiği gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-177">Create hello front-end IP as shown in hello following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="62dd4-178">Merhaba ön uç bağlantı noktası hello aşağıdaki örnekte gösterildiği gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-178">Create hello front-end port as shown in hello following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="62dd4-179">Merhaba arka uç sunucu havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-179">Create hello back-end server pool.</span></span>

<span data-ttu-id="62dd4-180">Merhaba sonraki örnekte gösterildiği gibi toohello arka uç sunucu havuzuna eklenmiş hello IP adreslerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="62dd4-180">Define hello IP addresses that are added toohello back-end server pool as shown in hello next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="62dd4-181">Merhaba $server tooadd hello değerleri toohello arka uç havuzu nesne ($pool) kullanın.</span><span class="sxs-lookup"><span data-stu-id="62dd4-181">Use hello $server object tooadd hello values toohello back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="62dd4-182">Merhaba arka uç sunucu havuzu ayarlarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-182">Create hello back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="62dd4-183">Merhaba dinleyici oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-183">Create hello listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="62dd4-184">Merhaba kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62dd4-184">Create hello rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="62dd4-185">2. Adım</span><span class="sxs-lookup"><span data-stu-id="62dd4-185">Step 2</span></span>

<span data-ttu-id="62dd4-186">Tüm Bireysel yapılandırma öğelerini tooan uygulama ağ geçidi yapılandırma nesnesi ($appgwconfig) atayın.</span><span class="sxs-lookup"><span data-stu-id="62dd4-186">Assign all individual configuration items tooan application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="62dd4-187">Merhaba ön uç IP toohello yapılandırmasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-187">Add hello front-end IP toohello configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="62dd4-188">Merhaba ön uç bağlantı noktası toohello yapılandırma ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-188">Add hello front-end port toohello configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="62dd4-189">Merhaba arka uç sunucu havuzu toohello yapılandırması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-189">Add hello back-end server pool toohello configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="62dd4-190">Merhaba arka uç havuzu ayarı toohello yapılandırması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-190">Add hello back-end pool setting toohello configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="62dd4-191">Merhaba dinleyici toohello yapılandırması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-191">Add hello listener toohello configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="62dd4-192">Merhaba kural toohello yapılandırma ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62dd4-192">Add hello rule toohello configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="62dd4-193">3. Adım</span><span class="sxs-lookup"><span data-stu-id="62dd4-193">Step 3</span></span>
<span data-ttu-id="62dd4-194">Merhaba yapılandırma nesnesi toohello uygulama ağ geçidi kaynağı kullanarak yürütme `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="62dd4-194">Commit hello configuration object toohello application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a><span data-ttu-id="62dd4-195">Merhaba ağ geçidi Başlat</span><span class="sxs-lookup"><span data-stu-id="62dd4-195">Start hello gateway</span></span>

<span data-ttu-id="62dd4-196">Hello ağ geçidi yapılandırıldıktan sonra hello kullanarak `Start-AzureApplicationGateway` cmdlet toostart hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="62dd4-196">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="62dd4-197">Bir uygulama ağ geçidi için fatura Hello ağ geçidi başarıyla başlatıldıktan sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="62dd4-197">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="62dd4-198">Merhaba `Start-AzureApplicationGateway` cmdlet too15-20 dakika toofinish alabilir.</span><span class="sxs-lookup"><span data-stu-id="62dd4-198">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="62dd4-199">Merhaba ağ geçidi durumunu doğrulama</span><span class="sxs-lookup"><span data-stu-id="62dd4-199">Verify hello gateway status</span></span>

<span data-ttu-id="62dd4-200">Kullanım hello `Get-AzureApplicationGateway` cmdlet toocheck hello hello ağ geçidi durumunu.</span><span class="sxs-lookup"><span data-stu-id="62dd4-200">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="62dd4-201">Varsa `Start-AzureApplicationGateway` hello önceki adımda başarılı *durumu* çalıştırması gerekir, ve *VIP* ve *DnsName* geçerli girdilere sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="62dd4-201">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="62dd4-202">Hello aşağıdaki örnekte gösterilir çalışır durumda, bir uygulama ağ geçidi ve hazır tootake trafiği hedefleyen için `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="62dd4-202">hello following example shows an application gateway that is up, running, and ready tootake traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="62dd4-203">Merhaba uygulama ağ geçidini Sil</span><span class="sxs-lookup"><span data-stu-id="62dd4-203">Delete hello application gateway</span></span>

<span data-ttu-id="62dd4-204">toodelete hello uygulama ağ geçidi:</span><span class="sxs-lookup"><span data-stu-id="62dd4-204">toodelete hello application gateway:</span></span>

1. <span data-ttu-id="62dd4-205">Kullanım hello `Stop-AzureApplicationGateway` cmdlet toostop hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="62dd4-205">Use hello `Stop-AzureApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="62dd4-206">Kullanım hello `Remove-AzureApplicationGateway` cmdlet tooremove hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="62dd4-206">Use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="62dd4-207">Bu hello ağ geçidi hello kullanarak kaldırıldı doğrulayın `Get-AzureApplicationGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="62dd4-207">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="62dd4-208">Merhaba aşağıdaki örnekte gösterilir hello `Stop-AzureApplicationGateway` cmdlet hello ilk satırdaki ardından tarafından hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="62dd4-208">hello following example shows hello `Stop-AzureApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="62dd4-209">Merhaba uygulama ağ geçidi durdurulmuş durumda olduğunda, hello kullan `Remove-AzureApplicationGateway` cmdlet tooremove hello hizmet.</span><span class="sxs-lookup"><span data-stu-id="62dd4-209">Once hello application gateway is in a stopped state, use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="62dd4-210">Hizmet hello tooverify kaldırıldı, hello kullanabilirsiniz `Get-AzureApplicationGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="62dd4-210">tooverify that hello service has been removed, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="62dd4-211">Bu adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="62dd4-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="62dd4-212">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62dd4-212">Next steps</span></span>

<span data-ttu-id="62dd4-213">SSL boşaltma tooconfigure istiyorsanız, bkz: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="62dd4-213">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="62dd4-214">Bir iç yük dengeleyici ile bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, bkz: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="62dd4-214">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="62dd4-215">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="62dd4-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="62dd4-216">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="62dd4-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="62dd4-217">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="62dd4-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
