---
title: "API denetçisi - Azure API Management ile aaaTrace çağrıları | Microsoft Docs"
description: "API denetçisi Azure API Management kullanarak tootrace aramaları nasıl hello öğrenin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 4b222327-c8a4-4f33-9a06-adff2a9834d9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: b0c401caa8da1b789f6cfe5edf97a5f118d78f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a><span data-ttu-id="f73f8-103">Azure API Management'te toouse hello API denetçisi tootrace nasıl çağırır</span><span class="sxs-lookup"><span data-stu-id="f73f8-103">How toouse hello API Inspector tootrace calls in Azure API Management</span></span>
<span data-ttu-id="f73f8-104">API Management aracı toohelp API Inspector sağlar, hata ayıklama ve Apı'lerinizi sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="f73f8-104">API Management provides an API Inspector tool toohelp you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="f73f8-105">Merhaba API denetçisi program aracılığıyla kullanılabilir ve doğrudan hello Geliştirici portalından da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f73f8-105">hello API Inspector can be used programmatically and can also be used directly from hello developer portal.</span></span> 

<span data-ttu-id="f73f8-106">Ayrıca tootracing operations API'si Inspector ayrıca izler [ilke ifadesi](https://msdn.microsoft.com/library/azure/dn910913.aspx) değerlendirmeleri.</span><span class="sxs-lookup"><span data-stu-id="f73f8-106">In addition tootracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="f73f8-107">Bir örnek için bkz: [bulut kapak bölüm 177: diğer API Management Özellikler](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too21:00 ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="f73f8-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too21:00.</span></span>

<span data-ttu-id="f73f8-108">Bu kılavuz, API Inspector'ı kullanarak bir adım adım kılavuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="f73f8-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="f73f8-109">API denetçisi izlemeleri yalnızca oluşturulan ve toohello ait abonelik anahtarlarını içeren istekler için kullanılabilir hale [yönetici](api-management-howto-create-groups.md) hesabı.</span><span class="sxs-lookup"><span data-stu-id="f73f8-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong toohello [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="f73f8-110"><a name="trace-call"></a> Kullanım API denetçisi tootrace çağrısı</span><span class="sxs-lookup"><span data-stu-id="f73f8-110"><a name="trace-call"> </a> Use API Inspector tootrace a call</span></span>
<span data-ttu-id="f73f8-111">toouse API denetleyici Ekle bir **ocp apim izleme: true** istek üstbilgisi tooyour işlem çağrısı ve ardından karşıdan yükleyip hello tarafından gösterilen hello URL'yi kullanarak hello izleme incelemek **apim izleme konumu ocp** yanıtı üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="f73f8-111">toouse API Inspector, add an **ocp-apim-trace: true** request header tooyour operation call, and then download and inspect hello trace using hello URL indicated by hello **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="f73f8-112">Bu programlı şekilde yapılabilir ve doğrudan hello Geliştirici portalından da yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="f73f8-112">This can be done programatically, and can also be done directly from hello developer portal.</span></span>

<span data-ttu-id="f73f8-113">Bu öğretici nasıl hello yapılandırılmış temel hesaplayıcı API'si kullanarak toouse hello API denetçisi tootrace işlemleri hello gösterir [ilk API'nizi yönetme](api-management-get-started.md) başlama Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="f73f8-113">This tutorial shows how toouse hello API Inspector tootrace operations using hello Basic Calculator API that is configured in hello [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="f73f8-114">Bu öğreticinin tamamlanan yapmadıysanız, yalnızca birkaç dakika sonra tooimport hello temel hesaplayıcı API'si alır veya seçtiğiniz Echo API'si hello gibi başka bir API kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f73f8-114">If you haven't completed that tutorial it only takes a few moments tooimport hello Basic Calculator API, or you can use another API of your choosing such as hello Echo API.</span></span> <span data-ttu-id="f73f8-115">Her API Management hizmet örneği ile kullanılan tooexperiment ve API Management hakkında bilgi edinin bir Echo API'si ile önceden yapılandırılmış olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="f73f8-115">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="f73f8-116">Merhaba Echo API'si, hangi giriş tooit gönderilen geri döndürür.</span><span class="sxs-lookup"><span data-stu-id="f73f8-116">hello Echo API returns back whatever input is sent tooit.</span></span> <span data-ttu-id="f73f8-117">toouse, tüm HTTP fiili çağırabileceği ve hello dönüş değeri, size gönderilen yalnızca olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f73f8-117">toouse it, you can invoke any HTTP verb, and hello return value will simply be what you sent.</span></span> 

<span data-ttu-id="f73f8-118">başlatıldı, tooget tıklatın **Geliştirici Portalı** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="f73f8-118">tooget started, click **Developer portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="f73f8-119">İşlemler uygun şekilde tooview sağlayan doğrudan hello Geliştirici portalından çağrılabilir ve bir API'nin işlemlerini hello test edin.</span><span class="sxs-lookup"><span data-stu-id="f73f8-119">Operations can be called directly from hello developer portal which provides a convenient way tooview and test hello operations of an API.</span></span>

> <span data-ttu-id="f73f8-120">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="f73f8-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![API Management Geliştirici Portalı][api-management-developer-portal-menu]

<span data-ttu-id="f73f8-122">Tıklatın **API'leri** hello üst menüsünden ve ardından **temel hesaplayıcı**.</span><span class="sxs-lookup"><span data-stu-id="f73f8-122">Click **APIs** from hello top menu, and then click **Basic Calculator**.</span></span>

![Echo API’si][api-management-api]

<span data-ttu-id="f73f8-124">Tıklatın **deneyin** tootry hello **iki tamsayı Ekle** işlemi.</span><span class="sxs-lookup"><span data-stu-id="f73f8-124">Click **Try it** tootry hello **Add two integers** operation.</span></span>

![Deneyin][api-management-open-console]

<span data-ttu-id="f73f8-126">Merhaba varsayılan parametre değerlerini ve istediğiniz hello ürün için select hello abonelik anahtar toouse hello tutmak **abonelik anahtarı** açılır.</span><span class="sxs-lookup"><span data-stu-id="f73f8-126">Keep hello default parameter values, and select hello subscription key for hello product you want toouse from hello **subscription-key** drop-down.</span></span>

<span data-ttu-id="f73f8-127">Varsayılan olarak hello Geliştirici Portalı hello **Ocp Apim izleme** üstbilgi zaten ayarlanmış çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="f73f8-127">By default in hello developer portal hello **Ocp-Apim-Trace** header is already set too**true**.</span></span> <span data-ttu-id="f73f8-128">Bir izleme oluşturulan olup olmadığına bakılmaksızın bu başlığı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f73f8-128">This header configures whether or not a trace is generated.</span></span>

![Gönder][api-management-http-get]

<span data-ttu-id="f73f8-130">Tıklatın **Gönder** tooinvoke hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="f73f8-130">Click **Send** tooinvoke hello operation.</span></span>

![Gönder][api-management-send-results]

<span data-ttu-id="f73f8-132">Hello yanıt üstbilgileri olacak bir **ocp apim izleme konumu** değeri benzer toohello aşağıdaki örneğine sahip.</span><span class="sxs-lookup"><span data-stu-id="f73f8-132">In hello response headers will be an **ocp-apim-trace-location** with a value similar toohello following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="f73f8-133">Merhaba izleme adresinden yüklenebilir hello konumu belirtilen ve hello sonraki adımda gösterildiği gibi gözden.</span><span class="sxs-lookup"><span data-stu-id="f73f8-133">hello trace can be downloaded from hello specified location and reviewed as demonstrated in hello next step.</span></span> <span data-ttu-id="f73f8-134">Yalnızca hello son 100 günlük girişlerini depolanır ve günlük konumlarını dönüş yeniden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f73f8-134">Note that only hello last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="f73f8-135">100'den fazla çağrı yapmak isterseniz bunu izlemenin etkin, sonunda hello ilk izlemeleri yerinde üzerine başlar.</span><span class="sxs-lookup"><span data-stu-id="f73f8-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting hello first traces in place.</span></span>

## <span data-ttu-id="f73f8-136"><a name="inspect-trace"></a>Hello izleme inceleyin.</span><span class="sxs-lookup"><span data-stu-id="f73f8-136"><a name="inspect-trace"> </a>Inspect hello trace</span></span>
<span data-ttu-id="f73f8-137">Merhaba izleme tooreview hello değerleri hello hello izleme dosyası karşıdan **ocp apim izleme konumu** URL.</span><span class="sxs-lookup"><span data-stu-id="f73f8-137">tooreview hello values in hello trace, download hello trace file from hello **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="f73f8-138">JSON biçiminde bir metin dosyasıdır ve örnek aşağıdaki girişleri benzer toohello içerir.</span><span class="sxs-lookup"><span data-stu-id="f73f8-138">It is a text file in JSON format, and contains entries similar toohello following example.</span></span>

```json
{
    "traceId": "abcd8ea63d134c1fabe6371566c7cbea",
    "traceEntries": {
        "inbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0725926",
                "data": {
                    "request": {
                        "method": "GET",
                        "url": "https://contoso5.azure-api.net/calc/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "Connection",
                                "value": "Keep-Alive"
                            },
                            {
                                "name": "Host",
                                "value": "contoso5.azure-api.net"
                            }
                        ]
                    }
                }
            },
            {
                "source": "mapper",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0726213",
                "data": {
                    "configuration": {
                        "api": {
                            "from": "/calc",
                            "to": {
                                "scheme": "http",
                                "host": "calcapi.cloudapp.net",
                                "port": 80,
                                "path": "/api",
                                "queryString": "",
                                "query": {},
                                "isDefaultPort": true
                            }
                        },
                        "operation": {
                            "method": "GET",
                            "uriTemplate": "/add?a={a}&b={b}"
                        },
                        "user": {
                            "id": 1,
                            "groups": [
                                "Administrators",
                                "Developers"
                            ]
                        },
                        "product": {
                            "id": 1
                        }
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0727522",
                "data": {
                    "message": "Request is being forwarded toohello backend service.",
                    "request": {
                        "method": "GET",
                        "url": "http://calcapi.cloudapp.net/api/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "X-Forwarded-For",
                                "value": "33.52.215.35"
                            }
                        ]
                    }
                }
            }
        ],
        "outbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1960601",
                "data": {
                    "response": {
                        "status": {
                            "code": 200,
                            "reason": "OK"
                        },
                        "headers": [
                            {
                                "name": "Pragma",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Length",
                                "value": "124"
                            },
                            {
                                "name": "Cache-Control",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Type",
                                "value": "application/xml; charset=utf-8"
                            },
                            {
                                "name": "Date",
                                "value": "Tue, 23 Jun 2015 19:51:35 GMT"
                            },
                            {
                                "name": "Expires",
                                "value": "-1"
                            },
                            {
                                "name": "Server",
                                "value": "Microsoft-IIS/8.5"
                            },
                            {
                                "name": "X-AspNet-Version",
                                "value": "4.0.30319"
                            },
                            {
                                "name": "X-Powered-By",
                                "value": "ASP.NET"
                            }
                        ]
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1961112",
                "data": {
                    "message": "Response headers have been sent toohello caller. Starting toostream hello response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming toohello caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="f73f8-139"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f73f8-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="f73f8-140">İlke ifadelerinde izleme, gösterisini izleyin [bulut kapak bölüm 177: diğer API Management Özellikler](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="f73f8-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="f73f8-141">İleri Sarma too21:00 toosee hello demo.</span><span class="sxs-lookup"><span data-stu-id="f73f8-141">Fast-forward too21:00 toosee hello demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector tootrace a call]: #trace-call
[Inspect hello trace]: #inspect-trace
[Next steps]: #next-steps

[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Azure Classic Portal]: https://manage.windowsazure.com/


[api-management-developer-portal-menu]: ./media/api-management-howto-api-inspector/api-management-developer-portal-menu.png
[api-management-api]: ./media/api-management-howto-api-inspector/api-management-api.png
[api-management-echo-api-get]: ./media/api-management-howto-api-inspector/api-management-echo-api-get.png
[api-management-developer-key]: ./media/api-management-howto-api-inspector/api-management-developer-key.png
[api-management-open-console]: ./media/api-management-howto-api-inspector/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-api-inspector/api-management-http-get.png
[api-management-send-results]: ./media/api-management-howto-api-inspector/api-management-send-results.png




