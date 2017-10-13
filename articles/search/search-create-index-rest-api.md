---
title: "Dizin oluşturma (REST API - Azure Search) | Microsoft Docs"
description: "Azure Search HTTP REST API'sini kullanarak kod içinde bir dizin oluşturun."
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
ms.openlocfilehash: 9a64d1436471e406b7d9b700257d3dd96b5edcde
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="create-an-azure-search-index-using-the-rest-api"></a>REST API'yi kullanarak Azure Search dizini oluşturma
> [!div class="op_single_selector"]
>
> * [Genel Bakış](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

Bu makale, Azure Search REST API'sini kullanarak Azure Search [dizini](https://docs.microsoft.com/rest/api/searchservice/Create-Index) oluşturma işlemi konusunda size yol gösterecektir.

Bu kılavuzu izlemeden ve dizin oluşturmadan önce, [Azure Search hizmeti oluşturmuş](search-create-service-portal.md) olmanız gerekir.

REST API'yi kullanan bir Azure Search dizini oluşturmak için, Azure Search hizmetinizin URL uç noktasına tek bir HTTP POST isteği göndereceksiniz. Dizin tanımınız, doğru biçimlendirilmiş JSON içeriği olarak istek gövdesinde yer alır.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Azure Search hizmet yöneticinizin api anahtarını tanımlama
Şimdi bir Azure Search hizmeti sağlamış olduğunuza göre, .REST API'yi kullanarak hizmetinizin URL uç noktasına HTTP istekleri gönderebilirsiniz. *Tüm* API isteklerinin sağladığınız Search hizmeti için oluşturulan API anahtarını içermesi gerekir. İstek başına geçerli bir anahtara sahip olmak, isteği gönderen uygulama ve bunu işleyen hizmet arasında güven oluşturur.

1. Hizmetinizin api anahtarlarını bulmak için [Azure portalında](https://portal.azure.com/) oturum açmanız gerekir.
2. Azure Search hizmetinizin dikey penceresine gidin
3. "Anahtarlar" simgesine tıklayın

Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.

* Birincil ve ikincil *yönetici anahtarlarınız*; hizmeti yönetme, dizinler, dizin oluşturucular ve veri kaynakları ekleme ve silme de dahil olmak üzere her türlü işlem için tüm hakları verir. Birincil anahtarı yeniden oluşturmaya karar verirseniz ikincil anahtarı kullanmaya devam edebilmeniz ve tam tersini yapabilmeniz için iki anahtar vardır.
* *Sorgu anahtarları*, dizinler ve belgeler için salt okunur erişim verir ve genellikle, arama istekleri gönderen istemci uygulamalarına dağıtılır.

Dizin oluşturma amacıyla, birincil ya da ikincil yönetici anahtarınızı kullanabilirsiniz.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Doğru biçimlendirilmiş JSON kullanarak Azure Search dizininizi tanımlama
Hizmetinize yönelik tek bir HTTP POST isteği dizininizi oluşturur. HTTP POST isteğinizin gövdesi, Azure Search dizininizi tanımlayan tek bir JSON nesnesi içerir.

1. Bu JSON nesnesinin ilk özelliği dizininizin adıdır.
2. Bu JSON nesnesinin ikinci özelliği, dizininizdeki her bir alan için ayrı bir JSON nesnesi içeren `fields` adlı bir JSON dizisidir. Bu JSON nesnelerinin her biri, her bir alan özniteliği için "ad", "tür" vb. de dahil olmak üzere birden çok ad/değer çifti içerir.

Her bir alan için [uygun öznitelikler](https://docs.microsoft.com/rest/api/searchservice/Create-Index) atanması gerektiğinden, dizininizi tasarlarken arama kullanıcı deneyiminizi ve iş gereksinimlerinizi göz önünde bulundurmanız önemlidir. Bu öznitelikler, hangi alanlar için hangi arama özelliklerinin (filtreleme, modelleme, tam metin araması sıralama vb.) geçerli olduğunu denetler. Belirtmediğiniz her öznitelik için ilgili arama özelliği, özellikle devre dışı bırakmadığınız sürece varsayılan olarak etkinleştirilir.

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

Her bir alan için dizin özniteliklerini, bunların bir uygulamada nasıl kullanılacağını düşünerek dikkatle seçtik. Örneğin; `hotelId`, oteller için arama yapan kişilerin büyük olasılıkla bilmediği benzersiz bir anahtardır. Bu nedenle, `searchable` değerini `false` olarak ayarlayarak bu alan için tam metin aramasını devre dışı bırakırız. Bu, dizinde yer kazandırır.

Lütfen `Edm.String` türündeki dizininizde yalnızca bir alanın "anahtar" alanı olarak belirlenmesi gerektiğini unutmayın 

Yukarıdaki dizin tanımı Fransızca metin depolamaya yönelik tasarlandığından, `description_fr` alanı için bir dil çözümleyicisi kullanır. Dil çözümleyicileri hakkında daha fazla bilgi için ilgili [blog yazısının](https://azure.microsoft.com/blog/language-support-in-azure-search/) yanı sıra [Dil desteği konu başlığına](https://docs.microsoft.com/rest/api/searchservice/Language-support) bakın.

## <a name="issue-the-http-request"></a>HTTP isteği gönderme
1. Dizin tanımınızı istek gövdesi olarak kullanarak Azure Search hizmeti uç nokta URL'nize HTTP POST isteği gönderin. URL'de hizmet adınızı ana bilgisayar adı olarak kullandığınızdan emin olun ve sorgu dizesi parametresi olarak uygun `api-version` öğesini kullanın (Bu belge yayımlandığı sırada, `2016-09-01` geçerli API sürümüdür).
2. İstek üst bilgilerinde, `Content-Type` öğesini `application/json` olarak belirtin. Ayrıca `api-key` üst bilgisinde, 1. Adımda tanımladığınız hizmet yöneticisi anahtarınızı sağlamanız gerekir.

Aşağıdaki isteği göndermek için kendi hizmet adınızı ve API anahtarınızı sağlamanız gerekir:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


Başarılı bir istek için 201 durum kodunu (Oluşturuldu) görmeniz gerekir. REST API aracılığıyla dizin oluşturma hakkında daha fazla bilgi için lütfen [buradaki API başvurusuna](https://docs.microsoft.com/rest/api/searchservice/Create-Index) bakın. Hata durumunda döndürülebilen diğer HTTP durum kodları hakkında daha fazla bilgi için bkz. [HTTP durum kodları (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

Dizin ile işiniz bittiğinde ve bunu silmek istediğinizde HTTP DELETE isteği gönderin. Örneğin, "oteller" dizinini aşağıdaki şekilde sileriz:

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Sonraki adımlar
Azure Search dizini oluşturduktan sonra, [içeriğinizi dizine yüklemek](search-what-is-data-import.md) için hazır olursunuz. Böylece, verilerinizi aramaya başlayabilirsiniz.
