---
title: "aaaURL tabanlı içerik yönlendirmeye genel bakış | Microsoft Docs"
description: "Bu sayfa uygulama ağ geçidi URL tabanlı hello içerik yönlendirme, UrlPathMap yapılandırma ve PathBasedRouting kuralı genel bakış sağlar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: gwallace
ms.openlocfilehash: 5094b42625baffeb395beace68db0d269e46080c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="url-path-based-routing-overview"></a>URL Yolu Tabanlı Yönlendirmeye genel bakış

Temel URL yolu yönlendirme hello isteğinin URL yollarına bağlı, tooroute trafiği tooback uç sunucu havuzu sağlar. 

Merhaba senaryolardan biri, farklı içerik türlerini toodifferent arka uç sunucu havuzu için tooroute isteği sayısıdır.

Aşağıdaki örneğine hello, uygulama ağ geçidi trafiği üç arka uç sunucu havuzlarından contoso.com için örneğin görevi gören: VideoServerPool, ImageServerPool ve DefaultServerPool.

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

İstekleri için http://contoso.com/video * yönlendirilmiş tooVideoServerPool olduğunda ve http://contoso.com/images * yönlendirilmiş tooImageServerPool. Merhaba yolu desenleri hiçbiri eşleşiyorsa DefaultServerPool seçilir.

> [!IMPORTANT]
> Merhaba Portalı'nda listelenen hello sırada işlenir. Yüksek oranda önerilen tooconfigure çok siteli dinleyicileri ilk önceki tooconfiguring temel bir dinleyici olduğundan.  Bu, bu trafiği alır yönlendirilmiş toohello sağ geri bitiş sağlar. Temel dinleyici listede ilk sıradaysa ve gelen bir istekle eşleşiyorsa, o dinleyici tarafından işlenir.

## <a name="urlpathmap-configuration-element"></a>UrlPathMap yapılandırma öğesi

Merhaba urlPathMap kullanılan toospecify yolu desenleri tooback uç sunucu havuzu eşlemeleri öğedir. Merhaba aşağıdaki kod örneğinde şablon dosyası urlPathMap öğesinden hello parçacığını ' dir.

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> PathPattern: Bu ayar, yol desenleri toomatch bir listesidir. Her ile başlamalıdır / ve hello yalnızca Yerleştir bir "*" Merhaba son izlemektir izin verilen bir "/." toohello yolu Eşleştirici sat hello dize herhangi bir metin hello sonra ilk içermiyor? veya # ve bu karakter burada izin verilmez.

Daha fazla bilgi için [URL tabanlı yönlendirme kullanan bir Resource Manager şablonunu](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) inceleyebilirsiniz.

## <a name="pathbasedrouting-rule"></a>PathBasedRouting kuralı

RequestRoutingRule PathBasedRouting türünde kullanılan toobind bir dinleyici tooa urlPathMap ' dir. Bu dinleyici için alınan tüm istekler, urlPathMap’te belirtilen ilkeye göre yönlendirilir.
PathBasedRouting kuralının kod parçacığı:

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a>Sonraki adımlar

URL tabanlı içerik yönlendirme hakkında daha fazla öğrenme sonra çok Git[URL tabanlı yönlendirme kullanarak bir uygulama ağ geçidi oluşturma](application-gateway-create-url-route-portal.md) toocreate URL yönlendirme kuralları ile uygulama ağ geçidi.
