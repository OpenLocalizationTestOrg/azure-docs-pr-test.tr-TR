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
# <a name="machine-learning-apis-text-analytics-for-sentiment-key-phrase-extraction-language-detection-and-topic-detection"></a><span data-ttu-id="332f8-103">Machine Learning API’leri: Yaklaşım, Anahtar İfade Ayıklama, Dil Algılama ve Konu Algılama için Metin Analizi</span><span class="sxs-lookup"><span data-stu-id="332f8-103">Machine Learning APIs: Text Analytics for Sentiment, Key Phrase Extraction, Language Detection and Topic Detection</span></span>
> [!NOTE]
> <span data-ttu-id="332f8-104">Bu kılavuz hello API için 1 sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="332f8-104">This guide is for version 1 of hello API.</span></span> <span data-ttu-id="332f8-105">Sürüm 2 için [ **toothis belge başvuran**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="332f8-105">For version 2, [**refer toothis document**](../cognitive-services/cognitive-services-text-analytics-quick-start.md).</span></span> <span data-ttu-id="332f8-106">Sürüm 2 şimdi hello tercih edilen bu API sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="332f8-106">Version 2 is now hello preferred version of this API.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="332f8-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="332f8-107">Overview</span></span>
<span data-ttu-id="332f8-108">Merhaba metin Analytics API olan metin analizi dizisi [web Hizmetleri](https://datamarket.azure.com/dataset/amla/text-analytics) Azure Machine Learning ile oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="332f8-108">hello Text Analytics API is a suite of text analytics [web services](https://datamarket.azure.com/dataset/amla/text-analytics) built with Azure Machine Learning.</span></span> <span data-ttu-id="332f8-109">Merhaba API kullanılan tooanalyze olabilir düşünceleri analiz, anahtar tümcecik ayıklama, dil algılama ve konu algılama gibi görevler için yapılandırılmamış metin.</span><span class="sxs-lookup"><span data-stu-id="332f8-109">hello API can be used tooanalyze unstructured text for tasks such as sentiment analysis, key phrase extraction, language detection and topic detection.</span></span> <span data-ttu-id="332f8-110">Bu API toouse veriler hiçbir eğitim gerekli: yalnızca metin verilerinizi getirin.</span><span class="sxs-lookup"><span data-stu-id="332f8-110">No training data is needed toouse this API: just bring your text data.</span></span> <span data-ttu-id="332f8-111">Bu API, Gelişmiş doğal dil teknikleri toodeliver en iyi sınıf tahminleri işleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="332f8-111">This API uses advanced natural language processing techniques toodeliver best in class predictions.</span></span>

<span data-ttu-id="332f8-112">Eylem metin analizleri görebileceğinizi bizim [gösteri sitesi](https://text-analytics-demo.azurewebsites.net/), ayrıca bulabileceğiniz [örnekleri](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) nasıl tooimplement metin analizi C# ve Python.</span><span class="sxs-lookup"><span data-stu-id="332f8-112">You can see text analytics in action on our [demo site](https://text-analytics-demo.azurewebsites.net/), where you will also find [samples](https://text-analytics-demo.azurewebsites.net/Home/SampleCode) on how tooimplement text analytics in C# and Python.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

- - -
## <a name="sentiment-analysis"></a><span data-ttu-id="332f8-113">Duygu analizi</span><span class="sxs-lookup"><span data-stu-id="332f8-113">Sentiment analysis</span></span>
<span data-ttu-id="332f8-114">Merhaba API 0 ve 1 arasında sayısal bir puan döndürür.</span><span class="sxs-lookup"><span data-stu-id="332f8-114">hello API returns a numeric score between 0 & 1.</span></span> <span data-ttu-id="332f8-115">Puanları Kapat too1 puanları Kapat too0 belirtmek sırada negatif düşünceleri pozitif düşünceleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="332f8-115">Scores close too1 indicate positive sentiment, while scores close too0 indicate negative sentiment.</span></span> <span data-ttu-id="332f8-116">Yaklaşım puanı, sınıflandırma teknikleri kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="332f8-116">Sentiment score is generated using classification techniques.</span></span> <span data-ttu-id="332f8-117">Merhaba giriş özellikleri toohello sınıflandırıcı n-gram, konuşma bölümü etiketleri ve word eklerinin oluşturulan özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="332f8-117">hello input features toohello classifier include n-grams, features generated from part-of-speech tags, and word embeddings.</span></span> <span data-ttu-id="332f8-118">Şu anda, İngilizce dil hello yalnızca desteklenen değil.</span><span class="sxs-lookup"><span data-stu-id="332f8-118">Currently, English is hello only supported language.</span></span>

## <a name="key-phrase-extraction"></a><span data-ttu-id="332f8-119">Anahtar tümcecik ayıklama</span><span class="sxs-lookup"><span data-stu-id="332f8-119">Key phrase extraction</span></span>
<span data-ttu-id="332f8-120">Merhaba API hello anahtar Konuşmayı noktaları hello giriş metin belirten dizelerinin listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="332f8-120">hello API returns a list of strings denoting hello key talking points in hello input text.</span></span> <span data-ttu-id="332f8-121">Microsoft Office’in kapsamlı Doğal Dil İşleme araç setinden alınan teknikleri kullanırız.</span><span class="sxs-lookup"><span data-stu-id="332f8-121">We employ techniques from Microsoft Office's sophisticated Natural Language Processing toolkit.</span></span> <span data-ttu-id="332f8-122">Şu anda, İngilizce dil hello yalnızca desteklenen değil.</span><span class="sxs-lookup"><span data-stu-id="332f8-122">Currently, English is hello only supported language.</span></span>

## <a name="language-detection"></a><span data-ttu-id="332f8-123">Dil algılama</span><span class="sxs-lookup"><span data-stu-id="332f8-123">Language detection</span></span>
<span data-ttu-id="332f8-124">Merhaba API hello algıladı dil ve 0 ve 1 arasında sayısal bir puan döndürür.</span><span class="sxs-lookup"><span data-stu-id="332f8-124">hello API returns hello detected language and a numeric score between 0 & 1.</span></span> <span data-ttu-id="332f8-125">Puanları Kapat too1% 100 çalışılarak tanımlanan hello dil doğru olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="332f8-125">Scores close too1 indicate 100% certainty that hello identified language is true.</span></span> <span data-ttu-id="332f8-126">Toplamda 120 dil desteklenir.</span><span class="sxs-lookup"><span data-stu-id="332f8-126">A total of 120 languages are supported.</span></span>

## <a name="topic-detection"></a><span data-ttu-id="332f8-127">Konu algılama</span><span class="sxs-lookup"><span data-stu-id="332f8-127">Topic detection</span></span>
<span data-ttu-id="332f8-128">Bu üst algılanan konuları gönderilen metin kayıtların listesini hello döndüren yeni yayımlanmış bir API'dir.</span><span class="sxs-lookup"><span data-stu-id="332f8-128">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="332f8-129">Konular, bir veya daha fazla ilgili sözcükten oluşan bir anahtar ifade ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="332f8-129">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="332f8-130">Bu API en az 100 metin gönderilen toobe kaydeder, ancak tasarlanmış toodetect konuları yüzlerce arasında olduğu gerektiriyor kayıtların toothousands.</span><span class="sxs-lookup"><span data-stu-id="332f8-130">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span> <span data-ttu-id="332f8-131">Bu API’de gönderilen metin kaydı başına 1 işlem ücreti uygulandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="332f8-131">Note that this API charges 1 transaction per text record submitted.</span></span> <span data-ttu-id="332f8-132">Merhaba API iyi incelemeler ve kullanıcı geri bildirim gibi metin yazılmış kısa, İnsan için tasarlanmış toowork ' dir.</span><span class="sxs-lookup"><span data-stu-id="332f8-132">hello API is designed toowork well for short, human written text such as reviews and user feedback.</span></span>

- - -
## <a name="api-definition"></a><span data-ttu-id="332f8-133">API tanımı</span><span class="sxs-lookup"><span data-stu-id="332f8-133">API Definition</span></span>
### <a name="headers"></a><span data-ttu-id="332f8-134">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="332f8-134">Headers</span></span>
<span data-ttu-id="332f8-135">Şu şekilde olmalıdır isteğinizin içinde hello doğru üstbilgileri eklediğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="332f8-135">Ensure that you include hello correct headers in your request, which should be as follows:</span></span>

    Authorization: Basic <creds>
    Accept: application/json

    Where <creds> = ConvertToBase64(“AccountKey:” + yourActualAccountKey);  

<span data-ttu-id="332f8-136">Hesap anahtarınızı hesabınızdan hello bulabilirsiniz [Azure veri Pazar](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="332f8-136">You can find your account key from your account in hello [Azure Data Market](https://datamarket.azure.com/account/keys).</span></span> <span data-ttu-id="332f8-137">Şu anda yalnızca JSON için girdi ve çıktı biçimleri kabul edildiğini not edin.</span><span class="sxs-lookup"><span data-stu-id="332f8-137">Note that currently only JSON is accepted for input and output formats.</span></span> <span data-ttu-id="332f8-138">XML desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="332f8-138">XML is not supported.</span></span>

- - -
## <a name="single-response-apis"></a><span data-ttu-id="332f8-139">Tek bir yanıt API'leri</span><span class="sxs-lookup"><span data-stu-id="332f8-139">Single Response APIs</span></span>
### <a name="getsentiment"></a><span data-ttu-id="332f8-140">GetSentiment</span><span class="sxs-lookup"><span data-stu-id="332f8-140">GetSentiment</span></span>
<span data-ttu-id="332f8-141">**URL**</span><span class="sxs-lookup"><span data-stu-id="332f8-141">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment

<span data-ttu-id="332f8-142">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="332f8-142">**Example request**</span></span>

<span data-ttu-id="332f8-143">Merhaba çağrısında aşağıdaki biz düşünceleri analiz hello deyimi "Hello World" istekte:</span><span class="sxs-lookup"><span data-stu-id="332f8-143">In hello call below, we are requesting sentiment analysis for hello phrase "Hello World":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentiment?Text=hello+world

<span data-ttu-id="332f8-144">Bu gibi bir yanıt döndürür:</span><span class="sxs-lookup"><span data-stu-id="332f8-144">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
        "Score":1.0
    }

- - -
### <a name="getkeyphrases"></a><span data-ttu-id="332f8-145">GetKeyPhrases</span><span class="sxs-lookup"><span data-stu-id="332f8-145">GetKeyPhrases</span></span>
<span data-ttu-id="332f8-146">**URL**</span><span class="sxs-lookup"><span data-stu-id="332f8-146">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases

<span data-ttu-id="332f8-147">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="332f8-147">**Example request**</span></span>

<span data-ttu-id="332f8-148">Merhaba çağrısında aşağıdaki biz hello anahtar tümcecikleri hello metinde "Bu harika bir otel toostay adresindeki, benzersiz dekorasyonu ve kolay personeli ile" bulundu isteyen:</span><span class="sxs-lookup"><span data-stu-id="332f8-148">In hello call below, we are requesting hello key phrases found in hello text "It was a wonderful hotel toostay at, with unique decor and friendly staff":</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrases?
    Text=It+was+a+wonderful+hotel+to+stay+at,+with+unique+decor+and+friendly+staff

<span data-ttu-id="332f8-149">Bu gibi bir yanıt döndürür:</span><span class="sxs-lookup"><span data-stu-id="332f8-149">This will return a response as follows:</span></span>

    {
      "odata.metadata":"https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/$metadata",
      "KeyPhrases":[
        "wonderful hotel",
        "unique decor",
        "friendly staff"
      ]
    }

- - -
### <a name="getlanguage"></a><span data-ttu-id="332f8-150">GetLanguage</span><span class="sxs-lookup"><span data-stu-id="332f8-150">GetLanguage</span></span>
<span data-ttu-id="332f8-151">**URL**</span><span class="sxs-lookup"><span data-stu-id="332f8-151">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguage

<span data-ttu-id="332f8-152">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="332f8-152">**Example request**</span></span>

<span data-ttu-id="332f8-153">Merhaba GET çağrı aşağıdaki biz hello anahtar tümcecikleri hello metin hello düşünceleri için istekte *Hello World*</span><span class="sxs-lookup"><span data-stu-id="332f8-153">In hello GET call below, we are requesting for hello sentiment for hello key phrases in hello text *Hello World*</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguages?
    Text=Hello+World

<span data-ttu-id="332f8-154">Bu gibi bir yanıt döndürür:</span><span class="sxs-lookup"><span data-stu-id="332f8-154">This will return a response as follows:</span></span>

    {
      "UnknownLanguage": false,
      "DetectedLanguages": [{
        "Name": "English",
        "Iso6391Name": "en",
        "Score": 1.0
      }]
    }

<span data-ttu-id="332f8-155">**İsteğe bağlı parametreler**</span><span class="sxs-lookup"><span data-stu-id="332f8-155">**Optional parameters**</span></span>

<span data-ttu-id="332f8-156">`NumberOfLanguagesToDetect`İsteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="332f8-156">`NumberOfLanguagesToDetect` is an optional parameter.</span></span> <span data-ttu-id="332f8-157">Merhaba, 1 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="332f8-157">hello default is 1.</span></span>

- - -
## <a name="batch-apis"></a><span data-ttu-id="332f8-158">Batch API'leri</span><span class="sxs-lookup"><span data-stu-id="332f8-158">Batch APIs</span></span>
<span data-ttu-id="332f8-159">Merhaba metin Analytics hizmeti, toodo düşünceleri ve anahtar tümcecik ayıklamaları toplu iş modunda sağlar.</span><span class="sxs-lookup"><span data-stu-id="332f8-159">hello Text Analytics service allows you toodo sentiment and key-phrase extractions in batch mode.</span></span> <span data-ttu-id="332f8-160">Merhaba kayıtların her birinde bir işlem olarak sayıları skoru unutmayın.</span><span class="sxs-lookup"><span data-stu-id="332f8-160">Note that each of hello records scored counts as one transaction.</span></span> <span data-ttu-id="332f8-161">Tek bir çağrı 1000 kayıtlarında düşünceleri isterse bir örnek olarak, 1000 işlemleri düşülür.</span><span class="sxs-lookup"><span data-stu-id="332f8-161">As an example, if you request sentiment for 1000 records in a single call, 1000 transactions will be deducted.</span></span>

<span data-ttu-id="332f8-162">Merhaba kimlikleri hello sisteme girildiğinde Not hello sistem tarafından döndürülen hello kimlikleri aynıdır.</span><span class="sxs-lookup"><span data-stu-id="332f8-162">Note that hello IDs entered into hello system are hello IDs returned by hello system.</span></span> <span data-ttu-id="332f8-163">Merhaba web hizmeti, bu kimlikleri benzersiz denetlemez.</span><span class="sxs-lookup"><span data-stu-id="332f8-163">hello web service does not check that these IDs are unique.</span></span> <span data-ttu-id="332f8-164">Bunu hello hello arayan tooverify benzersizlik sorumluluğundadır.</span><span class="sxs-lookup"><span data-stu-id="332f8-164">It is hello responsibility of hello caller tooverify uniqueness.</span></span> 

### <a name="getsentimentbatch"></a><span data-ttu-id="332f8-165">GetSentimentBatch</span><span class="sxs-lookup"><span data-stu-id="332f8-165">GetSentimentBatch</span></span>
<span data-ttu-id="332f8-166">**URL**</span><span class="sxs-lookup"><span data-stu-id="332f8-166">**URL**</span></span>    

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch

<span data-ttu-id="332f8-167">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="332f8-167">**Example request**</span></span>

<span data-ttu-id="332f8-168">Biz hello düşüncelerin hello tümce "Hello World", "Hello World Foo" ve "Merhaba My World" Merhaba hello istek gövdesi için istekte aşağıda Hello POST arayın:</span><span class="sxs-lookup"><span data-stu-id="332f8-168">In hello POST call below, we are requesting for hello sentiments of hello phrases "Hello World", "Hello Foo World" and "Hello My World" in hello body of hello request:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetSentimentBatch 

<span data-ttu-id="332f8-169">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="332f8-169">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"hello world"},
        {"Id":"2","Text":"hello foo world"},
        {"Id":"3","Text":"hello my world"},
    ]}

<span data-ttu-id="332f8-170">Aşağıdaki Hello yanıt olarak metin kimlikleri ile ilişkilendirilmiş puanları hello listesini alın:</span><span class="sxs-lookup"><span data-stu-id="332f8-170">In hello response below, you get hello list of scores associated with your text Ids:</span></span>

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
### <a name="getkeyphrasesbatch"></a><span data-ttu-id="332f8-171">GetKeyPhrasesBatch</span><span class="sxs-lookup"><span data-stu-id="332f8-171">GetKeyPhrasesBatch</span></span>
<span data-ttu-id="332f8-172">**URL**</span><span class="sxs-lookup"><span data-stu-id="332f8-172">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="332f8-173">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="332f8-173">**Example request**</span></span>

<span data-ttu-id="332f8-174">Bu örnekte, biz metinleri aşağıdaki hello hello anahtar tümcecikleri düşüncelerin hello listesi için istekte:</span><span class="sxs-lookup"><span data-stu-id="332f8-174">In this example, we are requesting for hello list of sentiments for hello key phrases in hello following texts:</span></span> 

* <span data-ttu-id="332f8-175">"Konumunda, benzersiz dekorasyonu ve kolay personeli ile harika bir otel toostay oluştu"</span><span class="sxs-lookup"><span data-stu-id="332f8-175">"It was a wonderful hotel toostay at, with unique decor and friendly staff"</span></span>
* <span data-ttu-id="332f8-176">"Çok ilginç konuşmaları ile harika bir yapı konferans oluştu"</span><span class="sxs-lookup"><span data-stu-id="332f8-176">"It was an amazing build conference, with very interesting talks"</span></span>
* <span data-ttu-id="332f8-177">"hello trafiği korkunç, üç toohello havaalanı giderek saat harcanan"</span><span class="sxs-lookup"><span data-stu-id="332f8-177">"hello traffic was terrible, I spent three hours going toohello airport"</span></span>

<span data-ttu-id="332f8-178">Bu istek bir POST çağrısı toohello uç noktası olarak yapılır:</span><span class="sxs-lookup"><span data-stu-id="332f8-178">This request is made as a POST call toohello endpoint:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetKeyPhrasesBatch

<span data-ttu-id="332f8-179">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="332f8-179">Request body:</span></span>

    {"Inputs":
    [
        {"Id":"1","Text":"It was a wonderful hotel toostay at, with unique decor and friendly staff"},
        {"Id":"2","Text":"It was an amazing build conference, with very interesting talks"},
        {"Id":"3","Text":"hello traffic was terrible, I spent three hours going toohello airport"}
    ]}

<span data-ttu-id="332f8-180">Aşağıdaki Hello yanıt olarak metninizi kimlikleri ile ilişkili anahtar tümcecikleri hello listesini alın:</span><span class="sxs-lookup"><span data-stu-id="332f8-180">In hello response below, you get hello list of key phrases associated with your text Ids:</span></span>

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
### <a name="getlanguagebatch"></a><span data-ttu-id="332f8-181">GetLanguageBatch</span><span class="sxs-lookup"><span data-stu-id="332f8-181">GetLanguageBatch</span></span>

<span data-ttu-id="332f8-182">Merhaba POST çağrısında aşağıdaki biz iki metin girdi için dil algılama isteyen:</span><span class="sxs-lookup"><span data-stu-id="332f8-182">In hello POST call below, we are requesting language detection for two text inputs:</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetLanguageBatch

<span data-ttu-id="332f8-183">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="332f8-183">Request body:</span></span>

    {
      "Inputs": [
        {"Text": "hello world", "Id": "1"},
        {"Text": "c'est la vie", "Id": "2"}
      ]
    }

<span data-ttu-id="332f8-184">Bu yanıt, burada İngilizce ilk giriş hello ve Fransızca hello ikinci giriş algılandığında aşağıdaki hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="332f8-184">This returns hello following response, where English is detected in hello first input and French in hello second input:</span></span>

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
## <a name="topic-detection-apis"></a><span data-ttu-id="332f8-185">Konu algılama API'leri</span><span class="sxs-lookup"><span data-stu-id="332f8-185">Topic Detection APIs</span></span>
<span data-ttu-id="332f8-186">Bu üst algılanan konuları gönderilen metin kayıtların listesini hello döndüren yeni yayımlanmış bir API'dir.</span><span class="sxs-lookup"><span data-stu-id="332f8-186">This is a newly released API which returns hello top detected topics for a list of submitted text records.</span></span> <span data-ttu-id="332f8-187">Konular, bir veya daha fazla ilgili sözcükten oluşan bir anahtar ifade ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="332f8-187">A topic is identified with a key phrase, which can be one or more related words.</span></span> <span data-ttu-id="332f8-188">Bu API’de gönderilen metin kaydı başına 1 işlem ücreti uygulandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="332f8-188">Note that this API charges 1 transaction per text record submitted.</span></span>

<span data-ttu-id="332f8-189">Bu API en az 100 metin gönderilen toobe kaydeder, ancak tasarlanmış toodetect konuları yüzlerce arasında olduğu gerektiriyor kayıtların toothousands.</span><span class="sxs-lookup"><span data-stu-id="332f8-189">This API requires a minimum of 100 text records toobe submitted, but is designed toodetect topics across hundreds toothousands of records.</span></span>

### <a name="topics--submit-job"></a><span data-ttu-id="332f8-190">Konular – gönderme iş</span><span class="sxs-lookup"><span data-stu-id="332f8-190">Topics – Submit job</span></span>
<span data-ttu-id="332f8-191">**URL**</span><span class="sxs-lookup"><span data-stu-id="332f8-191">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection

<span data-ttu-id="332f8-192">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="332f8-192">**Example request**</span></span>

<span data-ttu-id="332f8-193">Merhaba POST çağrısında aşağıdaki biz burada hello ilk ve son makaleleri gösterilir ve iki StopPhrases dahil edilen giriş 100 makaleleri bir dizi konuları istiyor.</span><span class="sxs-lookup"><span data-stu-id="332f8-193">In hello POST call below, we are requesting topics for a set of 100 articles, where hello first and last input articles are shown, and two StopPhrases are included.</span></span>

    POST https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/StartTopicDetection HTTP/1.1

<span data-ttu-id="332f8-194">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="332f8-194">Request body:</span></span>

    {"Inputs":[
        {"Id":"1","Text":"I loved hello food at this restaurant"},
        ...,
        {"Id":"100","Text":"I hated hello decor"}
    ],
    "StopPhrases":[
        "restaurant", “visitor"
    ]}

<span data-ttu-id="332f8-195">Aşağıdaki Hello yanıt olarak hello gönderilen iş için hello JobId alın:</span><span class="sxs-lookup"><span data-stu-id="332f8-195">In hello response below, you get hello JobId for hello submitted job:</span></span>

    {
        "odata.metadata":"<url>",
        "JobId":"<JobId>"
    }

<span data-ttu-id="332f8-196">Tek sözcük veya konuları döndürülmemesi gereken birden çok word tümcecikleri listesi.</span><span class="sxs-lookup"><span data-stu-id="332f8-196">A list of single word or multiple word phrases which should not be returned as topics.</span></span> <span data-ttu-id="332f8-197">Çok genel konular çıkışı kullanılan toofilter olabilir.</span><span class="sxs-lookup"><span data-stu-id="332f8-197">Can be used toofilter out very generic topics.</span></span> <span data-ttu-id="332f8-198">Örneğin, otel incelemeleri hakkında bir veri kümesinde duyarlı stop deyimleri "otel" ve "hostel" olabilir.</span><span class="sxs-lookup"><span data-stu-id="332f8-198">For example, in a dataset about hotel reviews, "hotel" and "hostel" may be sensible stop phrases.</span></span>  

### <a name="topics--poll-for-job-results"></a><span data-ttu-id="332f8-199">Konular – iş sonuçları için yoklama</span><span class="sxs-lookup"><span data-stu-id="332f8-199">Topics – Poll for job results</span></span>
<span data-ttu-id="332f8-200">**URL**</span><span class="sxs-lookup"><span data-stu-id="332f8-200">**URL**</span></span>

    https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult

<span data-ttu-id="332f8-201">**Örnek istek**</span><span class="sxs-lookup"><span data-stu-id="332f8-201">**Example request**</span></span>

<span data-ttu-id="332f8-202">JobId hello 'Gönderme iş' adım toofetch hello sonuçlarından döndürülen hello geçirin.</span><span class="sxs-lookup"><span data-stu-id="332f8-202">Pass hello JobId returned from hello ‘Submit job’ step toofetch hello results.</span></span> <span data-ttu-id="332f8-203">Durum kadar dakikada Bu uç noktasını çağırmak öneririz 'Tamamlandı' hello yanıtta =.</span><span class="sxs-lookup"><span data-stu-id="332f8-203">We recommend that you call this endpoint every minute until Status=’Complete’ in hello response.</span></span> <span data-ttu-id="332f8-204">İş toocomplete veya uzun süre binlerce kayıtları işleriyle yaklaşık 10 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="332f8-204">It will take around 10 mins for a job toocomplete, or longer for jobs with many thousands of records.</span></span>

    GET https://api.datamarket.azure.com/data.ashx/amla/text-analytics/v1/GetTopicDetectionResult?JobId=<JobId>


<span data-ttu-id="332f8-205">Bunu işlerken hello yanıt şu şekilde olacaktır:</span><span class="sxs-lookup"><span data-stu-id="332f8-205">While it is processing, hello response will be as follows:</span></span>

    {
        "odata.metadata":"<url>",
        "Status":"Running",
         "TopicInfo":[],
        "TopicAssignment":[],
        "Errors":[]
    }


<span data-ttu-id="332f8-206">Merhaba API çıktı biçimi aşağıdaki hello JSON biçiminde döndürür:</span><span class="sxs-lookup"><span data-stu-id="332f8-206">hello API returns output in JSON format in hello following format:</span></span>

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


<span data-ttu-id="332f8-207">Merhaba özellikleri hello yanıt her kısmı için aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="332f8-207">hello properties for each part of hello response are as follows:</span></span>

<span data-ttu-id="332f8-208">**TopicInfo özellikleri**</span><span class="sxs-lookup"><span data-stu-id="332f8-208">**TopicInfo properties**</span></span>

| <span data-ttu-id="332f8-209">Anahtar</span><span class="sxs-lookup"><span data-stu-id="332f8-209">Key</span></span> | <span data-ttu-id="332f8-210">Açıklama</span><span class="sxs-lookup"><span data-stu-id="332f8-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="332f8-211">TopicId</span><span class="sxs-lookup"><span data-stu-id="332f8-211">TopicId</span></span> |<span data-ttu-id="332f8-212">Her konu için benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="332f8-212">A unique identifier for each topic.</span></span> |
| <span data-ttu-id="332f8-213">Puan</span><span class="sxs-lookup"><span data-stu-id="332f8-213">Score</span></span> |<span data-ttu-id="332f8-214">Kayıt sayısı tootopic atanır.</span><span class="sxs-lookup"><span data-stu-id="332f8-214">Count of records assigned tootopic.</span></span> |
| <span data-ttu-id="332f8-215">Anahtar cümlesi</span><span class="sxs-lookup"><span data-stu-id="332f8-215">KeyPhrase</span></span> |<span data-ttu-id="332f8-216">Bir summarizing sözcük veya tümcecik hello konu için.</span><span class="sxs-lookup"><span data-stu-id="332f8-216">A summarizing word or phrase for hello topic.</span></span> <span data-ttu-id="332f8-217">1 veya birden çok sözcük olabilir.</span><span class="sxs-lookup"><span data-stu-id="332f8-217">Can be 1 or multiple words.</span></span> |

<span data-ttu-id="332f8-218">**TopicAssignment özellikleri**</span><span class="sxs-lookup"><span data-stu-id="332f8-218">**TopicAssignment properties**</span></span>

| <span data-ttu-id="332f8-219">Anahtar</span><span class="sxs-lookup"><span data-stu-id="332f8-219">Key</span></span> | <span data-ttu-id="332f8-220">Açıklama</span><span class="sxs-lookup"><span data-stu-id="332f8-220">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="332f8-221">Kimlik</span><span class="sxs-lookup"><span data-stu-id="332f8-221">Id</span></span> |<span data-ttu-id="332f8-222">Merhaba kaydı için tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="332f8-222">Identifier for hello record.</span></span> <span data-ttu-id="332f8-223">Merhaba girişinde dahil toohello kimliği karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="332f8-223">Equates toohello ID included in hello input.</span></span> |
| <span data-ttu-id="332f8-224">TopicId</span><span class="sxs-lookup"><span data-stu-id="332f8-224">TopicId</span></span> |<span data-ttu-id="332f8-225">Kayıt hello hello konu kimliği atandı.</span><span class="sxs-lookup"><span data-stu-id="332f8-225">hello topic ID which hello record has been assigned to.</span></span> |
| <span data-ttu-id="332f8-226">uzaklık</span><span class="sxs-lookup"><span data-stu-id="332f8-226">Distance</span></span> |<span data-ttu-id="332f8-227">Kayıt hello güvenirlik toohello konu aittir.</span><span class="sxs-lookup"><span data-stu-id="332f8-227">Confidence that hello record belongs toohello topic.</span></span> <span data-ttu-id="332f8-228">Uzaklık daha yakından toozero daha yüksek güvenilirlik gösterir.</span><span class="sxs-lookup"><span data-stu-id="332f8-228">Distance closer toozero indicates higher confidence.</span></span> |

