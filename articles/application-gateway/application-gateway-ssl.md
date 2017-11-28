---
title: "aaaConfigure SSL boşaltma - Azure uygulama ağ geçidi - PowerShell Klasik | Microsoft Docs"
description: "Bu makalede, bir uygulama ağ geçidi ile SSL boşaltma kullanarak toocreate hello Azure Klasik dağıtım modeli yönergeler sağlar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="374b9-103">Merhaba Klasik dağıtım modeli kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="374b9-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="374b9-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="374b9-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="374b9-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="374b9-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="374b9-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="374b9-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="374b9-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="374b9-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="374b9-108">Azure uygulama ağ geçidi yapılandırılmış tooterminate hello Güvenli Yuva Katmanı (SSL) hello ağ geçidi tooavoid maliyetli SSL şifre çözme görevleri toohappen hello web grubu adresindeki oturumunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="374b9-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="374b9-109">SSL boşaltma ayrıca hello ön uç sunucusunun kurulumunu ve hello web uygulamasının yönetimini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="374b9-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="374b9-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="374b9-110">Before you begin</span></span>

1. <span data-ttu-id="374b9-111">Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="374b9-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="374b9-112">Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="374b9-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="374b9-113">Geçerli bir alt ağla çalışan bir sanal ağa sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="374b9-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="374b9-114">Hiçbir sanal makine veya Bulut dağıtımları hello alt kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="374b9-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="374b9-115">Merhaba uygulama ağ geçidi tek başına bir sanal ağ alt ağında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="374b9-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="374b9-116">toouse hello uygulama ağ geçidi yapılandırma hello sunucular mevcut olmalıdır veya hello sanal ağ veya genel IP/VIP'ye ile oluşturulan uç noktaları atadınız.</span><span class="sxs-lookup"><span data-stu-id="374b9-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="374b9-117">tooconfigure SSL bir uygulama ağ geçidinde boşaltma, aşağıdaki adımları listelenen hello sırayla hello:</span><span class="sxs-lookup"><span data-stu-id="374b9-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="374b9-118">Bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="374b9-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="374b9-119">SSL sertifikalarını karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="374b9-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="374b9-120">Merhaba ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="374b9-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="374b9-121">Kümesi hello ağ geçidi yapılandırması</span><span class="sxs-lookup"><span data-stu-id="374b9-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="374b9-122">Merhaba ağ geçidi Başlat</span><span class="sxs-lookup"><span data-stu-id="374b9-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="374b9-123">Merhaba ağ geçidi durumunu doğrulama</span><span class="sxs-lookup"><span data-stu-id="374b9-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="374b9-124">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="374b9-124">Create an application gateway</span></span>

<span data-ttu-id="374b9-125">toocreate hello ağ geçidi, kullanım hello `New-AzureApplicationGateway` hello değerleri kendi değerlerinizle değiştirerek cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="374b9-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="374b9-126">Merhaba ağ geçidi için fatura bu noktada başlatılmaz.</span><span class="sxs-lookup"><span data-stu-id="374b9-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="374b9-127">Merhaba ağ geçidi başarıyla başlatıldığında faturalama bir sonraki adımda başlar.</span><span class="sxs-lookup"><span data-stu-id="374b9-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="374b9-128">ağ geçidi hello toovalidate oluşturuldu, hello kullanabilirsiniz `Get-AzureApplicationGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="374b9-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="374b9-129">Merhaba örneğinde, *açıklama*, *Instancecount*, ve *GatewaySize* isteğe bağlı parametrelerdir.</span><span class="sxs-lookup"><span data-stu-id="374b9-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="374b9-130">Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir.</span><span class="sxs-lookup"><span data-stu-id="374b9-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="374b9-131">Merhaba için varsayılan değer *GatewaySize* Orta'dır.</span><span class="sxs-lookup"><span data-stu-id="374b9-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="374b9-132">Küçük ve büyük diğer değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="374b9-132">Small and Large are other available values.</span></span> <span data-ttu-id="374b9-133">*VirtualIPs* ve *DnsName* hello ağ geçidi henüz başlatılmamış olduğundan boş olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="374b9-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="374b9-134">Merhaba ağ geçidi hello çalışır durumda olduğunda bu değerleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="374b9-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="374b9-135">SSL sertifikalarını karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="374b9-135">Upload SSL certificates</span></span>

<span data-ttu-id="374b9-136">Kullanım `Add-AzureApplicationGatewaySslCertificate` tooupload hello sunucu sertifikasında *pfx* biçimi toohello uygulama ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="374b9-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="374b9-137">Merhaba sertifika adı, bir kullanıcı tarafından seçilen adıdır ve hello uygulama ağ geçidi içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="374b9-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="374b9-138">Bu sertifika başvurulan tooby tüm sertifika yönetimi işlemlerinin hello uygulama ağ geçidi üzerinde bu adıdır.</span><span class="sxs-lookup"><span data-stu-id="374b9-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="374b9-139">Bu aşağıdaki örnek gösterir cmdlet Merhaba, hello örnek hello değerleri kendinizinkilerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="374b9-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="374b9-140">Ardından, hello sertifika yükleme doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="374b9-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="374b9-141">Kullanım hello `Get-AzureApplicationGatewayCertificate` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="374b9-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="374b9-142">Bu örnek hello cmdlet'i hello ilk satırında, gösterilmektedir hello çıktı tarafından izlenen.</span><span class="sxs-lookup"><span data-stu-id="374b9-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> <span data-ttu-id="374b9-143">Merhaba sertifika parolası 4 too12 karakterler, harf veya sayı arasında toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="374b9-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="374b9-144">Özel karakterleri kabul edilmedi.</span><span class="sxs-lookup"><span data-stu-id="374b9-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="374b9-145">Merhaba ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="374b9-145">Configure hello gateway</span></span>

<span data-ttu-id="374b9-146">Bir uygulama ağ geçidi yapılandırması birden çok değerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="374b9-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="374b9-147">Merhaba değerleri bağlı birlikte tooconstruct hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="374b9-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="374b9-148">Merhaba değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="374b9-148">hello values are:</span></span>

* <span data-ttu-id="374b9-149">**Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi.</span><span class="sxs-lookup"><span data-stu-id="374b9-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="374b9-150">listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="374b9-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="374b9-151">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="374b9-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="374b9-152">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="374b9-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="374b9-153">**Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="374b9-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="374b9-154">Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="374b9-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="374b9-155">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="374b9-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="374b9-156">**Kural:** hello kural hello dinleyicisi ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler.</span><span class="sxs-lookup"><span data-stu-id="374b9-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="374b9-157">Şu anda yalnızca hello *temel* kural desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="374b9-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="374b9-158">Merhaba *temel* hepsini bir kez deneme yük dağıtımı kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="374b9-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="374b9-159">**Ek yapılandırma notları**</span><span class="sxs-lookup"><span data-stu-id="374b9-159">**Additional configuration notes**</span></span>

<span data-ttu-id="374b9-160">SSL sertifikaları yapılandırma, protokolünde hello **HttpListener** çok değiştirmelisiniz*Https* (büyük küçük harf duyarlı).</span><span class="sxs-lookup"><span data-stu-id="374b9-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="374b9-161">Merhaba **SslCert** öğesi çok eklenen**HttpListener** hello ile aynı ad olarak kullanılan SSL sertifikaları bölüm önceki, hello karşıya toohello değerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="374b9-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="374b9-162">Merhaba ön uç bağlantı noktası güncelleştirilmiş too443 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="374b9-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="374b9-163">**tooenable tanımlama bilgisi temelli benzeşimi**: bir uygulama ağ geçidi isteği bir istemci oturumundan her zaman yönlendirilmiş toohello olduğunu yapılandırılmış tooensure olabilir hello web grubundaki aynı VM.</span><span class="sxs-lookup"><span data-stu-id="374b9-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="374b9-164">Bu senaryo, uygun şekilde hello ağ geçidi toodirect trafiğe izin veren bir oturum tanımlama bilgisi ekleme işlemi tarafından yapılır.</span><span class="sxs-lookup"><span data-stu-id="374b9-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="374b9-165">tanımlama bilgisi temelli benzeşimi tooenable ayarlamak **CookieBasedAffinity** çok*etkin* hello içinde **BackendHttpSettings** öğesi.</span><span class="sxs-lookup"><span data-stu-id="374b9-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="374b9-166">Bir yapılandırma nesnesi oluşturma veya bir XML yapılandırma dosyası kullanarak yapılandırmanızı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="374b9-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="374b9-167">bir yapılandırma XML dosyasını kullanarak yapılandırmanızı tooconstruct kullanmak hello örnek:</span><span class="sxs-lookup"><span data-stu-id="374b9-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="374b9-168">**Yapılandırma XML örneği**</span><span class="sxs-lookup"><span data-stu-id="374b9-168">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="374b9-169">Kümesi hello ağ geçidi yapılandırması</span><span class="sxs-lookup"><span data-stu-id="374b9-169">Set hello gateway configuration</span></span>

<span data-ttu-id="374b9-170">Ardından, hello uygulama ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="374b9-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="374b9-171">Merhaba kullanabilirsiniz `Set-AzureApplicationGatewayConfig` cmdlet'i bir yapılandırma nesnesi veya bir XML yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="374b9-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="374b9-172">Merhaba ağ geçidi Başlat</span><span class="sxs-lookup"><span data-stu-id="374b9-172">Start hello gateway</span></span>

<span data-ttu-id="374b9-173">Hello ağ geçidi yapılandırıldıktan sonra hello kullanarak `Start-AzureApplicationGateway` cmdlet toostart hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="374b9-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="374b9-174">Bir uygulama ağ geçidi için fatura Hello ağ geçidi başarıyla başlatıldıktan sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="374b9-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="374b9-175">Merhaba `Start-AzureApplicationGateway` cmdlet too15-20 dakika toofinish alabilir.</span><span class="sxs-lookup"><span data-stu-id="374b9-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="374b9-176">Merhaba ağ geçidi durumunu doğrulama</span><span class="sxs-lookup"><span data-stu-id="374b9-176">Verify hello gateway status</span></span>

<span data-ttu-id="374b9-177">Kullanım hello `Get-AzureApplicationGateway` cmdlet toocheck hello hello ağ geçidi durumunu.</span><span class="sxs-lookup"><span data-stu-id="374b9-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="374b9-178">Varsa `Start-AzureApplicationGateway` hello önceki adımda başarılı *durumu* çalıştırması gerekir, ve *VirtualIPs* ve *DnsName* geçerli girdilere sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="374b9-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="374b9-179">Bu örnek, çalışır ve hazır tootake trafiği olan bir uygulama ağ geçidi gösterir.</span><span class="sxs-lookup"><span data-stu-id="374b9-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="374b9-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="374b9-180">Next steps</span></span>

<span data-ttu-id="374b9-181">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="374b9-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="374b9-182">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="374b9-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="374b9-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="374b9-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

