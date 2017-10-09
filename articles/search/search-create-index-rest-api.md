---
title: "aaa \"(REST API - Azure Search) dizin oluşturma | Microsoft Docs\""
description: "Hello Azure Search HTTP REST API'sini kullanarak kod içinde bir dizin oluşturun."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>Merhaba REST API kullanarak Azure Search dizini oluşturma
> [!div class="op_single_selector"]
>
> * [Genel Bakış](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

Bu makale bir Azure Search oluşturma hello işleminde size kılavuzluk edecektir [dizin](https://docs.microsoft.com/rest/api/searchservice/Create-Index) hello Azure Search REST API'sini kullanarak.

Bu kılavuzu izlemeden ve dizin oluşturmadan önce, [Azure Search hizmeti oluşturmuş](search-create-service-portal.md) olmanız gerekir.

Merhaba REST API kullanarak Azure Search dizini, bir tek HTTP POST isteği tooyour Azure Search hizmet URL uç verecek toocreate. Dizin tanımınızı doğru biçimlendirilmiş JSON içeriği olarak hello istek gövdesinde yer alır.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Azure Search hizmet yöneticinizin api anahtarını tanımlama
Azure Search Hizmeti sağlamış olduğunuza göre hizmetinizin URL uç hello REST API kullanarak HTTP istekleri gönderebilirsiniz. *Tüm* API istekleri hello API hello sağladığınız arama hizmeti için oluşturulan anahtar içermelidir. Geçerli bir anahtar sahip istek başına temelinde, hello isteği gönderiliyor hello uygulama ve bunu işleyen hello hizmeti arasında güven oluşturur.

1. toofind hizmetinizin api hello kapatmalıdır anahtarlarından [Azure portalı](https://portal.azure.com/)
2. Tooyour Azure Search hizmet dikey penceresine gidin
3. Merhaba üzerinde "Anahtarlar" simgesine tıklayın

Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.

* Birincil ve ikincil *yönetici anahtarları* tooall operations hello özelliği toomanage hello hizmeti dahil olmak üzere, tam haklar, oluşturun ve dizinler, dizin oluşturucular ve veri kaynaklarını silin. Tooregenerate hello birincil anahtar ve tam tersini karar verirseniz toouse hello ikincil anahtar devam edebilmesi için bu iki anahtar vardır.
* *Sorgu anahtarları* salt okunur erişim tooindexes ve belgeleri verin ve arama istekleri gönderen genellikle dağıtılmış tooclient uygulamalardır.

Merhaba amacıyla dizin oluşturma ya da kullanabilirsiniz, birincil veya ikincil yönetici anahtarınızı.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Doğru biçimlendirilmiş JSON kullanarak Azure Search dizininizi tanımlama
Tek bir HTTP POST isteği tooyour hizmeti dizininizi oluşturur. Merhaba HTTP POST isteğinizin gövdesi, Azure Search dizininizi tanımlayan tek bir JSON nesnesi içerir.

1. Bu JSON nesnesinin ilk özelliği Hello hello dizininizin adıdır.
2. Bu JSON nesnesinin ikinci özelliği Hello olan adlı bir JSON dizisi `fields` , dizininizdeki her bir alan için ayrı bir JSON nesnesi içerir. Bu JSON nesnelerin her biri birden çok ad/değer çiftleri içeren her "ad" dahil olmak üzere hello alan özniteliklerini "tür" vb..

Bu, arama kullanıcı deneyiminizi ve iş gereksinimlerinizi göz önünde her bir alan hello atanması gerektiğinden, dizininizi tasarlarken tutmanız önemlidir [uygun öznitelikler](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Toowhich alanlar geçerli hangi arama özelliklerinin (filtreleme, modelleme tam metin araması sıralama vb. olduğunu) bu öznitelikler denetler. Belirtmediğiniz her öznitelik için özellikle devre dışı sürece hello varsayılan tooenable hello ilgili arama özelliği olacaktır.

Bizim örneğimizde, dizinimizi "oteller" olarak adlandırdık ve alanlarımızı aşağıdaki şekilde tanımladık:

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

Biz hello dizin öznitelikleri nasıl biz bir uygulamada kullanılacak düşünerek her bir alan için dikkatle seçtiniz. Örneğin, `hotelId` Oteller büyük olasılıkla bilmediği Biz bu alan için tam metin aramasını ayarlayarak devre dışı bırakmak için arama yapan kişilerin benzersiz bir anahtardır `searchable` çok`false`, hello dizinde alanı kaydeder.

Lütfen türündeki dizininizde yalnızca bir alanın Not `Edm.String` hello hello 'key' alan olarak işaretlenmesi gerekir.

Yukarıdaki dizin tanımı Hello hello için bir dil Çözümleyicisi kullanır `description_fr` hedeflenen toostore Fransızca metin olduğundan alan. Bkz: [hello dil desteği konu](https://docs.microsoft.com/rest/api/searchservice/Language-support) hello karşılık gelen yanı sıra [blog gönderisi](https://azure.microsoft.com/blog/language-support-in-azure-search/) dil Çözümleyicileri hakkında daha fazla bilgi.

## <a name="issue-hello-http-request"></a>Sorunu hello HTTP isteği
1. Dizin tanımınızı hello istek gövdesi olarak kullanarak, bir HTTP POST isteği tooyour Azure Search Hizmeti uç noktası URL'si gönderin. Hello URL'de hizmet adınızı hello ana bilgisayar adı olarak emin toouse olması ve hello uygun put `api-version` bir sorgu dizesi parametresi olarak (Merhaba geçerli API sürümü `2016-09-01` bu belgenin yayımlandığı hello zaman).
2. Merhaba istek üst bilgilerinde hello belirtin `Content-Type` olarak `application/json`. Tooprovide hello adımda tanımlanan hizmetinizin yönetici anahtarını gerekir `api-key` üstbilgi.

Kendi hizmet adınızı ve API anahtar tooissue hello isteği aşağıda tooprovide olacaktır:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


Başarılı bir istek için 201 durum kodunu (Oluşturuldu) görmeniz gerekir. Merhaba REST API aracılığıyla dizin oluşturma hakkında daha fazla bilgi için lütfen başlangıç adresini ziyaret edin [API başvurusunu Buraya](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Hata durumunda döndürülebilen diğer HTTP durum kodları hakkında daha fazla bilgi için bkz. [HTTP durum kodları (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

Bir dizin ve istediğiniz toodelete ile bu bittiğinde, yalnızca HTTP DELETE isteği gönderin. Örneğin, bu nasıl biz hello "hotels" dizinini silmek.

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Sonraki adımlar
Azure Search dizini oluşturduktan sonra çok hazır olacak[içeriğinizi hello dizine yüklemek](search-what-is-data-import.md) şekilde, verilerinizi aramaya başlayabilirsiniz.
