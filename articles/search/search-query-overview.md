---
title: Azure arama aaaQuery dizin | Microsoft Docs
description: "Azure Search'te bir arama sorgusu oluşturun ve arama parametrelerini toofilter ve sıralama arama sonuçlarını kullanın."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>Azure Search dizininizi sorgulama
> [!div class="op_single_selector"]
> * [Genel Bakış](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Arama istekleri tooAzure arama gönderirken, uygulamanızın arama kutusuna hello yazılan hello gerçek sözcüklerin yanı sıra belirtilen parametre sayısı vardır. Bu sorgu parametreleri tooachieve izin hello biraz daha derin denetim [tam metin arama deneyimi](search-lucene-query-architecture.md).

Azure Search hello Sorgu parametrelerinin ortak kullanımlarını kısaca açıklayan bir listesi aşağıda verilmiştir. Sorgu parametrelerinin ve bunların davranışlarının'ün tam kapsamını için lütfen bkz. hello sayfaları hello için ayrıntılı [REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) ve [.NET SDK'sı](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary).

## <a name="types-of-queries"></a>Sorgu türleri
Azure arama birçok seçenekleri toocreate son derece güçlü sorgular sunar. Merhaba iki ana sorgu türleri `search` ve `filter`. A `search` sorgu bir veya daha çok terimi arar tüm *aranabilir* dizininizdeki alanları ve Google veya Bing toowork gibi bir arama motoru beklediğiniz hello şekilde çalışır. `filter` sorgusu, bir dizindeki tüm *filtrelenebilir* alanlarda bir boole ifadesini değerlendirir. Farklı `search` sorguları, `filter` sorguları eşleşen dize alanları için büyük küçük harfe duyarlı oldukları anlamına gelir bir alanın tam içeriğini hello.

Aramaları ve filtreleri birlikte veya ayrı olarak kullanabilirsiniz. Bunları birlikte kullandığınızda hello filtredir ilk toohello tüm dizin uygulanır ve ardından hello filtre hello sonuçlarını hello araması gerçekleştirilir. Arama sorgusu gereksinimlerini tooprocess hello belgeleri hello kümesini azalttığından filtreler bu nedenle yararlı yöntem tooimprove sorgu performansı olabilir.

Hello için filtre ifadeleri söz dizimi hello kümesini [OData filtre dilinin](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search). Arama sorguları için her iki hello kullanabilirsiniz [Basitleştirilmiş söz dizimini](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) veya hello [Lucene sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) aşağıda ele alınmıştır.

### <a name="simple-query-syntax"></a>Basit sorgu söz dizimi
Merhaba [Basit Sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) hello Azure Search'te kullanılan varsayılan sorgu dildir. Merhaba Basit Sorgu söz dizimi hello AND, OR, değil, tümcecik, sonek ve öncelik işleçleri dahil olmak üzere ortak arama işleçlerini destekler.

### <a name="lucene-query-syntax"></a>Lucene sorgu söz dizimi
Merhaba [Lucene sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) toouse hello yaygın şekilde benimsenmiş ve açıklayıcı sorgu dili parçası olarak geliştirilen verir [Apache Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html).

Bu sorgu sözdizimini kullanarak, sağlar, tooeasily elde özellikleri aşağıdaki hello: [alan kapsamlı sorgular](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields), [benzer arama](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy), [yakınlık araması](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity), [ Terim](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost), [normal ifade araması](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex), [joker karakterle arama](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard), [sözdizimi Temelleri](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax), ve [kullanan sorgular Boole işleçleri](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean).

## <a name="ordering-results"></a>Sonuçları sıralama
Bir arama sorgusunun sonuçları alınırken, Azure Search hello sonuçları belirli bir alandaki değerlere göre sıralayarak sunmasını isteyebilirsiniz. Varsayılan olarak, Azure Search türetildiği her bir belgenin arama puanı hello derecesini temel hello arama sonuçlarını sıralar [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).

Azure Search tooreturn sonuçlarınızı hello arama puanı dışında bir değere göre sıralayarak istiyorsanız hello kullanabilirsiniz `orderby` arama parametresi. Merhaba hello değerini belirtebilirsiniz `orderby` parametresi tooinclude alan adları ve toohello çağırır [ `geo.distance()` işlevi](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search) Jeo-uzamsal değerler. Her deyim tarafından izlenebilir `asc` tooindicate sonuçları artan sırada istenir ve `desc` tooindicate sonuçları azalan sırada istenir. artan hello varsayılandır.

## <a name="paging"></a>Sayfalama
Azure arama yapar, kolay tooimplement arama sonuçlarını disk belleği. Hello kullanarak `top` ve `skip` parametreleri tooreceive hello toplam arama sonuçları kümesini, iyi arama kullanıcı Arabirimi uygulamalarını kolayca etkinleştiren yönetilebilir ve sıralı alt kümeler halinde izin arama isteklerini sorunsuz verebilir. Sonuç daha küçük bu alt kümelerini alırken hello toplam arama sonuçları kümesindeki belge sayısını hello de alabilir.

Merhaba makalesi arama sonuçlarında disk belleği hakkında daha fazla bilgiyi [nasıl Azure Search'te toopage arama sonuçları](search-pagination-page-layout.md).

## <a name="hit-highlighting"></a>İsabet vurgulama
Azure Search'te hello tam hello arama sorgusuyla eşleşen arama sonuçları kısmı vurgulayan hello kullanarak kolaylaştırılmıştır `highlight`, `highlightPreTag`, ve `highlightPostTag` parametreleri. Belirtebilirsiniz *aranabilir* alanları hello dize tooappend toohello başlangıç etiketleri ve hello sonuna Azure arama metni eşleşen tam döndürür vurgulanacağının yanı sıra eşleşen metninin sahip olmalıdır.

## <a name="try-out-query-syntax"></a>Sorgu söz dizimini deneme

Merhaba en iyi şekilde toounderstand söz dizimi farkları olan sorguları gönderme ve sonuçları gözden geçirme.

+ Kullanım [arama Gezgini](search-explorer.md) hello Azure Portalı'nda. Dağıtarak [hello örnek dizin](search-get-started-portal.md), hello Portalı'nda araçlarını kullanarak dakika cinsinden başlangıç dizini sorgulama yapabilirsiniz.

+ Kullanım [Fiddler](search-fiddler.md) veya tooyour arama hizmeti yüklediğiniz Chrome Postman toosubmit sorguları tooan dizini. Her iki araçları REST çağrılarını tooan HTTP uç noktasını destekler. 
