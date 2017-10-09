---
title: Azure Search'te aaaFull metin arama motoru (Lucene) mimarisi | Microsoft Docs
description: "Açıklama Lucene sorgu işleme ve belge alma kavramları için tam metin araması, ilgili tooAzure arama olarak."
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a>Azure Search'te nasıl tam metin araması çalışır

Bu makale, Azure Search'te Lucene tam metin araması nasıl çalıştığını daha derin bir anlayış isteyen geliştiriciler için yazılmıştır. Metin sorguları için sorunsuz bir şekilde beklenen sonuçları Azure Search Çoğu senaryoda teslim eder, ancak bazen "kapalı" şekilde görünen bir sonuç almak. Bu durumlarda Lucene sorgu yürütme dört aşamaları hello bir arka plana sahip (ayrıştırma, sözcük analiz sorgusu, belge eşleşen, Puanlama) belirli değişiklikleri tooquery parametrelerini tanımlamak veya dizin hello dağıtılacak yapılandırma yardımcı olur İstenen sonuca. 

> [!Note] 
> Azure arama için tam metin araması Lucene kullanır, ancak Lucene tümleştirme geniş kapsamlı değildir. Biz seçmeli olarak kullanıma sunmak ve Lucene işlevselliği tooenable hello senaryoları önemli tooAzure arama genişletebilirsiniz. 

## <a name="architecture-overview-and-diagram"></a>Mimarisine genel bakış ve diyagramı

Bir tam metin arama sorgusu işlemeye başlıyor hello sorgu metni tooextract arama terimleri ayrıştırma ile. Merhaba arama motoru tooretrieve belgelerin dizinini eşleşen şartlarını kullanır. Tek tek sorgu terimleri bazen ayrılmıştır ve ne olası bir eşleşme olarak kabul edilebilir üzerinde daha geniş bir net yeni forms toocast reconstituted. Bir sonuç kümesi sonra bir ilgi puan atanan tooeach eşleşen belgenin tarafından sıralanır. Bu liste derece hello hello üstündeki toohello çağıran uygulama döndürülür.

Sorgu yürütme açıklandı, dört aşamadan oluşur: 

1. Sorgu ayrıştırma 
2. Sözcük çözümleme 
3. Belge alma 
4. Puanlama 

Merhaba diyagramda hello kullanılan bileşenler tooprocess bir arama isteğine gösterilmiştir. 

 ![Azure Search'te Lucene sorgu mimarisi diyagramı][1]


| Başlıca bileşenler | İşlev açıklaması | 
|----------------|------------------------|
|**Sorgu ayrıştırıcıları** | Sorgu işleçleri sorgu terimlerinin ayırın ve hello sorgu yapısını (sorgu ağacı) gönderilen toobe toohello arama motoru oluşturun. |
|**Çözümleyiciler** | Sözcük analiz sorgu terimlerinin üzerinde gerçekleştirin. Bu işlem, dönüştürme, kaldırma veya sorgu koşullarını genişletme içerebilir. |
|**Dizin** | Verimli veri yapısı toostore kullanılan ve dizinli belgelerden ayıklanan aranabilir koşullarını düzenleyebilirsiniz. |
|**Arama motoru** | Alır ve eşleşen hello Merhaba içeriğine göre belgelerin puanlarını dizin tersine. |

## <a name="anatomy-of-a-search-request"></a>Bir arama isteğine anatomisi

Bir arama isteğine bir sonuç kümesi döndürdü, tam bir özelliğidir. Basit haliyle, hiçbir ölçüt içermeyen boş bir sorgu değil. Birkaç koşulları, belki de kapsamlı toocertain alanlarla büyük olasılıkla bir filtre ifadesi ve kuralları sipariş sorgu parametreleri daha gerçekçi bir örnek içerir.  

Merhaba aşağıdaki örnekte olduğu tooAzure arama Gönder bir arama isteğine hello kullanarak [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

Bu istek için aşağıdaki hello arama motoru hello:

1. Giden belgeleri hello fiyat en az 60 ve değerinden 300 olduğu filtreler.
2. Merhaba sorgusunu çalıştırır. Bu örnekte, hello arama sorgusu tümcecikleri ve şartları oluşur: `"Spacious, air-condition* +\"Ocean view\""` (kullanıcılar genellikle noktalama girin yoktur, ancak hello örnekte dahil olmak üzere verir bize tooexplain nasıl çözümleyiciler tanıtıcı). Bu sorgu için hello arama motoru hello açıklama tarar ve belirtilen başlık alanları `searchFields` "Okyanusu Görünüm" içeren belgeleri ve ayrıca "spacious" Merhaba terim veya hello önekiyle başlayan koşulları "air-condition". Merhaba `searchMode` parametredir kullanılan toomatch herhangi terim (varsayılan) veya bir terim olduğu kesinlikle gerekli durumlarda bunların tümünün (`+`).
3. Siparişleri Oteller sonuç kümesini Coğrafya konumu verilen ve toohello çağıran uygulama döndürülen yakınlık tooa tarafından hello. 

Merhaba, bu makalenin çoğunluğu hello hakkında işlemesidir *arama sorgusu*: `"Spacious, air-condition* +\"Ocean view\""`. Filtreleme ve Sıralama kapsamının dışına markalarıdır. Daha fazla bilgi için bkz: Merhaba [arama API başvuru belgeleri](https://docs.microsoft.com/rest/api/searchservice/search-documents).

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a>1. Aşama: ayrıştırma sorgu 

Belirtildiği gibi hello sorgu dizesi hello ilk satır hello isteğinin şöyledir: 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

Merhaba sorgu ayrıştırıcı ayıran işleçleri (gibi `*` ve `+` hello örnekte) arama koşulları ve hello arama sorgusu içine deconstructs *alt sorgulara* desteklenen bir türde: 

+ *Terim sorgu* (gibi spacious) tek başına koşulları için
+ *Tümcecik sorgusu* tırnak işaretli şartlarının (gibi Okyanusu görünümü)
+ *önek sorgu* önek işleci tarafından izlenen koşulları için `*` (air-condition gibi)

Desteklenen sorgu türlerinin tam listesi için bkz: [Lucene sorgu sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

Bir alt sorgu ile ilişkili işleçleri belirlemek hello sorgu "olmalıdır" veya "olmalıdır" bir belge için sırayla memnun toobe kabul bir eşleşme. Örneğin, `+"Ocean view"` "ayarlanmalıdır" son toohello `+` işleci. 

Merhaba sorgu ayrıştırıcı yeniden yapılandırır hello alt sorgulara içine bir *sorgu ağaç* isteğe bağlı olarak (Merhaba sorgu temsil eden bir iç yapısı) toohello arama motorunda geçirir. Merhaba ilk aşamasında ayrıştırma sorgu hello sorgu ağaç şöyle görünür.  

 ![Boolean sorgu searchmode herhangi][2]

### <a name="supported-parsers-simple-and-full-lucene"></a>Ayrıştırıcıları desteklenen: Basit ve tam Lucene 

 Azure arama gösteren iki farklı sorgu dili, `simple` (varsayılan) ve `full`. Merhaba ayarı tarafından `queryType` arama isteğinizi parametresi, size hello sorgu ayrıştırıcı bunu bilen sorgu dili, toointerpret nasıl hello işleçleri ve sözdizimi seçin. Merhaba [basit sorgu dili](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) sezgisel ve sağlam, genellikle uygun toointerpret kullanıcı girişi olarak-istemci tarafı işleme olmadan. Sorgu işleçleri web arama motorlarından tanıdık destekler. Merhaba [tam Lucene sorgu dili](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), hangi ayarlayarak alma `queryType=full`, daha fazla işleçler ve joker karakter, benzer gibi sorgu türleri, regex ve alan kapsamlı sorgular için destek ekleyerek hello varsayılan Basit Sorgu Dili genişletir. Örneğin, Basit Sorgu söz dizimi gönderilen bir normal ifade bir sorgu dizesi ve bir ifade yorumlanır. Bu makalede Hello örnek istek hello tam Lucene sorgu dilini kullanır.

### <a name="impact-of-searchmode-on-hello-parser"></a>SearchMode hello ayrıştırıcı üzerindeki etkisi 

Ayrıştırma etkileyen başka bir arama isteği hello parametredir `searchMode` parametresi. Boole sorgular için varsayılan işleç hello denetler: herhangi bir (varsayılan) veya tüm.  

Zaman `searchMode=any`, hello varsayılan, hello alanı bölücüyü spacious ve air-condition veya (`||`), hello örnek sorgu metni eşdeğer yapma: 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

Açık işleçleri gibi `+` içinde `+"Ocean view"`, boolean sorgu yapısında anlaşılır olan (Merhaba terim *gerekir* eşleşen). Kalan toointerpret hello nasıl koşulları daha az açıktır: spacious ve air-condition. Merhaba arama motoru Okyanusu görünümünde eşleşen bulmalısınız *ve* spacious *ve* air-condition? Veya Okyanusu görünüm bulmalısınız artı *herhangi birini* koşulları kalan Merhaba? 

Varsayılan olarak (`searchMode=any`), hello arama motoru hello daha geniş yorumlama varsayar. Her iki alan *gereken* eşleştirilmesi, yansıtma "veya" semantiği. Hello ilk sorgu ağaç daha önce iki işlem, "gerekir" gösterir hello varsayılan hello ile gösterilmiştir.  

Şimdi ayarlarız varsayalım `searchMode=all`. Bu durumda, hello alanı "ve" bir işlem olarak yorumlanır. Her hello kalan terimlerin her ikisi de bir eşleşme olarak hello belge tooqualify mevcut olması gerekir. Merhaba sonuçta elde edilen örnek sorgu şu şekilde yorumlanacağını: 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

Bu sorgu için değiştirilmiş sorgu ağacı eşleşen belgenin tüm üç alt sorgulara hello kesişimi olduğu aşağıdaki gibi olur: 

 ![Boole Sorgusu searchmode tüm][3]

> [!Note] 
> Seçme `searchMode=any` üzerinden `searchMode=all` en iyi kararı temsilcisi sorguları çalıştırarak gelen değil. Büyük olasılıkla tooinclude işleçleri (arama belge depoladığında ortak) olan kullanıcıların sonuçlarını daha sezgisel, bulabileceğiniz `searchMode=all` boolean sorgu yapıları bildirir. Merhaba Interplay arasında hakkında daha fazla bilgi için `searchMode` ve işleçleri [Basit Sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a>2. Aşama: Sözcük çözümleme 

Sözcük çözümleyiciler işlem *terim sorguları* ve *tümcecik sorguları* hello sorgu ağaç yapılandırılmış sonra. Bir Çözümleyicisi metin girişleri verilen tooit hello ayrıştırıcı tarafından Merhaba, işlemleri metin hello ve sonra geri simgeleştirilmiş gönderir koşulları içine toobe birleştirilmiş sorgu ağaç hello kabul eder. 

Merhaba en sık kullanılan sözcük analiz biçimidir *dil analiz* kuralları belirli tooa dil verilen üzerinde temel sorgu terimlerinin dönüştürür: 

* Bir sorgu Terime toohello kök formu bir word'ün azaltma 
* Gerekli olmayan sözcükler kaldırma ("" gibi bir Durma sözcükleri veya "ve" İngilizce) 
* Bileşen parçalara bileşik bir sözcük bölme 
* Küçük büyük harf word büyük/küçük harfleri 

Bu işlemlerin tümü hello dizininde depolanan hello kullanıcı ve hello koşulları tarafından sağlanan hello metin girişi tooerase farklarını eğilimi gösterir. Bu tür işlemler metin işleme ötesine gidin ve hello dilinin kendisini kapsamlı bilgi gerektirir. tooadd dil tanıma, Azure Search bu katmanını destekler uzun bir listesi [dil Çözümleyicileri](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene ve Microsoft tarafından.

> [!Note]
> Analiz gereksinimleri en az tooelaborate senaryonuza bağlı olarak değişebilir. Önceden tanımlanmış hello çözümleyiciler birini seçerek hello veya kendi oluşturarak sözcük analiz karmaşıklığını denetleyebilirsiniz [özel Çözümleyicisi](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search). Çözümleyiciler kapsamlı toosearchable alanlar ve alan tanımının bir parçası belirtilir. Bu, toovary sözcük analiz bir alan başına temelinde sağlar. Belirtilmezse, hello *standart* Lucene Çözümleyicisi kullanılır.

Örneğimizde, önceki tooanalysis hello ilk sorgu ağacı hello terimi "bir büyük harf"S"ile" Spacious sahiptir ve sorgu ayrıştırıcı hello virgül (virgül bir sorgu dili işleci sayılmaz) hello sorgu Terime bir parçası olarak yorumlar.  

Merhaba varsayılan Çözümleyicisi hello terim işlediğinde, bu "Okyanusu Görünüm" ve "spacious" küçük harf ve hello virgül karakterini kaldırma. Merhaba değiştirilmiş sorgu ağacında aşağıdaki gibi görünür: 

 ![Çözümlenen koşullarla Boole Sorgusu][4]

### <a name="testing-analyzer-behaviors"></a>Test Çözümleyicisi davranışları 

bir Çözümleyicisi Hello davranışını hello kullanarak test edilmiş [analiz API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer). Merhaba metin tooanalyze toosee Çözümleyicisi verilen hangi koşulları oluşturacak istediğinizi belirtin. Örneğin, hello standart Çözümleyicisi işleminin nasıl toosee hello "metni air-condition", istek aşağıdaki hello gönderebilirsiniz:

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

Merhaba standart Çözümleyicisi iki belirteçleri, bunları konumlarını (tümcecik eşleştirmek için kullanılır) yanı sıra başlangıç ve bitiş kaydırmalar (isabet vurgulama için kullanılan) gibi özniteliklerle yorumlama aşağıdaki hello içine hello giriş metni keser:

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a>Özel durumlar toolexical çözümleme 

Sözcük analiz tüm koşullar – bir terim sorgu veya tümcecik sorgusu gerektiren tooquery türleri geçerlidir. Tamamlanmamış koşulları – önek sorgu, joker karakter sorgu, regex sorgu – veya tooa benzer sorgu tooquery türleriyle uygulanmaz. Bu terim hello önek sorguyla dahil olmak üzere türü, sorgu *air-condition\**  Bizim örneğimizde, doğrudan hello analysis aşaması atlayarak toohello sorgu ağaç eklenir. Merhaba yalnızca bu türlerde sorgu koşullarını gerçekleştirilen dönüştürmeyi lowercasing.

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a>3. Aşama: Belge alma 

Belge alma hello dizindeki eşleşen terimleri toofinding belgelerle başvuruyor. Bu aşama örneği arasında en iyi anlaşılmalıdır. Basit şema aşağıdaki hello sahip Oteller diziniyle başlayalım: 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

Daha fazla bu dizini dört belge aşağıdaki hello içeren varsayın: 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

**Koşulları nasıl dizini**

toounderstand alma tooknow yardımcı dizin oluşturma hakkındaki bazı temel bilgileri. Merhaba depolama ters dizin, aranabilir her alan için bir tane birimidir. Ters dizin tüm belgelerden tüm koşulları sıralanmış bir listesidir. Her terim bunu, aşağıdaki hello örnekte korumalı oluştuğu belgelerin toohello listesini eşler.

tooproduce hello koşulları ters bir dizinde hello arama motoru sözcük analizi belgeleri hello içerik üzerinde benzer toowhat sorgu işleme sırasında olur gerçekleştirir. Metin girişleri tooan analyzer, alt ortası noktalama işaretleri ve hello Çözümleyicisi yapılandırmasına bağlı olarak belirli bir benzeri atılmış geçirilir. Ortak, ancak gerekli değildir, toouse hello arama ve böylece sorgu terimlerinin hello dizini içinde koşulları gibi daha fazla ara işlemleri dizin oluşturma için aynı Çözümleyicileri.

> [!Note]
> Azure arama sağlar, dizin oluşturma için farklı çözümleyiciler belirtin ve arama aracılığıyla ek `indexAnalyzer` ve `searchAnalyzer` alan parametreleri. Belirtilmezse, hello ile ayarlamak Çözümleyicisi hello `analyzer` özelliği, hem dizin oluşturma ve arama için kullanılır.  

**Örnek belgeler için ters dizin**

Tooour örneğin hello döndürme **başlık** alanı, ters çevrilmiş hello dizini şu şekilde görünür:

| Sözleşme Dönemi | Belge listesi |
|------|---------------|
| atman | 1 |
| Plaj | 2 |
| Otel | 1, 3 |
| Okyanusu | 4  |
| playa | 3 |
| çare | 3 |
| Retreat | 4 |

Merhaba başlığı alanında, yalnızca *otel* iki belgelerde görüntülenir: 1, 3.

Hello için **açıklama** alanı, başlangıç dizini aşağıdaki gibidir:

| Sözleşme Dönemi | Belge listesi |
|------|---------------|
| Hava | 3
| ve | 4
| Plaj | 1
| söylediğinizde | 3
| rahat | 3
| uzaklık | 1
| Adası | 2
| kauaʻi | 2
| bulunan | 2
| Kuzey | 2
| Okyanusu | 1, 2, 3
| / | 2
| üzerinde |2
| Sessiz | 4
| odaları  | 1, 3
| secluded | 4
| Deniz Kıyısı | 2
| spacious | 1
| Merhaba | 1, 2
| çok| 1
| görünüm | 1, 2, 3
| taramasını | 1
| İle | 3


**Dizinli koşulları karşı sorgu terimlerinin eşleştirme**

Şimdi dönmek toohello örnek sorgu ters hello dizinlerini yukarıdaki verildiğinde ve nasıl eşleşen belgeleri görmek için bizim örnek sorgu bulunamadı. Geri çağırma hello son sorgu ağacı şöyle görünür: 

 ![Çözümlenen koşullarla Boole Sorgusu][4]

Sorgu yürütme sırasında tek tek sorguları hello aranabilir alanlara karşı bağımsız olarak yürütülür. 

+ Merhaba TermQuery "spacious" eşleşen 1 (otel Atman) belgesi. 

+ Merhaba PrefixQuery, "air-condition *", herhangi bir belgeniz eşleşmiyor. 

  Bazen geliştiriciler kafasını karıştırabilirler bir davranış budur. Merhaba terim Air-conditioned hello belgede var ancak iki terimleri hello varsayılan Çözümleyicisi tarafından ayrılır. Kısmi terimleri içeren, önek sorguları çözümlenmediğini geri çağırma. Bu nedenle "air-condition" hello aranır önek şartlarını dizin ters ve bulunamadı.

+ Merhaba PhraseQuery "Okyanusu Görünüm" Merhaba koşulları "Okyanusu" ve "Görünüm" arar ve hello yakınlık hello özgün belgede koşulları denetler. Belgeleri 1, 2 ve 3 Bu sorguyu hello açıklama alanı eşleşmesi. Bildirim belgesi 4 hello terim Okyanusu hello başlığında olsa da hello "Okyanusu Görünüm" tümceciği için tek sözcük yerine bekliyoruz gibi bir eşleşme olarak kabul değil. 

> [!Note]
> Bir arama sorgusu bağımsız olarak Azure arama dizini hello alanlar ile Merhaba kümesine sınırlamak sürece hello tüm aranabilir alanları karşı yürütülebilir `searchFields` hello örnek arama isteğinde gösterildiği gibi parametre. Seçili hello alanların hiçbirini eşleşen belgeleri döndürülür. 

Söz konusu hello sorgu için tüm Hello üzerinde eşleşen hello belgelerdir 1, 2, 3. 

## <a name="stage-4-scoring"></a>4. Aşama: Puanlama  

Her belge arama sonuç kümesinde bir ilgi puan atanır. Merhaba hello ilgi puanının toorank hello arama sorgusu ifade edilen en iyi bir kullanıcı yanıt bu belgeleri soru daha yüksek işlevdir. Merhaba puan eşleşen koşulları istatistiksel özelliklerini göre hesaplanır. Formül Puanlama hello çekirdek Hello olan [TF/IDF (terim sıklığı ters belge sıklığı)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf). Nadir ve sık kullanılan terimleri içeren sorgularda TF/IDF hello nadir terimi içeren sonuçları yükseltir. Örneğin, tüm Wikipedia makalelerde kuramsal bir dizinde eşleşen hello sorgu belgelerini *hello Başkanı*, üzerinde eşleşen belgeler *Başkanı* daha ilgili olarak kabul edilir üzerinde eşleşen belgeler **.


### <a name="scoring-example"></a>Puanlama örneği

Geri çağırma hello bizim örnek sorgu eşleşen üç belgeler:
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

Her ikisi de hello çünkü 1 eşleşen hello sorgu en iyi belge terim *spacious* ve hello gerekli deyimi *Okyanusu Görünüm* hello Açıklama alanına oluşur. Merhaba sonraki iki belgeleri yalnızca hello tümcecik eşleşen *Okyanusu Görünüm*. Merhaba hello sorguda eşleşen olsa bile belge 2 ve 3 farklı olduğu için o hello ilgi puan önler aynı şekilde. Formül Puanlama hello yalnızca TF/IDF'den daha fazla bileşenlere sahip olmasıdır. Bu durumda, belge 3 açıklamasını kısa olduğundan biraz daha yüksek bir puan atanmıştır. Hakkında bilgi edinin [Lucene'nın pratik Puanlama formülü](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) alan uzunluğu ve diğer etkenlere bağlı nasıl etkileyeceğini toounderstand hello ilgi puanı.

Bazı sorgu türü (joker karakter öneki, regex) her zaman sabit bir puan katkıda toohello genel belge puanı. Bu sorgu genişletme toobe hello sonuçlarında ancak hello derecelendirme etkilemeden dahil aracılığıyla bulunan eşleşmeler sağlar. 

Bu önemli neden bir örnek gösterilmektedir. Merhaba giriş olası eşleşmeleri ile kısmi dize çok fazla sayıda farklı koşulları üzerinde olduğundan önek aramaları da dahil olmak üzere, joker karakter aramaları tanımına göre belirsiz (girişi "tur *", "tur üzerinde", "tourettes" bulunan eşleşmeler göz önünde bulundurun, ve " tourmaline"). Bu sonuçları Hello yapısını verildiğinde, hangi koşulları diğerlerinden daha değerli tooreasonably Infer yolu yoktur. Bu nedenle, biz terim sıklıklarını sonuçları türleri joker karakter, önek ve regex sorgularda Puanlama zaman yoksay. Bir sabit ile birleştirilmiş kısmi ve tam koşulları içeren bir çok parçalı arama isteğinde hello kısmi giriş sonuçlarından puan tooavoid sapması büyük olasılıkla beklenmeyen eşleşmeleri bulunun.

### <a name="score-tuning"></a>Puan ayarlama

Azure Search'te tootune ilgi puanları iki yolu vardır:

1. **Profilleri Puanlama** bir dizi kurala göre sonuçları derece hello listesi belgelerde Yükselt. Bizim örneğimizde, biz hello başlığı alanında hello Açıklama alanına eşleşen belgeleri daha ilgili eşleşen belgeleri düşünebilirsiniz. Ayrıca, dizinimizi her otel için bir fiyat alan olsaydı, biz alt fiyat belgelerle yükseltmek. Daha fazla bilgi edinin nasıl çok[Puanlama profilleri tooa arama dizini ekleyin.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
2. **Terim** (yalnızca kullanılabilir hello tam Lucene sorgu söz dizimi) artırma işleci sağlar `^` , olabilir uygulanan tooany hello sorgu ağacının bir parçası. Merhaba ön ekini temel arama yerine örneğimizde *air-condition*\*, bir ya da hello tam dönem için arama *air-condition* veya hello önek ancak hello tam eşleşen belgeleri Terim derece yüksek artırma toohello terim sorgu uygulayarak: *hava durumu ^ 2 || Air-Condition**. Daha fazla bilgi edinmek [terim](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).


### <a name="scoring-in-a-distributed-index"></a>Dağıtılmış bir dizinde Puanlama

Azure Search'te tüm dizinleri otomatik olarak olan birden fazla parça bölme, birden çok arasında hello dizin dağıtmak bize tooquickly izin vererek düğümleri hizmet ölçek sırasında yukarı veya ölçeklendirmeyi azaltın. Bir arama isteğine verildiğinde, her parça karşı bağımsız olarak verilir. Merhaba her parça sonuçlarından ardından birleştirilmiş ve (diğer sıralamaya tanımlanmışsa) puana göre sıralanmış. Puanlama işlevi ağırlıkları sorgu Terime sıklığı hello parça, tüm belgelerde ters belge sıklığının karşı değil tüm parça hello önemli tooknow kadar!

Bu bir ilgi puan anlamına gelir *verebilir* üzerinde farklı parça bulunuyorsa aynı belgeler için farklı olabilir. Neyse ki, bu farklara toomore bile terim dağıtım hello dizin belgelerde Hello sayısı arttıkça toodisappear eğilimi gösterir. Belirli bir belge üzerinde hangi parça yerleştirilecek olası tooassume değil. Ancak, bir belge anahtarı değiştirmez varsayıldığında, bu her zaman toohello atanacak aynı parça.

Genel olarak, belge puan hello sipariş kararlılık önemliyse belgeleri sıralama için en iyi öznitelik değil. Örneğin, iki belgeyle aynı puan verildiğinde, hangisinin görünür hello sonraki çalıştırmalarında ilk garantisi yoktur aynı sorgu. Belge puan yalnızca belge ilgi genel bir fikir göreli tooother belgeleri hello sonuç kümesinde vermesi gerekir.

## <a name="conclusion"></a>Sonuç

Internet arama motorları Hello başarısını tam metin araması için beklentiler özel veriler üzerinde yükseltilmiş. Arama deneyimi neredeyse her türlü için şimdi hello altyapısı toounderstand bizim amacı dahi koşulları yanlış veya tamamlanmamış bekliyoruz. Hatta eşdeğer terimler veya hiçbir zaman gerçekte belirtilen eş anlamlıları dayalı eşleşmeler bekliyoruz.

Teknik açıdan, tam metin araması Gelişmiş bir dil analiz ve sistematik bir yaklaşım tooprocessing biçimlendirebilir, genişletin ve sorgu koşulları toodeliver ilgili bir sonuç dönüştürme şekillerde gerektiren yüksek oranda karmaşık bir işlemdir. Hello devralınmış karmaşıklık göz önüne alındığında, bir sorgu sonucunu hello etkileyen faktörler çok vardır. Bu nedenle, başlangıç saati toounderstand hello tam metin araması mekanikleri yatırım, beklenmeyen sonuçlara aracılığıyla toowork çalışırken somut avantajları sunar.  

Bu makalede, Azure Search'ün hello bağlamında tam metin araması incelediniz. Bu, yeterli arka plan toorecognize olası nedenleri ve çözümlemeleri ortak sorgu sorunları ele almak için sağlar umuyoruz. 

## <a name="next-steps"></a>Sonraki adımlar

+ Merhaba örnek dizini oluşturun, farklı sorguları deneyin ve sonuçları gözden geçirin. Yönergeler için bkz: [oluşturmak ve hello Portalı'nda bir dizin sorgu](search-get-started-portal.md#query-index).

+ Merhaba ek sorgu sözdiziminde deneyin [Search belgeleri](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) örnek bölümüne veya [Basit Sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) hello Portalı'nda arama Gezgini'nde.

+ Gözden geçirme [profilleri Puanlama](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) arama uygulamanızda sıralaması tootune istiyorsanız.

+ Bilgi nasıl tooapply [dile özgü sözcük çözümleyiciler](https://docs.microsoft.com/rest/api/searchservice/language-support).

+ [Özel çözümleyiciler yapılandırma](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) en az işleme veya belirli alanları üzerindeki özel işleme için.

+ [Standart ve İngilizce çözümleyiciler karşılaştırmak](http://alice.unearth.ai/)) yana birimi bu demo web sitesinde. 

## <a name="see-also"></a>Ayrıca bkz.

[REST API belgelerde arama](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[Basit sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[Tam Lucene sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[Arama sonuçlarını işleme](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
