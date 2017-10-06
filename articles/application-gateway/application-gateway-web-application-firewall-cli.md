---
title: "aaaConfigure web uygulaması güvenlik duvarı - Azure uygulama ağ geçidi | Microsoft Docs"
description: "Bu makalede, nasıl toostart kullanarak izin ver web uygulaması Güvenlik Duvarı'nı varolan veya yeni uygulama ağ geçidi hakkında yönergeleri sunar."
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
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="47a32-103">Web uygulaması güvenlik duvarı bir yeni veya var olan uygulama ağ geçidi ile Azure CLI yapılandırın</span><span class="sxs-lookup"><span data-stu-id="47a32-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="47a32-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="47a32-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="47a32-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47a32-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="47a32-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="47a32-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="47a32-107">Web uygulaması güvenlik duvarı tooan varolan uygulama ağ geçidi eklemek veya nasıl uygulama ağ geçidi toocreate bir web uygulaması Güvenlik Duvarı etkin öğrenin.</span><span class="sxs-lookup"><span data-stu-id="47a32-107">Learn how toocreate a web application firewall enabled application gateway or add web application firewall tooan existing application gateway.</span></span>

<span data-ttu-id="47a32-108">Hello web uygulaması Güvenlik Duvarı (WAF) Azure uygulama ağ geçidi, web uygulamaları, SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini korur.</span><span class="sxs-lookup"><span data-stu-id="47a32-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="47a32-109">Azure Application Gateway, bir katman 7 yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="47a32-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="47a32-110">Merhaba Bulut veya şirket içinde olmalarından bağımsız yük devretme, HTTP isteklerini, farklı sunucular arasında performans amaçlı yönlendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="47a32-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="47a32-111">Uygulama ağ geçidi HTTP dahil olmak üzere pek çok uygulama teslim denetleyici (ADC) özelliklerini Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının, çoklu site desteği ve diğer birçok sağlar.</span><span class="sxs-lookup"><span data-stu-id="47a32-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="47a32-112">toofind desteklenen özelliklerin tam bir listesi ziyaret edin: [genel bakış, uygulama ağ geçidi](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47a32-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="47a32-113">Merhaba aşağıdaki makalede nasıl çok gösterilmektedir[web uygulaması güvenlik duvarı tooan varolan uygulama ağ geçidi eklemek](#add-web-application-firewall-to-an-existing-application-gateway) ve [web uygulaması Güvenlik Duvarı'nı kullanan bir uygulama ağ geçidini oluşturmak](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="47a32-113">hello following article shows how too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![Senaryo görüntüsü][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="47a32-115">Önkoşul: hello Azure CLI 2.0 yükleyin</span><span class="sxs-lookup"><span data-stu-id="47a32-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="47a32-116">Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="47a32-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="47a32-117">WAF yapılandırma farklılıkları</span><span class="sxs-lookup"><span data-stu-id="47a32-117">WAF configuration differences</span></span>

<span data-ttu-id="47a32-118">Okuma [Azure CLI ile bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-cli.md), bir uygulama ağ geçidi oluştururken hello SKU ayarları tooconfigure anlayın.</span><span class="sxs-lookup"><span data-stu-id="47a32-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand hello SKU settings tooconfigure when creating an application gateway.</span></span> <span data-ttu-id="47a32-119">WAF ek ayarlar toodefine hello SKU üzerinde bir uygulama ağ geçidini yapılandırırken sağlar.</span><span class="sxs-lookup"><span data-stu-id="47a32-119">WAF provides additional settings toodefine when configuring hello SKU on an application gateway.</span></span> <span data-ttu-id="47a32-120">Merhaba uygulama ağ geçidinde kendisini oluşturan ek değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="47a32-120">There are no additional changes that you make on hello application gateway itself.</span></span>

| <span data-ttu-id="47a32-121">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="47a32-121">**Setting**</span></span> | <span data-ttu-id="47a32-122">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="47a32-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="47a32-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="47a32-123">**SKU**</span></span> |<span data-ttu-id="47a32-124">Normal uygulama ağ geçidi WAF destekler olmadan **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**boyutları.</span><span class="sxs-lookup"><span data-stu-id="47a32-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="47a32-125">WAF Hello başlanmasıyla, iki ek SKU vardır **WAF\_orta** ve **WAF\_büyük**.</span><span class="sxs-lookup"><span data-stu-id="47a32-125">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="47a32-126">WAF küçük uygulama ağ geçitleri üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="47a32-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="47a32-127">**Modu**</span><span class="sxs-lookup"><span data-stu-id="47a32-127">**Mode**</span></span> | <span data-ttu-id="47a32-128">Bu ayar, WAF, hello modudur.</span><span class="sxs-lookup"><span data-stu-id="47a32-128">This setting is hello mode of WAF.</span></span> <span data-ttu-id="47a32-129">izin verilen değerler **algılama** ve **önleme**.</span><span class="sxs-lookup"><span data-stu-id="47a32-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="47a32-130">WAF algılama modunda ayarlandığında, tüm tehditler bir günlük dosyasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="47a32-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="47a32-131">Önleme modda olayları yine kaydedilir ancak hello saldırgan 403 yetkisiz yanıt hello uygulama ağ geçidi'nden alır.</span><span class="sxs-lookup"><span data-stu-id="47a32-131">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello application gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="47a32-132">Web uygulaması güvenlik duvarı tooan varolan uygulama ağ geçidi Ekle</span><span class="sxs-lookup"><span data-stu-id="47a32-132">Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="47a32-133">Merhaba, mevcut bir standart uygulama ağ geçidi tooa WAF kullanan bir uygulama ağ geçidi komutu değişikliklerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="47a32-133">hello follow command changes an existing standard application gateway tooa WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="47a32-134">Bu komut hello uygulama ağ geçidi web uygulaması güvenlik duvarı ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="47a32-134">This command updates hello application gateway with web application firewall.</span></span> <span data-ttu-id="47a32-135">Ziyaret [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md) toounderstand tooview uygulama ağ geçidiniz için nasıl günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="47a32-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your application gateway.</span></span> <span data-ttu-id="47a32-136">Güvenlik yapısı toohello WAF, günlükleri gerek toobe toounderstand hello güvenlik yaklaşımı, web uygulamalarınızı, düzenli olarak gözden.</span><span class="sxs-lookup"><span data-stu-id="47a32-136">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="47a32-137">Web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="47a32-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="47a32-138">komutu aşağıdaki hello web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="47a32-138">hello following command creates an Application Gateway with web application firewall.</span></span>

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
> <span data-ttu-id="47a32-139">Merhaba temel web uygulaması güvenlik duvarı yapılandırması ile oluşturulmuş uygulama ağ geçitleri için koruma CRS 3.0 ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="47a32-139">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="47a32-140">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="47a32-140">Get application gateway DNS name</span></span>

<span data-ttu-id="47a32-141">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="47a32-141">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="47a32-142">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="47a32-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="47a32-143">hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="47a32-143">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="47a32-144">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47a32-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="47a32-145">tooconfigure bir CNAME kaydı ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adını alır.</span><span class="sxs-lookup"><span data-stu-id="47a32-145">tooconfigure a CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="47a32-146">Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="47a32-146">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="47a32-147">Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="47a32-147">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="47a32-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="47a32-148">Next steps</span></span>

<span data-ttu-id="47a32-149">Nasıl toocustomize WAF adresini ziyaret ederek kurallar öğrenin: [hello Azure CLI 2.0 aracılığıyla web uygulaması güvenlik duvarı kurallarını özelleştirmek](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="47a32-149">Learn how toocustomize WAF rules by visiting: [Customize web application firewall rules through hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
