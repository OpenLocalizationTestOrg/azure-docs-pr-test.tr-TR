---
title: "aaaCreate özel araştırma - Azure uygulama ağ geçidi - PowerShell Klasik | Microsoft Docs"
description: "Nasıl toocreate özel bir araştırma uygulama ağ geçidi için hello Klasik dağıtım modelinde PowerShell kullanarak bilgi edinin"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="5706a-103">Özel bir araştırma için Azure uygulama ağ geçidi (Klasik) PowerShell kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="5706a-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5706a-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="5706a-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="5706a-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="5706a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="5706a-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="5706a-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="5706a-107">Bu makalede, bir özel araştırma tooan varolan uygulama ağ geçidi PowerShell ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5706a-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="5706a-108">Özel araştırmalara başarılı bir yanıt hello varsayılan web uygulaması üzerinde sağlamaz, uygulamaları veya belirli bir sağlık denetimi sayfası uygulamaları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="5706a-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5706a-109">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5706a-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5706a-110">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="5706a-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="5706a-111">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="5706a-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5706a-112">Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5706a-112">Learn how too[perform these steps using hello Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="5706a-113">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5706a-113">Create an application gateway</span></span>

<span data-ttu-id="5706a-114">bir uygulama ağ geçidi toocreate:</span><span class="sxs-lookup"><span data-stu-id="5706a-114">toocreate an application gateway:</span></span>

1. <span data-ttu-id="5706a-115">Uygulama ağ geçidi kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5706a-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="5706a-116">Bir XML yapılandırma dosyası veya yapılandırma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5706a-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="5706a-117">Hello yapılandırma toohello yeni oluşturulmuş uygulama ağ geçidi kaynağına uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5706a-117">Commit hello configuration toohello newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="5706a-118">Özel bir araştırma ile uygulama ağ geçidi kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5706a-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="5706a-119">toocreate hello ağ geçidi, kullanım hello `New-AzureApplicationGateway` hello değerleri kendi değerlerinizle değiştirerek cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5706a-119">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="5706a-120">Merhaba ağ geçidi için fatura bu noktada başlatılmaz.</span><span class="sxs-lookup"><span data-stu-id="5706a-120">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="5706a-121">Merhaba ağ geçidi başarıyla başlatıldığında faturalama bir sonraki adımda başlar.</span><span class="sxs-lookup"><span data-stu-id="5706a-121">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="5706a-122">Merhaba aşağıdaki örnek bir uygulama ağ geçidi "testvnet1" ve "subnet-1" adlı bir alt ağ olarak adlandırılan bir sanal ağ kullanarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5706a-122">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="5706a-123">ağ geçidi hello toovalidate oluşturuldu, hello kullanabilirsiniz `Get-AzureApplicationGateway` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5706a-123">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="5706a-124">Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir.</span><span class="sxs-lookup"><span data-stu-id="5706a-124">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="5706a-125">Merhaba için varsayılan değer *GatewaySize* Orta'dır.</span><span class="sxs-lookup"><span data-stu-id="5706a-125">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="5706a-126">Küçük, Orta ve büyük arasında seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5706a-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="5706a-127">*VirtualIPs* ve *DnsName* hello ağ geçidi henüz başlatılmamış olduğundan boş olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5706a-127">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="5706a-128">Merhaba ağ geçidi hello çalışır durumda olduğunda bu değerleri oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5706a-128">These values are created once hello gateway is in hello running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="5706a-129">XML kullanarak uygulama ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5706a-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="5706a-130">Aşağıdaki örneğine hello, tüm uygulama ağ geçidi ayarları bir XML dosyası tooconfigure kullanın ve toohello uygulama ağ geçidi kaynağına uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5706a-130">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

<span data-ttu-id="5706a-131">Metin tooNotepad aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5706a-131">Copy hello following text tooNotepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="5706a-132">Merhaba yapılandırma öğeleri için hello parantez Hello değerlerini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="5706a-132">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="5706a-133">Merhaba dosyası .xml. uzantısıyla kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5706a-133">Save hello file with extension .xml.</span></span>

<span data-ttu-id="5706a-134">Merhaba aşağıdaki örnekte nasıl toouse bir yapılandırma dosyası tooset hello uygulama ağ geçidi tooload yukarı ortak bağlantı noktası 80 üzerinde HTTP trafiği dengelemek ve ağ trafiğini iki IP adreslerini özel bir araştırma kullanarak arasında tooback uç bağlantı noktası 80 Gönder gösterir.</span><span class="sxs-lookup"><span data-stu-id="5706a-134">hello following example shows how toouse a configuration file tooset up hello application gateway tooload balance HTTP traffic on public port 80 and send network traffic tooback-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5706a-135">Http veya Https Hello protokol öğesi büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="5706a-135">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="5706a-136">Yeni bir yapılandırma öğesi \<araştırma\> tooconfigure özel araştırmalara eklenir.</span><span class="sxs-lookup"><span data-stu-id="5706a-136">A new configuration item \<Probe\> is added tooconfigure custom probes.</span></span>

<span data-ttu-id="5706a-137">Merhaba yapılandırma Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5706a-137">hello configuration parameters are:</span></span>

|<span data-ttu-id="5706a-138">Parametre</span><span class="sxs-lookup"><span data-stu-id="5706a-138">Parameter</span></span>|<span data-ttu-id="5706a-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5706a-139">Description</span></span>|
|---|---|
|<span data-ttu-id="5706a-140">**Ad**</span><span class="sxs-lookup"><span data-stu-id="5706a-140">**Name**</span></span> |<span data-ttu-id="5706a-141">Özel araştırma için başvuru adı.</span><span class="sxs-lookup"><span data-stu-id="5706a-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="5706a-142">* **Protokolü**</span><span class="sxs-lookup"><span data-stu-id="5706a-142">* **Protocol**</span></span> | <span data-ttu-id="5706a-143">Kullanılan protokol (olası değerler HTTP veya HTTPS).</span><span class="sxs-lookup"><span data-stu-id="5706a-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="5706a-144">**Ana bilgisayar** ve **yolu**</span><span class="sxs-lookup"><span data-stu-id="5706a-144">**Host** and **Path**</span></span> | <span data-ttu-id="5706a-145">Merhaba uygulama ağ geçidi toodetermine hello sistem hello örneğinin tarafından çağrılan tam URL yolu.</span><span class="sxs-lookup"><span data-stu-id="5706a-145">Complete URL path that is invoked by hello application gateway toodetermine hello health of hello instance.</span></span> <span data-ttu-id="5706a-146">Örneğin, sonra da Hello özel araştırma için yapılandırılabilir bir Web sitesi http://contoso.com/ varsa araştırma için "http://contoso.com/path/custompath.htm" toohave başarılı bir HTTP yanıt denetler.</span><span class="sxs-lookup"><span data-stu-id="5706a-146">For example, if you have a website http://contoso.com/, then hello custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks toohave a successful HTTP response.</span></span>|
| <span data-ttu-id="5706a-147">**Aralığı**</span><span class="sxs-lookup"><span data-stu-id="5706a-147">**Interval**</span></span> | <span data-ttu-id="5706a-148">Merhaba yoklama aralığı denetimleri saniye olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5706a-148">Configures hello probe interval checks in seconds.</span></span>|
| <span data-ttu-id="5706a-149">**Zaman aşımı**</span><span class="sxs-lookup"><span data-stu-id="5706a-149">**Timeout**</span></span> | <span data-ttu-id="5706a-150">Bir HTTP yanıt denetimi için Hello yoklama zaman aşımını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5706a-150">Defines hello probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="5706a-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="5706a-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="5706a-152">Merhaba başarısız HTTP yanıt sayısı tooflag hello arka uç örnek olarak *sağlıksız*.</span><span class="sxs-lookup"><span data-stu-id="5706a-152">hello number of failed HTTP responses needed tooflag hello back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="5706a-153">Merhaba araştırma adı hello başvurulan \<BackendHttpSettings\> yapılandırma tooassign hangi arka uç havuzuna özel araştırma ayarlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5706a-153">hello probe name is referenced in hello \<BackendHttpSettings\> configuration tooassign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a><span data-ttu-id="5706a-154">Bir özel araştırma tooan varolan uygulama ağ geçidi Ekle</span><span class="sxs-lookup"><span data-stu-id="5706a-154">Add a custom probe tooan existing application gateway</span></span>

<span data-ttu-id="5706a-155">Bir uygulama ağ geçidi değişen hello geçerli yapılandırmasını üç adımı gerektirir: Get hello geçerli XML yapılandırma dosyası, toohave özel bir araştırma değiştirmek ve hello uygulama ağ geçidi hello yeni XML ayarlarla yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5706a-155">Changing hello current configuration of an application gateway requires three steps: Get hello current XML configuration file, modify toohave a custom probe, and configure hello application gateway with hello new XML settings.</span></span>

1. <span data-ttu-id="5706a-156">Merhaba XML dosyasını kullanarak alma `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="5706a-156">Get hello XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="5706a-157">Bu cmdlet dışarı hello yapılandırma XML toobe tooadd bir yoklama ayarı değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="5706a-157">This cmdlet exports hello configuration XML toobe modified tooadd a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. <span data-ttu-id="5706a-158">Merhaba XML dosyasını bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="5706a-158">Open hello XML file in a text editor.</span></span> <span data-ttu-id="5706a-159">Ekleme bir `<probe>` sonra bölümünde `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="5706a-159">Add a `<probe>` section after `<frontendport>`.</span></span>

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  <span data-ttu-id="5706a-160">Merhaba backendHttpSettings bölümünde hello XML hello araştırma adı hello aşağıdaki örnekte gösterildiği gibi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5706a-160">In hello backendHttpSettings section of hello XML, add hello probe name as shown in hello following example:</span></span>

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  <span data-ttu-id="5706a-161">Merhaba XML dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5706a-161">Save hello XML file.</span></span>

1. <span data-ttu-id="5706a-162">Güncelleştirme hello uygulama ağ geçidi yapılandırmasını kullanarak hello yeni bir XML dosyası ile `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="5706a-162">Update hello application gateway configuration with hello new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="5706a-163">Bu cmdlet, uygulama ağ geçidi hello yeni yapılandırmayla güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5706a-163">This cmdlet updates your application gateway with hello new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a><span data-ttu-id="5706a-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5706a-164">Next steps</span></span>

<span data-ttu-id="5706a-165">Güvenli Yuva Katmanı (SSL) yük boşaltma tooconfigure istiyorsanız, bkz: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="5706a-165">If you want tooconfigure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="5706a-166">Bir iç yük dengeleyici ile bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, bkz: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="5706a-166">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

