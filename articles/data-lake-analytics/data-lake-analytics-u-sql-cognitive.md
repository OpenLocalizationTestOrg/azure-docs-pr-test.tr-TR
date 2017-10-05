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
# <a name="tutorial-get-started-with-the-cognitive-capabilities-of-u-sql"></a>Öğretici: U-SQL Bilişsel yetenekleri ile çalışmaya başlama

U-SQL için bilişsel özellikleri geliştiricilerin kendi büyük veri programlarda put Intelligence kullanmak etkinleştirin. Basit genel işleminde:

* U-SQL komut dosyası için bilişsel özelliklerini etkinleştirmek için referans DERLEMESİNİ deyimi kullanın
* Bilişsel özellikleri kullanmak için işlem işlemini çağırın 

## <a name="imaging-scenarios"></a>Görüntü oluşturma senaryoları

### <a name="example-image-tagging"></a>Örnek: Görüntü etiketleme

Aşağıdaki örnek nesneleri görüntülerinde algılamak için görüntüleme yetenekleri uçtan uca kullanımını gösterir.

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


### <a name="extract-emotions-from-human-faces"></a>İnsan yüzeyleri duygular Ayıkla 

    @emotions =
        PROCESS @imgs
        PRODUCE FileName string,
                NumFaces int,
                Emotion string
        READONLY FileName
        USING new Cognition.Vision.EmotionAnalyzer();

### <a name="estimate-age-and-gender-for-human-faces"></a>Geçerlilik süresi ve İnsan yüzeyleri cinsiyetiniz tahmin etme

    @faces = 
            PROCESS @imgs
            PRODUCE FileName,
                    NumFaces int,
                    FaceAge string,
                    FaceGender string
            READONLY FileName
            USING new Cognition.Vision.FaceDetector();

### <a name="detect-text-in-images-ocr"></a>Görüntüleri (OCR) metnini Algıla

    @ocrs =
            PROCESS @imgs
            PRODUCE FileName,
                    Text string
            READONLY FileName
            USING new Cognition.Vision.OcrExtractor();

## <a name="text-scenarios"></a>Metin senaryoları

### <a name="input-data"></a>Giriş verisi

Leo Tolstoy tarafından biz "War ve rahatlık" oluşan bir giriş olduğunu varsayalım.

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

### <a name="extract-key-phrases-for-each-paragraph"></a>Her paragraf için anahtar tümcecikleri Ayıkla

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
    
### <a name="perform-sentiment-analysis-on-each-paragraph"></a>Her paragrafı düşünceleri çözümlemesi

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

