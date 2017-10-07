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
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a>Azure API Management'te toouse hello API denetçisi tootrace nasıl çağırır
API Management aracı toohelp API Inspector sağlar, hata ayıklama ve Apı'lerinizi sorun giderme. Merhaba API denetçisi program aracılığıyla kullanılabilir ve doğrudan hello Geliştirici portalından da kullanılabilir. 

Ayrıca tootracing operations API'si Inspector ayrıca izler [ilke ifadesi](https://msdn.microsoft.com/library/azure/dn910913.aspx) değerlendirmeleri. Bir örnek için bkz: [bulut kapak bölüm 177: diğer API Management Özellikler](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) ve too21:00 ileri sarma.

Bu kılavuz, API Inspector'ı kullanarak bir adım adım kılavuz sağlar.

> [!NOTE]
> API denetçisi izlemeleri yalnızca oluşturulan ve toohello ait abonelik anahtarlarını içeren istekler için kullanılabilir hale [yönetici](api-management-howto-create-groups.md) hesabı.
> 
> 

## <a name="trace-call"></a> Kullanım API denetçisi tootrace çağrısı
toouse API denetleyici Ekle bir **ocp apim izleme: true** istek üstbilgisi tooyour işlem çağrısı ve ardından karşıdan yükleyip hello tarafından gösterilen hello URL'yi kullanarak hello izleme incelemek **apim izleme konumu ocp** yanıtı üstbilgisi. Bu programlı şekilde yapılabilir ve doğrudan hello Geliştirici portalından da yapılabilir.

Bu öğretici nasıl hello yapılandırılmış temel hesaplayıcı API'si kullanarak toouse hello API denetçisi tootrace işlemleri hello gösterir [ilk API'nizi yönetme](api-management-get-started.md) başlama Öğreticisi. Bu öğreticinin tamamlanan yapmadıysanız, yalnızca birkaç dakika sonra tooimport hello temel hesaplayıcı API'si alır veya seçtiğiniz Echo API'si hello gibi başka bir API kullanabilirsiniz. Her API Management hizmet örneği ile kullanılan tooexperiment ve API Management hakkında bilgi edinin bir Echo API'si ile önceden yapılandırılmış olarak gelir. Merhaba Echo API'si, hangi giriş tooit gönderilen geri döndürür. toouse, tüm HTTP fiili çağırabileceği ve hello dönüş değeri, size gönderilen yalnızca olacaktır. 

başlatıldı, tooget tıklatın **Geliştirici Portalı** API Management hizmetiniz için hello Azure Portalı'nda. İşlemler uygun şekilde tooview sağlayan doğrudan hello Geliştirici portalından çağrılabilir ve bir API'nin işlemlerini hello test edin.

> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.
> 
> 

![API Management Geliştirici Portalı][api-management-developer-portal-menu]

Tıklatın **API'leri** hello üst menüsünden ve ardından **temel hesaplayıcı**.

![Echo API’si][api-management-api]

Tıklatın **deneyin** tootry hello **iki tamsayı Ekle** işlemi.

![Deneyin][api-management-open-console]

Merhaba varsayılan parametre değerlerini ve istediğiniz hello ürün için select hello abonelik anahtar toouse hello tutmak **abonelik anahtarı** açılır.

Varsayılan olarak hello Geliştirici Portalı hello **Ocp Apim izleme** üstbilgi zaten ayarlanmış çok**doğru**. Bir izleme oluşturulan olup olmadığına bakılmaksızın bu başlığı yapılandırır.

![Gönder][api-management-http-get]

Tıklatın **Gönder** tooinvoke hello işlemi.

![Gönder][api-management-send-results]

Hello yanıt üstbilgileri olacak bir **ocp apim izleme konumu** değeri benzer toohello aşağıdaki örneğine sahip.

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

Merhaba izleme adresinden yüklenebilir hello konumu belirtilen ve hello sonraki adımda gösterildiği gibi gözden. Yalnızca hello son 100 günlük girişlerini depolanır ve günlük konumlarını dönüş yeniden unutmayın. 100'den fazla çağrı yapmak isterseniz bunu izlemenin etkin, sonunda hello ilk izlemeleri yerinde üzerine başlar.

## <a name="inspect-trace"></a>Hello izleme inceleyin.
Merhaba izleme tooreview hello değerleri hello hello izleme dosyası karşıdan **ocp apim izleme konumu** URL. JSON biçiminde bir metin dosyasıdır ve örnek aşağıdaki girişleri benzer toohello içerir.

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

## <a name="next-steps"> </a>Sonraki adımlar
* İlke ifadelerinde izleme, gösterisini izleyin [bulut kapak bölüm 177: diğer API Management Özellikler](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/). İleri Sarma too21:00 toosee hello demo.

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




