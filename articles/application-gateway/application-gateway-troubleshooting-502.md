---
title: "aaaTroubleshoot Azure uygulama ağ geçidi hatalı ağ geçidi (502) hataları | Microsoft Docs"
description: "Bilgi nasıl tootroubleshoot uygulama ağ geçidi 502 hataları"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="986c2-103">Uygulama ağ geçidi olarak hatalı ağ geçidi hatalarında sorun giderme</span><span class="sxs-lookup"><span data-stu-id="986c2-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="986c2-104">Uygulama ağ geçidi kullanırken nasıl alınan tootroubleshoot hatalı ağ geçidi (502) hataları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="986c2-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="986c2-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="986c2-105">Overview</span></span>

<span data-ttu-id="986c2-106">Bir uygulama ağ geçidi yapılandırdıktan sonra kullanıcılar karşılaşabilirsiniz hello hatalardan biri olan "sunucu hatası: 502 - Web sunucusu alınan geçersiz bir yanıt bir ağ geçidi veya proxy sunucu olarak çalışırken".</span><span class="sxs-lookup"><span data-stu-id="986c2-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="986c2-107">Bu hata nedeniyle toohello aşağıdaki oluşabilir nedenler:</span><span class="sxs-lookup"><span data-stu-id="986c2-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="986c2-108">Azure uygulama ağ geçidi [arka uç havuzu yapılandırılmış ya da boş değil](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="986c2-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="986c2-109">Merhaba VM'ler veya durumlarda hiçbiri [VM ölçek kümesi sağlıklı](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="986c2-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="986c2-110">Arka uç VM'ler veya VM ölçek kümesi örneklerinin [vermiyor toohello varsayılan durumu araştırması](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="986c2-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="986c2-111">Geçersiz veya hatalı [özel sistem durumu araştırmalarının yapılandırmasını](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="986c2-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="986c2-112">[İstek zaman aşımı veya bağlantı sorunları](#request-time-out) kullanıcı istekleri ile.</span><span class="sxs-lookup"><span data-stu-id="986c2-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="986c2-113">Boş BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="986c2-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="986c2-114">Nedeni</span><span class="sxs-lookup"><span data-stu-id="986c2-114">Cause</span></span>

<span data-ttu-id="986c2-115">Merhaba uygulama ağ geçidi VM veya VM ölçek kümesi hello arka uç adres havuzunda yapılandırılmış, herhangi bir müşteri istek yönlendiremezsiniz ve hatalı ağ geçidi hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="986c2-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="986c2-116">Çözüm</span><span class="sxs-lookup"><span data-stu-id="986c2-116">Solution</span></span>

<span data-ttu-id="986c2-117">Merhaba arka uç adres havuzu boş olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="986c2-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="986c2-118">Bu da PowerShell'i, CLI veya portal aracılığıyla yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="986c2-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="986c2-119">cmdlet'in önceki hello Hello çıktısını boş arka uç adres havuzu içermelidir.</span><span class="sxs-lookup"><span data-stu-id="986c2-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="986c2-120">Aşağıdaki iki havuzları, burada döndürülen bir örnek verilmiştir arka uç VM'ler için FQDN veya IP adresleriyle yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="986c2-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="986c2-121">sağlama durumu hello BackendAddressPool hello 'başarılı' olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="986c2-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="986c2-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="986c2-122">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="986c2-123">BackendAddressPool kötü durumda</span><span class="sxs-lookup"><span data-stu-id="986c2-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="986c2-124">Nedeni</span><span class="sxs-lookup"><span data-stu-id="986c2-124">Cause</span></span>

<span data-ttu-id="986c2-125">BackendAddressPool tüm hello örneklerini sağlam olmaması ise, uygulama ağ geçidi için herhangi bir arka uç tooroute kullanıcı istek bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="986c2-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="986c2-126">Arka uç örnekleri sağlıklı ancak dağıtılan hello gerekli uygulama yoksa zaman bu hello durumda olabilir.</span><span class="sxs-lookup"><span data-stu-id="986c2-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="986c2-127">Çözüm</span><span class="sxs-lookup"><span data-stu-id="986c2-127">Solution</span></span>

<span data-ttu-id="986c2-128">Merhaba örnekleri sağlıklı olduğunu ve Merhaba uygulaması'nın düzgün yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="986c2-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="986c2-129">Onay hello arka uç örnekleri mümkün toorespond tooa ping içinde başka bir VM'den varsa, aynı sanal ağı hello.</span><span class="sxs-lookup"><span data-stu-id="986c2-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="986c2-130">Ortak bir uç nokta ile yapılandırılmışsa, bir tarayıcı isteğini toohello web uygulaması tarafından bakımı yapılabilen olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="986c2-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="986c2-131">Varsayılan durumu araştırması sorunları</span><span class="sxs-lookup"><span data-stu-id="986c2-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="986c2-132">Nedeni</span><span class="sxs-lookup"><span data-stu-id="986c2-132">Cause</span></span>

<span data-ttu-id="986c2-133">502 hataları da varsayılan durumu araştırması hello sık göstergeleri olması arka uç VM'ler erişilemiyor tooreach olduğu.</span><span class="sxs-lookup"><span data-stu-id="986c2-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="986c2-134">Bir uygulama ağ geçidi örneği sağlandığında, varsayılan sistem durumu araştırma tooeach BackendAddressPool otomatik olarak yapılandırır hello BackendHttpSetting özelliklerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="986c2-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="986c2-135">Hiçbir kullanıcı girişi gerekli tooset Bu araştırma.</span><span class="sxs-lookup"><span data-stu-id="986c2-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="986c2-136">Özellikle, bir Yük Dengeleme kuralı yapılandırıldığında, bir ilişki BackendHttpSetting ve BackendAddressPool arasında yapılır.</span><span class="sxs-lookup"><span data-stu-id="986c2-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="986c2-137">Bir varsayılan araştırma her bu ilişkilerini ve uygulama ağ geçidi başlatır düzenli sistem durumu denetimi bağlantı tooeach örneğinde hello BackendAddressPool hello BackendHttpSetting öğesinde belirtilen hello bağlantı noktasında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="986c2-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="986c2-138">Aşağıdaki tabloda hello varsayılan durumu araştırması ile ilişkili hello değerleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="986c2-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="986c2-139">Araştırma özelliği</span><span class="sxs-lookup"><span data-stu-id="986c2-139">Probe property</span></span> | <span data-ttu-id="986c2-140">Değer</span><span class="sxs-lookup"><span data-stu-id="986c2-140">Value</span></span> | <span data-ttu-id="986c2-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="986c2-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="986c2-142">Araştırma URL'si</span><span class="sxs-lookup"><span data-stu-id="986c2-142">Probe URL</span></span> |<span data-ttu-id="986c2-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="986c2-143">http://127.0.0.1/</span></span> |<span data-ttu-id="986c2-144">URL yolu</span><span class="sxs-lookup"><span data-stu-id="986c2-144">URL path</span></span> |
| <span data-ttu-id="986c2-145">aralığı</span><span class="sxs-lookup"><span data-stu-id="986c2-145">Interval</span></span> |<span data-ttu-id="986c2-146">30</span><span class="sxs-lookup"><span data-stu-id="986c2-146">30</span></span> |<span data-ttu-id="986c2-147">Saniye cinsinden yoklama aralığı</span><span class="sxs-lookup"><span data-stu-id="986c2-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="986c2-148">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="986c2-148">Time-out</span></span> |<span data-ttu-id="986c2-149">30</span><span class="sxs-lookup"><span data-stu-id="986c2-149">30</span></span> |<span data-ttu-id="986c2-150">Zaman aşımı saniye cinsinden araştırma</span><span class="sxs-lookup"><span data-stu-id="986c2-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="986c2-151">Sağlıksız durum eşiği.</span><span class="sxs-lookup"><span data-stu-id="986c2-151">Unhealthy threshold</span></span> |<span data-ttu-id="986c2-152">3</span><span class="sxs-lookup"><span data-stu-id="986c2-152">3</span></span> |<span data-ttu-id="986c2-153">Yeniden deneme sayısı araştırma.</span><span class="sxs-lookup"><span data-stu-id="986c2-153">Probe retry count.</span></span> <span data-ttu-id="986c2-154">Merhaba arka arkaya araştırma hatası sayısı hello sağlıksız durum eşiği ulaştıktan sonra hello arka uç sunucu işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="986c2-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="986c2-155">Çözüm</span><span class="sxs-lookup"><span data-stu-id="986c2-155">Solution</span></span>

* <span data-ttu-id="986c2-156">Varsayılan site yapılandırıldığından ve 127.0.0.1 dinleme emin olun.</span><span class="sxs-lookup"><span data-stu-id="986c2-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="986c2-157">BackendHttpSetting 80 dışında bir bağlantı noktası belirtiyorsa, bu bağlantı noktasında yapılandırılmış toolisten hello varsayılan site olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="986c2-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="986c2-158">Merhaba çağrısı toohttp://127.0.0.1:port bir HTTP Sonuç kodu 200 döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="986c2-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="986c2-159">Bu hello 30 saniye zaman aşımı süresi içinde döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="986c2-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="986c2-160">Yapılandırılan bağlantı noktası açık olduğundan ve hiçbir güvenlik duvarı kurallarının veya yapılandırılmış hello bağlantı noktasında gelen veya giden trafiği engellemek Azure ağ güvenlik grupları olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="986c2-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="986c2-161">Azure Klasik sanal makineleri veya Bulut hizmeti FQDN veya genel IP ile kullanılırsa, karşılık gelen hello olun [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) açılır.</span><span class="sxs-lookup"><span data-stu-id="986c2-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="986c2-162">Merhaba VM Azure Resource Manager aracılığıyla yapılandırılır ve uygulama ağ geçidi dağıtıldığı, VNet hello dışında ise [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) yapılandırılmalıdır hello tooallow erişimi istenen bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="986c2-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="986c2-163">Özel durum araştırması sorunları</span><span class="sxs-lookup"><span data-stu-id="986c2-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="986c2-164">Nedeni</span><span class="sxs-lookup"><span data-stu-id="986c2-164">Cause</span></span>

<span data-ttu-id="986c2-165">Özel sistem durumu araştırmalarının ek esneklik toohello varsayılan davranışı yoklama izin verir.</span><span class="sxs-lookup"><span data-stu-id="986c2-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="986c2-166">Özel araştırmalara kullanırken, kullanıcılar hello yoklama aralığı, hello URL ve yol tootest ve kaç tane başarısız yanıtları tooaccept hello arka uç havuzu örneği sağlıksız olarak işaretleme önce yapılandırabilir.</span><span class="sxs-lookup"><span data-stu-id="986c2-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="986c2-167">Aşağıdaki ek özelliklere hello eklenir.</span><span class="sxs-lookup"><span data-stu-id="986c2-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="986c2-168">Araştırma özelliği</span><span class="sxs-lookup"><span data-stu-id="986c2-168">Probe property</span></span> | <span data-ttu-id="986c2-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="986c2-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="986c2-170">Ad</span><span class="sxs-lookup"><span data-stu-id="986c2-170">Name</span></span> |<span data-ttu-id="986c2-171">Merhaba araştırma adı.</span><span class="sxs-lookup"><span data-stu-id="986c2-171">Name of hello probe.</span></span> <span data-ttu-id="986c2-172">Arka uç HTTP Ayarları'nda kullanılan toorefer toohello araştırma adıdır.</span><span class="sxs-lookup"><span data-stu-id="986c2-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="986c2-173">Protokol</span><span class="sxs-lookup"><span data-stu-id="986c2-173">Protocol</span></span> |<span data-ttu-id="986c2-174">Toosend hello araştırma kullanılan protokol.</span><span class="sxs-lookup"><span data-stu-id="986c2-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="986c2-175">Merhaba araştırma hello arka uç HTTP Ayarları'nda tanımlanan hello protokolünü kullanır</span><span class="sxs-lookup"><span data-stu-id="986c2-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="986c2-176">Host</span><span class="sxs-lookup"><span data-stu-id="986c2-176">Host</span></span> |<span data-ttu-id="986c2-177">Ana bilgisayar adı toosend hello araştırma.</span><span class="sxs-lookup"><span data-stu-id="986c2-177">Host name toosend hello probe.</span></span> <span data-ttu-id="986c2-178">Yalnızca uygulama ağ geçidinde çok siteli yapılandırıldığında uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="986c2-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="986c2-179">Bu VM ana bilgisayar adından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="986c2-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="986c2-180">Yol</span><span class="sxs-lookup"><span data-stu-id="986c2-180">Path</span></span> |<span data-ttu-id="986c2-181">Merhaba araştırma göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="986c2-181">Relative path of hello probe.</span></span> <span data-ttu-id="986c2-182">Merhaba geçerli bir yol başlatır '/'.</span><span class="sxs-lookup"><span data-stu-id="986c2-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="986c2-183">Merhaba araştırma çok gönderilen\<Protokolü\>://\<konak\>:\<bağlantı noktası\>\<yolu\></span><span class="sxs-lookup"><span data-stu-id="986c2-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="986c2-184">aralığı</span><span class="sxs-lookup"><span data-stu-id="986c2-184">Interval</span></span> |<span data-ttu-id="986c2-185">Aralığı saniye cinsinden araştırma.</span><span class="sxs-lookup"><span data-stu-id="986c2-185">Probe interval in seconds.</span></span> <span data-ttu-id="986c2-186">İki ardışık araştırmalar arasındaki hello zaman aralığını budur.</span><span class="sxs-lookup"><span data-stu-id="986c2-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="986c2-187">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="986c2-187">Time-out</span></span> |<span data-ttu-id="986c2-188">Zaman aşımı saniye cinsinden araştırma.</span><span class="sxs-lookup"><span data-stu-id="986c2-188">Probe time-out in seconds.</span></span> <span data-ttu-id="986c2-189">Bu zaman aşımı süresi içinde geçerli bir yanıt alınmazsa, hello araştırma başarısız olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="986c2-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="986c2-190">Sağlıksız durum eşiği.</span><span class="sxs-lookup"><span data-stu-id="986c2-190">Unhealthy threshold</span></span> |<span data-ttu-id="986c2-191">Yeniden deneme sayısı araştırma.</span><span class="sxs-lookup"><span data-stu-id="986c2-191">Probe retry count.</span></span> <span data-ttu-id="986c2-192">Merhaba arka arkaya araştırma hatası sayısı hello sağlıksız durum eşiği ulaştıktan sonra hello arka uç sunucu işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="986c2-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="986c2-193">Çözüm</span><span class="sxs-lookup"><span data-stu-id="986c2-193">Solution</span></span>

<span data-ttu-id="986c2-194">Özel durumu araştırma tablo önceki hello doğru bir şekilde yapılandırıldığından bu hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="986c2-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="986c2-195">Ayrıca toohello önceki sorun giderme adımları, ayrıca olun hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="986c2-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="986c2-196">Bu hello araştırma göredir hello doğru belirtildiğinden emin olun [Kılavuzu](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="986c2-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="986c2-197">Uygulama ağ geçidi tek bir site için yapılandırılmışsa, varsayılan hello ana bilgisayar tarafından adı '127.0.0.1', içinde özel araştırma aksi belirtilmedikçe belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="986c2-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="986c2-198">Çağrı toohttp emin olun: / /\<konak\>:\<bağlantı noktası\>\<yolu\> 200 bir HTTP Sonuç kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="986c2-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="986c2-199">Aralık, zaman aşımı ve UnhealtyThreshold hello kabul edilebilir aralık içinde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="986c2-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="986c2-200">Bir HTTPS kullanarak araştırma hello arka uç sunucu hello arka uç sunucusunun kendisi üzerinde bir geri dönüş sertifikası yapılandırarak SNI gerektirmeyen emin olun.</span><span class="sxs-lookup"><span data-stu-id="986c2-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="986c2-201">Aralık, zaman aşımı ve UnhealtyThreshold hello kabul edilebilir aralık içinde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="986c2-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="986c2-202">İstek zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="986c2-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="986c2-203">Nedeni</span><span class="sxs-lookup"><span data-stu-id="986c2-203">Cause</span></span>

<span data-ttu-id="986c2-204">Bir kullanıcı isteği alındığında, uygulama ağ geçidi yapılandırılmış hello kuralları toohello isteği uygular ve tooa arka uç havuzu örnek yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="986c2-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="986c2-205">Merhaba arka uç örnek yanıt süresinin yapılandırılabilir bir zaman aralığı için bekler.</span><span class="sxs-lookup"><span data-stu-id="986c2-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="986c2-206">Varsayılan olarak, bu aralığıdır **30 saniye**.</span><span class="sxs-lookup"><span data-stu-id="986c2-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="986c2-207">Uygulama ağ geçidi, bu aralıkta arka uç uygulamasından bir yanıt alamazsa, kullanıcı isteği 502 bir hata görür.</span><span class="sxs-lookup"><span data-stu-id="986c2-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="986c2-208">Çözüm</span><span class="sxs-lookup"><span data-stu-id="986c2-208">Solution</span></span>

<span data-ttu-id="986c2-209">Uygulama ağ geçidi olabilir sonra toodifferent havuzları uygulanan BackendHttpSetting aracılığıyla bu ayarı kullanıcıların tooconfigure sağlar.</span><span class="sxs-lookup"><span data-stu-id="986c2-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="986c2-210">Farklı arka uç havuzları farklı BackendHttpSetting ve bu nedenle farklı istek zaman aşımına yapılandırılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="986c2-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="986c2-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="986c2-211">Next steps</span></span>

<span data-ttu-id="986c2-212">Merhaba önceki adımları hello sorunu çözmezse, açık bir [destek bileti](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="986c2-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

