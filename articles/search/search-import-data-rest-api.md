---
title: "aaa \"verileri (REST API - Azure Search) yükleme | Microsoft Docs\""
description: "REST API kullanarak Azure Search tooupload veri tooan dizini hello nasıl öğrenin."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a>Karşıya veri tooAzure arama'yı kullanarak hello REST API'si
> [!div class="op_single_selector"]
>
> * [Genel Bakış](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
>
>

Bu makale size nasıl gösterir toouse hello [Azure Search REST API'sini](https://docs.microsoft.com/rest/api/searchservice/) tooimport verileri Azure Search dizini.

Bu kılavuza başlamadan önce bir [Azure Search dizini oluşturmuş](search-what-is-an-index.md) olmanız gerekir.

Sipariş toopush belgelerde hello REST API kullanarak dizininizi içine bir HTTP POST isteği tooyour dizinin URL uç gönderirsiniz. Merhaba gövdesi hello HTTP istek gövdesi toobe eklenen, değiştirilen veya silinen hello belgeleri içeren bir JSON nesnesidir.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Azure Search hizmet yöneticinizin api anahtarını tanımlama
Merhaba REST API kullanarak hizmetinize karşı HTTP istekleri gönderirken *her* API isteğinin sağladığınız Search Hizmeti hello için oluşturulan hello API-anahtarını içermesi gerekir. Geçerli bir anahtar sahip istek başına temelinde, hello isteği gönderiliyor hello uygulama ve bunu işleyen hello hizmeti arasında güven oluşturur.

1. toofind hizmetinizin api anahtarlarından, toohello kaydolabilirsiniz [Azure portalı](https://portal.azure.com/)
2. Tooyour Azure Search hizmet dikey penceresine gidin
3. Merhaba üzerinde "Anahtarlar" simgesine tıklayın

Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.

* Birincil ve ikincil *yönetici anahtarları* tooall operations hello özelliği toomanage hello hizmeti dahil olmak üzere, tam haklar, oluşturun ve dizinler, dizin oluşturucular ve veri kaynaklarını silin. Tooregenerate hello birincil anahtar ve tam tersini karar verirseniz toouse hello ikincil anahtar devam edebilmesi için bu iki anahtar vardır.
* *Sorgu anahtarları* salt okunur erişim tooindexes ve belgeleri verin ve arama istekleri gönderen genellikle dağıtılmış tooclient uygulamalardır.

Merhaba amacıyla bir dizine veri alma ya da kullanabilirsiniz, birincil veya ikincil yönetici anahtarınızı.

## <a name="decide-which-indexing-action-toouse"></a>Hangi dizin oluşturma eylemini toouse karar verin
Merhaba REST API kullanırken, JSON istek gövdesi tooyour Azure Search dizinine ait uç nokta URL'si ile HTTP POST istekleri gönderirsiniz. HTTP isteği gövdesinin Hello JSON nesnesinde, tek bir JSON dizisi içerecek "tooadd tooyour dizin istediğiniz belgeleri temsil eden JSON nesnelerini içeren değer" adlı, güncelleştirme veya silme.

Merhaba "value" dizisindeki her bir JSON nesnesi, dizine bir belge toobe temsil eder. Bu nesnelerin her biri hello belgenin anahtarını içerir ve istenen hello dizin oluşturma eylemini (karşıya yükleme, birleştirme, silme, vb.) belirtir. Seçtiğiniz Eylemler aşağıda hello bağlı olarak, yalnızca belirli alanlar her belge için dahil edilmelidir:

| @search.action | Açıklama | Her bir belge için gerekli alanlar | Notlar |
| --- | --- | --- | --- |
| `upload` |Bir `upload` benzer tooan "upsert" nerede hello belgenin yeni olması durumunda ekleneceği ve olması mevcut durumunda güncelleştirileceği/değiştirileceği bir eylemdir. |anahtar ve toodefine istediğiniz diğer alanlar |Güncelleştirme/var olan bir belgeyi değiştirirken, hello istekte belirtilen olmayan herhangi bir alan kendi alan çok kümesini sahip`null`. Bu durum, hatta hello alan tooa null olmayan değer önceden ayarlandı oluşur. |
| `merge` |Varolan bir belge ile Merhaba güncelleştirmeleri alanları belirtilmiş. Merhaba belge hello dizininde mevcut değilse hello birleştirme işlemi başarısız olur. |anahtar ve toodefine istediğiniz diğer alanlar |Birleştirmede belirttiğiniz herhangi bir alan varolan bir alana hello hello belgedeki yerini alır. Buna `Collection(Edm.String)` türünde alanlar dahildir. Örneğin, hello belge bir alanı varsa, `tags` değerle `["budget"]` ve değeriyle bir birleştirme yürütme `["economy", "pool"]` için `tags`, hello hello son değerini `tags` alan `["economy", "pool"]`. `["budget", "economy", "pool"]` olmayacaktır. |
| `mergeOrUpload` |Bu eylem gibi davranır `merge` anahtar zaten verilen hello belgeyle hello dizinde varsa. Merhaba belge mevcut değilse gibi davranır `upload` yeni bir belgeyle. |anahtar ve toodefine istediğiniz diğer alanlar |- |
| `delete` |Merhaba belirtilen belge hello dizinden kaldırır. |yalnızca anahtar |Merhaba anahtar alanı yoksayılacak dışında belirttiğiniz tüm alanlar. Bir belgeden tek bir alanı tooremove istiyorsanız kullanın `merge` yerine ve basit şekilde hello alan açık olarak ayarlanıp toonull. |

## <a name="construct-your-http-request-and-request-body"></a>HTTP isteğinizi ve istek gövdenizi oluşturma
Dizin eylemleriniz için hello gerekli alan değerlerini topladıktan, hazır tooconstruct hello asıl HTTP isteğini olan ve JSON istek gövdesi tooimport verilerinizi.

#### <a name="request-and-request-headers"></a>İstek ve İstek Üst Bilgileri
Merhaba URL'de tooprovide, hizmet adı, dizin adı (Bu durumda "hotels") yanı sıra düzgün API sürümünü hello gerekir (Merhaba geçerli API sürümü `2016-09-01` bu belgenin yayımlandığı hello zaman). Toodefine hello gerekir `Content-Type` ve `api-key` istek üstbilgileri. İkinci Hello için hizmetinizin yönetici anahtarlarından birini kullanın.

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a>İstek Gövdesi
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

Bu durumda arama eylemlerimiz olarak `upload`, `mergeOrUpload` ve `delete` kullanıyoruz.

Bu "hotels" dizini örneğinin, birçok belgeyle önceden doldurulduğunu varsayın. Nasıl biz toospecify tüm hello olası belge alanlarını kullanırken sahip değildi Not `mergeOrUpload` ve yalnızca hello belge anahtarını belirttiğimize (`hotelId`) kullanırken `delete`.

Ayrıca, yalnızca too1000 belgeleri (veya 16 MB) tek bir dizin oluşturma isteğine dahil edebileceğinizi unutmayın.

## <a name="understand-your-http-response-code"></a>HTTP yanıt kodunuzu anlama
#### <a name="200"></a>200
Başarılı bir dizin oluşturma isteği gönderdikten sonra `200 OK` durum koduna sahip bir HTTP yanıtı alırsınız. Merhaba hello HTTP yanıtının JSON gövdesi aşağıdaki gibi olur:

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a>207
En az bir öğenin dizine alınması başarısız olduğunda `207` durum kodu döndürülür. Merhaba hello HTTP yanıtının JSON gövdesi hello başarısız belgeler hakkındaki bilgileri içerir.

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> Bu genellikle hello yük gelir aramanızı hizmet burada dizin oluşturma isteklerinin başlayacak tooreturn bir noktaya eriştiği `503` yanıtlar. Bu durumda, istemci kodunuzun geri alınmasını ve yeniden denemeden önce beklenmesini kesinlikle öneririz. Gelecekteki isteklerin başarılı olma hello şansı artırılmış bazı zaman toorecover hello sistem verir. İsteklerinizi hızla yeniden hello durumu yalnızca uzatır.
>
>

#### <a name="429"></a>429
Durum kodu `429` hello dizin başına belge sayısı kotanızı aştığınızda döndürülür.

#### <a name="503"></a>503
Durum kodu `503` hello isteği hello öğelerde hiçbiri başarılı bir şekilde dizine alınamazsa döndürülür. Bu hata, ağır yük altında hello sistemidir ve isteğiniz şu anda işlenemiyor anlamına gelir.

> [!NOTE]
> Bu durumda, istemci kodunuzun geri alınmasını ve yeniden denemeden önce beklenmesini kesinlikle öneririz. Gelecekteki isteklerin başarılı olma hello şansı artırılmış bazı zaman toorecover hello sistem verir. İsteklerinizi hızla yeniden hello durumu yalnızca uzatır.
>
>

Belge eylemleri ve başarı/hata yanıtları hakkında daha fazla bilgi için lütfen bkz. [Belge Ekleme, Güncelleştirme veya Silme](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents). Hata durumunda döndürülebilen diğer HTTP durum kodları hakkında daha fazla bilgi için bkz. [HTTP durum kodları (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

## <a name="next-steps"></a>Sonraki adımlar
Azure Search dizininizi doldurduktan sonra belgeler için sorguları toosearch veren hazır toostart olacaktır. Ayrıntılı bilgi için bkz. [Azure Search Dizininizi Sorgulama](search-query-overview.md).
