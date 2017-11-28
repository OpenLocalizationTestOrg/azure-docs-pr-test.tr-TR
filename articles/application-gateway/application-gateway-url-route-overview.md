---
title: "URL tabanlı içerik yönlendirmeye genel bakış | Microsoft Belgeleri"
description: "Bu sayfada, Application Gateway URL'si tabanlı içerik yönlendirme, UrlPathMap yapılandırması ve PathBasedRouting kuralı için genel bir bakış sunulmuştur."
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
ms.openlocfilehash: 75c3279d2d02cb3c6e949d191c88a1eb18b58a27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="b1b4c-103">URL Yolu Tabanlı Yönlendirmeye genel bakış</span><span class="sxs-lookup"><span data-stu-id="b1b4c-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="b1b4c-104">URL Yolu Tabanlı Yönlendirme, trafiği isteğin URL Yollarına göre arka uç sunucu havuzlarına yönlendirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span></span> 

<span data-ttu-id="b1b4c-105">Senaryolardan biri, farklı içerik türleri için istekleri farklı arka uç sunucu havuzlarına yönlendirmektir.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-105">One of the scenarios is to route requests for different content types to different backend server pools.</span></span>

<span data-ttu-id="b1b4c-106">Aşağıdaki örnekte, Application Gateway contoso.com için VideoServerPool, ImageServerPool ve DefaultServerPool gibi üç arka uç sunucu havuzlarından trafik sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="b1b4c-108">http://contoso.com/video* istekleri VideoServerPool'a ve http://contoso.com/images* istekleri ImageServerPool'a yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-108">Requests for http://contoso.com/video* are routed to VideoServerPool, and http://contoso.com/images* are routed to ImageServerPool.</span></span> <span data-ttu-id="b1b4c-109">Yol desenlerinden hiçbiri eşleşmiyorsa DefaultServerPool seçilir.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-109">DefaultServerPool is selected if none of the path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1b4c-110">Kurallar, portalda listelendikleri sırayla işlenir.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-110">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="b1b4c-111">Temel dinleyiciyi yapılandırmadan önce çok siteli dinleyicileri yapılandırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-111">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="b1b4c-112">Bu işlem, trafiğin doğru arka uca yönlendirilmesini güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-112">This ensures that traffic gets routed to the right back end.</span></span> <span data-ttu-id="b1b4c-113">Temel dinleyici listede ilk sıradaysa ve gelen bir istekle eşleşiyorsa, o dinleyici tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="b1b4c-114">UrlPathMap yapılandırma öğesi</span><span class="sxs-lookup"><span data-stu-id="b1b4c-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="b1b4c-115">UrlPathMap öğesi, arka uç sunucu havuzu eşlemeleri için Yol desenleri belirtmek üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-115">The urlPathMap element is used to specify Path patterns to back-end server pool mappings.</span></span> <span data-ttu-id="b1b4c-116">Aşağıdaki kod örneği, şablon dosyasındaki urlPathMap öğesinin kod parçacığıdır.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-116">The following code example is the snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="b1b4c-117">PathPattern: Bu ayar, eşleştirilecek yol desenlerinin listesidir.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-117">PathPattern: This setting is a list of path patterns to match.</span></span> <span data-ttu-id="b1b4c-118">Her biri / ile başlamalıdır. "*" işareti, yalnızca "/" işaretinin ardından en sona koyulabilir.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-118">Each must start with / and the only place a "*" is allowed is at the end following a "/."</span></span> <span data-ttu-id="b1b4c-119">Desen eşleştiricisine verilen dize, ilk ? veya # işaretinden sonra herhangi bir metin içermez ve burada, bu karakterlere izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-119">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="b1b4c-120">Daha fazla bilgi için [URL tabanlı yönlendirme kullanan bir Resource Manager şablonunu](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="b1b4c-121">PathBasedRouting kuralı</span><span class="sxs-lookup"><span data-stu-id="b1b4c-121">PathBasedRouting rule</span></span>

<span data-ttu-id="b1b4c-122">PathBasedRouting türündeki RequestRoutingRule, bir dinleyiciyi urlPathMap’e bağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-122">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span></span> <span data-ttu-id="b1b4c-123">Bu dinleyici için alınan tüm istekler, urlPathMap’te belirtilen ilkeye göre yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="b1b4c-124">PathBasedRouting kuralının kod parçacığı:</span><span class="sxs-lookup"><span data-stu-id="b1b4c-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b1b4c-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b1b4c-125">Next steps</span></span>

<span data-ttu-id="b1b4c-126">URL tabanlı içerik yönlendirme hakkında bilgi edindikten sonra, URL yönlendirme kurallarıyla bir uygulama ağ geçidi oluşturmak için [URL tabanlı yönlendirme kullanan uygulama ağ geçidi oluşturma](application-gateway-create-url-route-portal.md) bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="b1b4c-126">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) to create an application gateway with URL routing rules.</span></span>
