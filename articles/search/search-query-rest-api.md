---
title: "Ayrıca \"bir dizin (REST API - Azure Search) sorgu | Microsoft Docs\""
description: "Azure Search'te bir arama sorgusu oluşturun ve arama parametrelerini toofilter ve sıralama arama sonuçlarını kullanın."
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a>Merhaba REST API kullanarak Azure Search dizininizi sorgulama
> [!div class="op_single_selector"]
>
> * [Genel Bakış](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Bu makalede tooquery kullanarak bir dizinin nasıl hello gösterilmektedir [Azure Search REST API'sini](https://docs.microsoft.com/rest/api/searchservice/).

Bu kılavuzda başlamadan önce, [Azure Search dizini oluşturmuş](search-what-is-an-index.md) ve [bunu verilerle doldurmuş](search-what-is-data-import.md) olmanız gerekir. Arka plan bilgileri için bkz. [Azure Search'te tam metin araması nasıl çalışır](search-lucene-query-architecture.md)?

## <a name="identify-your-azure-search-services-query-api-key"></a>Azure Search hizmet sorgunuzun api anahtarını tanımlama
Bir anahtar hello Azure Search REST API'sini karşı tüm arama işlemlerinin hello bileşenidir *api anahtarını* sağladığınız hello hizmeti için oluşturulan. Geçerli bir anahtar sahip istek başına temelinde, hello isteği gönderiliyor hello uygulama ve bunu işleyen hello hizmeti arasında güven oluşturur.

1. toofind hizmetinizin api anahtarlarından, toohello kaydolabilirsiniz [Azure portalı](https://portal.azure.com/)
2. Tooyour Azure Search hizmet dikey penceresine gidin
3. Merhaba "Anahtarlar" simgesine tıklayın

Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.

* Birincil ve ikincil *yönetici anahtarları* tooall operations hello özelliği toomanage hello hizmeti dahil olmak üzere, tam haklar, oluşturun ve dizinler, dizin oluşturucular ve veri kaynaklarını silin. Tooregenerate hello birincil anahtar ve tam tersini karar verirseniz toouse hello ikincil anahtar devam edebilmesi için bu iki anahtar vardır.
* *Sorgu anahtarları* salt okunur erişim tooindexes ve belgeleri verin ve arama istekleri gönderen genellikle dağıtılmış tooclient uygulamalardır.

Bir dizini sorgulama hello amacıyla, sorgu anahtarlarınızdan birini kullanabilirsiniz. Yönetici anahtarlarınız da sorgular için kullanılabilir, ancak bu daha iyi hello aşağıdaki gibi uygulama kodunuzda bir sorgu anahtarı kullanmanız gerekir [en az ayrıcalık prensibi](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="formulate-your-query"></a>Sorgunuzu düzenleme
İki yolu vardır çok[hello REST API kullanarak dizininizi aramanın](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Bir HTTP POST isteği tooissue sorgu parametrelerinizin hello istek gövdesindeki bir JSON nesnesinde tanımlandığı yoludur. Merhaba başka bir yolla tooissue bir HTTP GET isteği burada sorgu parametrelerinizin hello istek URL'si içinde tanımlanır. POST sahip daha [esnek sınırlara](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) hello Sorgu parametrelerinin boyutu açısından get'ten üzerinde. Bu nedenle, GET'i kullanmanın daha kullanışlı olduğu özel durumlar olmadığı sürece POST kullanmanızı öneririz.

POST ve GET için tooprovide gerekir, *hizmet adı*, *dizin adı*ve hello uygun *API sürümü* (Merhaba geçerli API sürümü `2016-09-01` hello zaman Bu belgenin yayımlandığı) hello istek URL'si. GET için hello *sorgu dizesi* hello hello URL hello sorgu parametreleri Burada sağladığınız sonudur. Aşağıda hello URL biçimi için bkz:

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

Merhaba olduğu POST hello için aynı, ancak yalnızca api sürümü hello sorgu dizesi parametreleri ile biçimlendirin.

#### <a name="example-queries"></a>Örnek Sorgular
Burada "hotels" adlı bir dizinde birkaç örnek sorgu verilmiştir. Bu sorgular, hem GET hem de POST biçiminde gösterilir.

Merhaba tüm dizinde "budget" Merhaba dönem için arama ve yalnızca hello dönmek `hotelName` alan:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

Bir filtre toohello dizin toofind Oteller geceliği 150 gece dolardan ucuz uygulamak ve dönüş hello `hotelId` ve `description`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

Arama hello tüm dizin, belirli bir alana göre sıralama (`lastRenovationDate`) azalan sırada hello ilk iki sonucu alın ve yalnızca Göster `hotelName` ve `lastRenovationDate`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a>HTTP isteğinizi gönderme
Artık HTTP istek URL'nizin (GET için) veya gövdenizin (POST için) parçası olarak sorgunuzu düzenlediğinize göre, istek üst bilgilerinizi tanımlayıp sorgunuzu gönderebilirsiniz.

#### <a name="request-and-request-headers"></a>İstek ve İstek Üst Bilgileri
GET için iki, POST için ise üç istek üst bilgisi tanımlamanız gerekir:

1. Merhaba `api-key` üstbilgi bulunan adımda ı yukarıdaki toohello sorgu anahtarını ayarlamanız gerekir. Bir yönetici anahtarı hello kullanabilirsiniz `api-key` üstbilgisi, ancak önerilir salt okunur erişim tooindexes ve belgeler özel olarak verir gibi bir sorgu anahtarı kullanmanızı öneririz.
2. Merhaba `Accept` üstbilgisi çok ayarlanmalıdır`application/json`.
3. Yalnızca POST için hello `Content-Type` üstbilgisi çok ayarlanmalıdır`application/json`.

Merhaba hello "motel" terimini arayan basit bir sorgu kullanarak Azure Search REST API'sini kullanarak HTTP GET isteği toosearch hello "hotels" dizini için aşağıya bakın:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

İşte aynı hello örnek sorgu, HTTP POST kullanılarak bu süre:

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

Başarılı bir sorgu isteği bir durum koduna neden olacak `200 OK` ve hello arama sonuçları hello yanıt gövdesinde JSON olarak döndürülür. İşte hello "hotels" dizininin içinde hello örnek verilerle varsayıldığında hello sorgunun yukarıda için hangi hello sonuçları [Veri Al'ı kullanarak Azure Search REST API hello](search-import-data-rest-api.md) (JSON, daha anlaşılır olması için biçimlendirilmiş bu hello unutmayın).

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

toolearn daha, lütfen şu adresi ziyaret hello "Yanıt" bölümünü [Search belgeleri](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Hata durumunda döndürülebilen diğer HTTP durum kodları hakkında daha fazla bilgi için bkz. [HTTP durum kodları (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).
