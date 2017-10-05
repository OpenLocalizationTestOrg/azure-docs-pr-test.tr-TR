---
title: "Azure Application Gateway'de birden fazla siteyi barındırma | Microsoft Docs"
description: "Bu sayfada, Application Gateway çoklu site desteği için genel bir bakış sunulmuştur."
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
ms.openlocfilehash: 645f68d836babf11f32fc391e6dacc9430f0070c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="b3657-103">Application Gateway birden çok site barındırma</span><span class="sxs-lookup"><span data-stu-id="b3657-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="b3657-104">Birden çok site barındırma, aynı uygulama ağ geçidi örneğinde birden fazla web uygulaması yapılandırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3657-104">Multiple site hosting enables you to configure more than one web application on the same application gateway instance.</span></span> <span data-ttu-id="b3657-105">Bu özellik, bir uygulama ağ geçidine en fazla 20 web sitesi ekleyerek dağıtımlarınız için daha verimli bir topoloji yapılandırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b3657-105">This feature allows you to configure a more efficient topology for your deployments by adding up to 20 websites to one application gateway.</span></span> <span data-ttu-id="b3657-106">Her web sitesi, kendi arka uç havuzuna yönlendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b3657-106">Each website can be directed to its own backend pool.</span></span> <span data-ttu-id="b3657-107">Aşağıdaki örnekte, uygulama ağ geçidi ContosoServerPool ve FabrikamServerPool adlı iki arka uç sunucu havuzundan contoso.com ve fabrikam.com için trafik sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b3657-107">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="b3657-109">Kurallar, portalda listelendikleri sırayla işlenir.</span><span class="sxs-lookup"><span data-stu-id="b3657-109">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="b3657-110">Temel dinleyiciyi yapılandırmadan önce çok siteli dinleyicileri yapılandırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="b3657-110">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="b3657-111">Bu işlem, trafiğin doğru arka uca yönlendirilmesini güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="b3657-111">This will ensure that traffic gets routed to the right back end.</span></span> <span data-ttu-id="b3657-112">Temel dinleyici listede ilk sıradaysa ve gelen bir istekle eşleşiyorsa, o dinleyici tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="b3657-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="b3657-113">http://contoso.com için istekler ContosoServerPool’a, http://fabrikam.com için istekler ise FabrikamServerPool’a yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="b3657-113">Requests for http://contoso.com are routed to ContosoServerPool, and http://fabrikam.com are routed to FabrikamServerPool.</span></span>

<span data-ttu-id="b3657-114">Benzer şekilde aynı üst etki alanının iki alt etki alanı, aynı uygulama ağ geçidi dağıtımında barındırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b3657-114">Similarly two subdomains of the same parent domain can be hosted on the same application gateway deployment.</span></span> <span data-ttu-id="b3657-115">Alt etki alanı kullanım örnekleri, tek bir uygulama ağ geçidi dağıtımında barındırılan http://blog.contoso.com ve http://app.contoso.com’u içerebilir.</span><span class="sxs-lookup"><span data-stu-id="b3657-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="b3657-116">Barındırma üstbilgileri ve Sunucu Adı Belirtme (SNI)</span><span class="sxs-lookup"><span data-stu-id="b3657-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="b3657-117">Aynı altyapıda birden çok site barındırmayı etkinleştirmek için üç yaygın mekanizma bulunur.</span><span class="sxs-lookup"><span data-stu-id="b3657-117">There are three common mechanisms for enabling multiple site hosting on the same infrastructure.</span></span>

1. <span data-ttu-id="b3657-118">Birden çok web uygulamasının her birini benzersiz bir IP adresinde barındırın.</span><span class="sxs-lookup"><span data-stu-id="b3657-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="b3657-119">Birden çok web uygulamasını aynı IP adresinde barındırmak için ana bilgisayar adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3657-119">Use host name to host multiple web applications on the same IP address.</span></span>
3. <span data-ttu-id="b3657-120">Birden çok web uygulamasını aynı IP adresinde barındırmak için farklı bağlantı noktalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3657-120">Use different ports to host multiple web applications on the same IP address.</span></span>

<span data-ttu-id="b3657-121">Şu anda bir uygulama ağ geçidi, üzerinde trafiği dinlediği tek bir genel IP adresi almaktadır.</span><span class="sxs-lookup"><span data-stu-id="b3657-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="b3657-122">Bu nedenle, her biri kendi IP adresine sahip olan birden çok uygulama şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="b3657-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="b3657-123">Application Gateway, her biri farklı bağlantı noktasında dinleme yapan birden çok uygulamanın barındırılmasını destekler, ancak bu senaryo uygulamaların standart olmayan bağlantı noktalarında trafiği kabul etmesini gerekli kılar ve çoğu zaman istenen bir yapılandırma değildir.</span><span class="sxs-lookup"><span data-stu-id="b3657-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require the applications to accept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="b3657-124">Application Gateway, aynı genel IP adresinde ve bağlantı noktasında birden çok web sitesini barındırmak için HTTP 1.1 barındırma bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b3657-124">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="b3657-125">Uygulama ağ geçidinde barındırılan siteler, Sunucu Adı Belirtme (SNI) uzantısına sahip SSL yük boşaltmayı da destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="b3657-125">The sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="b3657-126">Bu senaryo, istemci tarayıcısının ve arka uç web grubunun RFC 6066’da belirtildiği gibi HTTP/1.1 ve TLS uzantısını desteklemesi gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b3657-126">This scenario means that the client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="b3657-127">Dinleyici yapılandırma öğesi</span><span class="sxs-lookup"><span data-stu-id="b3657-127">Listener configuration element</span></span>

<span data-ttu-id="b3657-128">Mevcut HTTPListener yapılandırma öğesi, ana bilgisayar adını ve sunucu adı belirtme öğelerini destekleyecek şekilde geliştirilmiştir. Bu öğe, uygulama ağ geçidi tarafından trafiği uygun arka uç havuzuna yönlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b3657-128">Existing HTTPListener configuration element is enhanced to support host name and server name indication elements, which is used by application gateway to route traffic to appropriate backend pool.</span></span> <span data-ttu-id="b3657-129">Aşağıdaki kod örneği, şablon dosyasındaki HttpListeners öğesinin kod parçacığıdır.</span><span class="sxs-lookup"><span data-stu-id="b3657-129">The following code example is the snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="b3657-130">Uçtan uca şablon tabanlı dağıtım için [birden çok site barındırma kullanan Resource Manager şablonunu](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) ziyaret edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3657-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end to end template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="b3657-131">Yönlendirme kuralı</span><span class="sxs-lookup"><span data-stu-id="b3657-131">Routing rule</span></span>

<span data-ttu-id="b3657-132">Yönlendirme kuralında yapılması gereken bir değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="b3657-132">There is no change required in the routing rule.</span></span> <span data-ttu-id="b3657-133">Uygun site dinleyicisini ilgili arka uç adres havuzuna bağlamak için 'Temel' yönlendirme kuralını kullanmaya devam etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3657-133">The routing rule 'Basic' should continue to be chosen to tie the appropriate site listener to the corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b3657-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b3657-134">Next steps</span></span>

<span data-ttu-id="b3657-135">Birden çok site barındırma hakkında bilgi aldıktan sonra birden fazla web uygulamasını destekleyebilen uygulama ağ geçidi oluşturmak için [birden çok site barındırma kullanan uygulama ağ geçidi oluşturma](application-gateway-create-multisite-azureresourcemanager-powershell.md) bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="b3657-135">After learning about multiple site hosting, go to [create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) to create an application gateway with ability to support more than one web application.</span></span>

