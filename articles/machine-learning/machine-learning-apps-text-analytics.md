---
title: 'Machine Learning API: Metin analizi | Microsoft Docs'
description: "Microsoft'un Machine Learning metin Analytics API'leri kullanılan tooanalyze olabilir düşünceleri analiz, anahtar tümcecik ayıklama, dil algılama ve konu algılama için yapılandırılmamış metin."
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
redirect_document_id: True
ms.openlocfilehash: 49380c83849c5d5fdd8dce4f3899ebcb3d6870f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a>Machine Learning API’leri: Yaklaşım, Anahtar İfade Ayıklama, Dil Algılama ve Konu Algılama için Metin Analizi
> [!NOTE]
> Bu kılavuz hello API için 1 sürümüdür. Sürüm 2 için [ **toothis belge başvuran**](../cognitive-services/cognitive-services-text-analytics-quick-start.md). Sürüm 2 şimdi hello tercih edilen bu API sürümüdür.
> 
> 

## <a name="overview"></a>Genel Bakış
Merhaba metin Analytics API olan metin analizi dizisi [web Hizmetleri](https://datamarket.azure.com/dataset/amla/text-analytics) Azure Machine Learning ile oluşturulmuş. Merhaba API kullanılan tooanalyze olabilir düşünceleri analiz, anahtar tümcecik ayıklama, dil algılama ve konu algılama gibi görevler için yapılandırılmamış metin. Bu API toouse veriler hiçbir eğitim gerekli: yalnızca metin verilerinizi getirin. Bu API, Gelişmiş doğal dil teknikleri toodeliver en iyi sınıf tahminleri işleme kullanır.

Eylem metin analizleri görebileceğinizi bizim [gösteri sitesi](https://text-analytics-demo.azurewebsites.net/), ayrıca bulabileceğiniz [örnekleri](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) nasıl tooimplement metin analizi C# ve Python.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a>Duygu analizi
Merhaba API 0 ve 1 arasında sayısal bir puan döndürür. Puanları Kapat too1 puanları Kapat too0 belirtmek sırada negatif düşünceleri pozitif düşünceleri gösterir. Yaklaşım puanı, sınıflandırma teknikleri kullanılarak oluşturulur. Merhaba giriş özellikleri toohello sınıflandırıcı n-gram, konuşma bölümü etiketleri ve word eklerinin oluşturulan özellikler içerir. Şu anda, İngilizce dil hello yalnızca desteklenen değil.

## <a name="key-phrase-extraction"></a>Anahtar tümcecik ayıklama
Merhaba API hello anahtar Konuşmayı noktaları hello giriş metin belirten dizelerinin listesini döndürür. Microsoft Office’in kapsamlı Doğal Dil İşleme araç setinden alınan teknikleri kullanırız. Şu anda, İngilizce dil hello yalnızca desteklenen değil.

## <a name="language-detection"></a>Dil algılama
Merhaba API hello algıladı dil ve 0 ve 1 arasında sayısal bir puan döndürür. Puanları Kapat too1% 100 çalışılarak tanımlanan hello dil doğru olduğunu gösterir. Toplamda 120 dil desteklenir.

## <a name="topic-detection"></a>Konu algılama
Bu üst algılanan konuları gönderilen metin kayıtların listesini hello döndüren yeni yayımlanmış bir API'dir. Konular, bir veya daha fazla ilgili sözcükten oluşan bir anahtar ifade ile tanımlanır. Bu API en az 100 metin gönderilen toobe kaydeder, ancak tasarlanmış toodetect konuları yüzlerce arasında olduğu gerektiriyor kayıtların toothousands. Bu API’de gönderilen metin kaydı başına 1 işlem ücreti uygulandığını unutmayın. Merhaba API iyi incelemeler ve kullanıcı geri bildirim gibi metin yazılmış kısa, İnsan için tasarlanmış toowork ' dir.

- - -
## <a name="api-definition"></a>API tanımı
### <a name="headers"></a>Üstbilgileri
Şu şekilde olmalıdır isteğinizin içinde hello doğru üstbilgileri eklediğinizden emin olun:

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

Hesap anahtarınızı hesabınızdan hello bulabilirsiniz [Azure veri Pazar](https://datamarket.azure.com/account/keys). Şu anda yalnızca JSON için girdi ve çıktı biçimleri kabul edildiğini not edin. XML desteklenmiyor.

- - -
## <a name="single-response-apis"></a>Tek bir yanıt API'leri
### <a name="getsentiment"></a>GetSentiment
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

**Örnek istek**

Merhaba çağrısında aşağıdaki biz düşünceleri analiz hello deyimi "Hello World" istekte:

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

Merhaba çağrısında aşağıdaki biz hello anahtar tümcecikleri hello metinde "Bu harika bir otel toostay adresindeki, benzersiz dekorasyonu ve kolay personeli ile" bulundu isteyen:

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

Merhaba GET çağrı aşağıdaki biz hello anahtar tümcecikleri hello metin hello düşünceleri için istekte *Hello World*

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

`NumberOfLanguagesToDetect`İsteğe bağlı bir parametredir. Merhaba, 1 varsayılandır.

- - -
## <a name="batch-apis"></a>Batch API'leri
Merhaba metin Analytics hizmeti, toodo düşünceleri ve anahtar tümcecik ayıklamaları toplu iş modunda sağlar. Merhaba kayıtların her birinde bir işlem olarak sayıları skoru unutmayın. Tek bir çağrı 1000 kayıtlarında düşünceleri isterse bir örnek olarak, 1000 işlemleri düşülür.

Merhaba kimlikleri hello sisteme girildiğinde Not hello sistem tarafından döndürülen hello kimlikleri aynıdır. Merhaba web hizmeti, bu kimlikleri benzersiz denetlemez. Bunu hello hello arayan tooverify benzersizlik sorumluluğundadır. 

### <a name="getsentimentbatch"></a>GetSentimentBatch
**URL**    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

**Örnek istek**

Biz hello düşüncelerin hello tümce "Hello World", "Hello World Foo" ve "Merhaba My World" Merhaba hello istek gövdesi için istekte aşağıda Hello POST arayın:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

İstek gövdesi:

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

Aşağıdaki Hello yanıt olarak metin kimlikleri ile ilişkilendirilmiş puanları hello listesini alın:

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

Bu örnekte, biz metinleri aşağıdaki hello hello anahtar tümcecikleri düşüncelerin hello listesi için istekte: 

* "Konumunda, benzersiz dekorasyonu ve kolay personeli ile harika bir otel toostay oluştu"
* "Çok ilginç konuşmaları ile harika bir yapı konferans oluştu"
* "hello trafiği korkunç, üç toohello havaalanı giderek saat harcanan"

Bu istek bir POST çağrısı toohello uç noktası olarak yapılır:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

İstek gövdesi:

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

Aşağıdaki Hello yanıt olarak metninizi kimlikleri ile ilişkili anahtar tümcecikleri hello listesini alın:

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

Merhaba POST çağrısında aşağıdaki biz iki metin girdi için dil algılama isteyen:

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

İstek gövdesi:

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

Bu yanıt, burada İngilizce ilk giriş hello ve Fransızca hello ikinci giriş algılandığında aşağıdaki hello döndürür:

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
Bu üst algılanan konuları gönderilen metin kayıtların listesini hello döndüren yeni yayımlanmış bir API'dir. Konular, bir veya daha fazla ilgili sözcükten oluşan bir anahtar ifade ile tanımlanır. Bu API’de gönderilen metin kaydı başına 1 işlem ücreti uygulandığını unutmayın.

Bu API en az 100 metin gönderilen toobe kaydeder, ancak tasarlanmış toodetect konuları yüzlerce arasında olduğu gerektiriyor kayıtların toothousands.

### <a name="topics--submit-job"></a>Konular – gönderme iş
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

**Örnek istek**

Merhaba POST çağrısında aşağıdaki biz burada hello ilk ve son makaleleri gösterilir ve iki StopPhrases dahil edilen giriş 100 makaleleri bir dizi konuları istiyor.

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

İstek gövdesi:

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

Aşağıdaki Hello yanıt olarak hello gönderilen iş için hello JobId alın:

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

Tek sözcük veya konuları döndürülmemesi gereken birden çok word tümcecikleri listesi. Çok genel konular çıkışı kullanılan toofilter olabilir. Örneğin, otel incelemeleri hakkında bir veri kümesinde duyarlı stop deyimleri "otel" ve "hostel" olabilir.  

### <a name="topics--poll-for-job-results"></a>Konular – iş sonuçları için yoklama
**URL**

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

**Örnek istek**

JobId hello 'Gönderme iş' adım toofetch hello sonuçlarından döndürülen hello geçirin. Durum kadar dakikada Bu uç noktasını çağırmak öneririz 'Tamamlandı' hello yanıtta =. İş toocomplete veya uzun süre binlerce kayıtları işleriyle yaklaşık 10 dakika sürer.

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


Bunu işlerken hello yanıt şu şekilde olacaktır:

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


Merhaba API çıktı biçimi aşağıdaki hello JSON biçiminde döndürür:

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


Merhaba özellikleri hello yanıt her kısmı için aşağıdaki gibidir:

**TopicInfo özellikleri**

| Anahtar | Açıklama |
|:--- |:--- |
| TopicId |Her konu için benzersiz bir tanımlayıcı. |
| Puan |Kayıt sayısı tootopic atanır. |
| Anahtar cümlesi |Bir summarizing sözcük veya tümcecik hello konu için. 1 veya birden çok sözcük olabilir. |

**TopicAssignment özellikleri**

| Anahtar | Açıklama |
|:--- |:--- |
| Kimlik |Merhaba kaydı için tanımlayıcı. Merhaba girişinde dahil toohello kimliği karşılık gelir. |
| TopicId |Kayıt hello hello konu kimliği atandı. |
| uzaklık |Kayıt hello güvenirlik toohello konu aittir. Uzaklık daha yakından toozero daha yüksek güvenilirlik gösterir. |

