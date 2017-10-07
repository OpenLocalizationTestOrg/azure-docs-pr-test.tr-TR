---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Ön belgeleri hello Azure Search REST API'sini sunulan hello anlamlıları (Önizleme) özelliği için."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a>Eş anlamlıları Azure Search'te (Önizleme)

Arama motorları eş anlamlı örtük olarak bir sorgu hello kapsamını hello terim sağlamak tooactually sahip hello kullanıcı genişletin eşdeğer terimler ilişkilendirin. Örneğin, belirli hello terimi "köpek" ve "köpek" ve "köpek yavrusu", "köpek", "köpek" veya "köpek yavrusu" içeren tüm belgeleri eş ilişkilendirmelerini hello hello sorgu kapsamında döner.

Azure Search'te sorgu zamanında eş genişletme yapılır. Eş anlamlı eşlemeleri tooa hiç kesintiye tooexisting işlemleri hizmetiyle ekleyebilirsiniz. Ekleyebileceğiniz bir **synonymMaps** toorebuild hello dizin kalmadan özellik tooa alan tanımı. Daha fazla bilgi için bkz: [güncelleştirme dizin](https://docs.microsoft.com/rest/api/searchservice/update-index).

## <a name="feature-availability"></a>Özellik kullanılabilirliği

Merhaba anlamlıları özelliği şu anda, Önizleme ve desteklenen yalnızca en son Önizleme api sürümü hello (API sürümü 2016-09-01-Önizleme =). Şu anda Azure portalı desteği yoktur. Olası toocombine genel olarak kullanılabilir (GA) ve hello API'leri önizlemede Hello API sürümü hello istek belirtilmediğinden olmasından aynı uygulama. Üretim uygulamalarında kullanma önermiyoruz şekilde ancak API SLA ve Özellikler altında olmayan Önizleme, değişebilir.

## <a name="how-toouse-synonyms-in-azure-search"></a>Azure toouse eş anlamlı nasıl arama

Azure Search'te eş anlamlı destek tanımlamak ve tooyour hizmet karşıya eş eşlemeleri temel alır. Bu eşlemeleri bağımsız bir kaynak (örneğin, veri kaynaklarını veya dizin) oluşturur ve herhangi bir dizinde arama hizmetinizi aranabilir herhangi bir alana tarafından kullanılabilir.

Eş anlamlı eşler ve dizinleri bağımsız olarak korunur. Bir eş anlamlı harita tanımlayın ve tooyour hizmet karşıya sonra adlı yeni bir özellik ekleyerek bir alan hello eş özelliğini etkinleştirebilirsiniz **synonymMaps** hello alan tanımında. Oluşturma, güncelleştirme ve bir eş anlamlı harita her zaman emin oluşturulamıyor, yani bir bütün belge işlemi siliyor güncelleştirmek veya hello eş harita bölümlerini artımlı olarak silin. Tek giriş güncelleştirme, bir yeniden yükleme gerektirir.

Eş anlamlıları arama uygulamanıza ekleme iki adımlı bir işlemdir:

1.  Bir eş anlamlı harita tooyour arama hizmeti hello aşağıdaki API'leri aracılığıyla ekleyin.  

2.  Aranabilir alan toouse hello eş eşleştirme hello dizin tanımında yapılandırın.

### <a name="synonymmaps-resource-apis"></a>SynonymMaps kaynak API'leri

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a>Eklemek veya bir eş anlamlı harita hizmetinizin altında güncelleştirmek, kullanarak gönderdiğiniz ya da yerleştirin.

Eş anlamlı eşlemeleri yüklenir POST veya PUT aracılığıyla toohello hizmet. Her kural hello yeni satır karakteri ('\n') ayrılmış gerekir. Too5, ücretsiz bir hizmettir eş eşlemesinde başına 000 kuralları ve diğer tüm SKU 10.000 kurallarında tanımlayabilirsiniz. Her kural too20 uzantılarına sahip olabilir.

Bu Önizleme'de, eş anlamlı eşlemeleri, aşağıda açıklandığı hello Apache Solr biçiminde olmalıdır. Var olan bir eş anlamlı sözlük farklı bir biçime sahip ve toouse istiyorsanız bunu doğrudan, lütfen bize bildirin üzerinde [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

HTTP POST aşağıdaki örneğine hello olduğu gibi kullanarak yeni bir eş anlamlı eşlemesi oluşturabilirsiniz:

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

Alternatif olarak, PUT kullanın ve URI hello üzerinde hello eş eşleme adı belirtin. Merhaba eş eşlemesi yoksa, oluşturulur.

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a>Apache Solr eş biçimi

Merhaba Solr biçimi eşdeğer ve açık eş eşlemeleri destekler. Eşleştirme kurallarına toohello açık kaynak eş filtre Apache Solr, bu belgede açıklanan belirtimi: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter). Aşağıda bir örnek için eşdeğer eş anlamlıları kuralıdır.
```
              USA, United States, United States of America
```

Yukarıdaki Hello kuralı ile bir arama sorgusu "ABD" çok genişletecek "ABD" veya "ABD" veya "Amerika Birleşik Devletleri".

Açık eşleme bir okla gösterilen "= >". Belirtildiğinde, hello sol tarafındaki eşleşen bir arama sorgu Terime bir dizi "= >" hello alternatifleri hello sağ taraftaki üzerinde ile değiştirilecek. Aşağıdaki Hello kural verildiğinde, arama sorgularını "Washington", "Wash." veya "WA" tüm yeniden yazılmıştır çok "WA". Belirtilen hello yönde uygular ve hello sorgu "WA" çok yeniden değil yalnızca açık eşleme bu durumda "Washington".
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a>Liste eş hizmetinizi altında eşler.

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a>Bir eş anlamlı harita hizmetinizin altında alın.

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a>Eş anlamlıları harita hizmetinizin altında silin.

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a>Aranabilir alan toouse hello eş eşleştirme hello dizin tanımında yapılandırın.

Yeni bir alan özelliği **synonymMaps** kullanılan toospecify aranabilir bir alan için eş anlamlı harita toouse olabilir. Eş anlamlı eşlemeleri hizmet düzeyi kaynaklar ve herhangi bir alan hello hizmeti altında bir dizinin başvurduğu.

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

**synonymMaps** hello türü 'Edm.String' veya 'Collection(Edm.String)' aranabilir alanları için belirtilebilir.

> [!NOTE]
> Bu Önizleme'de, yalnızca her alan eşleme bir eş anlamlı olabilir. Birden çok eş eşlemesi toouse istiyorsanız, lütfen bize bilmeniz [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="impact-of-synonyms-on-other-search-features"></a>Eş anlamlıları diğer arama özellikleri üzerinde etkisi

Merhaba eş anlamlıları özelliği hello özgün sorgu hello OR işleci ile anlamlıları ile yeniden yazar. Bu nedenle, isabet vurgulama ve profilleri Puanlama hello özgün terim ve eş anlamlıları eşdeğer olarak kabul eder.

Eş anlamlı özellik toosearch sorguları uygular ve toofilters veya modelleri geçerli değildir. Benzer şekilde, öneriler yalnızca hello özgün terimini temel alır; Eş anlamlı sözcük eşleşmeleri hello yanıt olarak görünmez.

Eş anlamlı genişletmeleri toowildcard arama terimi geçerli değildir; önek, benzer ve regex koşulları genişletilmiş değil.

## <a name="tips-for-building-a-synonym-map"></a>Bir eş anlamlı eşlemesi oluşturmak için ipuçları

- Kısa, iyi tasarlanmış eş harita olası eşleşmeler kapsamlı bir liste daha verimli olur. Aşırı büyük veya karmaşık sözlükler uzun tooparse alın ve toomany anlamlıları hello sorgu genişletir, hello sorgu gecikmesi etkiler. Hangi koşulları kullanılabilir tahmin yerine hello gerçek koşulları aracılığıyla elde edebilirsiniz bir [arama trafiği analiz raporu](search-traffic-analytics.md).

- Hem Başlangıç hem de doğrulama alıştırma olarak etkinleştirin ve sonra bu raporu tooprecisely hangi koşulları belirlemek yararlı bir eş anlamlı eşleşmeden ve toouse devam olarak eş haritanızı daha iyi sonuç üretme olduğunu doğrulama. Önceden tanımlanmış hello raporunda, "en yaygın arama sorguları" Merhaba yerleştirir ve "sıfır sonuç arama sorguları" verir hello gerekli bilgileri.

- Arama uygulamanız için birden çok eş eşlemeleri (çok dilli müşteri tabanı uygulamanız destekliyorsa, örneğin, dil tarafından) oluşturabilirsiniz. Şu anda bir alana yalnızca bunlardan birini kullanabilirsiniz. Herhangi bir anda bir alanın synonymMaps özelliği güncelleştirebilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar

- Varolan bir dizini geliştirme (üretim olmayan) ortamında varsa, eş anlamlıları hello eklenmesi profilleri Puanlama isabet vurgulama ve öneriler etkisini de dahil olmak üzere hello arama deneyimi nasıl değiştiğini küçük sözlük toosee ile deneyin.

- [Arama trafiği analytics etkinleştirmek](search-traffic-analytics.md) ve kullanım hello önceden tanımlanmış Power BI raporu hangi koşulları kullanılır toolearn hello çoğu ve hangi olanları dönüş sıfır belgeleri. Bu ınsights ile sayesinde hello sözlük tooinclude için eş anlamlı sözcükleri dizininizdeki toodocuments çözme üretken sorguları gözden geçirin.
