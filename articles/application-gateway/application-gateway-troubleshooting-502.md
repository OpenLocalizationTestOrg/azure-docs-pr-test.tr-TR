---
title: "Azure uygulama ağ geçidi hatalı ağ geçidi (502) hatalarında sorun giderme | Microsoft Docs"
description: "Uygulama ağ geçidi 502 hatalarında sorun giderme hakkında bilgi edinin"
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
ms.openlocfilehash: cbf9c552c4818b3925f449081539f1db6d61918e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="ab8cd-103">Uygulama ağ geçidi olarak hatalı ağ geçidi hatalarında sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ab8cd-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="ab8cd-104">Uygulama ağ geçidi kullanırken karşılaşılan hatalı ağ geçidi (502) hataları giderme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-104">Learn how to troubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="ab8cd-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ab8cd-105">Overview</span></span>

<span data-ttu-id="ab8cd-106">Bir uygulama ağ geçidi yapılandırdıktan sonra kullanıcılar karşılaşabilirsiniz hataları biri olan "sunucu hatası: 502 - Web sunucusu alınan geçersiz bir yanıt bir ağ geçidi veya proxy sunucu olarak çalışırken".</span><span class="sxs-lookup"><span data-stu-id="ab8cd-106">After configuring an application gateway, one of the errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="ab8cd-107">Bu hata, aşağıdaki ana nedenlerden ötürü oluşabilir:</span><span class="sxs-lookup"><span data-stu-id="ab8cd-107">This error may happen due to the following main reasons:</span></span>

* <span data-ttu-id="ab8cd-108">Azure uygulama ağ geçidi [arka uç havuzu yapılandırılmış ya da boş değil](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="ab8cd-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="ab8cd-109">Sanal makineler veya durumlarda hiçbiri [VM ölçek kümesi sağlıklı](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="ab8cd-109">None of the VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="ab8cd-110">Arka uç VM'ler veya VM ölçek kümesi örneklerinin [varsayılan durumu araştırması için yanıt vermiyor](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="ab8cd-110">Back-end VMs or instances of VM Scale Set are [not responding to the default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="ab8cd-111">Geçersiz veya hatalı [özel sistem durumu araştırmalarının yapılandırmasını](#problems-with-custom-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="ab8cd-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="ab8cd-112">[İstek zaman aşımı veya bağlantı sorunları](#request-time-out) kullanıcı istekleri ile.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="ab8cd-113">Boş BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="ab8cd-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="ab8cd-114">Nedeni</span><span class="sxs-lookup"><span data-stu-id="ab8cd-114">Cause</span></span>

<span data-ttu-id="ab8cd-115">Uygulama ağ geçidi hiçbir sanal makineleri veya arka uç adres havuzunda yapılandırılmış VM ölçek kümesi varsa, herhangi bir müşteri istek yönlendiremezsiniz ve hatalı ağ geçidi hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-115">If the Application Gateway has no VMs or VM Scale Set configured in the back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="ab8cd-116">Çözüm</span><span class="sxs-lookup"><span data-stu-id="ab8cd-116">Solution</span></span>

<span data-ttu-id="ab8cd-117">Arka uç adres havuzu boş olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-117">Ensure that the back-end address pool is not empty.</span></span> <span data-ttu-id="ab8cd-118">Bu da PowerShell'i, CLI veya portal aracılığıyla yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="ab8cd-119">Yukarıdaki cmdlet çıktısından boş arka uç adres havuzu içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-119">The output from the preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="ab8cd-120">Aşağıdaki iki havuzları, burada döndürülen bir örnek verilmiştir arka uç VM'ler için FQDN veya IP adresleriyle yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="ab8cd-121">BackendAddressPool sağlama durumunun 'başarılı' olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-121">The provisioning state of the BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="ab8cd-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="ab8cd-122">BackendAddressPoolsText:</span></span>

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

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="ab8cd-123">BackendAddressPool kötü durumda</span><span class="sxs-lookup"><span data-stu-id="ab8cd-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="ab8cd-124">Nedeni</span><span class="sxs-lookup"><span data-stu-id="ab8cd-124">Cause</span></span>

<span data-ttu-id="ab8cd-125">BackendAddressPool tüm örneklerini sağlam olmaması ise, uygulama ağ geçidi kullanıcı istek için tüm arka uç bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-125">If all the instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end to route user request to.</span></span> <span data-ttu-id="ab8cd-126">Arka uç örnekleri sağlıklı ancak dağıtılan gerekli uygulama yoksa olduğunda bu durum olabilir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-126">This could also be the case when back-end instances are healthy but do not have the required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="ab8cd-127">Çözüm</span><span class="sxs-lookup"><span data-stu-id="ab8cd-127">Solution</span></span>

<span data-ttu-id="ab8cd-128">Örnekleri sağlıklı olduğunu ve uygulama'nın düzgün yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-128">Ensure that the instances are healthy and the application is properly configured.</span></span> <span data-ttu-id="ab8cd-129">Arka uç örnekleri aynı sanal ağda başka bir VM'den bir ping işlemine yanıt verebilir durumda olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-129">Check if the back-end instances are able to respond to a ping from another VM in the same VNet.</span></span> <span data-ttu-id="ab8cd-130">Ortak bir uç nokta ile yapılandırılmışsa, bir tarayıcı isteğini web uygulamasına hizmet verilebilen olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-130">If configured with a public end point, ensure that a browser request to the web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="ab8cd-131">Varsayılan durumu araştırması sorunları</span><span class="sxs-lookup"><span data-stu-id="ab8cd-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="ab8cd-132">Nedeni</span><span class="sxs-lookup"><span data-stu-id="ab8cd-132">Cause</span></span>

<span data-ttu-id="ab8cd-133">502 hataları sık göstergeleri varsayılan durumu araştırması arka uç VM'ler ulaşabilmesi değil de olabilir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-133">502 errors can also be frequent indicators that the default health probe is not able to reach back-end VMs.</span></span> <span data-ttu-id="ab8cd-134">Bir uygulama ağ geçidi örneği sağlandığında, varsayılan durumu araştırması BackendHttpSetting özelliklerini kullanarak her BackendAddressPool için otomatik olarak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe to each BackendAddressPool using properties of the BackendHttpSetting.</span></span> <span data-ttu-id="ab8cd-135">Kullanıcı girişi yok, bu araştırma ayarlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-135">No user input is required to set this probe.</span></span> <span data-ttu-id="ab8cd-136">Özellikle, bir Yük Dengeleme kuralı yapılandırıldığında, bir ilişki BackendHttpSetting ve BackendAddressPool arasında yapılır.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="ab8cd-137">Bir varsayılan araştırma her bu ilişkileri için yapılandırılır ve uygulama ağ geçidi BackendHttpSetting öğesinde belirtilen bağlantı noktasında BackendAddressPool her örnek düzenli sistem durumu denetimi bağlantı başlatır.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection to each instance in the BackendAddressPool at the port specified in the BackendHttpSetting element.</span></span> <span data-ttu-id="ab8cd-138">Aşağıdaki tabloda varsayılan sistem durumu araştırma URL'siyle ilişkili değerleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-138">Following table lists the values associated with the default health probe.</span></span>

| <span data-ttu-id="ab8cd-139">Araştırma özelliği</span><span class="sxs-lookup"><span data-stu-id="ab8cd-139">Probe property</span></span> | <span data-ttu-id="ab8cd-140">Değer</span><span class="sxs-lookup"><span data-stu-id="ab8cd-140">Value</span></span> | <span data-ttu-id="ab8cd-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab8cd-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ab8cd-142">Araştırma URL'si</span><span class="sxs-lookup"><span data-stu-id="ab8cd-142">Probe URL</span></span> |<span data-ttu-id="ab8cd-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="ab8cd-143">http://127.0.0.1/</span></span> |<span data-ttu-id="ab8cd-144">URL yolu</span><span class="sxs-lookup"><span data-stu-id="ab8cd-144">URL path</span></span> |
| <span data-ttu-id="ab8cd-145">aralığı</span><span class="sxs-lookup"><span data-stu-id="ab8cd-145">Interval</span></span> |<span data-ttu-id="ab8cd-146">30</span><span class="sxs-lookup"><span data-stu-id="ab8cd-146">30</span></span> |<span data-ttu-id="ab8cd-147">Saniye cinsinden yoklama aralığı</span><span class="sxs-lookup"><span data-stu-id="ab8cd-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="ab8cd-148">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="ab8cd-148">Time-out</span></span> |<span data-ttu-id="ab8cd-149">30</span><span class="sxs-lookup"><span data-stu-id="ab8cd-149">30</span></span> |<span data-ttu-id="ab8cd-150">Zaman aşımı saniye cinsinden araştırma</span><span class="sxs-lookup"><span data-stu-id="ab8cd-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="ab8cd-151">Sağlıksız durum eşiği.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-151">Unhealthy threshold</span></span> |<span data-ttu-id="ab8cd-152">3</span><span class="sxs-lookup"><span data-stu-id="ab8cd-152">3</span></span> |<span data-ttu-id="ab8cd-153">Yeniden deneme sayısı araştırma.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-153">Probe retry count.</span></span> <span data-ttu-id="ab8cd-154">Sağlıksız eşik arka arkaya araştırma hatası sayısı ulaştıktan sonra arka uç sunucu işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-154">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="ab8cd-155">Çözüm</span><span class="sxs-lookup"><span data-stu-id="ab8cd-155">Solution</span></span>

* <span data-ttu-id="ab8cd-156">Varsayılan site yapılandırıldığından ve 127.0.0.1 dinleme emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="ab8cd-157">BackendHttpSetting 80 dışında bir bağlantı noktası belirtiyorsa, varsayılan site Bu bağlantı noktasını dinlemek üzere yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-157">If BackendHttpSetting specifies a port other than 80, the default site should be configured to listen at that port.</span></span>
* <span data-ttu-id="ab8cd-158">Http://127.0.0.1:port çağrısı bir HTTP Sonuç kodu 200 döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-158">The call to http://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="ab8cd-159">Bu 30 saniye zaman aşımı süresi içinde döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-159">This should be returned within the 30 sec time-out period.</span></span>
* <span data-ttu-id="ab8cd-160">Yapılandırılan bağlantı noktası açık olduğundan ve güvenlik duvarı kuralları ya da yapılandırılan bağlantı noktasındaki gelen veya giden trafiği engellemek Azure ağ güvenlik grupları olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on the port configured.</span></span>
* <span data-ttu-id="ab8cd-161">Azure Klasik sanal makineleri veya Bulut hizmeti FQDN veya genel IP ile kullanılırsa, karşılık gelen emin [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) açılır.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that the corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="ab8cd-162">VM Azure Resource Manager aracılığıyla yapılandırılır ve uygulama ağ geçidi dağıtıldığı, sanal ağ dışında ise [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) istenen bağlantı noktası erişime izin verecek şekilde yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-162">If the VM is configured via Azure Resource Manager and is outside the VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured to allow access on the desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="ab8cd-163">Özel durum araştırması sorunları</span><span class="sxs-lookup"><span data-stu-id="ab8cd-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="ab8cd-164">Nedeni</span><span class="sxs-lookup"><span data-stu-id="ab8cd-164">Cause</span></span>

<span data-ttu-id="ab8cd-165">Özel sistem durumu araştırmalarının davranışı yoklama varsayılan ek esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-165">Custom health probes allow additional flexibility to the default probing behavior.</span></span> <span data-ttu-id="ab8cd-166">Özel araştırmalara kullanırken, kullanıcılar yoklama aralığı, URL ve test etmek için yolu ve arka uç havuzu örneği sağlıksız olarak işaretleme önce kabul etmek için kaç tane başarısız yanıtları yapılandırabilir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-166">When using custom probes, users can configure the probe interval, the URL, and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span> <span data-ttu-id="ab8cd-167">Aşağıdaki ek özellikler eklenir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-167">The following additional properties are added.</span></span>

| <span data-ttu-id="ab8cd-168">Araştırma özelliği</span><span class="sxs-lookup"><span data-stu-id="ab8cd-168">Probe property</span></span> | <span data-ttu-id="ab8cd-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab8cd-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab8cd-170">Ad</span><span class="sxs-lookup"><span data-stu-id="ab8cd-170">Name</span></span> |<span data-ttu-id="ab8cd-171">Araştırma adı.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-171">Name of the probe.</span></span> <span data-ttu-id="ab8cd-172">Bu ad, arka uç HTTP Ayarları'nda araştırma başvurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-172">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="ab8cd-173">Protokol</span><span class="sxs-lookup"><span data-stu-id="ab8cd-173">Protocol</span></span> |<span data-ttu-id="ab8cd-174">Araştırma göndermek için kullanılan protokol.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-174">Protocol used to send the probe.</span></span> <span data-ttu-id="ab8cd-175">Araştırma arka uç HTTP Ayarları'nda tanımlanan protokolünü kullanır</span><span class="sxs-lookup"><span data-stu-id="ab8cd-175">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="ab8cd-176">Host</span><span class="sxs-lookup"><span data-stu-id="ab8cd-176">Host</span></span> |<span data-ttu-id="ab8cd-177">Araştırma göndermek için ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-177">Host name to send the probe.</span></span> <span data-ttu-id="ab8cd-178">Yalnızca uygulama ağ geçidinde çok siteli yapılandırıldığında uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="ab8cd-179">Bu VM ana bilgisayar adından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="ab8cd-180">Yol</span><span class="sxs-lookup"><span data-stu-id="ab8cd-180">Path</span></span> |<span data-ttu-id="ab8cd-181">Araştırma göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-181">Relative path of the probe.</span></span> <span data-ttu-id="ab8cd-182">Geçerli yol başlar '/'.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-182">The valid path starts from '/'.</span></span> <span data-ttu-id="ab8cd-183">Yoklama için gönderilen \<Protokolü\>://\<konak\>:\<bağlantı noktası\>\<yolu\></span><span class="sxs-lookup"><span data-stu-id="ab8cd-183">The probe is sent to \<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="ab8cd-184">aralığı</span><span class="sxs-lookup"><span data-stu-id="ab8cd-184">Interval</span></span> |<span data-ttu-id="ab8cd-185">Aralığı saniye cinsinden araştırma.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-185">Probe interval in seconds.</span></span> <span data-ttu-id="ab8cd-186">Bu iki ardışık araştırmalar arasında zaman aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-186">This is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="ab8cd-187">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="ab8cd-187">Time-out</span></span> |<span data-ttu-id="ab8cd-188">Zaman aşımı saniye cinsinden araştırma.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-188">Probe time-out in seconds.</span></span> <span data-ttu-id="ab8cd-189">Bu zaman aşımı süresi içinde geçerli bir yanıt alınmazsa, araştırma başarısız olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-189">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span> |
| <span data-ttu-id="ab8cd-190">Sağlıksız durum eşiği.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-190">Unhealthy threshold</span></span> |<span data-ttu-id="ab8cd-191">Yeniden deneme sayısı araştırma.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-191">Probe retry count.</span></span> <span data-ttu-id="ab8cd-192">Sağlıksız eşik arka arkaya araştırma hatası sayısı ulaştıktan sonra arka uç sunucu işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-192">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="ab8cd-193">Çözüm</span><span class="sxs-lookup"><span data-stu-id="ab8cd-193">Solution</span></span>

<span data-ttu-id="ab8cd-194">Özel durumu araştırma yukarıdaki tabloda olarak doğru bir şekilde yapılandırıldığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-194">Validate that the Custom Health Probe is configured correctly as the preceding table.</span></span> <span data-ttu-id="ab8cd-195">Önceki sorun giderme adımları yanı sıra, aynı zamanda aşağıdakilerden emin olun:</span><span class="sxs-lookup"><span data-stu-id="ab8cd-195">In addition to the preceding troubleshooting steps, also ensure the following:</span></span>

* <span data-ttu-id="ab8cd-196">Araştırma göre doğru belirtildiğinden emin olun [Kılavuzu](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ab8cd-196">Ensure that the probe is correctly specified as per the [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="ab8cd-197">Uygulama ağ geçidi tek bir site için yapılandırılmışsa, varsayılan olarak ana bilgisayar adı '127.0.0.1' içinde özel araştırma aksi belirtilmedikçe belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-197">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="ab8cd-198">Http:// çağrısına emin\<konak\>:\<bağlantı noktası\>\<yolu\> 200 bir HTTP Sonuç kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-198">Ensure that a call to http://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="ab8cd-199">Aralık, zaman aşımı ve UnhealtyThreshold kabul edilebilir aralık içinde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-199">Ensure that Interval, Time-out and UnhealtyThreshold are within the acceptable ranges.</span></span>
* <span data-ttu-id="ab8cd-200">Bir HTTPS kullanarak araştırma, arka uç sunucusunun kendisi üzerinde bir geri dönüş sertifikası yapılandırarak arka uç sunucusuna SNI gerektirmeyen emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-200">If using an HTTPS probe, make sure that the backend server doesn't require SNI by configuring a fallback certificate on the backend server itself.</span></span> 
* <span data-ttu-id="ab8cd-201">Aralık, zaman aşımı ve UnhealtyThreshold kabul edilebilir aralık içinde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within the acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="ab8cd-202">İstek zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="ab8cd-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="ab8cd-203">Nedeni</span><span class="sxs-lookup"><span data-stu-id="ab8cd-203">Cause</span></span>

<span data-ttu-id="ab8cd-204">Bir kullanıcı isteği alındığında, uygulama ağ geçidi isteği yapılandırılmış kurallarını uygular ve bir arka uç havuzu örneğine yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-204">When a user request is received, Application Gateway applies the configured rules to the request and routes it to a back-end pool instance.</span></span> <span data-ttu-id="ab8cd-205">Arka uç örnek yanıt süresinin yapılandırılabilir bir zaman aralığı için bekler.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-205">It waits for a configurable interval of time for a response from the back-end instance.</span></span> <span data-ttu-id="ab8cd-206">Varsayılan olarak, bu aralığıdır **30 saniye**.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="ab8cd-207">Uygulama ağ geçidi, bu aralıkta arka uç uygulamasından bir yanıt alamazsa, kullanıcı isteği 502 bir hata görür.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="ab8cd-208">Çözüm</span><span class="sxs-lookup"><span data-stu-id="ab8cd-208">Solution</span></span>

<span data-ttu-id="ab8cd-209">Uygulama ağ geçidi için farklı havuzlar uygulanabilir BackendHttpSetting aracılığıyla bu ayarı yapılandırmak kullanıcıların sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-209">Application Gateway allows users to configure this setting via BackendHttpSetting, which can be then applied to different pools.</span></span> <span data-ttu-id="ab8cd-210">Farklı arka uç havuzları farklı BackendHttpSetting ve bu nedenle farklı istek zaman aşımına yapılandırılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="ab8cd-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="ab8cd-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab8cd-211">Next steps</span></span>

<span data-ttu-id="ab8cd-212">Yukarıdaki adımlar sorunu çözmezse, açık bir [destek bileti](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="ab8cd-212">If the preceding steps do not resolve the issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

