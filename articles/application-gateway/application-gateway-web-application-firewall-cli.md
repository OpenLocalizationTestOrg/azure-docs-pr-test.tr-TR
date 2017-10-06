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
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Web uygulaması güvenlik duvarı bir yeni veya var olan uygulama ağ geçidi ile Azure CLI yapılandırın

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

Web uygulaması güvenlik duvarı tooan varolan uygulama ağ geçidi eklemek veya nasıl uygulama ağ geçidi toocreate bir web uygulaması Güvenlik Duvarı etkin öğrenin.

Hello web uygulaması Güvenlik Duvarı (WAF) Azure uygulama ağ geçidi, web uygulamaları, SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini korur.

Azure Application Gateway, bir katman 7 yük dengeleyicidir. Merhaba Bulut veya şirket içinde olmalarından bağımsız yük devretme, HTTP isteklerini, farklı sunucular arasında performans amaçlı yönlendirme sağlar. Uygulama ağ geçidi HTTP dahil olmak üzere pek çok uygulama teslim denetleyici (ADC) özelliklerini Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının, çoklu site desteği ve diğer birçok sağlar. toofind desteklenen özelliklerin tam bir listesi ziyaret edin: [genel bakış, uygulama ağ geçidi](application-gateway-introduction.md).

Merhaba aşağıdaki makalede nasıl çok gösterilmektedir[web uygulaması güvenlik duvarı tooan varolan uygulama ağ geçidi eklemek](#add-web-application-firewall-to-an-existing-application-gateway) ve [web uygulaması Güvenlik Duvarı'nı kullanan bir uygulama ağ geçidini oluşturmak](#create-an-application-gateway-with-web-application-firewall).

![Senaryo görüntüsü][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a>Önkoşul: hello Azure CLI 2.0 yükleyin

Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="waf-configuration-differences"></a>WAF yapılandırma farklılıkları

Okuma [Azure CLI ile bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-cli.md), bir uygulama ağ geçidi oluştururken hello SKU ayarları tooconfigure anlayın. WAF ek ayarlar toodefine hello SKU üzerinde bir uygulama ağ geçidini yapılandırırken sağlar. Merhaba uygulama ağ geçidinde kendisini oluşturan ek değişiklik yoktur.

| **Ayar** | **Ayrıntılar**
|---|---|
|**SKU** |Normal uygulama ağ geçidi WAF destekler olmadan **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**boyutları. WAF Hello başlanmasıyla, iki ek SKU vardır **WAF\_orta** ve **WAF\_büyük**. WAF küçük uygulama ağ geçitleri üzerinde desteklenmiyor.|
|**Modu** | Bu ayar, WAF, hello modudur. izin verilen değerler **algılama** ve **önleme**. WAF algılama modunda ayarlandığında, tüm tehditler bir günlük dosyasında depolanır. Önleme modda olayları yine kaydedilir ancak hello saldırgan 403 yetkisiz yanıt hello uygulama ağ geçidi'nden alır.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Web uygulaması güvenlik duvarı tooan varolan uygulama ağ geçidi Ekle

Merhaba, mevcut bir standart uygulama ağ geçidi tooa WAF kullanan bir uygulama ağ geçidi komutu değişikliklerini izleyin.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

Bu komut hello uygulama ağ geçidi web uygulaması güvenlik duvarı ile güncelleştirir. Ziyaret [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md) toounderstand tooview uygulama ağ geçidiniz için nasıl günlüğe kaydeder. Güvenlik yapısı toohello WAF, günlükleri gerek toobe toounderstand hello güvenlik yaklaşımı, web uygulamalarınızı, düzenli olarak gözden.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma

komutu aşağıdaki hello web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturur.

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
> Merhaba temel web uygulaması güvenlik duvarı yapılandırması ile oluşturulmuş uygulama ağ geçitleri için koruma CRS 3.0 ile yapılandırılır.

## <a name="get-application-gateway-dns-name"></a>Uygulama ağ geçidi DNS adını alma

Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır. Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir. hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir. [Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure bir CNAME kaydı ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adını alır. Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır. Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.

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

Nasıl toocustomize WAF adresini ziyaret ederek kurallar öğrenin: [hello Azure CLI 2.0 aracılığıyla web uygulaması güvenlik duvarı kurallarını özelleştirmek](application-gateway-customize-waf-rules-cli.md).

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
