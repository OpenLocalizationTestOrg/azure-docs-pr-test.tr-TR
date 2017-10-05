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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="9a889-103">Machine Learning API’leri: Yaklaşım, Anahtar İfade Ayıklama, Dil Algılama ve Konu Algılama için Metin Analizi</span><span class="sxs-lookup"><span data-stu-id="9a889-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="9a889-104">Bu kılavuz, API için 1 sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="9a889-104">This guide is for version 1 of the API.</span></span> <span data-ttu-id="9a889-105">Sürüm 2 için [ **bu belgesine bakın**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="9a889-105">For version 2, [**refer to this document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="9a889-106">Sürüm 2 artık tercih edilen bu API sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="9a889-106">Version 2 is now the preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="9a889-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9a889-107">Overview</span></span>
<span data-ttu-id="9a889-108">Metin analizi API metin analizi paketidir [web Hizmetleri](https://datamarket.azure.com/dataset/amla/text-analytics) Azure Machine Learning ile oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9a889-108">The Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="9a889-109">API düşünceleri analiz, anahtar tümcecik ayıklama, dil algılama ve konu algılama gibi görevler için yapılandırılmamış metin analiz etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9a889-109">The API can be used to analyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="9a889-110">Bu API kullanmak için hiçbir eğitim verisi gereklidir: yalnızca metin verilerinizi getirin.</span><span class="sxs-lookup"><span data-stu-id="9a889-110">No training data is needed to use this API: just bring your text data.</span></span> <span data-ttu-id="9a889-111">Bu API Gelişmiş doğal dil teknikleri işleme sınıfı tahminleri en iyi teslim etmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="9a889-111">This API uses advanced natural language processing techniques to deliver best in class predictions.</span></span>

<span data-ttu-id="9a889-112">Eylem metin analizleri görebileceğinizi bizim [gösteri sitesi](https://text-analytics-demo.azurewebsites.net/), ayrıca bulabileceğiniz [örnekleri](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) C# ve Python metin analizi uygulamak nasıl.</span><span class="sxs-lookup"><span data-stu-id="9a889-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how to implement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="9a889-113">Duygu analizi</span><span class="sxs-lookup"><span data-stu-id="9a889-113">Sentiment analysis</span></span>
<span data-ttu-id="9a889-114">API, 0 ve 1 arasında sayısal bir puan döndürür.</span><span class="sxs-lookup"><span data-stu-id="9a889-114">The API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="9a889-115">Puanları 0 yakın negatif düşünceleri belirtmek sırada 1 yakın puanları pozitif düşünceleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="9a889-115">Scores close to 1 indicate positive sentiment, while scores close to 0 indicate negative sentiment.</span></span> <span data-ttu-id="9a889-116">Yaklaşım puanı, sınıflandırma teknikleri kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9a889-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="9a889-117">Giriş özellikleri sınıflandırıcı n-gram, konuşma bölümü etiketleri ve word eklerinin oluşturulan özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="9a889-117">The input features to the classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="9a889-118">Şu anda, İngilizce yalnızca desteklenen dilidir.</span><span class="sxs-lookup"><span data-stu-id="9a889-118">Currently, English is the only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="9a889-119">Anahtar tümcecik ayıklama</span><span class="sxs-lookup"><span data-stu-id="9a889-119">Key phrase extraction</span></span>
<span data-ttu-id="9a889-120">API, giriş metnindeki başlıca konuşma noktalarını gösteren bir dize listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="9a889-120">The API returns a list of strings denoting the key talking points in the input text.</span></span> <span data-ttu-id="9a889-121">Microsoft Office’in kapsamlı Doğal Dil İşleme araç setinden alınan teknikleri kullanırız.</span><span class="sxs-lookup"><span data-stu-id="9a889-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="9a889-122">Şu anda, İngilizce yalnızca desteklenen dilidir.</span><span class="sxs-lookup"><span data-stu-id="9a889-122">Currently, English is the only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="9a889-123">Dil algılama</span><span class="sxs-lookup"><span data-stu-id="9a889-123">Language detection</span></span>
<span data-ttu-id="9a889-124">API, 0 ve 1 arasında algılanan dil ve sayısal bir puan döndürür.</span><span class="sxs-lookup"><span data-stu-id="9a889-124">The API returns the detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="9a889-125">Puanın 1’e yakın olması, tanımlanan dilin %100 olasılıkla doğru olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="9a889-125">Scores close to 1 indicate 100% certainty that the identified language is true.</span></span> <span data-ttu-id="9a889-126">Toplamda 120 dil desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9a889-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="9a889-127">Konu algılama</span><span class="sxs-lookup"><span data-stu-id="9a889-127">Topic detection</span></span>
<span data-ttu-id="9a889-128">Bu konular listesini görmek için üst algılanan döndüren metin kayıtları gönderilen yeni yayımlanmış bir API'dir.</span><span class="sxs-lookup"><span data-stu-id="9a889-128">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="9a889-129">Konular, bir veya daha fazla ilgili sözcükten oluşan bir anahtar ifade ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9a889-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="9a889-130">Bu API en az 100 metin kaydının gönderilmesini gerektirir, ancak yüzlerce veya binlerce kayıt içindeki konuları algılayacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9a889-130">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span> <span data-ttu-id="9a889-131">Bu API’de gönderilen metin kaydı başına 1 işlem ücreti uygulandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9a889-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="9a889-132">API incelemeler ve kullanıcı geri bildirim gibi kısa, İnsan yazılı metin için iyi çalışmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9a889-132">The API is designed to work well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="9a889-133">API tanımı</span><span class="sxs-lookup"><span data-stu-id="9a889-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="9a889-134">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="9a889-134">Headers</span></span>
<span data-ttu-id="9a889-135">Şu şekilde olmalıdır isteğinizin içinde doğru üstbilgileri eklediğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="9a889-135">Ensure that you include the correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="9a889-136">Hesabınızdaki hesap anahtarınızı bulabilirsiniz [Azure veri Pazar](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="9a889-136">You can find your account key from your account in the [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="9a889-137">Şu anda yalnızca JSON için girdi ve çıktı biçimleri kabul edildiğini not edin.</span><span class="sxs-lookup"><span data-stu-id="9a889-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="9a889-138">XML desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9a889-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="9a889-139">Tek bir yanıt API'leri</span><span class="sxs-lookup"><span data-stu-id="9a889-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="9a889-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="9a889-140">GetSentiment</span></span>
<span data-ttu-id="9a889-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="9a889-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="9a889-142">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="9a889-142">**Example request**</span></span>

<span data-ttu-id="9a889-143">Çağrısında biz "Hello World" ifadesi düşünceleri analize isteyen:</span><span class="sxs-lookup"><span data-stu-id="9a889-143">In the call below, we are requesting sentiment analysis for the phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="9a889-144">Bu gibi bir yanıt döndürür:</span><span class="sxs-lookup"><span data-stu-id="9a889-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="9a889-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="9a889-145">GetKeyPhrases</span></span>
<span data-ttu-id="9a889-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="9a889-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="9a889-147">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="9a889-147">**Example request**</span></span>

<span data-ttu-id="9a889-148">Şu çağrısında biz anahtar sözcükler metinde "Bu, benzersiz dekorasyonu ve kolay personeli ile kalmak için harika bir otel" bulundu isteyen:</span><span class="sxs-lookup"><span data-stu-id="9a889-148">In the call below, we are requesting the key phrases found in the text "It was a wonderful hotel to stay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="9a889-149">Bu gibi bir yanıt döndürür:</span><span class="sxs-lookup"><span data-stu-id="9a889-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="9a889-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="9a889-150">GetLanguage</span></span>
<span data-ttu-id="9a889-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="9a889-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="9a889-152">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="9a889-152">**Example request**</span></span>

<span data-ttu-id="9a889-153">Aşağıdaki GET çağrısında biz metindeki anahtar sözcükler düşünceleri için istekte *Hello World*</span><span class="sxs-lookup"><span data-stu-id="9a889-153">In the GET call below, we are requesting for the sentiment for the key phrases in the text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="9a889-154">Bu gibi bir yanıt döndürür:</span><span class="sxs-lookup"><span data-stu-id="9a889-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="9a889-155">**İsteğe bağlı parametreler**</span><span class="sxs-lookup"><span data-stu-id="9a889-155">**Optional parameters**</span></span>

<span data-ttu-id="9a889-156">`NumberOfLanguagesToDetect`İsteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="9a889-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="9a889-157">Varsayılan değer 1'dir.</span><span class="sxs-lookup"><span data-stu-id="9a889-157">The default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="9a889-158">Batch API'leri</span><span class="sxs-lookup"><span data-stu-id="9a889-158">Batch APIs</span></span>
<span data-ttu-id="9a889-159">Metin analizi hizmeti düşünceleri ve anahtar tümcecik ayıklamaları toplu iş modunda yapmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9a889-159">The Text Analytics service allows you to do sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="9a889-160">Kayıtların her birinde bir işlem olarak sayıları skoru unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9a889-160">Note that each of the records scored counts as one transaction.</span></span> <span data-ttu-id="9a889-161">Tek bir çağrı 1000 kayıtlarında düşünceleri isterse bir örnek olarak, 1000 işlemleri düşülür.</span><span class="sxs-lookup"><span data-stu-id="9a889-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="9a889-162">Sisteme girildiğinde kimlikleri sistem tarafından döndürülen kimlikleri olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9a889-162">Note that the IDs entered into the system are the IDs returned by the system.</span></span> <span data-ttu-id="9a889-163">Web hizmeti, bu kimlikleri benzersiz denetlemez.</span><span class="sxs-lookup"><span data-stu-id="9a889-163">The web service does not check that these IDs are unique.</span></span> <span data-ttu-id="9a889-164">Benzersizlik doğrulamak için arayan sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="9a889-164">It is the responsibility of the caller to verify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="9a889-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="9a889-165">GetSentimentBatch</span></span>
<span data-ttu-id="9a889-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="9a889-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="9a889-167">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="9a889-167">**Example request**</span></span>

<span data-ttu-id="9a889-168">POST çağrısına biz "Hello World", "Merhaba Foo World" ve "Merhaba My World" istek gövdesinde tümcecikleri düşüncelerin için istekte:</span><span class="sxs-lookup"><span data-stu-id="9a889-168">In the POST call below, we are requesting for the sentiments of the phrases "Hello World", "Hello Foo World" and "Hello My World" in the body of the request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="9a889-169">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="9a889-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="9a889-170">Yanıtta metin kimlikleri ile ilişkilendirilmiş puanları listesini alın:</span><span class="sxs-lookup"><span data-stu-id="9a889-170">In the response below, you get the list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="9a889-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="9a889-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="9a889-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="9a889-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="9a889-173">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="9a889-173">**Example request**</span></span>

<span data-ttu-id="9a889-174">Bu örnekte, biz aşağıdaki metinleri anahtar tümcecikleri düşüncelerin listesi için istekte:</span><span class="sxs-lookup"><span data-stu-id="9a889-174">In this example, we are requesting for the list of sentiments for the key phrases in the following texts:</span></span> 

* <span data-ttu-id="9a889-175">", Benzersiz dekorasyonu ve kolay personeli ile kalmak için harika bir otel oluştu"</span><span class="sxs-lookup"><span data-stu-id="9a889-175">"It was a wonderful hotel to stay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="9a889-176">"Çok ilginç konuşmaları ile harika bir yapı konferans oluştu"</span><span class="sxs-lookup"><span data-stu-id="9a889-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="9a889-177">"Trafiği korkunç, üç havaalanı giderek saat harcanan"</span><span class="sxs-lookup"><span data-stu-id="9a889-177">"The traffic was terrible, I spent three hours going to the airport"</span></span>

<span data-ttu-id="9a889-178">Bu istekte bir uç nokta POST çağrısına olarak:</span><span class="sxs-lookup"><span data-stu-id="9a889-178">This request is made as a POST call to the endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="9a889-179">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="9a889-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel to stay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"The traffic was terrible, I spent three hours going to the airport"}
    ]}

<span data-ttu-id="9a889-180">Yanıtta metninizi kimlikleri ile ilişkili anahtar tümcecikleri listesini alın:</span><span class="sxs-lookup"><span data-stu-id="9a889-180">In the response below, you get the list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="9a889-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="9a889-181">GetLanguageBatch</span></span>

<span data-ttu-id="9a889-182">İki metin girdi için dil algılama POST çağrısına biz isteyen:</span><span class="sxs-lookup"><span data-stu-id="9a889-182">In the POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="9a889-183">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="9a889-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="9a889-184">Bu, aşağıdaki yanıtı burada İngilizce ilk giriş ve Fransızca'nın ikinci girişinde algılandığında döndürür:</span><span class="sxs-lookup"><span data-stu-id="9a889-184">This returns the following response, where English is detected in the first input and French in the second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="9a889-185">Konu algılama API'leri</span><span class="sxs-lookup"><span data-stu-id="9a889-185">Topic Detection APIs</span></span>
<span data-ttu-id="9a889-186">Bu konular listesini görmek için üst algılanan döndüren metin kayıtları gönderilen yeni yayımlanmış bir API'dir.</span><span class="sxs-lookup"><span data-stu-id="9a889-186">This is a newly released API which returns the top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="9a889-187">Konular, bir veya daha fazla ilgili sözcükten oluşan bir anahtar ifade ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9a889-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="9a889-188">Bu API’de gönderilen metin kaydı başına 1 işlem ücreti uygulandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9a889-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="9a889-189">Bu API en az 100 metin kaydının gönderilmesini gerektirir, ancak yüzlerce veya binlerce kayıt içindeki konuları algılayacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9a889-189">This API requires a minimum of 100 text records to be submitted, but is designed to detect topics across hundreds to thousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="9a889-190">Konular – gönderme iş</span><span class="sxs-lookup"><span data-stu-id="9a889-190">Topics – Submit job</span></span>
<span data-ttu-id="9a889-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="9a889-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="9a889-192">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="9a889-192">**Example request**</span></span>

<span data-ttu-id="9a889-193">Aşağıdaki POST çağrısında biz 100 makaleler, burada ilk ve son giriş makaleleri gösterilir ve iki StopPhrases dahil edilen bir dizi konuları istiyor.</span><span class="sxs-lookup"><span data-stu-id="9a889-193">In the POST call below, we are requesting topics for a set of 100 articles, where the first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="9a889-194">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="9a889-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved the food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated the decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="9a889-195">Yanıtta gönderilen iş için JobId alın:</span><span class="sxs-lookup"><span data-stu-id="9a889-195">In the response below, you get the JobId for the submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="9a889-196">Tek sözcük veya konuları döndürülmemesi gereken birden çok word tümcecikleri listesi.</span><span class="sxs-lookup"><span data-stu-id="9a889-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="9a889-197">Çok genel konular filtrelemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9a889-197">Can be used to filter out very generic topics.</span></span> <span data-ttu-id="9a889-198">Örneğin, otel incelemeleri hakkında bir veri kümesinde duyarlı stop deyimleri "otel" ve "hostel" olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a889-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="9a889-199">Konular – iş sonuçları için yoklama</span><span class="sxs-lookup"><span data-stu-id="9a889-199">Topics – Poll for job results</span></span>
<span data-ttu-id="9a889-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="9a889-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="9a889-201">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="9a889-201">**Example request**</span></span>

<span data-ttu-id="9a889-202">Sonuçları getirmek için 'Gönderme iş' adımdan döndürülen JobId geçirin.</span><span class="sxs-lookup"><span data-stu-id="9a889-202">Pass the JobId returned from the ‘Submit job’ step to fetch the results.</span></span> <span data-ttu-id="9a889-203">Durum kadar dakikada Bu uç noktasını çağırmak öneririz 'Tamamlandı' yanıtta =.</span><span class="sxs-lookup"><span data-stu-id="9a889-203">We recommend that you call this endpoint every minute until Status=’Complete’ in the response.</span></span> <span data-ttu-id="9a889-204">Tam ya da binlerce kayıtları işleriyle için uzun bir iş için yaklaşık 10 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="9a889-204">It will take around 10 mins for a job to complete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="9a889-205">Bunu işlerken yanıt şu şekilde olacaktır:</span><span class="sxs-lookup"><span data-stu-id="9a889-205">While it is processing, the response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="9a889-206">API çıktı şu biçimde JSON biçiminde döndürür:</span><span class="sxs-lookup"><span data-stu-id="9a889-206">The API returns output in JSON format in the following format:</span></span>

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


<span data-ttu-id="9a889-207">Tüm yanıt için özellikler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9a889-207">The properties for each part of the response are as follows:</span></span>

<span data-ttu-id="9a889-208">**TopicInfo özellikleri**</span><span class="sxs-lookup"><span data-stu-id="9a889-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="9a889-209">Anahtar</span><span class="sxs-lookup"><span data-stu-id="9a889-209">Key</span></span> | <span data-ttu-id="9a889-210">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9a889-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a889-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="9a889-211">TopicId</span></span> |<span data-ttu-id="9a889-212">Her konu için benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="9a889-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="9a889-213">Puan</span><span class="sxs-lookup"><span data-stu-id="9a889-213">Score</span></span> |<span data-ttu-id="9a889-214">Konuya atanan kayıt sayısı.</span><span class="sxs-lookup"><span data-stu-id="9a889-214">Count of records assigned to topic.</span></span> |
| <span data-ttu-id="9a889-215">Anahtar cümlesi</span><span class="sxs-lookup"><span data-stu-id="9a889-215">KeyPhrase</span></span> |<span data-ttu-id="9a889-216">Bir summarizing sözcük veya tümcecik konu için.</span><span class="sxs-lookup"><span data-stu-id="9a889-216">A summarizing word or phrase for the topic.</span></span> <span data-ttu-id="9a889-217">1 veya birden çok sözcük olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a889-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="9a889-218">**TopicAssignment özellikleri**</span><span class="sxs-lookup"><span data-stu-id="9a889-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="9a889-219">Anahtar</span><span class="sxs-lookup"><span data-stu-id="9a889-219">Key</span></span> | <span data-ttu-id="9a889-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9a889-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9a889-221">Kimlik</span><span class="sxs-lookup"><span data-stu-id="9a889-221">Id</span></span> |<span data-ttu-id="9a889-222">Kaydı için tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="9a889-222">Identifier for the record.</span></span> <span data-ttu-id="9a889-223">Girdide bulunan kimliği karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="9a889-223">Equates to the ID included in the input.</span></span> |
| <span data-ttu-id="9a889-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="9a889-224">TopicId</span></span> |<span data-ttu-id="9a889-225">Kayıt atandı konu kimliği.</span><span class="sxs-lookup"><span data-stu-id="9a889-225">The topic ID which the record has been assigned to.</span></span> |
| <span data-ttu-id="9a889-226">uzaklık</span><span class="sxs-lookup"><span data-stu-id="9a889-226">Distance</span></span> |<span data-ttu-id="9a889-227">GÜVENİRLİK kaydı konuya ait.</span><span class="sxs-lookup"><span data-stu-id="9a889-227">Confidence that the record belongs to the topic.</span></span> <span data-ttu-id="9a889-228">Sıfıra yakın uzaklığı daha yüksek güvenilirlik gösterir.</span><span class="sxs-lookup"><span data-stu-id="9a889-228">Distance closer to zero indicates higher confidence.</span></span> |

