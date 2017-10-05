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
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Web uygulaması güvenlik duvarı bir yeni veya var olan uygulama ağ geçidi ile Azure CLI yapılandırın

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

Web uygulaması Güvenlik Duvarı etkin uygulama ağ geçidi oluşturmak veya mevcut bir uygulama ağ geçidi için web uygulaması güvenlik duvarı nasıl ekleneceğini öğrenin.

Azure uygulama ağ geçidi, web uygulaması Güvenlik Duvarı (WAF), SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini web uygulamaları korur.

Azure Application Gateway, bir katman 7 yük dengeleyicidir. Bulutta veya şirket içinde olmalarından bağımsız olarak, farklı sunucular arasında yük devretme ile HTTP istekleri için performans amaçlı yönlendirme sağlar. Uygulama ağ geçidi HTTP dahil olmak üzere pek çok uygulama teslim denetleyici (ADC) özelliklerini Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının, çoklu site desteği ve diğer birçok sağlar. Desteklenen özelliklerin tam listesi için ziyaret edin: [genel bakış, uygulama ağ geçidi](application-gateway-introduction.md).

Aşağıdaki makale gösterir nasıl [var olan bir uygulama ağ geçidi için web uygulaması güvenlik duvarı ekleme](#add-web-application-firewall-to-an-existing-application-gateway) ve [web uygulaması Güvenlik Duvarı'nı kullanan bir uygulama ağ geçidini oluşturmak](#create-an-application-gateway-with-web-application-firewall).

![Senaryo görüntüsü][scenario]

## <a name="prerequisite-install-the-azure-cli-20"></a>Önkoşul: Azure CLI 2.0 yükleyin

Bu makaledeki adımları gerçekleştirmek için gerek [Mac, Linux ve Windows (Azure CLI) için Azure komut satırı arabirimini yükleyin](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="waf-configuration-differences"></a>WAF yapılandırma farklılıkları

Okuma [Azure CLI ile bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-cli.md), bir uygulama ağ geçidi oluştururken yapılandırmak için SKU ayarları anlayın. WAF SKU üzerinde bir uygulama ağ geçidini yapılandırırken tanımlamak için ek ayarlar sağlar. Uygulama ağ geçidinde kendisini oluşturan ek değişiklik yoktur.

| **Ayar** | **Ayrıntılar**
|---|---|
|**SKU** |Normal uygulama ağ geçidi WAF destekler olmadan **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**boyutları. WAF başlanmasıyla, iki ek SKU vardır **WAF\_orta** ve **WAF\_büyük**. WAF küçük uygulama ağ geçitleri üzerinde desteklenmiyor.|
|**Modu** | Bu ayar WAF modudur. izin verilen değerler **algılama** ve **önleme**. WAF algılama modunda ayarlandığında, tüm tehditler bir günlük dosyasında depolanır. Önleme modda olayları yine kaydedilir ancak saldırgan 403 yetkisiz yanıt uygulama ağ geçidi'nden alır.|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Web uygulaması güvenlik duvarı için var olan bir uygulama ağ geçidi Ekle

İzleme komut WAF kullanan bir uygulama ağ geçidi için mevcut bir standart uygulama ağ geçidi değiştirir.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

Bu komut, uygulama ağ geçidi web uygulaması güvenlik duvarı ile güncelleştirir. Ziyaret [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md) uygulama ağ geçidiniz için günlükleri görüntülemek nasıl anlamak için. WAF güvenlik yapısı nedeniyle, günlükleri, web uygulamalarınızı güvenlik yaklaşımı anlamak için düzenli olarak gözden geçirilmesi gerekir.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma

Aşağıdaki komut, web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturur.

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
> Temel web uygulaması güvenlik duvarı yapılandırması ile oluşturulmuş uygulama ağ geçitleri için koruma CRS 3.0 ile yapılandırılır.

## <a name="get-application-gateway-dns-name"></a>Uygulama ağ geçidi DNS adını alma

Ağ geçidi oluşturulduktan sonraki adım, iletişim için ön uç yapılandırması yapmaktır. Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir. Son kullanıcıların uygulama ağ geçidine ulaşmasını sağlamak için uygulama ağ geçidinin genel uç noktasını işaret edecek bir CNAME kaydı kullanılabilir. [Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md). Bir CNAME kaydı yapılandırmak için uygulama ağ geçidi ve ilişkili IP/DNS adını kullanarak uygulama ağ geçidine bağlı Publicıpaddress öğesi ayrıntılarını alamadı. Uygulama ağ geçidinin DNS adı, iki web uygulamasını bu DNS adına götüren bir CNAME kaydı oluşturmak için kullanılmalıdır. Uygulama ağ geçidi yeniden başlatıldığında VIP değişebileceğinden A kaydı kullanımı önerilmez.

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

## <a name="next-steps"></a>Sonraki adımlar

WAF kuralları ziyaret ederek özelleştirmeyi öğrenin: [Azure CLI 2.0 aracılığıyla web uygulaması güvenlik duvarı kurallarını özelleştirmek](application-gateway-customize-waf-rules-cli.md).

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
