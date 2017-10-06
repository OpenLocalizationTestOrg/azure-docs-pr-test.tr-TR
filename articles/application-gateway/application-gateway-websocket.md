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
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="5d348-103">Uygulama ağ geçidi WebSocket desteği'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="5d348-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="5d348-104">Uygulama ağ geçidi tüm ağ geçidi boyutları arasında WebSocket için yerel destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="5d348-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="5d348-105">Kullanıcı tarafından yapılandırılabilir ayarı tooselectively etkinleştir veya devre dışı bırakma WebSocket desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="5d348-105">There is no user-configurable setting tooselectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="5d348-106">WebSocket Protokolü içinde standartlaştırılmış [RFC6455](https://tools.ietf.org/html/rfc6455) uzun süre çalışan bir TCP bağlantısı üzerinden bir sunucu ve istemci arasındaki tam çift yönlü iletişimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5d348-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="5d348-107">Bu özellik bir daha etkileşimli hello web sunucusu ve istemci arasındaki iletişimin çift yönlü yoklama için gereken HTTP tabanlı uygulamaları olarak hello gerek kalmadan olabilen Merhaba, sağlar.</span><span class="sxs-lookup"><span data-stu-id="5d348-107">This feature allows for a more interactive communication between hello web server and hello client, which can be bidirectional without hello need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="5d348-108">WebSocket sahip düşük yükü HTTP ve yeniden'ın aynı hello TCP bağlantısı kaynakları daha verimli bir kullanımı kaynaklanan birden çok istek/yanıt.</span><span class="sxs-lookup"><span data-stu-id="5d348-108">WebSocket has low overhead unlike HTTP and can reuse hello same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="5d348-109">WebSocket tasarlanmış toowork geleneksel HTTP bağlantı noktaları 80 ve 443 üzerinden protokollerdir.</span><span class="sxs-lookup"><span data-stu-id="5d348-109">WebSocket protocols are designed toowork over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="5d348-110">Standart bir HTTP dinleyicisi bağlantı noktası 80 veya 443 tooreceive WebSocket trafiği kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d348-110">You can continue using a standard HTTP listener on port 80 or 443 tooreceive WebSocket traffic.</span></span> <span data-ttu-id="5d348-111">Uygulama ağ geçidi kurallarını belirtildiği gibi hello uygun arka uç havuzu kullanarak arka uç sunucusuna yönlendirilmiş toohello WebSocket etkinleştirilirse WebSocket trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="5d348-111">WebSocket traffic is then directed toohello WebSocket enabled backend server using hello appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="5d348-112">Merhaba arka uç sunucu hello açıklanan toohello uygulama ağ geçidi araştırmalar yanıt gerekir [sistem durumu araştırma genel bakış](application-gateway-probe-overview.md) bölümü.</span><span class="sxs-lookup"><span data-stu-id="5d348-112">hello backend server must respond toohello application gateway probes, which are described in hello [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="5d348-113">Uygulama ağ geçidi sistem durumu araştırmalarının, yalnızca HTTP/HTTPS etkilenir.</span><span class="sxs-lookup"><span data-stu-id="5d348-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="5d348-114">Her arka uç sunucusu uygulama ağ geçidi tooroute WebSocket trafiği toohello sunucusu tooHTTP araştırmalar yanıtlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d348-114">Each backend server must respond tooHTTP probes for application gateway tooroute WebSocket traffic toohello server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="5d348-115">Dinleyici yapılandırma öğesi</span><span class="sxs-lookup"><span data-stu-id="5d348-115">Listener configuration element</span></span>

<span data-ttu-id="5d348-116">Varolan bir HTTP dinleyicisi kullanılan toosupport WebSocket trafik olabilir.</span><span class="sxs-lookup"><span data-stu-id="5d348-116">An existing HTTP listener can be used toosupport WebSocket traffic.</span></span> <span data-ttu-id="5d348-117">Merhaba, örnek şablon dosyası Httplistener öğeden parçacığıyla aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="5d348-117">hello following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="5d348-118">HTTP ve HTTPS dinleyicileri toosupport WebSocket gerekir ve WebSocket trafiğinin güvenliğini sağlamak.</span><span class="sxs-lookup"><span data-stu-id="5d348-118">You would need both HTTP and HTTPS listeners toosupport WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="5d348-119">Benzer şekilde hello kullanabilirsiniz [portal](application-gateway-create-gateway-portal.md) veya [PowerShell](application-gateway-create-gateway-arm.md) toocreate bağlantı noktası 80/443 toosupport WebSocket trafiği üzerindeki dinleyicileri sahip bir uygulama ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="5d348-119">Similarly you can use hello [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) toocreate an application gateway with listeners on port 80/443 toosupport WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="5d348-120">BackendAddressPool, BackendHttpSetting ve yönlendirme kuralı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5d348-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="5d348-121">Bir BackendAddressPool kullanılan toodefine bir arka uç havuzu etkin WebSocket sunucularıyla ' dir.</span><span class="sxs-lookup"><span data-stu-id="5d348-121">A BackendAddressPool is used toodefine a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="5d348-122">Merhaba backendHttpSetting bir arka uç bağlantı noktası 80 ve 443 tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="5d348-122">hello backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="5d348-123">tanımlama bilgisi temelli benzeşimi ve requestTimeouts Hello özelliklerini ilgili tooWebSocket trafiği olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="5d348-123">hello properties for cookie-based affinity and requestTimeouts are not relevant tooWebSocket traffic.</span></span> <span data-ttu-id="5d348-124">Merhaba yönlendirme kuralı gerekli bir değişiklik yapılmaz, 'Temel' arka uç adres havuzuna karşılık gelen kullanılan tootie hello uygun dinleyici toohello.</span><span class="sxs-lookup"><span data-stu-id="5d348-124">There is no change required in hello routing rule, 'Basic' is used tootie hello appropriate listener toohello corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="5d348-125">Etkin WebSocket arka uç</span><span class="sxs-lookup"><span data-stu-id="5d348-125">WebSocket enabled backend</span></span>

<span data-ttu-id="5d348-126">Arka yapılandırılmış hello üzerinde çalışan bir HTTP/HTTPS web sunucunuzun olması gerekir (genellikle 80/443) WebSocket toowork için bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="5d348-126">Your backend must have a HTTP/HTTPS web server running on hello configured port (usually 80/443) for WebSocket toowork.</span></span> <span data-ttu-id="5d348-127">WebSocket Protokolü hello ilk el sıkışma toobe HTTP üstbilgi alanı olarak yükseltme tooWebSocket kuralıyla gerektirdiğinden bu gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="5d348-127">This requirement is because WebSocket protocol requires hello initial handshake toobe HTTP with upgrade tooWebSocket protocol as a header field.</span></span> <span data-ttu-id="5d348-128">Merhaba, bir başlığı örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="5d348-128">hello following is an example of a header:</span></span>

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

<span data-ttu-id="5d348-129">Başka bir nedeni, bu uygulama ağ geçidi arka uç sistem durumu araştırma yalnızca HTTP ve HTTPS protokollerini destekler ' dir.</span><span class="sxs-lookup"><span data-stu-id="5d348-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="5d348-130">TooHTTP veya HTTPS araştırmaları Hello arka uç sunucu yanıt vermezse, arka uç havuzu dışında alınır.</span><span class="sxs-lookup"><span data-stu-id="5d348-130">If hello backend server does not respond tooHTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d348-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5d348-131">Next steps</span></span>

<span data-ttu-id="5d348-132">WebSocket desteği hakkında daha fazla öğrenme sonra çok Git[bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway.md) WebSocket ile başlatılan tooget etkin web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="5d348-132">After learning about WebSocket support, go too[create an application gateway](application-gateway-create-gateway.md) tooget started with a WebSocket enabled web application.</span></span>

