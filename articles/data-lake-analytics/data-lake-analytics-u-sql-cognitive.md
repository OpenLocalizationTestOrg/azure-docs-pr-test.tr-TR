---
title: "Azure Data Lake Analytics U-SQL Bilişsel özelliklerini kullanarak | Microsoft Docs"
description: "U-SQL Bilişsel yetenekleri Intelligence kullanmayı öğrenin"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: 019c1d53-4e61-4cad-9b2c-7a60307cbe19
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: f77329f9838d6e824afa7234de90f62257a004de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-the-cognitive-capabilities-of-u-sql"></a><span data-ttu-id="145cc-103">Öğretici: U-SQL Bilişsel yetenekleri ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="145cc-103">Tutorial: Get started with the Cognitive capabilities of U-SQL</span></span>

<span data-ttu-id="145cc-104">U-SQL için bilişsel özellikleri geliştiricilerin kendi büyük veri programlarda put Intelligence kullanmak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="145cc-104">Cognitive capabilities for U-SQL enable developers to use put intelligence in their big data programs.</span></span> <span data-ttu-id="145cc-105">Basit genel işleminde:</span><span class="sxs-lookup"><span data-stu-id="145cc-105">The overall process in simple:</span></span>

* <span data-ttu-id="145cc-106">U-SQL komut dosyası için bilişsel özelliklerini etkinleştirmek için referans DERLEMESİNİ deyimi kullanın</span><span class="sxs-lookup"><span data-stu-id="145cc-106">Use the REFERENCE ASSEMBLY statement to enable the cognitive features for the U-SQL Script</span></span>
* <span data-ttu-id="145cc-107">Bilişsel özellikleri kullanmak için işlem işlemini çağırın</span><span class="sxs-lookup"><span data-stu-id="145cc-107">Call the PROCESS operation to use the Cognitive capabilities</span></span> 

## <a name="imaging-scenarios"></a><span data-ttu-id="145cc-108">Görüntü oluşturma senaryoları</span><span class="sxs-lookup"><span data-stu-id="145cc-108">Imaging scenarios</span></span>

### <a name="example-image-tagging"></a><span data-ttu-id="145cc-109">Örnek: Görüntü etiketleme</span><span class="sxs-lookup"><span data-stu-id="145cc-109">Example: Image tagging</span></span>

<span data-ttu-id="145cc-110">Aşağıdaki örnek nesneleri görüntülerinde algılamak için görüntüleme yetenekleri uçtan uca kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="145cc-110">The following example shows an end-to-end use of the imaging capabilities to detect objects in images.</span></span>

    REFERENCE ASSEMBLY ImageCommon;
    REFERENCE ASSEMBLY FaceSdk;
    REFERENCE ASSEMBLY ImageEmotion;
    REFERENCE ASSEMBLY ImageTagging;
    REFERENCE ASSEMBLY ImageOcr;

    @imgs =
        EXTRACT FileName string, ImgData byte[]
        FROM @"/images/{FileName:*}.jpg"
        USING new Cognition.Vision.ImageExtractor();

    // Extract the number of objects on each image and tag them 
    @objects =
        PROCESS @imgs 
        PRODUCE FileName,
                NumObjects int,
                Tags string
        READONLY FileName
        USING new Cognition.Vision.ImageTagger();


### <a name="extract-emotions-from-human-faces"></a><span data-ttu-id="145cc-111">İnsan yüzeyleri duygular Ayıkla</span><span class="sxs-lookup"><span data-stu-id="145cc-111">Extract emotions from human faces</span></span> 

    @emotions =
        PROCESS @imgs
        PRODUCE FileName string,
                NumFaces int,
                Emotion string
        READONLY FileName
        USING new Cognition.Vision.EmotionAnalyzer();

### <a name="estimate-age-and-gender-for-human-faces"></a><span data-ttu-id="145cc-112">Geçerlilik süresi ve İnsan yüzeyleri cinsiyetiniz tahmin etme</span><span class="sxs-lookup"><span data-stu-id="145cc-112">Estimate age and gender for human faces</span></span>

    @faces = 
            PROCESS @imgs
            PRODUCE FileName,
                    NumFaces int,
                    FaceAge string,
                    FaceGender string
            READONLY FileName
            USING new Cognition.Vision.FaceDetector();

### <a name="detect-text-in-images-ocr"></a><span data-ttu-id="145cc-113">Görüntüleri (OCR) metnini Algıla</span><span class="sxs-lookup"><span data-stu-id="145cc-113">Detect text in Images (OCR)</span></span>

    @ocrs =
            PROCESS @imgs
            PRODUCE FileName,
                    Text string
            READONLY FileName
            USING new Cognition.Vision.OcrExtractor();

## <a name="text-scenarios"></a><span data-ttu-id="145cc-114">Metin senaryoları</span><span class="sxs-lookup"><span data-stu-id="145cc-114">Text scenarios</span></span>

### <a name="input-data"></a><span data-ttu-id="145cc-115">Giriş verisi</span><span class="sxs-lookup"><span data-stu-id="145cc-115">Input data</span></span>

<span data-ttu-id="145cc-116">Leo Tolstoy tarafından biz "War ve rahatlık" oluşan bir giriş olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="145cc-116">Assume that we have an input that consists of “War and Peace” by Leo Tolstoy.</span></span>

    REFERENCE ASSEMBLY [TextCommon];
    REFERENCE ASSEMBLY [TextSentiment];
    REFERENCE ASSEMBLY [TextKeyPhrase];

    @WarAndPeace =
        EXTRACT No int,
                Year string,
                Book string,
                Chapter string,
                Text string
        FROM @"/usqlext/samples/cognition/war_and_peace.csv"
        USING Extractors.Csv();

### <a name="extract-key-phrases-for-each-paragraph"></a><span data-ttu-id="145cc-117">Her paragraf için anahtar tümcecikleri Ayıkla</span><span class="sxs-lookup"><span data-stu-id="145cc-117">Extract key phrases for each paragraph</span></span>

    @keyphrase =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                KeyPhrase string
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.KeyPhraseExtractor();

    // Tokenize the key phrases.
    @kpsplits =
        SELECT No,
            Year,
            Book,
            Chapter,
            Text,
            T.KeyPhrase
        FROM @keyphrase
            CROSS APPLY
                new Cognition.Text.Splitter("KeyPhrase") AS T(KeyPhrase);
    
### <a name="perform-sentiment-analysis-on-each-paragraph"></a><span data-ttu-id="145cc-118">Her paragrafı düşünceleri çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="145cc-118">Perform sentiment analysis on each paragraph</span></span>

    @sentiment =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                Sentiment string,
                Conf double
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.SentimentAnalyzer(true);

