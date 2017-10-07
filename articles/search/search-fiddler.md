---
title: aaaHow toouse Fiddler tooevaluate ve Azure Search REST API'lerini test | Microsoft Docs
description: "Bir yaklaşım Kodsuz tooverifying Azure Search hizmetinin kullanılabilirliğini ve REST API'leri hello çalışırken için fiddler'ı kullanın."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a>Fiddler tooevaluate kullanın ve Azure Search REST API'lerini test etme
> [!div class="op_single_selector"]
>
> * [Genel Bakış](search-query-overview.md)
> * [Arama Gezgini](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Bu makalede açıklanır nasıl toouse Fiddler'ın, bir [telerik'ten ücretsiz indirme](http://www.telerik.com/fiddler), herhangi bir kod toowrite gerek kalmadan hello Azure Search REST API'sini kullanarak tooissue HTTP isteklerini tooand yanıtları görüntüle. Azure Search; Microsoft Azure'da barındırılan, .NET ve REST API'ler aracılığıyla kolayca programlanabilen ve tamamen yönetilen bir bulut arama hizmetidir. Hello Azure Search Hizmeti REST API'leri açıklanmaktadır [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).

Aşağıdaki adımları hello dizin oluşturma, belgeleri, sorgu hello dizini ve ardından hizmet bilgisi için sorgu hello sistemi yükleyin.

Aşağıdaki adımları toocomplete, Azure Search hizmeti gerekir ve `api-key`. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) tooget nasıl başlatılacağını hakkında yönergeler için.

## <a name="create-an-index"></a>Dizin oluşturma
1. Fiddler'ı başlatın. Merhaba üzerinde **dosya** menüsünde kapatmak **trafiği Yakala** ilgisiz toohello geçerli görev toohide yabancı HTTP etkinliğini.
2. Merhaba üzerinde **Oluşturucu** sekmesinde, aşağıdaki ekran görüntüsü hello gibi görünen bir istek formüle.

      ![][1]
3. **PUT**'u seçin.
4. Hello hizmet URL'si, istek özniteliklerini ve hello api sürümü belirten bir URL girin. Birkaç işaretçileri tookeep unutmayın:

   * HTTPS hello önek olarak kullanın.
   * İstek özniteliği "indexes/hotels"dir. Bu, "Oteller" adlı bir dizin arama toocreate bildirir.
   * API sürümü küçük harfle yazılır, "?api-version=2016-09-01" olarak belirtilir. Azure Search düzenli olarak güncelleştirme dağıttığından, API sürümleri önemlidir. Nadir durumlarda, bir hizmet güncelleştirmesi sonu değişiklik toohello API çıkarabilir. Bu nedenle Azure Search, her bir istek için api sürümünü gerekli kılar. Böylece, hangisinin kullanıldığına ilişkin tam denetiminiz olur.

     Merhaba tam URL aşağıdaki örneğine benzer toohello görünmelidir.

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. Merhaba konak ve api anahtarını hizmetiniz için geçerli olan değerleri değiştirerek hello istek üstbilgisi belirtin.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. İstek gövdesinde hello dizin tanımını oluşturan hello alanları yapıştırın.

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. **Yürüt**’e tıklayın.

Birkaç saniye içinde HTTP 201 yanıtını hello oturum listesinde görmeniz gerekir, belirten hello Dizin başarıyla oluşturuldu.

HTTP 504 yanıtı alırsanız HTTPS'yi belirten hello URL'yi doğrulayın. HTTP 400 veya 404 yanıtı görürseniz, onay hello istek gövdesi tooverify var. hatalar hiçbir kopyalayıp yapıştırın. HTTP 403 genelde hello api anahtarını (Geçersiz anahtar veya hello api anahtarını nasıl belirtilen bir söz dizimi sorunu) bir sorun olduğunu gösterir.

## <a name="load-documents"></a>Belge yükleme
Merhaba üzerinde **Oluşturucu** sekmesi, istek toopost belgelerinizi hello aşağıdaki gibi görünür. Merhaba hello istek gövdesi 4 otel için arama verilerini hello içerir.

   ![][2]

1. **POST**'u seçin.
2. HTTPS ile başlayan, sırasıyla hizmet URL'niz ve "/indexes/<'indexname'>/docs/index?api-version=2016-09-01" ile devam eden bir URL girin. Merhaba tam URL aşağıdaki örneğine benzer toohello görünmelidir.

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. İstek üstbilgisi olması hello aynı önceki gibi. Hizmetiniz için geçerli değerlerle hello konak ve api anahtarını yerini unutmayın.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Merhaba iste gövde dört belgeleri toobe eklenen toohello hotels dizini içerir.

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
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
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. **Yürüt**’e tıklayın.

Birkaç saniye içinde bir hello oturum listesinde HTTP 200 yanıtı görmeniz gerekir. Bu, belgelerin başarıyla oluşturulduğunu hello gösterir. 207 yanıtı alırsanız en az bir belge tooupload başarısız oldu. 404 yanıtı alırsanız, hello üstbilgi veya hello istek gövdesi bir sözdizimi hatası var.

## <a name="query-hello-index"></a>Sorgu hello dizini
Şimdi dizin ve belgeler karşıya yüklendiğine göre, bunlara sorgu gönderebilirsiniz.  Merhaba üzerinde **Oluşturucu** sekmesinde bir **almak** hizmetinizi sorgulayan komutu aşağıdaki ekran görüntüsü benzer toohello görünür.

   ![][3]

1. **GET**'i seçin.
2. HTTPS ile başlayan, sırasıyla hizmet URL'niz, "/indexes/<'indexname'>/docs?" ve sorgu parametreleri ile devam eden bir URL girin. Örnek olarak, URL aşağıdaki, hizmetiniz için geçerli olan bir hello örnek ana bilgisayar adı yerine hello kullanın.

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   Bu sorgu "motel" Merhaba terimini arar ve derecelendirmeler için model kategorileri alır.
3. İstek üstbilgisi olması hello aynı önceki gibi. Hizmetiniz için geçerli değerlerle hello konak ve api anahtarını yerini unutmayın.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

Merhaba yanıt kodu 200 olmalıdır ve hello yanıt çıkışı aşağıdaki ekran görüntüsü benzer toohello görünmelidir.

   ![][4]

Merhaba aşağıdaki örnek sorgu olan hello [Search dizin işlemi (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) konusuna bakın. Bu konudaki hello örnek sorguları çoğunu Fiddler'da izin verilmeyen boşluklar içerir. Her alanı ile + karakteri hello yapıştırarak sorgu önce dize hello fiddler'da sorguyu denemeden önce değiştirin.

**Boşluklar değiştirilmeden önce:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**Boşluklar + ile değiştirildikten sonra:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a>Sorgu hello sistemi
Sayıları ve depolama hello sistem tooget belge kullanımı da sorgulayabilirsiniz. Merhaba üzerinde **Oluşturucu** sekmesinde isteğiniz benzer toohello aşağıdaki görünür ve hello yanıt Merhaba, belge sayısı ve kullanılan alan için bir sayı döndürür.

 ![][5]

1. **GET**'i seçin.
2. Hizmet URL'nizi içeren ve ardından "/indexes/hotels/stats?api-version=2016-09-01" ile devam eden bir URL girin:

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. Merhaba konak ve api anahtarını hizmetiniz için geçerli olan değerleri değiştirerek hello istek üstbilgisi belirtin.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Merhaba istek gövdesini boş bırakın.
5. **Yürüt**’e tıklayın. Bir HTTP 200 durum kodu hello oturum listesinde görmeniz gerekir. Komutunuz için gönderilen hello girişi seçin.
6. Merhaba tıklatın **denetçiler** sekmesini ve ardından hello **üstbilgileri** sekmesini ve ardından hello JSON biçimi. Merhaba belge sayısını ve depolama boyutu (KB) görmeniz gerekir.

## <a name="next-steps"></a>Sonraki adımlar
Bkz: [azure'da Search hizmetinizi yönetme](search-manage.md) kod içermeyen bir yaklaşım toomanaging ve Azure Search kullanma.

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
