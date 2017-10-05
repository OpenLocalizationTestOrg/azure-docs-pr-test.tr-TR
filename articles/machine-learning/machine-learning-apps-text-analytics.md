---
title: 'Machine Learning API: Metin analizi | Microsoft Docs'
description: "Microsoft'un Machine Learning metin Analytics API'leri düşünceleri analiz, anahtar tümcecik ayıklama, dil algılama ve konu algılama için yapılandırılmamış metin analiz etmek için kullanılabilir."
services: machine-learning
documentationcenter: 
author: onewth
manager: jhubbard
editor: cgronlun
ms.assetid: 5b60694e-5521-4e4d-bf6a-1a92fdf94b65
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: onewth
ROBOTS: NOINDEX
redirect_url: ../cognitive-services/cognitive-services-text-analytics-quick-start
redirect_document_id: TRUE
ms.openlocfilehash: 10eae2ff5624dcb57de1cf72b326147f35bc2a0b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>Machine Learning API’leri: Yaklaşım, Anahtar İfade Ayıklama, Dil Algılama ve Konu Algılama için Metin Analizi
> [!NOTE]
> Bu kılavuz, API için 1 sürümüdür. Sürüm 2 için [ **bu belgesine bakın**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Sürüm 2 artık tercih edilen bu API sürümüdür.
> 
> 

## <a name="overview"></a>Genel Bakış
Metin analizi API metin analizi paketidir [web Hizmetleri](https://datamarket.azure.com/dataset/amla/text-analytics) Azure Machine Learning ile oluşturulmuş. API düşünceleri analiz, anahtar tümcecik ayıklama, dil algılama ve konu algılama gibi görevler için yapılandırılmamış metin analiz etmek için kullanılabilir. Bu API kullanmak için hiçbir eğitim verisi gereklidir: yalnızca metin verilerinizi getirin. Bu API Gelişmiş doğal dil teknikleri işleme sınıfı tahminleri en iyi teslim etmek için kullanır.

Eylem metin analizleri görebileceğinizi bizim [gösteri sitesi](https://text-analytics-demo.azurewebsites.net/), ayrıca bulabileceğiniz [örnekleri](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) C# ve Python metin analizi uygulamak nasıl.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>Duygu analizi
API, 0 ve 1 arasında sayısal bir puan döndürür. Puanları 0 yakın negatif düşünceleri belirtmek sırada 1 yakın puanları pozitif düşünceleri gösterir. Yaklaşım puanı, sınıflandırma teknikleri kullanılarak oluşturulur. Giriş özellikleri sınıflandırıcı n-gram, konuşma bölümü etiketleri ve word eklerinin oluşturulan özellikler içerir. Şu anda, İngilizce yalnızca desteklenen dilidir.

## <a name="key-phrase-extraction"></a>Anahtar tümcecik ayıklama
API, giriş metnindeki başlıca konuşma noktalarını gösteren bir dize listesi döndürür. Microsoft Office’in kapsamlı Doğal Dil İşleme araç setinden alınan teknikleri kullanırız. Şu anda, İngilizce yalnızca desteklenen dilidir.

## <a name="language-detection"></a>Dil algılama
API, 0 ve 1 arasında algılanan dil ve sayısal bir puan döndürür. Puanın 1’e yakın olması, tanımlanan dilin %100 olasılıkla doğru olduğunu gösterir. Toplamda 120 dil desteklenir.

## <a name="topic-detection"></a>Konu algılama
Bu konular listesini görmek için üst algılanan döndüren metin kayıtları gönderilen yeni yayımlanmış bir API'dir. Konular, bir veya daha fazla ilgili sözcükten oluşan bir anahtar ifade ile tanımlanır. Bu API en az 100 metin kaydının gönderilmesini gerektirir, ancak yüzlerce veya binlerce kayıt içindeki konuları algılayacak şekilde tasarlanmıştır. Bu API’de gönderilen metin kaydı başına 1 işlem ücreti uygulandığını unutmayın. API incelemeler ve kullanıcı geri bildirim gibi kısa, İnsan yazılı metin için iyi çalışmak üzere tasarlanmıştır.

- - -
## <a name="api-definition"></a>API tanımı
### <a name="headers"></a>Üstbilgileri
Şu şekilde olmalıdır isteğinizin içinde doğru üstbilgileri eklediğinizden emin olun:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

Hesabınızdaki hesap anahtarınızı bulabilirsiniz [Azure veri Pazar](https://datamarket.azure.com/account/keys). Şu anda yalnızca JSON için girdi ve çıktı biçimleri kabul edildiğini not edin. XML desteklenmiyor.

- - -
## <a name="single-response-apis"></a>Tek bir yanıt API'leri
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Örnek istek**

Çağrısında biz "Hello World" ifadesi düşünceleri analize isteyen:

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

Bu gibi bir yanıt döndürür:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a>GetKeyPhrases
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

**Örnek istek**

Şu çağrısında biz anahtar sözcükler metinde "Bu, benzersiz dekorasyonu ve kolay personeli ile kalmak için harika bir otel" bulundu isteyen:

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

Bu gibi bir yanıt döndürür:

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a>GetLanguage
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

**Örnek istek**

Aşağıdaki GET çağrısında biz metindeki anahtar sözcükler düşünceleri için istekte *Hello World*

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

Bu gibi bir yanıt döndürür:

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

**İsteğe bağlı parametreler**

`NumberOfLanguagesToDetect`İsteğe bağlı bir parametredir. Varsayılan değer 1'dir.

- - -
## <a name="batch-apis"></a>Batch API'leri
Metin analizi hizmeti düşünceleri ve anahtar tümcecik ayıklamaları toplu iş modunda yapmanıza olanak sağlar. Kayıtların her birinde bir işlem olarak sayıları skoru unutmayın. Tek bir çağrı 1000 kayıtlarında düşünceleri isterse bir örnek olarak, 1000 işlemleri düşülür.

Sisteme girildiğinde kimlikleri sistem tarafından döndürülen kimlikleri olduğunu unutmayın. Web hizmeti, bu kimlikleri benzersiz denetlemez. Benzersizlik doğrulamak için arayan sorumluluğundadır. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Örnek istek**

POST çağrısına biz "Hello World", "Merhaba Foo World" ve "Merhaba My World" istek gövdesinde tümcecikleri düşüncelerin için istekte:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

İstek gövdesi:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

Yanıtta metin kimlikleri ile ilişkilendirilmiş puanları listesini alın:

    {
      "odata.metadata":"<url>", 
      "SentimentBatch":
      [
        {"Score":0.9549767,"Id":"1"},
        {"Score":0.7767222,"Id":"2"},
        {"Score":0.8988889,"Id":"3"}
      ],  
      "Errors":[]
    }


- - -
### <a name="getkeyphrasesbatch"></a>GetKeyPhrasesBatch
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

**Örnek istek**

Bu örnekte, biz aşağıdaki metinleri anahtar tümcecikleri düşüncelerin listesi için istekte: 

* ", Benzersiz dekorasyonu ve kolay personeli ile kalmak için harika bir otel oluştu"
* "Çok ilginç konuşmaları ile harika bir yapı konferans oluştu"
* "Trafiği korkunç, üç havaalanı giderek saat harcanan"

Bu istekte bir uç nokta POST çağrısına olarak:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

İstek gövdesi:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

Yanıtta metninizi kimlikleri ile ilişkili anahtar tümcecikleri listesini alın:

    { "odata.metadata":"<url>",
         "KeyPhrasesBatch":
        [
           {"KeyPhrases":["unique decor","friendly staff","wonderful hotel"],"Id":"1"},
           {"KeyPhrases":["amazing build conference","interesting talks"],"Id":"2"},
           {"KeyPhrases":["hours","traffic","airport"],"Id":"3" }
        ],
        "Errors":[]
    }

- - -
### <a name="getlanguagebatch"></a>GetLanguageBatch

İki metin girdi için dil algılama POST çağrısına biz isteyen:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

İstek gövdesi:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Bu, aşağıdaki yanıtı burada İngilizce ilk giriş ve Fransızca'nın ikinci girişinde algılandığında döndürür:

    {
       "LanguageBatch": [{
         "Id": "1",
         "DetectedLanguages": [{
            "Name": "English",
            "Iso6391Name": "en",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       },
       {
         "Id": "2",
         "DetectedLanguages": [{
            "Name": "French",
            "Iso6391Name": "fr",
            "Score": 1.0
         }],
         "UnknownLanguage": false
       }],
       "Errors": []
    }

- - -
## <a name="topic-detection-apis"></a>Konu algılama API'leri
Bu konular listesini görmek için üst algılanan döndüren metin kayıtları gönderilen yeni yayımlanmış bir API'dir. Konular, bir veya daha fazla ilgili sözcükten oluşan bir anahtar ifade ile tanımlanır. Bu API’de gönderilen metin kaydı başına 1 işlem ücreti uygulandığını unutmayın.

Bu API en az 100 metin kaydının gönderilmesini gerektirir, ancak yüzlerce veya binlerce kayıt içindeki konuları algılayacak şekilde tasarlanmıştır.

### <a name="topics--submit-job"></a>Konular – gönderme iş
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Örnek istek**

Aşağıdaki POST çağrısında biz 100 makaleler, burada ilk ve son giriş makaleleri gösterilir ve iki StopPhrases dahil edilen bir dizi konuları istiyor.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

İstek gövdesi:

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

Yanıtta gönderilen iş için JobId alın:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Tek sözcük veya konuları döndürülmemesi gereken birden çok word tümcecikleri listesi. Çok genel konular filtrelemek için kullanılabilir. Örneğin, otel incelemeleri hakkında bir veri kümesinde duyarlı stop deyimleri "otel" ve "hostel" olabilir.  

### <a name="topics--poll-for-job-results"></a>Konular – iş sonuçları için yoklama
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Örnek istek**

Sonuçları getirmek için 'Gönderme iş' adımdan döndürülen JobId geçirin. Durum kadar dakikada Bu uç noktasını çağırmak öneririz 'Tamamlandı' yanıtta =. Tam ya da binlerce kayıtları işleriyle için uzun bir iş için yaklaşık 10 dakika sürer.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Bunu işlerken yanıt şu şekilde olacaktır:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


API çıktı şu biçimde JSON biçiminde döndürür:

    {
        "odata.metadata":"<url>",
        "Status":"Finished",
        "TopicInfo":[
        {
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Score":8.0,
            "KeyPhrase":"food"
        },
        ...
        {
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Score":6.0,
            "KeyPhrase":"decor"
            }
          ],
        "TopicAssignment":[
        {
            "Id":"1",
            "TopicId":"ed00480e-f0a0-41b3-8fe4-07c1593f4afd",
            "Distance":0.7809
        },
        ...
        {
            "Id":"100",
            "TopicId":"a5ca3f1a-fdb1-4f02-8f1b-89f2f626d692",
            "Distance":0.8034
        }
        ],
        "Errors":[]


Tüm yanıt için özellikler aşağıdaki gibidir:

**TopicInfo özellikleri**

| Anahtar | Açıklama |
|:--- |:--- |
| TopicId |Her konu için benzersiz bir tanımlayıcı. |
| Puan |Konuya atanan kayıt sayısı. |
| Anahtar cümlesi |Bir summarizing sözcük veya tümcecik konu için. 1 veya birden çok sözcük olabilir. |

**TopicAssignment özellikleri**

| Anahtar | Açıklama |
|:--- |:--- |
| Kimlik |Kaydı için tanımlayıcı. Girdide bulunan kimliği karşılık gelir. |
| TopicId |Kayıt atandı konu kimliği. |
| uzaklık |GÜVENİRLİK kaydı konuya ait. Sıfıra yakın uzaklığı daha yüksek güvenilirlik gösterir. |

