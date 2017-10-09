---
title: "aaa \"(.NET API - Azure Search) dizin oluşturma | Microsoft Docs\""
description: "Hello Azure Search .NET SDK'sını kullanarak kod içinde bir dizin oluşturun."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7fa4030b8c3565bc02b1d6bb4426331657cf3a5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-net-sdk"></a>Merhaba .NET SDK kullanarak Azure Search dizini oluşturma
> [!div class="op_single_selector"]
> * [Genel Bakış](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

Bu makale bir Azure Search oluşturma hello işleminde size kılavuzluk edecektir [dizin](https://docs.microsoft.com/rest/api/searchservice/Create-Index) hello kullanarak [Azure Search .NET SDK'sı](https://aka.ms/search-sdk).

Bu kılavuzu izlemeden ve dizin oluşturmadan önce, [Azure Search hizmeti oluşturmuş](search-create-service-portal.md) olmanız gerekir.

> [!NOTE]
> Bu makaledeki örnek kodun tamamı C# dilinde yazılmıştır. Merhaba tam kaynak kodu bulabilirsiniz [github'da](http://aka.ms/search-dotnet-howto). Merhaba hakkında bilgi edinebilirsiniz [Azure Search .NET SDK'sı](search-howto-dotnet-sdk.md) daha ayrıntılı ilerlemesi hello örnek kod için.


## <a name="identify-your-azure-search-services-admin-api-key"></a>Azure Search hizmet yöneticinizin api anahtarını tanımlama
Azure Search Hizmeti sağlamış olduğunuza göre neredeyse hazır tooissue hello .NET SDK kullanarak hizmet uç karşı isteklerdir. Öncelikle, sağladığınız hello arama hizmeti için tooobtain hello yönetici API oluşturulmasının anahtarlarından biri gerekir. Merhaba .NET SDK'sı her isteği tooyour hizmette bu api anahtarını gönderir. Geçerli bir anahtar sahip istek başına temelinde, hello isteği gönderiliyor hello uygulama ve bunu işleyen hello hizmeti arasında güven oluşturur.

1. toofind hizmetinizin api anahtarlarından, oturum içinde toohello [Azure portalı](https://portal.azure.com/)
2. Tooyour Azure Search hizmet dikey penceresine gidin
3. Merhaba üzerinde "Anahtarlar" simgesine tıklayın

Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.

* Birincil ve ikincil *yönetici anahtarları* tooall operations hello özelliği toomanage hello hizmeti dahil olmak üzere, tam haklar, oluşturun ve dizinler, dizin oluşturucular ve veri kaynaklarını silin. Tooregenerate hello birincil anahtar ve tam tersini karar verirseniz toouse hello ikincil anahtar devam edebilmesi için bu iki anahtar vardır.
* *Sorgu anahtarları* salt okunur erişim tooindexes ve belgeleri verin ve arama istekleri gönderen genellikle dağıtılmış tooclient uygulamalardır.

Merhaba amacıyla dizin oluşturma ya da kullanabilirsiniz, birincil veya ikincil yönetici anahtarınızı.

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-hello-searchserviceclient-class"></a>Merhaba SearchServiceClient sınıfının bir örneğini oluşturun
toostart kullanarak Azure Search .NET SDK'sı Merhaba, toocreate hello örneği gerekir `SearchServiceClient` sınıfı. Bu sınıfın birkaç oluşturucusu vardır. Merhaba istediğiniz bir arama hizmeti adınızı alır ve bir `SearchCredentials` nesnesini parametre olarak. `SearchCredentials`, api anahtarınızı sarmalar.

Aşağıdaki Hello kodu oluşturur Yeni bir `SearchServiceClient` hello arama hizmeti adı ve hello uygulamanın yapılandırma dosyasında depolanan api anahtarı için değerleri kullanarak (`appsettings.json` hello hello durumda [örnek uygulama](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

`SearchServiceClient`, `Indexes` özelliğine sahiptir. Bu özellik gerekir toocreate, listesi, güncelleştirme ya da Azure Search dizinlerini silmek tüm hello yöntemleri sağlar.

> [!NOTE]
> Merhaba `SearchServiceClient` sınıfı bağlantıları tooyour arama hizmeti yönetir. Çok fazla bağlantı açmayı sipariş tooavoid içinde tek bir örneğini tooshare denemelisiniz `SearchServiceClient` mümkünse uygulamanızda. Yöntemlerinin iş parçacığı tooenable tür paylaşımları olan.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a>Azure Search dizininizi tanımlama
Tek çağrı toohello `Indexes.Create` yöntemi dizininizi oluşturur. Bu yöntem, Azure Search dizininizi tanımlayan bir `Index` nesnesini parametre olarak alır. Toocreate gereken bir `Index` nesne ve şu şekilde başlatın:

1. Set hello `Name` hello özelliğinin `Index` dizininizi nesne toohello adı.
2. Set hello `Fields` hello özelliğinin `Index` nesne tooan dizisi `Field` nesneleri. Merhaba en kolay yolu toocreate hello `Field` nesnedir tarafından arama hello `FieldBuilder.BuildForType` hello tür parametresi için bir model sınıfı geçirme yöntemi. Bir model sınıfı dizininizi toohello alanlarını eşleme özellikleri vardır. Bu, arama dizini tooinstances modeli sınıfınızın toobind belgelerden sağlar.

> [!NOTE]
> Bir model sınıfı toouse planlamıyorsanız, hala dizininizi oluşturarak tanımlayabilirsiniz `Field` nesnelerini doğrudan. Merhaba veri türü (veya dize alanları Çözümleyicisi) ile birlikte hello alan toohello Oluşturucusu hello adını sağlayabilirsiniz. `IsSearchable`, `IsFilterable` vb. gibi başka özellikler de ayarlayabilirsiniz.
>
>

Bu, arama kullanıcı deneyiminizi ve iş gereksinimlerinizi göz önünde her bir alan hello atanması gerektiğinden, dizininizi tasarlarken tutmanız önemlidir [uygun özellikler](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Toowhich alanlar geçerli hangi arama özelliklerinin (filtreleme, modelleme tam metin araması sıralama vb. olduğunu) bu özellikleri denetler. Siz açıkça ayarlamadığınız her özellik için hello `Field` sınıfı varsayılan olarak toodisabling hello karşılık gelen arama özelliğini özellikle etkinleştirmediğiniz sürece.

Bizim örneğimizde, dizinimizi "oteller" olarak adlandırdık ve alanlarımızı model sınıfı kullanarak tanımladık. Merhaba modeli sınıfının her bir özellik hello arama ile ilgili davranışları hello karşılık gelen dizini alanı belirleyen özniteliklere sahiptir. Merhaba model sınıfı şu şekilde tanımlanır:

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

Biz hello öznitelikleri nasıl biz bir uygulamada kullanılacak düşünerek her bir özellik için dikkatle seçtiniz. Örneğin, Oteller için arama yapan kişiler hello anahtar sözcük eşleşmeleri ile ilgi olacağını büyük olasılıkla `description` alan hello ekleyerek bu alan için tam metin aramasını etkinleştiririz şekilde `IsSearchable` toohello özniteliği `Description` özelliği.

Türündeki dizininizde yalnızca bir alanın lütfen unutmayın `string` hello hello işaretlenmesi gerekir *anahtar* hello ekleyerek alan `Key` özniteliği (bkz `HotelId` örnek yukarıda hello içinde).

Yukarıdaki dizin tanımı Hello hello için bir dil Çözümleyicisi kullanır `description_fr` hedeflenen toostore Fransızca metin olduğundan alan. Bkz: [hello dil desteği konu](https://docs.microsoft.com/rest/api/searchservice/Language-support) hello karşılık gelen yanı sıra [blog gönderisi](https://azure.microsoft.com/blog/language-support-in-azure-search/) dil Çözümleyicileri hakkında daha fazla bilgi.

> [!NOTE]
> Varsayılan olarak, her özelliğin model sınıfınızda hello adı hello karşılık gelen alanın hello dizindeki hello adı olarak kullanılır. Tüm özellik adları toocamel durumda alan adları toomap istiyorsanız hello hello sınıfıyla işaretlemek `SerializePropertyNamesAsCamelCase` özniteliği. Toomap tooa farklı bir ad isterseniz hello kullanabilirsiniz `JsonProperty` özniteliği hello gibi `DescriptionFr` yukarıdaki özelliği. Merhaba `JsonProperty` özniteliği hello göre önceliklidir `SerializePropertyNamesAsCamelCase` özniteliği.
> 
> 

Bir model sınıfı tanımladık, şimdi bir dizin tanımını kolayca oluşturabilirsiniz:

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-hello-index"></a>Merhaba dizini oluşturma
Başlatılan bir sahip olduğunuza `Index` nesne çağrısı yaparak hello dizin oluşturabilirsiniz `Indexes.Create` üzerinde `SearchServiceClient` nesnesi:

```csharp
serviceClient.Indexes.Create(definition);
```

Başarılı bir istek için hello yöntemi normal olarak döndürür. Geçersiz bir parametre gibi hello isteği ile ilgili bir sorun varsa, hello yöntemi özel durum oluşturacak `CloudException`.

Bir dizin ve istediğiniz toodelete ile bu bittiğinde, yalnızca hello çağrısı `Indexes.Delete` yöntemi, `SearchServiceClient`. Örneğin, bu nasıl biz hello "hotels" dizinini silmek.

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> Bu makaledeki örnek kod Hello hello Azure Search .NET SDK'sı zaman uyumlu yöntemleri hello kolaylık sağlamak için kullanır. Kendi uygulamaları tookeep hello zaman uyumsuz yöntemleri kullanmanızı öneririz bunları ölçeklenebilir ve esnek. Örneğin, yukarıdaki örnek hello kullanabilirsiniz `CreateAsync` ve `DeleteAsync` yerine `Create` ve `Delete`.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Azure Search dizini oluşturduktan sonra çok hazır olacak[içeriğinizi hello dizine yüklemek](search-what-is-data-import.md) şekilde, verilerinizi aramaya başlayabilirsiniz.

