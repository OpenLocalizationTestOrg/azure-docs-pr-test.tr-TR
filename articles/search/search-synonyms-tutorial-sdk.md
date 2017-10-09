---
title: "aaaSynonyms Önizleme Azure Search'te Öğreticisi | Microsoft Docs"
description: "Azure Search'te Hello eş anlamlıları önizleme özelliği tooan dizin ekleyin."
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a>Azure Search için eş anlamlı (önizleme) C# öğreticisi

Eş anlamlıları anlam olarak eşdeğer toohello giriş terim kabul koşullarınızda eşleştirerek bir sorgu genişletin. Örneğin, "araba" toomatch belgeleri hello koşulları "otomobil" veya "araç" içeren isteyebilirsiniz.

Azure Search’te, eş anlamlılar eşdeğer terimleri ilişkilendiren *eşleme kuralları* aracılığıyla bir *eş anlamlı eşleminde* tanımlanır. Birden çok eş eşlemesi oluşturmak, bir hizmet geneli kaynak kullanılabilir tooany dizini gönderme ve hello alan düzeyinde bir hangi toouse başvuru. Merhaba sorguda kullanılan alanları belirtilmişse, sorgu zamanında toosearching dizin, Azure Search ayrıca eş eşlemesindeki bir arama yapar.

> [!NOTE]
> Merhaba anlamlıları özelliği şu anda, Önizleme ve desteklenen yalnızca en son Önizleme API ve SDK sürümleri hello (API sürümü 2016-09-01-Önizleme, SDK sürüm 4.x-Önizleme =). Şu anda Azure portalı desteği yoktur. Önizleme API’leri SLA kapsamında değildir ve önizleme özellikleri değişebilir; bu nedenle, üretim uygulamalarında kullanılması önerilmez.

## <a name="prerequisites"></a>Ön koşullar

Eğitmen gereksinimleri hello şunları içerir:

* [Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure Search hizmeti](search-create-service-portal.md)
* [Microsoft.Azure.Search .NET kitaplığının önizleme sürümü](https://aka.ms/search-sdk-preview)
* [Bir .NET uygulamasından Azure toouse arama nasıl](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a>Genel Bakış

Önce ve sonra sorguları eş anlamlıları hello değerini gösterir. Bu öğreticide, sorguları yürüten ve sonuçları bir örnek dizinde döndüren örnek bir uygulama kullanılır. Merhaba örnek uygulaması "iki belgelerle doldurulmuş hotels" adlı küçük bir dizin oluşturur. Merhaba uygulaması hüküm ve hello dizinde görünmez tümcecikleri kullanarak arama sorguları çalıştırır, sorunları aynı aramaları yeniden hello sonra hello eş anlamlıları özelliği sağlar. Aşağıdaki Hello kodu gösterir hello genel akış.

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
Merhaba adımları toocreate ve hello örnek dizinini doldurmak açıklanacak [toouse Azure arama nasıl bir .NET uygulamasından](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

## <a name="before-queries"></a>"Öncesi" sorguları

`RunQueriesWithNonExistentTermsInIndex` içinde "beş yıldızlı", "internet" ve "ekonomik VE otel" ile arama sorguları gönderdik.
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
Böylece biz hello ilk çıkış hello aşağıdaki elde hello iki dizinlenmiş belgeleri hiçbiri hello terimleri içeren `RunQueriesWithNonExistentTermsInIndex`.
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a>Eş anlamlıları etkinleştirme

Eş anlamlıların etkinleştirilmesi iki adımlı bir işlemdir. Biz öncelikle tanımlamanız ve eş kuralları karşıya yükleme ve alanları toouse yapılandırmak bunları. Merhaba işlem özetlenen içinde `UploadSynonyms` ve `EnableSynonymsInHotelsIndex`.

1. Bir eş anlamlı harita tooyour arama hizmeti ekleyin. İçinde `UploadSynonyms`, bizim eş eşlemesinde 'desc-synonymmap' dört kurallar tanımlamak ve toohello hizmet karşıya yükleyin.
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
Bir eş anlamlı harita toohello açık kaynak standart uymalıdır `solr` biçimi. Merhaba biçimi içinde açıklanan [Azure Search eş anlamlı](search-synonyms.md) hello bölümünde `Apache Solr synonym format`.

2. Aranabilir alanlara toouse hello eş harita hello dizin tanımında yapılandırın. İçinde `EnableSynonymsInHotelsIndex`, iki alanlar anlamlıları etkinleştirme `category` ve `tags` hello ayarı tarafından `synonymMaps` özellik toohello hello adını yeni karşıya eş eşleme.
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
Bir eş anlamlı eşlemi eklediğinizde, dizinin yeniden oluşturulması gerekmez. Bir eş anlamlı harita tooyour hizmet eklemek ve varolan alan tanımları eşlemindeki tüm dizin toouse hello yeni eş düzeltmek. Yeni öznitelikler Hello eklenmesi dizin kullanılabilirliğine hiçbir etkisi olmaz. Merhaba aynı devre dışı bırakılırken bir alan için eş anlamlı sözcükleri uygular. Merhaba yalnızca ayarlayabileceğiniz `synonymMaps` özelliği tooan boş bir liste.
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a>"Sonrası" sorguları

Merhaba eş harita yüklendiği ve hello dizin güncelleştirilmiş toouse hello eş harita sonra ikinci hello `RunQueriesWithNonExistentTermsInIndex` çağrısı hello aşağıdaki çıkarır:

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
Merhaba ilk sorgu bulur hello hello kural belgeden `five star=>luxury`. Merhaba ikinci sorguyu genişletir hello arama'yı kullanarak `internet,wifi` ve üçüncü her ikisini de kullanarak hello `hotel, motel` ve `economy,inexpensive=>budget` hello belgeleri bulma bunlar eşleşti.

Eş anlamlıları tamamen ekleme hello arama deneyimi değiştirir. Bu öğreticide, dizinimizi Hello belgelerde ilgili olsa bile hello özgün sorguları tooreturn anlamlı sonuçlar başarısız oldu. Eş anlamlıları etkinleştirerek, genelde, hello dizindeki değişiklikleri toounderlying veri içermeyen kullanım koşullarına bir dizin tooinclude genişletebilirsiniz.

## <a name="sample-application-source-code"></a>Örnek uygulama kaynak kodu
Merhaba örnek uygulaması bu ilerlemesi üzerinde kullanılan hello tam kaynak kodunu bulabilirsiniz [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).

## <a name="next-steps"></a>Sonraki adımlar

* Gözden geçirme [nasıl Azure Search toouse eş anlamlı](search-synonyms.md)
* [Eş anlamlılar REST API belgelerini](https://aka.ms/rgm6rq) gözden geçirin
* Hello için Hello başvuruları Gözat [.NET SDK'sı](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) ve [REST API](https://docs.microsoft.com/rest/api/searchservice/).
