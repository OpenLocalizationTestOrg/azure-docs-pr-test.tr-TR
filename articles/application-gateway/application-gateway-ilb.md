---
title: "Azure uygulama ağ geçidi iç yük dengeleyici ile kullanma | Microsoft Docs"
description: "Bu sayfa, Azure uygulama ağ geçidi ile iç yük dengeli uç nokta yapılandırmaya yönelik yönergeler sağlar"
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
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="49ea6-103">İç Load Balancer (ILB) aracılığıyla Application Gateway oluşturun</span><span class="sxs-lookup"><span data-stu-id="49ea6-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="49ea6-104">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="49ea6-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="49ea6-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="49ea6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="49ea6-106">Uygulama ağ geçidi olarak da bilinen iç yük dengeleyici (ILB) uç nokta Internet'e açık olmayan bir iç uç nokta veya internet'e yönelik sanal IP ile yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="49ea6-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="49ea6-107">Ağ geçidini bir ILB ile yapılandırma internet'e açık değil iç iş kolu satır uygulamaları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="49ea6-108">İnternet'e açık olmayan bir güvenlik sınırı içinde bulunur, ancak hala hepsini bir kez deneme yük dağıtımı, oturum sürekliliği veya SSL sonlandırması gerektiren çok katmanlı uygulama içinde Hizmetleri/katmanları için de yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="49ea6-109">Bu makale, ILB ile uygulama ağ geçidi yapılandırma adımlarında size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="49ea6-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="49ea6-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="49ea6-110">Before you begin</span></span>

1. <span data-ttu-id="49ea6-111">Web Platformu Yükleyicisi'ni kullanarak Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="49ea6-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="49ea6-112">En son sürümü yükleyip **Windows PowerShell** bölümünü [indirme sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="49ea6-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="49ea6-113">Geçerli bir alt ağ ile çalışan bir sanal ağa sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="49ea6-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="49ea6-114">Sanal ağda veya atanan genel IP/VIP'ye ile arka uç sunucularına sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="49ea6-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="49ea6-115">Bir uygulama ağ geçidi oluşturmak için listelenen sırayla aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="49ea6-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="49ea6-116">Bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="49ea6-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="49ea6-117">Ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="49ea6-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="49ea6-118">Ağ geçidi yapılandırmasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="49ea6-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="49ea6-119">Ağ geçidini başlatma</span><span class="sxs-lookup"><span data-stu-id="49ea6-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="49ea6-120">Ağ geçidi doğrulayın</span><span class="sxs-lookup"><span data-stu-id="49ea6-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="49ea6-121">Bir uygulama ağ geçidi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="49ea6-121">Create an application gateway:</span></span>

<span data-ttu-id="49ea6-122">**Ağ geçidi oluşturmak için**, kullanın `New-AzureApplicationGateway` cmdlet'ini değerleri kendi değerlerinizle değiştirerek.</span><span class="sxs-lookup"><span data-stu-id="49ea6-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="49ea6-123">Ağ geçidinin faturalanmasının henüz bu aşamada başlamadığını hatırlatmak isteriz. </span><span class="sxs-lookup"><span data-stu-id="49ea6-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="49ea6-124">Daha sonra ağ geçidi başarıyla başlatıldığında faturalama da başlar. </span><span class="sxs-lookup"><span data-stu-id="49ea6-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

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

<span data-ttu-id="49ea6-125">**Doğrulanacak** ağ geçidinin oluşturulduğunu, kullanabileceğiniz `Get-AzureApplicationGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="49ea6-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="49ea6-126">Örnekte, *açıklama*, *Instancecount*, ve *GatewaySize* isteğe bağlı parametrelerdir.</span><span class="sxs-lookup"><span data-stu-id="49ea6-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="49ea6-127">*InstanceCount* için varsayılan değer 2 ile 10 arasıdır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="49ea6-128">*GatewaySize* için varsayılan değer Medium’dur.</span><span class="sxs-lookup"><span data-stu-id="49ea6-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="49ea6-129">Küçük ve büyük diğer değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="49ea6-129">Small and Large are other available values.</span></span> <span data-ttu-id="49ea6-130">*VIP* ve *DnsName* ağ geçidi henüz başlatılmamış olduğundan boş olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="49ea6-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="49ea6-131">Bunlar ağ geçidi çalışma durumuna geçtiğinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="49ea6-131">These are created once the gateway is in the running state.</span></span> 

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

## <a name="configure-the-gateway"></a><span data-ttu-id="49ea6-132">Ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="49ea6-132">Configure the gateway</span></span>
<span data-ttu-id="49ea6-133">Bir uygulama ağ geçidi yapılandırması birden çok değerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="49ea6-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="49ea6-134">Değerleri bağlı yapılandırma birlikte oluşturulamadı.</span><span class="sxs-lookup"><span data-stu-id="49ea6-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="49ea6-135">Değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="49ea6-135">The values are:</span></span>

* <span data-ttu-id="49ea6-136">**Arka uç sunucusu havuzu:** arka uç sunucularının IP adreslerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="49ea6-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="49ea6-137">Listede bulunan IP adresleri ya da sanal ağ alt ağına ait olması gerekir veya genel IP/VIP'ye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="49ea6-138">**Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="49ea6-139">Bu ayarlar bir havuza bağlıdır ve havuzdaki tüm sunuculara uygulanır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="49ea6-140">**Ön uç bağlantı noktası:** Bu bağlantı noktası uygulama ağ geçidinde açılan genel bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="49ea6-141">Bu bağlantı noktasında trafik olursa arka uç sunuculardan birine yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="49ea6-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="49ea6-142">**Dinleyici:** dinleyicisinde bir ön uç bağlantı noktası, bir iletişim kuralı kullanılır (Http veya Https, bunlar büyük küçük harfe duyarlı) ve (SSL yük boşaltımı yapılandırılıyorsa) SSL sertifika adı.</span><span class="sxs-lookup"><span data-stu-id="49ea6-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="49ea6-143">**Kural:** kural dinleyiciyi ve arka uç sunucusu havuzunu bağlar ve trafiği için belli bir Dinleyicide trafik olduğunda hangi arka uç sunucu havuzuna yönlendirileceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="49ea6-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="49ea6-144">Şu anda yalnızca *temel* kural desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="49ea6-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="49ea6-145">*Temel* kural hepsini bir kez deneme yöntemiyle yük dağıtımıdır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="49ea6-146">Bir yapılandırma nesnesi oluşturarak veya bir XML yapılandırma dosyası kullanarak yapılandırmanızı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49ea6-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="49ea6-147">Bir XML yapılandırma dosyası kullanarak yapılandırmanızı oluşturmak için aşağıdaki örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="49ea6-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="49ea6-148">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="49ea6-148">Note the following:</span></span>

* <span data-ttu-id="49ea6-149">*Frontendıpconfigurations'a* öğesi bir ILB ile uygulama ağ geçidi yapılandırılmasıyla ilgili ILB ayrıntıları açıklar.</span><span class="sxs-lookup"><span data-stu-id="49ea6-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="49ea6-150">Ön uç IP *türü* 'Özel' olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="49ea6-151">*StaticIPAddress* ağ geçidi üzerinde trafiği alır istenen iç IP ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="49ea6-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="49ea6-152">Unutmayın *StaticIPAddress* öğesidir isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="49ea6-153">Aksi durumda kümesi, kullanılabilir bir iç IP dağıtılan alt ağdan seçilir.</span><span class="sxs-lookup"><span data-stu-id="49ea6-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="49ea6-154">Değeri *adı* belirtilen öğesi *Frontendıpconfiguration* HTTPListener içinde 's kullanılmalıdır *FrontendIP* Frontendıpconfiguration başvurmak için öğesi.</span><span class="sxs-lookup"><span data-stu-id="49ea6-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="49ea6-155">**Yapılandırma XML örneği**</span><span class="sxs-lookup"><span data-stu-id="49ea6-155">**Configuration XML sample**</span></span>
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


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="49ea6-156">Ağ geçidi yapılandırmasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="49ea6-156">Set the gateway configuration</span></span>
<span data-ttu-id="49ea6-157">Ardından, uygulama ağ geçidi ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="49ea6-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="49ea6-158">Kullanabileceğiniz `Set-AzureApplicationGatewayConfig` cmdlet'i bir yapılandırma nesnesi veya bir XML yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="49ea6-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

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

## <a name="start-the-gateway"></a><span data-ttu-id="49ea6-159">Ağ geçidini başlatma</span><span class="sxs-lookup"><span data-stu-id="49ea6-159">Start the gateway</span></span>

<span data-ttu-id="49ea6-160">Ağ geçidi yapılandırıldıktan sonra, ağ geçidini başlatmak için `Start-AzureApplicationGateway` cmdlet’ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="49ea6-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="49ea6-161">Uygulama ağ geçidinin faturalanması ağ geçidi başarıyla başlatıldıktan sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="49ea6-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="49ea6-162">`Start-AzureApplicationGateway` Cmdlet 15-20 tamamlamak için dakika kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="49ea6-162">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete.</span></span> 
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

## <a name="verify-the-gateway-status"></a><span data-ttu-id="49ea6-163">Ağ geçidi durumunu doğrulama</span><span class="sxs-lookup"><span data-stu-id="49ea6-163">Verify the gateway status</span></span>

<span data-ttu-id="49ea6-164">Kullanım `Get-AzureApplicationGateway` cmdlet'ini ağ geçidi durumunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="49ea6-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="49ea6-165">Varsa `Start-AzureApplicationGateway` önceki adımda başarılı oldu, durum olmalıdır *çalıştıran*, ve VIP ve DnsName geçerli girdilere sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="49ea6-166">Bu örnek cmdlet ilk satırında gösterir çıktı tarafından takip.</span><span class="sxs-lookup"><span data-stu-id="49ea6-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="49ea6-167">Bu örnek, ağ geçidi çalışıyor ve trafiği almaya hazır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="49ea6-168">Uygulama ağ geçidi 10.0.0.10 Bu örnekte, yapılandırılmış ILB uç noktada trafiğini kabul edecek şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="49ea6-168">The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="49ea6-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="49ea6-169">Next steps</span></span>
<span data-ttu-id="49ea6-170">Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.</span><span class="sxs-lookup"><span data-stu-id="49ea6-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="49ea6-171">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="49ea6-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="49ea6-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="49ea6-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

