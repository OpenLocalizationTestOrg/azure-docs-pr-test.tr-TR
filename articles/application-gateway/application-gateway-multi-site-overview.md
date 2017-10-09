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
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="85d98-103">Application Gateway birden çok site barındırma</span><span class="sxs-lookup"><span data-stu-id="85d98-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="85d98-104">Birden çok siteyi barındıran bir web uygulaması hello üzerinde birden çok tooconfigure sağlar aynı uygulama ağ geçidi örneği.</span><span class="sxs-lookup"><span data-stu-id="85d98-104">Multiple site hosting enables you tooconfigure more than one web application on hello same application gateway instance.</span></span> <span data-ttu-id="85d98-105">Bu özellik too20 Web siteleri tooone uygulama ağ geçidi kurun ekleyerek tooconfigure dağıtımlarınız için daha verimli bir topolojiyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="85d98-105">This feature allows you tooconfigure a more efficient topology for your deployments by adding up too20 websites tooone application gateway.</span></span> <span data-ttu-id="85d98-106">Her Web sitesi yönlendirilebilir tooits kendi arka uç havuzu.</span><span class="sxs-lookup"><span data-stu-id="85d98-106">Each website can be directed tooits own backend pool.</span></span> <span data-ttu-id="85d98-107">Aşağıdaki örnek hello, uygulama ağ geçidi trafiği contoso.com ve fabrikam.com ContosoServerPool ve FabrikamServerPool adlı iki arka uç sunucu havuzlarından için hizmet veriyor.</span><span class="sxs-lookup"><span data-stu-id="85d98-107">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="85d98-109">Merhaba Portalı'nda listelenen hello sırada işlenir.</span><span class="sxs-lookup"><span data-stu-id="85d98-109">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="85d98-110">Yüksek oranda önerilen tooconfigure çok siteli dinleyicileri ilk önceki tooconfiguring temel bir dinleyici olduğundan.</span><span class="sxs-lookup"><span data-stu-id="85d98-110">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="85d98-111">Bu, bu trafiği alır yönlendirilmiş toohello sağ geri bitiş güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="85d98-111">This will ensure that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="85d98-112">Temel dinleyici listede ilk sıradaysa ve gelen bir istekle eşleşiyorsa, o dinleyici tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="85d98-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="85d98-113">Http://contoso.com isteklerinde yönlendirilmiş tooContosoServerPool olduğunda ve http://fabrikam.com yönlendirilmiş tooFabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="85d98-113">Requests for http://contoso.com are routed tooContosoServerPool, and http://fabrikam.com are routed tooFabrikamServerPool.</span></span>

<span data-ttu-id="85d98-114">Benzer şekilde aynı üst etki alanı üzerinde barındırılan hello iki alt etki alanları aynı uygulama ağ geçidi dağıtımı hello.</span><span class="sxs-lookup"><span data-stu-id="85d98-114">Similarly two subdomains of hello same parent domain can be hosted on hello same application gateway deployment.</span></span> <span data-ttu-id="85d98-115">Alt etki alanı kullanım örnekleri, tek bir uygulama ağ geçidi dağıtımında barındırılan http://blog.contoso.com ve http://app.contoso.com’u içerebilir.</span><span class="sxs-lookup"><span data-stu-id="85d98-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="85d98-116">Barındırma üstbilgileri ve Sunucu Adı Belirtme (SNI)</span><span class="sxs-lookup"><span data-stu-id="85d98-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="85d98-117">Birden çok sitesi hello üzerinde aynı barındırma etkinleştirilmesi için üç ortak mekanizma vardır altyapı.</span><span class="sxs-lookup"><span data-stu-id="85d98-117">There are three common mechanisms for enabling multiple site hosting on hello same infrastructure.</span></span>

1. <span data-ttu-id="85d98-118">Birden çok web uygulamasının her birini benzersiz bir IP adresinde barındırın.</span><span class="sxs-lookup"><span data-stu-id="85d98-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="85d98-119">Kullanım konak adı toohost hello birden çok web uygulamalarını aynı IP adresi.</span><span class="sxs-lookup"><span data-stu-id="85d98-119">Use host name toohost multiple web applications on hello same IP address.</span></span>
3. <span data-ttu-id="85d98-120">Kullanım farklı bağlantı noktaları toohost hello birden çok web uygulamalarını aynı IP adresi.</span><span class="sxs-lookup"><span data-stu-id="85d98-120">Use different ports toohost multiple web applications on hello same IP address.</span></span>

<span data-ttu-id="85d98-121">Şu anda bir uygulama ağ geçidi, üzerinde trafiği dinlediği tek bir genel IP adresi almaktadır.</span><span class="sxs-lookup"><span data-stu-id="85d98-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="85d98-122">Bu nedenle, her biri kendi IP adresine sahip olan birden çok uygulama şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="85d98-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="85d98-123">Uygulama ağ geçidi birden çok uygulamayı barındıran her farklı bağlantı noktalarını dinler destekler ancak bu senaryo hello uygulamaları tooaccept trafiği standart olmayan bağlantı noktalarını gerektirir ve sık istenen bir yapılandırma değildir.</span><span class="sxs-lookup"><span data-stu-id="85d98-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require hello applications tooaccept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="85d98-124">Uygulama ağ geçidi HTTP 1.1 dayanır bir Web sitesinde birden çok konak üstbilgileri toohost hello aynı genel IP adresi ve bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="85d98-124">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="85d98-125">Uygulama ağ geçidinde barındırılan hello siteleri destek SSL boşaltma sunucu adı göstergesi (SNI) TLS uzantılı de gruplandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85d98-125">hello sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="85d98-126">Bu senaryo o hello istemci tarayıcısı ve arka uç web grubu HTTP/1.1 ve TLS uzantısı RFC 6066 içinde tanımlanan desteklemelidir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="85d98-126">This scenario means that hello client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="85d98-127">Dinleyici yapılandırma öğesi</span><span class="sxs-lookup"><span data-stu-id="85d98-127">Listener configuration element</span></span>

<span data-ttu-id="85d98-128">Yapılandırma öğesi varolan HTTPListener toosupport ana bilgisayar adı ve sunucu adı göstergesi öğeleri, uygulama ağ geçidi tooroute trafiği tooappropriate arka uç havuzu tarafından kullanılan geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="85d98-128">Existing HTTPListener configuration element is enhanced toosupport host name and server name indication elements, which is used by application gateway tooroute traffic tooappropriate backend pool.</span></span> <span data-ttu-id="85d98-129">Merhaba aşağıdaki kod örneğinde şablon dosyası Httplistener öğesinden hello parçacığını ' dir.</span><span class="sxs-lookup"><span data-stu-id="85d98-129">hello following code example is hello snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="85d98-130">Ziyaret ettiğiniz [Resource Manager şablonu kullanarak birden çok siteyi barındıran](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) şablona dayalı bir uç tooend dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="85d98-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end tooend template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="85d98-131">Yönlendirme kuralı</span><span class="sxs-lookup"><span data-stu-id="85d98-131">Routing rule</span></span>

<span data-ttu-id="85d98-132">Merhaba yönlendirme kuralı gerekli değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="85d98-132">There is no change required in hello routing rule.</span></span> <span data-ttu-id="85d98-133">'Temel' seçilen toobe tootie hello uygun site dinleyici toohello karşılık gelen arka uç adres havuzu devam etmelidir yönlendirme kuralı hello.</span><span class="sxs-lookup"><span data-stu-id="85d98-133">hello routing rule 'Basic' should continue toobe chosen tootie hello appropriate site listener toohello corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="85d98-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85d98-134">Next steps</span></span>

<span data-ttu-id="85d98-135">Birden çok siteyi barındıran hakkında daha fazla öğrenme sonra çok Git[birden çok siteyi barındıran kullanarak bir uygulama ağ geçidi oluşturma](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate bir web uygulaması birden çok özelliği toosupport sahip bir uygulama ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="85d98-135">After learning about multiple site hosting, go too[create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate an application gateway with ability toosupport more than one web application.</span></span>

