---
title: "Web uygulaması güvenlik duvarı - Azure uygulama ağ geçidi yapılandırma | Microsoft Docs"
description: "Bu makalede bir mevcut veya yeni uygulama ağ geçidi üzerinde web uygulaması Güvenlik Duvarı'nı kullanmaya başlamak hakkında yönergeler açıklanmaktadır."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: ac6c629ceaf1a8036643f593ce3d7ef9ea096ef8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="4c154-103">Web uygulaması güvenlik duvarı bir yeni veya var olan uygulama ağ geçidi ile Azure CLI yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4c154-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c154-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="4c154-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="4c154-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c154-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="4c154-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4c154-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="4c154-107">Web uygulaması Güvenlik Duvarı etkin uygulama ağ geçidi oluşturmak veya mevcut bir uygulama ağ geçidi için web uygulaması güvenlik duvarı nasıl ekleneceğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4c154-107">Learn how to create a web application firewall enabled application gateway or add web application firewall to an existing application gateway.</span></span>

<span data-ttu-id="4c154-108">Azure uygulama ağ geçidi, web uygulaması Güvenlik Duvarı (WAF), SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini web uygulamaları korur.</span><span class="sxs-lookup"><span data-stu-id="4c154-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="4c154-109">Azure Application Gateway, bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="4c154-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="4c154-110">Bulutta veya şirket içinde olmalarından bağımsız olarak, farklı sunucular arasında yük devretme ile HTTP istekleri için performans amaçlı yönlendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="4c154-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="4c154-111">Uygulama ağ geçidi HTTP dahil olmak üzere pek çok uygulama teslim denetleyici (ADC) özelliklerini Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının, çoklu site desteği ve diğer birçok sağlar.</span><span class="sxs-lookup"><span data-stu-id="4c154-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="4c154-112">Desteklenen özelliklerin tam listesi için ziyaret edin: [genel bakış, uygulama ağ geçidi](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c154-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="4c154-113">Aşağıdaki makale gösterir nasıl [var olan bir uygulama ağ geçidi için web uygulaması güvenlik duvarı ekleme](#add-web-application-firewall-to-an-existing-application-gateway) ve [web uygulaması Güvenlik Duvarı'nı kullanan bir uygulama ağ geçidini oluşturmak](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="4c154-113">The following article shows how to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![Senaryo görüntüsü][scenario]

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="4c154-115">Önkoşul: Azure CLI 2.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="4c154-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="4c154-116">Bu makaledeki adımları gerçekleştirmek için gerek [Mac, Linux ve Windows (Azure CLI) için Azure komut satırı arabirimini yükleyin](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="4c154-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="4c154-117">WAF yapılandırma farklılıkları</span><span class="sxs-lookup"><span data-stu-id="4c154-117">WAF configuration differences</span></span>

<span data-ttu-id="4c154-118">Okuma [Azure CLI ile bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-cli.md), bir uygulama ağ geçidi oluştururken yapılandırmak için SKU ayarları anlayın.</span><span class="sxs-lookup"><span data-stu-id="4c154-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand the SKU settings to configure when creating an application gateway.</span></span> <span data-ttu-id="4c154-119">WAF SKU üzerinde bir uygulama ağ geçidini yapılandırırken tanımlamak için ek ayarlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="4c154-119">WAF provides additional settings to define when configuring the SKU on an application gateway.</span></span> <span data-ttu-id="4c154-120">Uygulama ağ geçidinde kendisini oluşturan ek değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="4c154-120">There are no additional changes that you make on the application gateway itself.</span></span>

| <span data-ttu-id="4c154-121">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="4c154-121">**Setting**</span></span> | <span data-ttu-id="4c154-122">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="4c154-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="4c154-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="4c154-123">**SKU**</span></span> |<span data-ttu-id="4c154-124">Normal uygulama ağ geçidi WAF destekler olmadan **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**boyutları.</span><span class="sxs-lookup"><span data-stu-id="4c154-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="4c154-125">WAF başlanmasıyla, iki ek SKU vardır **WAF\_orta** ve **WAF\_büyük**.</span><span class="sxs-lookup"><span data-stu-id="4c154-125">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="4c154-126">WAF küçük uygulama ağ geçitleri üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="4c154-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="4c154-127">**Modu**</span><span class="sxs-lookup"><span data-stu-id="4c154-127">**Mode**</span></span> | <span data-ttu-id="4c154-128">Bu ayar WAF modudur.</span><span class="sxs-lookup"><span data-stu-id="4c154-128">This setting is the mode of WAF.</span></span> <span data-ttu-id="4c154-129">izin verilen değerler **algılama** ve **önleme**.</span><span class="sxs-lookup"><span data-stu-id="4c154-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="4c154-130">WAF algılama modunda ayarlandığında, tüm tehditler bir günlük dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="4c154-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="4c154-131">Önleme modda olayları yine kaydedilir ancak saldırgan 403 yetkisiz yanıt uygulama ağ geçidi'nden alır.</span><span class="sxs-lookup"><span data-stu-id="4c154-131">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the application gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="4c154-132">Web uygulaması güvenlik duvarı için var olan bir uygulama ağ geçidi Ekle</span><span class="sxs-lookup"><span data-stu-id="4c154-132">Add web application firewall to an existing application gateway</span></span>

<span data-ttu-id="4c154-133">İzleme komut WAF kullanan bir uygulama ağ geçidi için mevcut bir standart uygulama ağ geçidi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="4c154-133">The follow command changes an existing standard application gateway to a WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="4c154-134">Bu komut, uygulama ağ geçidi web uygulaması güvenlik duvarı ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4c154-134">This command updates the application gateway with web application firewall.</span></span> <span data-ttu-id="4c154-135">Ziyaret [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md) uygulama ağ geçidiniz için günlükleri görüntülemek nasıl anlamak için.</span><span class="sxs-lookup"><span data-stu-id="4c154-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your application gateway.</span></span> <span data-ttu-id="4c154-136">WAF güvenlik yapısı nedeniyle, günlükleri, web uygulamalarınızı güvenlik yaklaşımı anlamak için düzenli olarak gözden geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c154-136">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="4c154-137">Web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c154-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="4c154-138">Aşağıdaki komut, web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4c154-138">The following command creates an Application Gateway with web application firewall.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> <span data-ttu-id="4c154-139">Temel web uygulaması güvenlik duvarı yapılandırması ile oluşturulmuş uygulama ağ geçitleri için koruma CRS 3.0 ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="4c154-139">Application gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="4c154-140">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="4c154-140">Get application gateway DNS name</span></span>

<span data-ttu-id="4c154-141">Ağ geçidi oluşturulduktan sonraki adım, iletişim için ön uç yapılandırması yapmaktır.</span><span class="sxs-lookup"><span data-stu-id="4c154-141">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="4c154-142">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="4c154-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="4c154-143">Son kullanıcıların uygulama ağ geçidine ulaşmasını sağlamak için uygulama ağ geçidinin genel uç noktasını işaret edecek bir CNAME kaydı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4c154-143">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="4c154-144">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4c154-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="4c154-145">Bir CNAME kaydı yapılandırmak için uygulama ağ geçidi ve ilişkili IP/DNS adını kullanarak uygulama ağ geçidine bağlı Publicıpaddress öğesi ayrıntılarını alamadı.</span><span class="sxs-lookup"><span data-stu-id="4c154-145">To configure a CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="4c154-146">Uygulama ağ geçidinin DNS adı, iki web uygulamasını bu DNS adına götüren bir CNAME kaydı oluşturmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4c154-146">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="4c154-147">Uygulama ağ geçidi yeniden başlatıldığında VIP değişebileceğinden A kaydı kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="4c154-147">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="next-steps"></a><span data-ttu-id="4c154-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c154-148">Next steps</span></span>

<span data-ttu-id="4c154-149">WAF kuralları ziyaret ederek özelleştirmeyi öğrenin: [Azure CLI 2.0 aracılığıyla web uygulaması güvenlik duvarı kurallarını özelleştirmek](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4c154-149">Learn how to customize WAF rules by visiting: [Customize web application firewall rules through the Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
