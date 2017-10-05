---
title: "API denetçisi - Azure API Management ile çağrıları izleme | Microsoft Docs"
description: "Azure API Management'te API Inspector'ı kullanarak çağrıları izleme öğrenin."
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
ms.openlocfilehash: a9d4d3be7f046af975f6dc25670070204848588c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-api-inspector-to-trace-calls-in-azure-api-management"></a><span data-ttu-id="b0a06-103">Azure API Management'te izleme API denetleyici kullanma çağırır</span><span class="sxs-lookup"><span data-stu-id="b0a06-103">How to use the API Inspector to trace calls in Azure API Management</span></span>
<span data-ttu-id="b0a06-104">API Management Apı'lerinizi sorun giderme ve hata ayıklama ile yardımcı olacak bir API denetçisi aracı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0a06-104">API Management provides an API Inspector tool to help you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="b0a06-105">API denetçisi program aracılığıyla kullanılabilir ve doğrudan Geliştirici portalından da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b0a06-105">The API Inspector can be used programmatically and can also be used directly from the developer portal.</span></span> 

<span data-ttu-id="b0a06-106">İzleme işlemlerinin ek olarak, API Inspector ayrıca izler [ilke ifadesi](https://msdn.microsoft.com/library/azure/dn910913.aspx) değerlendirmeleri.</span><span class="sxs-lookup"><span data-stu-id="b0a06-106">In addition to tracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="b0a06-107">Bir örnek için bkz: [bulut kapak bölüm 177: diğer API Management Özellikler](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve 21:00 için ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="b0a06-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 21:00.</span></span>

<span data-ttu-id="b0a06-108">Bu kılavuz, API Inspector'ı kullanarak bir adım adım kılavuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0a06-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="b0a06-109">API denetçisi izlemeleri yalnızca oluşturulan ve ait abonelik anahtarlarını içeren istekler için kullanılabilir hale [yönetici](api-management-howto-create-groups.md) hesabı.</span><span class="sxs-lookup"><span data-stu-id="b0a06-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong to the [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="b0a06-110"><a name="trace-call"></a> Kullanım API Inspector'ı bir çağrı izlemek için</span><span class="sxs-lookup"><span data-stu-id="b0a06-110"><a name="trace-call"> </a> Use API Inspector to trace a call</span></span>
<span data-ttu-id="b0a06-111">API denetçisi kullanmak için ekleyin bir **ocp apim izleme: true** isteği işlemi aramanız başlığına ve yükleyin ve belirtilen URL'yi kullanarak izleme incelemek **ocp apim izleme konumu** yanıt Üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="b0a06-111">To use API Inspector, add an **ocp-apim-trace: true** request header to your operation call, and then download and inspect the trace using the URL indicated by the **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="b0a06-112">Bu programlı şekilde yapılabilir ve doğrudan Geliştirici portalından da yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="b0a06-112">This can be done programatically, and can also be done directly from the developer portal.</span></span>

<span data-ttu-id="b0a06-113">Bu öğretici yapılandırılan temel hesaplayıcı API'si kullanarak izleme işlemleri için API denetçisi kullanmayı gösterir [ilk API'nizi yönetme](api-management-get-started.md) başlama Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b0a06-113">This tutorial shows how to use the API Inspector to trace operations using the Basic Calculator API that is configured in the [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="b0a06-114">Bu öğreticinin tamamlanan yapmadıysanız, yalnızca temel hesaplayıcı API'si almak için birkaç dakika sürer veya seçtiğiniz Echo API'si gibi başka bir API kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0a06-114">If you haven't completed that tutorial it only takes a few moments to import the Basic Calculator API, or you can use another API of your choosing such as the Echo API.</span></span> <span data-ttu-id="b0a06-115">Her API Management hizmeti örneği, API Management’i denemek ve hakkında bilgi almak için kullanılabilecek bir Echo API’si ile önceden yapılandırılmış olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="b0a06-115">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="b0a06-116">Echo API'si, hangi giriş kendisine gönderilen geri döndürür.</span><span class="sxs-lookup"><span data-stu-id="b0a06-116">The Echo API returns back whatever input is sent to it.</span></span> <span data-ttu-id="b0a06-117">Kullanmak için bir HTTP fiili çağırabileceği ve dönüş değeri, yalnızca size gönderilen olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b0a06-117">To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.</span></span> 

<span data-ttu-id="b0a06-118">Kullanmaya başlamak için tıklayın **Geliştirici Portalı** API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="b0a06-118">To get started, click **Developer portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="b0a06-119">İşlemleri görüntülemek ve bir API'nin işlemlerini test etmek için kullanışlı bir yol sağlayan doğrudan Geliştirici portalından çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="b0a06-119">Operations can be called directly from the developer portal which provides a convenient way to view and test the operations of an API.</span></span>

> <span data-ttu-id="b0a06-120">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b0a06-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![API Management Geliştirici Portalı][api-management-developer-portal-menu]

<span data-ttu-id="b0a06-122">Tıklatın **API'leri** üst menüsünden ve ardından **temel hesaplayıcı**.</span><span class="sxs-lookup"><span data-stu-id="b0a06-122">Click **APIs** from the top menu, and then click **Basic Calculator**.</span></span>

![Echo API’si][api-management-api]

<span data-ttu-id="b0a06-124">Tıklatın **deneyin** denemek için **iki tamsayı Ekle** işlemi.</span><span class="sxs-lookup"><span data-stu-id="b0a06-124">Click **Try it** to try the **Add two integers** operation.</span></span>

![Deneyin][api-management-open-console]

<span data-ttu-id="b0a06-126">Varsayılan parametre değerlerini koruyun ve abonelik anahtar için kullanmak istediğiniz ürün **abonelik anahtarı** açılır.</span><span class="sxs-lookup"><span data-stu-id="b0a06-126">Keep the default parameter values, and select the subscription key for the product you want to use from the **subscription-key** drop-down.</span></span>

<span data-ttu-id="b0a06-127">Geliştirici Portalı'nda varsayılan **Ocp Apim izleme** üstbilgisi zaten ayarlandı **doğru**.</span><span class="sxs-lookup"><span data-stu-id="b0a06-127">By default in the developer portal the **Ocp-Apim-Trace** header is already set to **true**.</span></span> <span data-ttu-id="b0a06-128">Bir izleme oluşturulan olup olmadığına bakılmaksızın bu başlığı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="b0a06-128">This header configures whether or not a trace is generated.</span></span>

![Gönder][api-management-http-get]

<span data-ttu-id="b0a06-130">Tıklatın **Gönder** işlemini çağırmak için.</span><span class="sxs-lookup"><span data-stu-id="b0a06-130">Click **Send** to invoke the operation.</span></span>

![Gönder][api-management-send-results]

<span data-ttu-id="b0a06-132">Yanıt Üstbilgileri olacak bir **ocp apim izleme konumu** aşağıdaki örneğe benzer bir değere sahip.</span><span class="sxs-lookup"><span data-stu-id="b0a06-132">In the response headers will be an **ocp-apim-trace-location** with a value similar to the following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="b0a06-133">İzleme belirtilen konumdan indirilir ve sonraki adımda gösterildiği gibi gözden.</span><span class="sxs-lookup"><span data-stu-id="b0a06-133">The trace can be downloaded from the specified location and reviewed as demonstrated in the next step.</span></span> <span data-ttu-id="b0a06-134">Yalnızca son 100 günlük girişlerini depolanır ve günlük konumlarını dönüş yeniden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b0a06-134">Note that only the last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="b0a06-135">100'den fazla çağrı yapmak isterseniz bunu izlemenin etkin, sonunda yerinde ilk izlemeleri üzerine başlar.</span><span class="sxs-lookup"><span data-stu-id="b0a06-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting the first traces in place.</span></span>

## <span data-ttu-id="b0a06-136"><a name="inspect-trace"></a>İzleme inceleyin.</span><span class="sxs-lookup"><span data-stu-id="b0a06-136"><a name="inspect-trace"> </a>Inspect the trace</span></span>
<span data-ttu-id="b0a06-137">İzleme değerlerde gözden geçirmek için izleme dosyasını indirin **ocp apim izleme konumu** URL.</span><span class="sxs-lookup"><span data-stu-id="b0a06-137">To review the values in the trace, download the trace file from the **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="b0a06-138">JSON biçiminde bir metin dosyasıdır ve aşağıdaki örneğe benzer girdiler içerir.</span><span class="sxs-lookup"><span data-stu-id="b0a06-138">It is a text file in JSON format, and contains entries similar to the following example.</span></span>

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
                    "message": "Request is being forwarded to the backend service.",
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
                    "message": "Response headers have been sent to the caller. Starting to stream the response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming to the caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="b0a06-139"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b0a06-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="b0a06-140">İlke ifadelerinde izleme, gösterisini izleyin [bulut kapak bölüm 177: diğer API Management Özellikler](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="b0a06-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="b0a06-141">21: demo görmek için 00 için ileri sarma.</span><span class="sxs-lookup"><span data-stu-id="b0a06-141">Fast-forward to 21:00 to see the demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector to trace a call]: #trace-call
[Inspect the trace]: #inspect-trace
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




