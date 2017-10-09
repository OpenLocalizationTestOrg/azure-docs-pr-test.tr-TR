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
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="a07c4-103">URL Yolu Tabanlı Yönlendirmeye genel bakış</span><span class="sxs-lookup"><span data-stu-id="a07c4-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="a07c4-104">Temel URL yolu yönlendirme hello isteğinin URL yollarına bağlı, tooroute trafiği tooback uç sunucu havuzu sağlar.</span><span class="sxs-lookup"><span data-stu-id="a07c4-104">URL Path Based Routing allows you tooroute traffic tooback-end server pools based on URL Paths of hello request.</span></span> 

<span data-ttu-id="a07c4-105">Merhaba senaryolardan biri, farklı içerik türlerini toodifferent arka uç sunucu havuzu için tooroute isteği sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="a07c4-105">One of hello scenarios is tooroute requests for different content types toodifferent backend server pools.</span></span>

<span data-ttu-id="a07c4-106">Aşağıdaki örneğine hello, uygulama ağ geçidi trafiği üç arka uç sunucu havuzlarından contoso.com için örneğin görevi gören: VideoServerPool, ImageServerPool ve DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="a07c4-106">In hello following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="a07c4-108">İstekleri için http://contoso.com/video * yönlendirilmiş tooVideoServerPool olduğunda ve http://contoso.com/images * yönlendirilmiş tooImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="a07c4-108">Requests for http://contoso.com/video* are routed tooVideoServerPool, and http://contoso.com/images* are routed tooImageServerPool.</span></span> <span data-ttu-id="a07c4-109">Merhaba yolu desenleri hiçbiri eşleşiyorsa DefaultServerPool seçilir.</span><span class="sxs-lookup"><span data-stu-id="a07c4-109">DefaultServerPool is selected if none of hello path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a07c4-110">Merhaba Portalı'nda listelenen hello sırada işlenir.</span><span class="sxs-lookup"><span data-stu-id="a07c4-110">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="a07c4-111">Yüksek oranda önerilen tooconfigure çok siteli dinleyicileri ilk önceki tooconfiguring temel bir dinleyici olduğundan.</span><span class="sxs-lookup"><span data-stu-id="a07c4-111">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="a07c4-112">Bu, bu trafiği alır yönlendirilmiş toohello sağ geri bitiş sağlar.</span><span class="sxs-lookup"><span data-stu-id="a07c4-112">This ensures that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="a07c4-113">Temel dinleyici listede ilk sıradaysa ve gelen bir istekle eşleşiyorsa, o dinleyici tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="a07c4-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="a07c4-114">UrlPathMap yapılandırma öğesi</span><span class="sxs-lookup"><span data-stu-id="a07c4-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="a07c4-115">Merhaba urlPathMap kullanılan toospecify yolu desenleri tooback uç sunucu havuzu eşlemeleri öğedir.</span><span class="sxs-lookup"><span data-stu-id="a07c4-115">hello urlPathMap element is used toospecify Path patterns tooback-end server pool mappings.</span></span> <span data-ttu-id="a07c4-116">Merhaba aşağıdaki kod örneğinde şablon dosyası urlPathMap öğesinden hello parçacığını ' dir.</span><span class="sxs-lookup"><span data-stu-id="a07c4-116">hello following code example is hello snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="a07c4-117">PathPattern: Bu ayar, yol desenleri toomatch bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="a07c4-117">PathPattern: This setting is a list of path patterns toomatch.</span></span> <span data-ttu-id="a07c4-118">Her ile başlamalıdır / ve hello yalnızca Yerleştir bir "*" Merhaba son izlemektir izin verilen bir "/."</span><span class="sxs-lookup"><span data-stu-id="a07c4-118">Each must start with / and hello only place a "*" is allowed is at hello end following a "/."</span></span> <span data-ttu-id="a07c4-119">toohello yolu Eşleştirici sat hello dize herhangi bir metin hello sonra ilk içermiyor? veya # ve bu karakter burada izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="a07c4-119">hello string fed toohello path matcher does not include any text after hello first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="a07c4-120">Daha fazla bilgi için [URL tabanlı yönlendirme kullanan bir Resource Manager şablonunu](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a07c4-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="a07c4-121">PathBasedRouting kuralı</span><span class="sxs-lookup"><span data-stu-id="a07c4-121">PathBasedRouting rule</span></span>

<span data-ttu-id="a07c4-122">RequestRoutingRule PathBasedRouting türünde kullanılan toobind bir dinleyici tooa urlPathMap ' dir.</span><span class="sxs-lookup"><span data-stu-id="a07c4-122">RequestRoutingRule of type PathBasedRouting is used toobind a listener tooa urlPathMap.</span></span> <span data-ttu-id="a07c4-123">Bu dinleyici için alınan tüm istekler, urlPathMap’te belirtilen ilkeye göre yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="a07c4-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="a07c4-124">PathBasedRouting kuralının kod parçacığı:</span><span class="sxs-lookup"><span data-stu-id="a07c4-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a07c4-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a07c4-125">Next steps</span></span>

<span data-ttu-id="a07c4-126">URL tabanlı içerik yönlendirme hakkında daha fazla öğrenme sonra çok Git[URL tabanlı yönlendirme kullanarak bir uygulama ağ geçidi oluşturma](application-gateway-create-url-route-portal.md) toocreate URL yönlendirme kuralları ile uygulama ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="a07c4-126">After learning about URL-based content routing, go too[create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) toocreate an application gateway with URL routing rules.</span></span>
