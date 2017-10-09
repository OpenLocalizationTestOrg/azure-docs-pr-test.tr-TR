---
title: "aaaHosting Azure uygulama ağ geçidi birden çok site | Microsoft Docs"
description: "Bu sayfa hello uygulama ağ geçidi çok siteli Destek genel bir bakış sağlar."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a>Application Gateway birden çok site barındırma

Birden çok siteyi barındıran bir web uygulaması hello üzerinde birden çok tooconfigure sağlar aynı uygulama ağ geçidi örneği. Bu özellik too20 Web siteleri tooone uygulama ağ geçidi kurun ekleyerek tooconfigure dağıtımlarınız için daha verimli bir topolojiyi sağlar. Her Web sitesi yönlendirilebilir tooits kendi arka uç havuzu. Aşağıdaki örnek hello, uygulama ağ geçidi trafiği contoso.com ve fabrikam.com ContosoServerPool ve FabrikamServerPool adlı iki arka uç sunucu havuzlarından için hizmet veriyor.

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> Merhaba Portalı'nda listelenen hello sırada işlenir. Yüksek oranda önerilen tooconfigure çok siteli dinleyicileri ilk önceki tooconfiguring temel bir dinleyici olduğundan.  Bu, bu trafiği alır yönlendirilmiş toohello sağ geri bitiş güvence altına alır. Temel dinleyici listede ilk sıradaysa ve gelen bir istekle eşleşiyorsa, o dinleyici tarafından işlenir.

Http://contoso.com isteklerinde yönlendirilmiş tooContosoServerPool olduğunda ve http://fabrikam.com yönlendirilmiş tooFabrikamServerPool.

Benzer şekilde aynı üst etki alanı üzerinde barındırılan hello iki alt etki alanları aynı uygulama ağ geçidi dağıtımı hello. Alt etki alanı kullanım örnekleri, tek bir uygulama ağ geçidi dağıtımında barındırılan http://blog.contoso.com ve http://app.contoso.com’u içerebilir.

## <a name="host-headers-and-server-name-indication-sni"></a>Barındırma üstbilgileri ve Sunucu Adı Belirtme (SNI)

Birden çok sitesi hello üzerinde aynı barındırma etkinleştirilmesi için üç ortak mekanizma vardır altyapı.

1. Birden çok web uygulamasının her birini benzersiz bir IP adresinde barındırın.
2. Kullanım konak adı toohost hello birden çok web uygulamalarını aynı IP adresi.
3. Kullanım farklı bağlantı noktaları toohost hello birden çok web uygulamalarını aynı IP adresi.

Şu anda bir uygulama ağ geçidi, üzerinde trafiği dinlediği tek bir genel IP adresi almaktadır. Bu nedenle, her biri kendi IP adresine sahip olan birden çok uygulama şu anda desteklenmemektedir. Uygulama ağ geçidi birden çok uygulamayı barındıran her farklı bağlantı noktalarını dinler destekler ancak bu senaryo hello uygulamaları tooaccept trafiği standart olmayan bağlantı noktalarını gerektirir ve sık istenen bir yapılandırma değildir. Uygulama ağ geçidi HTTP 1.1 dayanır bir Web sitesinde birden çok konak üstbilgileri toohost hello aynı genel IP adresi ve bağlantı noktası. Uygulama ağ geçidinde barındırılan hello siteleri destek SSL boşaltma sunucu adı göstergesi (SNI) TLS uzantılı de gruplandırabilirsiniz. Bu senaryo o hello istemci tarayıcısı ve arka uç web grubu HTTP/1.1 ve TLS uzantısı RFC 6066 içinde tanımlanan desteklemelidir anlamına gelir.

## <a name="listener-configuration-element"></a>Dinleyici yapılandırma öğesi

Yapılandırma öğesi varolan HTTPListener toosupport ana bilgisayar adı ve sunucu adı göstergesi öğeleri, uygulama ağ geçidi tooroute trafiği tooappropriate arka uç havuzu tarafından kullanılan geliştirilmiştir. Merhaba aşağıdaki kod örneğinde şablon dosyası Httplistener öğesinden hello parçacığını ' dir.

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

Ziyaret ettiğiniz [Resource Manager şablonu kullanarak birden çok siteyi barındıran](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) şablona dayalı bir uç tooend dağıtımı.

## <a name="routing-rule"></a>Yönlendirme kuralı

Merhaba yönlendirme kuralı gerekli değişiklik yoktur. 'Temel' seçilen toobe tootie hello uygun site dinleyici toohello karşılık gelen arka uç adres havuzu devam etmelidir yönlendirme kuralı hello.

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a>Sonraki adımlar

Birden çok siteyi barındıran hakkında daha fazla öğrenme sonra çok Git[birden çok siteyi barındıran kullanarak bir uygulama ağ geçidi oluşturma](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate bir web uygulaması birden çok özelliği toosupport sahip bir uygulama ağ geçidi.

