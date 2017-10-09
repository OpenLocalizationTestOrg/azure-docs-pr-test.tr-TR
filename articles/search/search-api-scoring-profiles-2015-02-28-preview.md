---
title: "aaaScoring profilleri (Azure Search REST API sürümü 2015-02-28-Önizleme) | Microsoft Docs"
description: "Azure arama, kullanıcı tanımlı Puanlama profilleri temel alarak dereceli sonuçlarının ayarlamayı destekleyen bir barındırılan bulut arama hizmetidir."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: 17f83fdf6818dc6ffcc3e04f5d0185c6f646b63d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>Puanlama profilleri (Azure Search REST API sürümü 2015-02-28-Önizleme)
> [!NOTE]
> Bu makalede hello Puanlama profillerinde [2015-02-28-Önizleme](search-api-2015-02-28-preview.md). Şu anda hello arasında fark yoktur `2016-09-01` sürüm belgelenen [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) ve hello `2015-02-28-Preview` sürüm açıklanan Burada, ancak bu belgenin yine de sipariş tooprovide belge kapsamını arasında hello sunuyoruz Tüm API.
>
>

## <a name="overview"></a>Genel Bakış
Puanlama arama sonuçlarında döndürülen her öğe için bir arama puanı toohello hesaplaması başvuruyor. Merhaba puan hello geçerli arama işlemini Merhaba içeriğine öğenin ilgi bir göstergesidir. daha yüksek hello puan Merhaba, daha ilgili hello öğesi hello. Arama sonuçlarında her öğe için hesaplanan hello arama puanı göre yüksek toolow gelen Sıralı derece öğelerdir.

Bir başlangıç puanı toocompute Puanlama varsayılan Azure arama kullanır, ancak hello hesaplama Puanlama profili üzerinden özelleştirebilirsiniz. Puanlama profilleri, arama sonuçlarında öğeleri hello sıralamasını üzerinde daha fazla denetim sağlar. Örneğin, olası gelir üzerinde kendi dayanan tooboost öğelerini istediğiniz yeni öğeleri yükseltmek veya belki de envanter çok uzun olan öğeleri artırma.

Puanlama profili hello dizin tanımı, alanları, işlevleri ve parametreleri oluşan bir parçasıdır.

toogive hello aşağıdaki örnekte gösterilir basit bir profili gibi bir fikir Puanlama profili göründüğünü 'coğrafi' adlı. Bu bir hello hello arama terimi olan öğeler artırır `hotelName` alan. Ayrıca hello kullanır `distance` içinde on kilometre hello geçerli konumunun toofavor öğeleri işlev. Birisi 'inn' hello terimini arar ve 'inn' hello otel adı toobe parçası olur, Oteller 'inn' ile içeren belgeleri hello arama sonuçlarında daha yüksek görünür.

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

Bu Puanlama profili sorgunuzu toouse hello sorgu dizesi toospecify hello profilde şeklide. Merhaba sorgu parametresi, aşağıdaki Hello sorgu içinde fark `scoringProfile=geo` hello isteği.

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

Bu sorgu, 'inn' hello terimini arar ve hello geçerli konumda geçirir. Bu sorgu gibi diğer parametreleri içeren Not `scoringParameter`. Sorgu parametreleri açıklanmıştır [Search belgeleri (Azure Search API)](search-api-2015-02-28-preview.md#SearchDocs).

Tıklatın [örnek](#example) tooreview Puanlama profili daha ayrıntılı bir örnek.

## <a name="what-is-default-scoring"></a>Ne varsayılan Puanlama olduğu?
Puanlama derece sıralı sonuç kümesinde her öğe için bir arama puanı hesaplar. Her öğe bir arama sonuç kümesinde arama puanı atanan sonra yüksek toolowest derece. Merhaba yüksek puanları öğeleriyle toohello uygulama döndürülür. Varsayılan olarak, hello üst 50 döndürülür, ancak hello kullanabilirsiniz `$top` parametresi tooreturn küçük veya büyük bir öğe (yukarı, tek bir yanıt too1000) sayısı.

Varsayılan olarak, bir arama puanı istatistiksel özelliklerini hello veri ve hello sorgu göre hesaplanır. Azure arama hello sorgu dizesinde hello arama terimleri içeren belgeleri bulur (bazıları veya tümü, bağlı olarak `searchMode`), birçok hello arama terimi örneklerini içeren belgeleri öncelik tanıdığından. Merhaba terim hello belge içinde ortak ancak hello veri gövde arasında nadiren ise hello arama puanı bile yüksek artar. Bu yaklaşım toocomputing ilgi Hello temelini TF-IDF bilinen veya (terim sıklığı ters belge sıklığı).

Toohello çağıran uygulama döndürmeden yoktur özel sıralama varsayıldığında, sonuçları sonra arama puanı göre sıralanır. Varsa `$top` , 50 öğeleri hello yüksek arama puanı döndürülür sahip belirtilmedi.

Arama puanı değerleri bir sonuç kümesi yinelenebilir. Örneğin, 10 öğelerinin 1.2, puanı olabilir bir puan 20 öğeleriyle 1.0 ve 20 öğelerinin 0,5 puanı. Merhaba aynı puanlanmış öğeleri sıralama sahip birden çok isabet Merhaba, aynı arama puanı tanımlı değil ve tutarlı değil. Merhaba sorguyu yeniden çalıştırın ve görebilirsiniz öğeleri shift konumu. İki özdeş bir puan öğeleriyle verildiğinde, hangisinin ilk olarak görünür garantisi yoktur.

## <a name="when-toouse-custom-scoring"></a>Zaman toouse özel Puanlama
Merhaba varsayılan davranışı sıralaması yetecek kadar iş hedeflerinize Git değil sağlandığında, bir veya daha fazla Puanlama profili oluşturmanız gerekir. Örneğin, arama kesinliğini yeni eklenen öğeler favor karar verebilirsiniz. Benzer şekilde, kar oranı içeren bir alan veya gelir olası gösteren başka bir alan olabilir. Tooyour iş faydaları Getir isabet artırmanın profilleri Puanlama toouse karar önemli bir etken olabilir.

İlgi tabanlı sıralama profilleri Puanlama da uygulanır. Arama sonuçları olanak tanıyan hello son kullandığınız sayfaları fiyat, tarih, derecelendirme veya ilgi göre sıralama göz önünde bulundurun. Azure Search'te Puanlama profilleri hello 'ilgi' seçeneği sürücü. ilgi Hello tanımı tarafından denetlenen, toodeliver istediğiniz iş hedeflerini ve arama deneyimi hello türü predicated.

<a name="example"></a>

## <a name="example"></a>Örnek
Belirtildiği gibi özelleştirilmiş Puanlama dizin şeması'nda tanımlanan profilleri Puanlama uygulanır.

Gösterir hello iki Puanlama profili olan bir dizin şemasını Bu örnek (`boostGenre`, `newAndHighlyRated`). Herhangi bir sorgu karşı sorgu parametresi hello profil tooscore hello sonuç kümesini kullanacak şekilde, her iki profil içeren bu dizini.

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a>İş akışı
tooimplement özel davranış, Puanlama hello dizini tanımlayan bir Puanlama profili toohello şema ekleyin. Bir dizin içinde too16 Puanlama profilleri yukarı olabilir (bakın [hizmet sınırları](search-limits-quotas-capacity.md)), ancak belirli bir sorgu zaman yalnızca bir profil belirtebilirsiniz.

Başlangıç ile Merhaba [şablon](#bkmk_template) bu konuda sağlanan.

Bir ad sağlayın. Puanlama profili isteğe bağlıdır, ancak bir eklerseniz, hello adı gereklidir. Alanlar için adlandırma kurallarını hello emin toofollow olabilir (özel karakterler ve ayrılmış sözcükler önler bir harf ile başlayan). Bkz: [adlandırma kurallarını](http://msdn.microsoft.com/library/azure/dn857353.aspx) daha fazla bilgi için.

Puanlama profili hello Hello gövdesi ağırlıklı alanları ve işlevleri oluşturulur.

### <a name="weights"></a>Ağırlıkları
Merhaba `weights` Puanlama profili özelliği göreli ağırlık tooa alanını atamak ad-değer çiftleri belirtir. Merhaba, [örnek](#example), hello albumTitle, tarzını ve artistName alanlardır boosted 1.5, 5 ve 2 ' sırasıyla. Neden Tarz başkalarının hello çok yüksek boosted? Arama biraz homojen veriler üzerinde gerçekleştirilen varsa (Merhaba hello 'Tarz' ile olduğu gibi `musicstoreindex`), daha büyük bir hello göreli ağırlığı varyans gerekebilir. Örneğin, hello içinde `musicstoreindex`, 'rock' hem bir tarzını ve aynı tümcecik oluşturulmuş bir tarzını açıklamalarında görüntülenir. Tarz toooutweigh Tarz açıklama istiyorsanız, çok daha yüksek göreli ağırlık hello Tarz alan gerekir.

### <a name="functions"></a>İşlevler
İşlevleri, diğer hesaplamalar için belirli bağlamları gerekli olduğunda kullanılır. Geçerli bir işlev türleri `freshness`, `magnitude`, `distance` ve `tag`. Her işlevi benzersiz tooit parametre içeriyor.

* `freshness`nasıl yeni veya eski bir öğe tarafından tooboost olan istediğinizde kullanılmalıdır. Bu işlev yalnızca datetime alanları ile kullanılabilir (`Edm.DataTimeOffset`). Not hello `boostingDuration` özniteliği yalnızca hello yenilik işlevi ile kullanılır.
* `magnitude`nasıl yüksek veya düşük bir sayısal değerini temel tooboost olan istediğinizde kullanılmalıdır. Bu işlev için çağrı senaryolar, kar marjı, en yüksek fiyat, en düşük fiyat veya yüklemeleri sayısını artırma içerir. Merhaba ters desenini (örneğin, tooboost daha düşük fiyatlı öğeleri Yüksek fiyatlı öğeleri'den fazla) istiyorsanız hello aralık, yüksek toolow ters çevirebilirsiniz. Fiyatlar $100 arasında bir dizi verilen çok$ 1, ayarlamalısınız `boostingRangeStart` 100 ve `boostingRangeEnd` 1 tooboost hello daha düşük fiyatlı öğeleri. Bu işlev yalnızca çift ve tamsayı alanları ile kullanılabilir.
* `distance`tooboost istediğinizde yakınlık veya coğrafi konum tarafından kullanılmalıdır. Bu işlev yalnızca kullanılabilir `Edm.GeographyPoint` alanları.
* `tag`belgeler ve arama sorguları arasında ortak etiketleriyle tooboost istediğinizde kullanılmalıdır. Bu işlev yalnızca kullanılabilir `Edm.String` ve `Collection(Edm.String)` alanları.

#### <a name="rules-for-using-functions"></a>İşlevleri kullanmak için kurallar
* İşlev türü (yenilik, büyüklük, uzaklığı, etiket) küçük olmalıdır.
* İşlevler null veya boş değer içeremez. Fieldname eklerseniz, özellikle tooset sahip onu toosomething.
* İşlevler yalnızca uygulanan toofilterable alanları olabilir. Bkz: [Create Index](search-api-2015-02-28-preview.md#CreateIndex) filtrelenebilir alanları hakkında daha fazla bilgi.
* İşlevler yalnızca bir dizinin hello alanlar koleksiyonu içinde tanımlanan uygulanan toofields olabilir.

Merhaba dizin tanımlandıktan sonra belgeleri tarafından izlenen hello dizin şemasını yükleyerek hello dizini oluşturun. Bkz: [Create Index](search-api-2015-02-28-preview.md#CreateIndex) ve [ekleme veya güncelleştirme belgeler](search-api-2015-02-28-preview.md#AddOrUpdateDocuments) bu işlemler hakkında yönergeler için. Merhaba dizin oluşturulduktan sonra arama verilerinizle çalışır işlevsel bir Puanlama profili olması gerekir.

<a name="bkmk_template"></a>

## <a name="template"></a>Şablon
Bu bölümde hello sözdizimi ve profilleri Puanlama şablonu göstermektedir. Çok başvuran[dizin öznitelik başvurusu](#bkmk_indexref) hello sonraki bölümde hello öznitelikler açıklaması.

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies toosearchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
            ...
          }
        },
        "functions": (optional) [
          {
            "type": "magnitude | freshness | distance | tag",
            "boost": # (positive number used as multiplier for raw score != 1),
            "fieldName": "...",
            "interpolation": "constant | linear (default) | quadratic | logarithmic",

            "magnitude": {
              "boostingRangeStart": #,
              "boostingRangeEnd": #,
              "constantBoostBeyondRange": true | false (default)
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location)
              "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a>Puanlama profili Özellik Başvurusu
> [!NOTE]
> Puanlama işlevi yalnızca filtrelenebilir uygulanan toofields olabilir.
>
>

| Özellik | Açıklama |
| --- | --- |
| `name` |Gereklidir. Bu hello profil Puanlama hello adıdır. Bunu şu şekilde hello alanının aynı adlandırma kuralları. Bir harfle başlamalı, nokta, iki nokta üst üste içeremez veya sembolleri, @ ve hello deyim "azureSearch" (büyük küçük harfe duyarlı) ile başlayamaz. |
| `text` |Merhaba ağırlıkları özelliği içerir. |
| `weights` |İsteğe bağlı. Alan adı ve göreli ağırlık belirtir ad-değer çifti. Göreli ağırlık bir pozitif tamsayı veya kayan noktalı sayı olmalıdır. Karşılık gelen bir ağırlık olmadan hello alan adı belirtebilirsiniz. Ağırlıkları kullanılan tooindicate hello bir alan göreli tooanother önemini ' dir. |
| `functions` |İsteğe bağlı. Puanlama işlevi yalnızca filtrelenebilir uygulanan toofields olabileceğini unutmayın. |
| `type` |Puanlama işlevleri için gereklidir. İşlev toouse Hello türünü belirtir. Geçerli değerler arasında `magnitude`, `freshness`, `distance` ve `tag`. Her Puanlama profiline birden fazla işlev ekleyebilirsiniz. Merhaba işlev adı küçük olmalıdır. |
| `boost` |Puanlama işlevleri için gereklidir. Ham puan çarpanı olarak kullanılan pozitif bir sayı. Eşit too1 olamaz. |
| `fieldName` |Puanlama işlevleri için gereklidir. Puanlama işlevi yalnızca hello alanı koleksiyonu hello dizinin parçası olan ve filtrelenebilir uygulanan toofields olabilir. Ayrıca, her işlev türü (yenilik datetime alanları, tamsayı veya çift alanlarıyla büyüklük, konum alanlarla uzaklığı ve dize veya dize koleksiyonu alanları etiketiyle kullanılır) ek kısıtlamalar getirir. Yalnızca işlev tanımı başına tek bir alan belirtebilirsiniz. İçin örnek, iki kez içinde toouse büyüklük Merhaba aynı profili, tooinclude iki tanımları büyüklük, her bir alan için bir tane gerekir. |
| `interpolation` |Puanlama işlevleri için gereklidir. Merhaba aralığı toohello hello aralığın sonuna hello başından artırmanın hangi hello puan Hello eğimi tanımlar. Geçerli değerler arasında `linear` (varsayılan), `constant`, `quadratic`, ve `logarithmic`. Bkz: [ayarlamak ilişkilendirme](#bkmk_interpolation) Ayrıntılar için. |
| `magnitude` |Merhaba büyüklük Puanlama işlevi hello bir sayısal alana ait değer aralığına bağlı olarak kullanılan tooalter derecelendirmeleri ' dir. Merhaba en yaygın kullanım örnekleri bu bazıları şunlardır:<ul><li>Yıldız derecelendirmeleri: hello Alter Puanlama hello değere dayanarak hello "Yıldız derecelendirmesi" alanı içinde. Hello yüksek derecelendirme hello öğesiyle ilk iki öğe ilgili olduğunda görüntülenir.</li><li>Kenar boşluğu: iki belge ilgili olduğunda, bir satıcıya yüksek kenar boşlukları içeren tooboost belgelerin isteyebilir.</li><li>Sayıları tıklayın: Eylemler tooproducts veya sayfaları arasında izlemek Uygulamalar'a tıklayın için tooget hello trafiğinin çoğu eğilimindedir büyüklük tooboost öğeleri kullanabilirsiniz.</li><li>Sayıları indirin: yüklemeleri izlemek uygulamaları hello için büyüklük işlevi sağlar hello çoğu yüklemeleri olan öğeler artırın.</li></ul> |
| `magnitude:boostingRangeStart` |Ayarlar hello puanlandığı hello aralığın değeri başlatın. Merhaba değeri bir tamsayı ya da kayan noktalı sayı olmalıdır. 1-4 arasındaki yıldız derecelendirmesi bu 1 olur. % 50 üzerindeki aralıklar için bu 50 olur. |
| `magnitude:boostingRangeEnd` |Merhaba puanlandığı hello aralığın bitiş değerini ayarlar. Merhaba değeri bir tamsayı ya da kayan noktalı sayı olmalıdır. 1-4 arasındaki yıldız derecelendirmesi bu 4 olur. |
| `magnitude:constantBoostBeyondRange` |Geçerli değerler true veya false (varsayılan) değerleridir. Tootrue, ayarlandığında hello tam artırma hello aralığının hello üst noktasından yüksek hello hedef alan için bir değere sahip tooapply toodocuments devam edecek. False ise, bu işlevin artırma özelliği hello uygulanan toodocuments hello aralığın dışında hello hedef alan için bir değer sahip olmayacaktır. |
| `freshness` |Merhaba yenilik Puanlama işlevi puanları DateTimeOffset alanlarındaki değerlere bağlı olarak öğelere sıralaması kullanılan tooalter ' dir. Örneğin, eski öğeleri daha yüksek bir öğesiyle daha yakın bir tarih sıralanabilir. (Bu da olası toorank öğeleri olduğuna dikkat edin benzeri gelecek tarihler Takvim olaylarla öğeleri daha yakından toohello mevcut hello gelecekte daha fazla öğe daha yüksek sıralanabilir şekilde.) Merhaba geçerli hizmet sürümü, bir hello aralığın sonuna geçerli saati toohello düzeltilecektir. Merhaba diğer hello geçmiş üzerinde hello dayalı bir sürede sonudur `boostingDuration`. tooboost hello gelecekteki kez aralığı kullanın negatif `boostingDuration`. hangi hello profil Puanlama hello uygulanan ilişkilendirme toohello tarafından belirlenir maksimum ve minimum bir aralıktan değişiklikleri artırmanın hello oranı (aşağıdaki şekilde hello bakın). tooreverse uygulanan artırma faktörü Merhaba, 1'den yükseltme faktörü seçin. |
| `freshness:boostingDuration` |Belirli bir belge için artırma işleminin duracağı sona erme dönemini belirler. Bkz: [ayarlamak boostingDuration](#bkmk_boostdur) bölüm söz dizimi ve örnekler için aşağıdaki hello içinde. |
| `distance` |Merhaba uzaklık Puanlama işlevi düzeyine bağlı olarak belgelerin kapatın kullanılan tooaffect hello olduğu kadar veya bunlar göreli tooa başvuru coğrafi konumu. Merhaba başvuru konumu olarak bir parametre hello sorguda bir parçası olarak verilir (hello kullanarak `scoringParameter` sorgu parametresi) bir lon lat bağımsız değişkeni olarak. |
| `distance:referencePointParameter` |Bir parametre toobe sorguları toouse başvuru konumu olarak geçirildi. scoringParameter bir sorgu parametresidir. Bkz: [Search belgeleri](search-api-2015-02-28-preview.md#SearchDocs) sorgu parametreleri açıklamaları için. |
| `distance:boostingDistance` |Merhaba mesafeyi kilometre aralığı artırmanın hello bittiği hello başvuru konumundan cinsinden belirten bir sayı. |
| `tag` |Merhaba işlevi Puanlama etiket kullanılır etiketleri belgelerde ve arama sorguları temel tooaffect hello puanı belgeleri. Etiketler hello arama sorgusu ortak olan belgeler boosted. Merhaba arama sorgusu her arama isteği Puanlama parametre olarak sağlanan için etiketler Hello (hello kullanarak `scoringParameter` sorgu parametresi). |
| `tag:tagsParameter` |Bir parametre toobe sorgularda belirli bir istek için toospecify etiketler geçirildi. `scoringParameter`bir sorgu parametresidir. Bkz: [Search belgeleri](search-api-2015-02-28-preview.md#SearchDocs) sorgu parametreleri açıklamaları için. |
| `functionAggregation` |İsteğe bağlı. Yalnızca zaman işlevlerinin belirtilen geçerlidir. Geçerli değerler şunlardır: `sum` (varsayılan), `average`, `minimum`, `maximum`, ve `firstMatching`. Bir arama puanı birden çok işlevleri dahil olmak üzere birden çok değişkenlerinden hesaplanan tek bir değerdir. Bu öznitelikler gösteren tüm hello işlevlerin hello boosts uygulanan toohello temel sonra belge puanı olan tek bir birleşik artırma nasıl birleştirilir. Merhaba temel puanı hesaplanan hello belge ve hello arama sorgusu hello tf-IDF değeri temel alır. |
| `defaultScoringProfile` |Hiçbir Puanlama profili belirtilmişse, bir arama isteği yürütmeden yüklediğinizde, varsayılan Puanlama kullanılan (tf-IDF yalnızca) olur. Profil adı Puanlama varsayılan belirli bir profil hello arama isteğinde verildiğinde Azure Search toouse bu profili neden burada ayarlayabilirsiniz. |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>Set ilişkilendirme
İlişkilendirme toodefine hello eğimi hello aralığı toohello hello aralığın sonuna hello başından artırmanın hangi hello skoru için izin verin. ilişkilendirme aşağıdaki hello kullanılabilir:

* `Linear`: Hello en fazla ve en küçük aralık içinde olan öğeleri için sürekli olarak azalan tutarındaki hello uygulanan artırma toohello öğesi yapılacaktır. Puanlama profili Hello varsayılan ilişkilendirme doğrusal ' dir.
* `Constant`: Merhaba başlangıç ve bitiş aralığı içinde olan öğeleri için sürekli artırma uygulanan toohello derece sonuçlar olacaktır.
* `Quadratic`: Karşılaştırma tooa sürekli azalan artırma sahip doğrusal ilişkilendirme, ikinci derece başlangıçta daha küçük hızı düşürür ve hello Bitiş aralığı yaklaşımı olarak bir çok daha yüksek aralıkta azaltır. Bu ilişkilendirme seçeneği işlevleri Puanlama etiketinde izin verilmiyor.
* `Logarithmic`: Karşılaştırma tooa sürekli azalan artırma sahip doğrusal ilişkilendirme, logaritmik başlangıçta daha yüksek hızı düşürür ve hello Bitiş aralığı yaklaştığında bir kadar küçük aralığında azaltır. Bu ilişkilendirme seçeneği işlevleri Puanlama etiketinde izin verilmiyor.

<a name="Figure1"></a> ![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>Set boostingDuration
`boostingDuration`Merhaba yenilik işlevinin bir özniteliktir. İşleminin duracağı sona erme dönemini durdurur tooset belirli bir belge için kullanırsınız. Örneğin, tooboost ürün satırı ya da 10 gün tanıtım belirli bir marka hello 10 gün süreyle "P10D" olarak bu belgeleri belirtmeniz gerekir. Veya tooboost Yaklaşan olayları hello sonraki hafta belirtin "-P7D".

`boostingDuration`bir XSD "dayTimeDuration" değeri (bir ISO 8601 süre değerinin sınırlı alt) biçimlendirilmiş olması gerekir. Bu Hello deseni: `[-]P[nD][T[nH][nM][nS]]`.

Aşağıdaki tablonun hello çeşitli örnekler sağlar.

| Süre | boostingDuration |
| --- | --- |
| 1 gün |"P1D" |
| 2 gün ve 12 saat |"P2DT12H" |
| 15 dakika |"PT15M" |
| 30 gün, 5 saat, 10 dakika, ve 6.334 saniye |"P30DT5H10M6.334S" |

Daha fazla örnek için bkz: [XML şeması: veri türleri (W3.org web sitesi)](http://www.w3.org/TR/xmlschema11-2/).

**Ayrıca bkz.**
[Azure Search Hizmeti REST API'si](http://msdn.microsoft.com/library/azure/dn798935.aspx) MSDN'de <br/>
[Dizini (Azure Search API) oluşturma](http://msdn.microsoft.com/library/azure/dn798941.aspx) MSDN'de<br/>
[Puanlama profili tooa arama dizini eklemek](http://msdn.microsoft.com/library/azure/dn798928.aspx) MSDN'de<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
