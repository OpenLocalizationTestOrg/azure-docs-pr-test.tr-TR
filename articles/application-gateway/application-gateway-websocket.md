---
title: "Azure uygulama ağ geçidi aaaWebSocket desteği | Microsoft Docs"
description: "Bu sayfa uygulama ağ geçidi WebSocket desteği hello genel bir bakış sağlar."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a>Uygulama ağ geçidi WebSocket desteği'ne genel bakış

Uygulama ağ geçidi tüm ağ geçidi boyutları arasında WebSocket için yerel destek sağlar. Kullanıcı tarafından yapılandırılabilir ayarı tooselectively etkinleştir veya devre dışı bırakma WebSocket desteği yoktur. 

WebSocket Protokolü içinde standartlaştırılmış [RFC6455](https://tools.ietf.org/html/rfc6455) uzun süre çalışan bir TCP bağlantısı üzerinden bir sunucu ve istemci arasındaki tam çift yönlü iletişimi sağlar. Bu özellik bir daha etkileşimli hello web sunucusu ve istemci arasındaki iletişimin çift yönlü yoklama için gereken HTTP tabanlı uygulamaları olarak hello gerek kalmadan olabilen Merhaba, sağlar. WebSocket sahip düşük yükü HTTP ve yeniden'ın aynı hello TCP bağlantısı kaynakları daha verimli bir kullanımı kaynaklanan birden çok istek/yanıt. WebSocket tasarlanmış toowork geleneksel HTTP bağlantı noktaları 80 ve 443 üzerinden protokollerdir.

Standart bir HTTP dinleyicisi bağlantı noktası 80 veya 443 tooreceive WebSocket trafiği kullanmaya devam edebilirsiniz. Uygulama ağ geçidi kurallarını belirtildiği gibi hello uygun arka uç havuzu kullanarak arka uç sunucusuna yönlendirilmiş toohello WebSocket etkinleştirilirse WebSocket trafiğidir. Merhaba arka uç sunucu hello açıklanan toohello uygulama ağ geçidi araştırmalar yanıt gerekir [sistem durumu araştırma genel bakış](application-gateway-probe-overview.md) bölümü. Uygulama ağ geçidi sistem durumu araştırmalarının, yalnızca HTTP/HTTPS etkilenir. Her arka uç sunucusu uygulama ağ geçidi tooroute WebSocket trafiği toohello sunucusu tooHTTP araştırmalar yanıtlaması gerekir.

## <a name="listener-configuration-element"></a>Dinleyici yapılandırma öğesi

Varolan bir HTTP dinleyicisi kullanılan toosupport WebSocket trafik olabilir. Merhaba, örnek şablon dosyası Httplistener öğeden parçacığıyla aşağıdadır. HTTP ve HTTPS dinleyicileri toosupport WebSocket gerekir ve WebSocket trafiğinin güvenliğini sağlamak. Benzer şekilde hello kullanabilirsiniz [portal](application-gateway-create-gateway-portal.md) veya [PowerShell](application-gateway-create-gateway-arm.md) toocreate bağlantı noktası 80/443 toosupport WebSocket trafiği üzerindeki dinleyicileri sahip bir uygulama ağ geçidi.

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>BackendAddressPool, BackendHttpSetting ve yönlendirme kuralı yapılandırma

Bir BackendAddressPool kullanılan toodefine bir arka uç havuzu etkin WebSocket sunucularıyla ' dir. Merhaba backendHttpSetting bir arka uç bağlantı noktası 80 ve 443 tanımlanır. tanımlama bilgisi temelli benzeşimi ve requestTimeouts Hello özelliklerini ilgili tooWebSocket trafiği olup olmadığı. Merhaba yönlendirme kuralı gerekli bir değişiklik yapılmaz, 'Temel' arka uç adres havuzuna karşılık gelen kullanılan tootie hello uygun dinleyici toohello. 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a>Etkin WebSocket arka uç

Arka yapılandırılmış hello üzerinde çalışan bir HTTP/HTTPS web sunucunuzun olması gerekir (genellikle 80/443) WebSocket toowork için bağlantı noktası. WebSocket Protokolü hello ilk el sıkışma toobe HTTP üstbilgi alanı olarak yükseltme tooWebSocket kuralıyla gerektirdiğinden bu gerekli değildir. Merhaba, bir başlığı örneği aşağıdadır:

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

Başka bir nedeni, bu uygulama ağ geçidi arka uç sistem durumu araştırma yalnızca HTTP ve HTTPS protokollerini destekler ' dir. TooHTTP veya HTTPS araştırmaları Hello arka uç sunucu yanıt vermezse, arka uç havuzu dışında alınır.

## <a name="next-steps"></a>Sonraki adımlar

WebSocket desteği hakkında daha fazla öğrenme sonra çok Git[bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway.md) WebSocket ile başlatılan tooget etkin web uygulaması.

