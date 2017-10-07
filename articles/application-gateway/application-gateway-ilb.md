---
title: "Azure uygulama ağ geçidi iç yük dengeleyici ile aaaUsing | Microsoft Docs"
description: "Bu sayfa, Azure uygulama ağ geçidi ile bir iç yük dengeli uç nokta yönergeleri tooconfigure sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="395be-103">İç Load Balancer (ILB) aracılığıyla Application Gateway oluşturun</span><span class="sxs-lookup"><span data-stu-id="395be-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="395be-104">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="395be-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="395be-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="395be-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="395be-106">Bir iç uç nokta sunulmaz toohello veya internet'e yönelik sanal IP ile uygulama ağ geçidi yapılandırılabilir Internet, olarak da bilinen iç yük dengeleyici (ILB) uç noktası.</span><span class="sxs-lookup"><span data-stu-id="395be-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed toohello internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="395be-107">Bir ILB ile yapılandırma hello ağ geçidi sunulmaz iç iş kolu satır uygulamaları toointernet için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="395be-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications not exposed toointernet.</span></span> <span data-ttu-id="395be-108">Güvenlik sunulmaz sınır toointernet içinde bulunur, ancak hala hepsini bir kez deneme yük dağıtımı, oturum sürekliliği veya SSL sonlandırması gerektiren çok katmanlı uygulama içinde Hizmetleri/katmanları için de yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="395be-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed toointernet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="395be-109">Bu makalede, hello adımları tooconfigure bir uygulama ağ geçidini bir ILB ile adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="395be-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="395be-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="395be-110">Before you begin</span></span>

1. <span data-ttu-id="395be-111">Merhaba Web Platformu yükleyicisi kullanılarak hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="395be-111">Install latest version of hello Azure PowerShell cmdlets using hello Web Platform Installer.</span></span> <span data-ttu-id="395be-112">Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirme sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="395be-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="395be-113">Geçerli bir alt ağ ile çalışan bir sanal ağa sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="395be-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="395be-114">Merhaba sanal ağda veya atanan genel IP/VIP'ye ile arka uç sunucularına sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="395be-114">Verify that you have backend servers either in hello virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="395be-115">bir uygulama ağ geçidi toocreate hello sırayı adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="395be-115">toocreate an application gateway, perform hello following steps in hello order listed.</span></span> 

1. [<span data-ttu-id="395be-116">Bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="395be-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="395be-117">Merhaba ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="395be-117">Configure hello gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="395be-118">Kümesi hello ağ geçidi yapılandırması</span><span class="sxs-lookup"><span data-stu-id="395be-118">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="395be-119">Merhaba ağ geçidi Başlat</span><span class="sxs-lookup"><span data-stu-id="395be-119">Start hello gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="395be-120">Merhaba ağ geçidini doğrulama</span><span class="sxs-lookup"><span data-stu-id="395be-120">Verify hello gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="395be-121">Bir uygulama ağ geçidi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="395be-121">Create an application gateway:</span></span>

<span data-ttu-id="395be-122">**toocreate hello ağ geçidi**, hello kullan `New-AzureApplicationGateway` hello değerleri kendi değerlerinizle değiştirerek cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="395be-122">**toocreate hello gateway**, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="395be-123">Merhaba ağ geçidi için fatura bu noktada başlamıyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="395be-123">Note that billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="395be-124">Merhaba ağ geçidi başarıyla başlatıldığında faturalama bir sonraki adımda başlar.</span><span class="sxs-lookup"><span data-stu-id="395be-124">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="395be-125">**toovalidate** hello ağ geçidi oluşturuldu, hello kullanabilirsiniz `Get-AzureApplicationGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="395be-125">**toovalidate** that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="395be-126">Merhaba örneğinde, *açıklama*, *Instancecount*, ve *GatewaySize* isteğe bağlı parametrelerdir.</span><span class="sxs-lookup"><span data-stu-id="395be-126">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="395be-127">Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir.</span><span class="sxs-lookup"><span data-stu-id="395be-127">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="395be-128">Merhaba için varsayılan değer *GatewaySize* Orta'dır.</span><span class="sxs-lookup"><span data-stu-id="395be-128">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="395be-129">Küçük ve büyük diğer değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="395be-129">Small and Large are other available values.</span></span> <span data-ttu-id="395be-130">*VIP* ve *DnsName* hello ağ geçidi henüz başlatılmamış olduğundan boş olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="395be-130">*Vip* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="395be-131">Merhaba ağ geçidi çalışır durumda hello olduğunda bunlar oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="395be-131">These are created once hello gateway is in hello running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a><span data-ttu-id="395be-132">Merhaba ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="395be-132">Configure hello gateway</span></span>
<span data-ttu-id="395be-133">Bir uygulama ağ geçidi yapılandırması birden çok değerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="395be-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="395be-134">Merhaba değerleri bağlı birlikte tooconstruct hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="395be-134">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="395be-135">Merhaba değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="395be-135">hello values are:</span></span>

* <span data-ttu-id="395be-136">**Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adreslerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="395be-136">**Backend server pool:** hello list of IP addresses of hello backend servers.</span></span> <span data-ttu-id="395be-137">listede hello IP adresleri ya da toohello sanal alt ait olması gerekir veya genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="395be-137">hello IP addresses listed should either belong toohello VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="395be-138">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="395be-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="395be-139">Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.</span><span class="sxs-lookup"><span data-stu-id="395be-139">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="395be-140">**Ön uç bağlantı noktası:** Bu bağlantı noktası hello uygulama ağ geçidinde açılan hello genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="395be-140">**Frontend Port:** This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="395be-141">Trafiği, bu bağlantı noktasında trafik ve yeniden yönlendirilen tooone hello arka uç sunucularının alır.</span><span class="sxs-lookup"><span data-stu-id="395be-141">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="395be-142">**Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bunlar büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="395be-142">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="395be-143">**Kural:** hello kural hello dinleyici ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğini olmalıdır belirler.</span><span class="sxs-lookup"><span data-stu-id="395be-143">**Rule:** hello rule binds hello listener and hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="395be-144">Şu anda yalnızca hello *temel* kural desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="395be-144">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="395be-145">Merhaba *temel* hepsini bir kez deneme yük dağıtımı kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="395be-145">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="395be-146">Bir yapılandırma nesnesi oluşturarak veya bir XML yapılandırma dosyası kullanarak yapılandırmanızı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="395be-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="395be-147">tooconstruct yapılandırma XML dosyası, kullanım hello kullanarak yapılandırmanızı Aşağıda örnek.</span><span class="sxs-lookup"><span data-stu-id="395be-147">tooconstruct your configuration by using a configuration XML file, use hello sample below.</span></span>

<span data-ttu-id="395be-148">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="395be-148">Note hello following:</span></span>

* <span data-ttu-id="395be-149">Merhaba *Frontendıpconfigurations'a* öğesi hello ILB ayrıntıları uygulama ağ geçidini bir ILB ile yapılandırılmasıyla ilgili açıklar.</span><span class="sxs-lookup"><span data-stu-id="395be-149">hello *FrontendIPConfigurations* element describes hello ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="395be-150">Merhaba ön uç IP *türü* too'Private ayarlanmalıdır '</span><span class="sxs-lookup"><span data-stu-id="395be-150">hello Frontend IP *Type* should be set too'Private'</span></span>
* <span data-ttu-id="395be-151">Merhaba *StaticIPAddress* istenen toohello iç IP hangi hello üzerinde ağ geçidi alır trafiği ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="395be-151">hello *StaticIPAddress* should be set toohello desired internal IP on which hello gateway receives traffic.</span></span> <span data-ttu-id="395be-152">Bu hello Not *StaticIPAddress* öğesidir isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="395be-152">Note that hello *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="395be-153">Aksi durumda kümesi, kullanılabilir bir iç IP dağıtılan hello alt ağdan seçilir.</span><span class="sxs-lookup"><span data-stu-id="395be-153">If not set, an available internal IP from hello deployed subnet is chosen.</span></span> 
* <span data-ttu-id="395be-154">Merhaba hello değerini *adı* belirtilen öğesi *Frontendıpconfiguration* hello HTTPListener's kullanılmalıdır *FrontendIP* öğesi toorefer toohello Frontendıpconfiguration.</span><span class="sxs-lookup"><span data-stu-id="395be-154">hello value of hello *Name* element specified in *FrontendIPConfiguration* should be used in hello HTTPListener's *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="395be-155">**Yapılandırma XML örneği**</span><span class="sxs-lookup"><span data-stu-id="395be-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="395be-156">Kümesi hello ağ geçidi yapılandırması</span><span class="sxs-lookup"><span data-stu-id="395be-156">Set hello gateway configuration</span></span>
<span data-ttu-id="395be-157">Ardından, hello uygulama ağ geçidi ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="395be-157">Next, you'll set hello application gateway.</span></span> <span data-ttu-id="395be-158">Merhaba kullanabilirsiniz `Set-AzureApplicationGatewayConfig` cmdlet'i bir yapılandırma nesnesi veya bir XML yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="395be-158">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a><span data-ttu-id="395be-159">Merhaba ağ geçidi Başlat</span><span class="sxs-lookup"><span data-stu-id="395be-159">Start hello gateway</span></span>

<span data-ttu-id="395be-160">Hello ağ geçidi yapılandırıldıktan sonra hello kullanarak `Start-AzureApplicationGateway` cmdlet toostart hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="395be-160">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="395be-161">Bir uygulama ağ geçidi için fatura Hello ağ geçidi başarıyla başlatıldıktan sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="395be-161">Billing for an application gateway begins after hello gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="395be-162">Merhaba `Start-AzureApplicationGateway` cmdlet too15-20 dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="395be-162">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toocomplete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="395be-163">Merhaba ağ geçidi durumunu doğrulama</span><span class="sxs-lookup"><span data-stu-id="395be-163">Verify hello gateway status</span></span>

<span data-ttu-id="395be-164">Kullanım hello `Get-AzureApplicationGateway` cmdlet toocheck hello ağ geçidi durumunu.</span><span class="sxs-lookup"><span data-stu-id="395be-164">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of gateway.</span></span> <span data-ttu-id="395be-165">Varsa `Start-AzureApplicationGateway` hello önceki adımda başarılı oldu, hello durumu olmalıdır *çalıştıran*, VIP hello ve DnsName geçerli girişi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="395be-165">If `Start-AzureApplicationGateway` succeeded in hello previous step, hello State should be *Running*, and hello Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="395be-166">Bu örnek hello cmdlet'i hello ilk satırında, gösterilmektedir hello çıktı tarafından izlenen.</span><span class="sxs-lookup"><span data-stu-id="395be-166">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span> <span data-ttu-id="395be-167">Bu örnek hello ağ geçidi çalışıyor ve hazır tootake trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="395be-167">In this sample, hello gateway is running, and is ready tootake traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="395be-168">Merhaba uygulama ağ geçidi yapılandırılmış hello tooaccept trafiğinin Bu örnekte 10.0.0.10 ILB uç noktasını yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="395be-168">hello application gateway is configured tooaccept traffic at hello configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="395be-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="395be-169">Next steps</span></span>
<span data-ttu-id="395be-170">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="395be-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="395be-171">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="395be-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="395be-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="395be-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

