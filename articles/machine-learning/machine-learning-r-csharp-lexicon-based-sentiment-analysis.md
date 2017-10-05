---
title: "(kullanım dışı) Sözlüğü Azure düşünceleri analiz - tabanlı | Microsoft Docs"
description: "(kullanım dışı) Düşünceleri çözümleme sözlüğü dayalı"
services: machine-learning
documentationcenter: 
author: pengxia
manager: jhubbard
editor: cgronlun
ms.assetid: 912f41af-966c-4d79-a413-6f9fc02823df
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: pengxia
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 7bc80a1e1067296528eca1a843ea30b0c27af616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>(kullanım dışı) Düşünceleri çözümleme sözlüğü dayalı

> [!NOTE]
> Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Nasıl, ölçüm kullanıcıların görüşlerini ve alışkanlıklarınızı markalar veya çevrimiçi sosyal ağlar konularında doğru Facebook yazılarını gibi tweet'leri, incelemeler vb..? Düşünceleri analiz gibi soruları çözümlemek için bir yöntem sağlar.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Genellikle düşünceleri analiz için iki yöntem vardır. Bir denetimli öğrenme algoritmasını kullanıyor ve diğer Denetimsiz öğrenme olarak işlenebilir. Denetimli öğrenme algoritmasını genellikle büyük bir açıklama gövde üzerinde bir sınıflandırma modeli oluşturur. Doğruluğunu çoğunlukla ek açıklamanın kalitesinden temel alır ve genellikle Eğitim işlemini bir uzun sürer. Biz başka bir etki alanı için algoritma uyguladığınızda, yanı sıra, sonuç genellikle iyi değil. Denetimli öğrenme, sözlüğü tabanlı Denetimsiz öğrenme kullanan bir büyük veri gövde depolamak ve eğitim gerektirmeyen bir düşünceleri sözlük karşılaştırılan - hangi tüm çok daha hızlı hale getirir. 

Bizim [hizmet](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) MPQA Subjectivity en yaygın kullanılan subjectivity sözlüklerinin biri olan sözlüğü üzerinde (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), yerleşik olarak bulunur. İçinde MPQA 5097 negatif ve 2533 pozitif sözcükleri vardır. Ve tüm bu sözcüklerin güçlü veya zayıf polarite açıklama. Tüm gövde GNU Genel Kamu Lisansı altında olur. Web hizmeti tweet'leri ve Facebook gönderileri gibi kısa bir cümle uygulanabilir. 

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla veya yerel bilgisayarda bile örneğin tüketilmesi. Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Giriş verisi herhangi bir metin olabilir, ancak web hizmeti ile kısa tümce daha iyi çalışır. Çıkış, -1 ile 1 arasında sayısal bir değerdir. Herhangi bir değer 0 aşağıda metni düşünceleri negatif olduğunu gösterir; pozitif 0 ise yukarıda. Sonuç mutlak değerini ilişkili düşünceleri gücünü gösterir. 

> Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/)).

### <a name="starting-c-code-for-web-service-consumption"></a>Web hizmet tüketimi için C# kodunu başlatılıyor:
    public class ScoreResult
    {
            [DataMember]
            public double result
            {
                get;
                set;
            }
    }

    void main()
    {
            using (var wb = new WebClient())
            {
                var acitionUri = new Uri("PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score");
                DataServiceContext ctx = new DataServiceContext(acitionUri);
                var cred = new NetworkCredential("PutEmailAddressHere", "ChangeToAPIKey");
                var cache = new CredentialCache();

                cache.Add(acitionUri, "Basic", cred);
                ctx.Credentials = cache;
                var query = ctx.Execute<ScoreResult>(acitionUri, "POST", true, new BodyOperationParameter("Text", TextBox1.Text));
                ScoreResult scoreResult = query.ElementAt(0);
                double result = scoreResult.result;
            }
    }



Giriş "Bugün iyi gün" metnidir. Çıktı, giriş cümlesi ile ilişkili bir pozitif düşünceleri gösterir "1" şeklindedir. 

## <a name="creation-of-web-service"></a>Web hizmeti oluşturma
> Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu. Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml). Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.
> 
> 

Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu. Aşağıdaki şekilde sözlüğü tabanlı düşünceleri analiz deneme akışı gösterilmektedir. "Sent_dict.csv" dosya MPQA subjectivity sözlüğü ve girişleri biri olarak ayarlandığından [R betiği yürütün][execute-r-script]. Başka bir giriş burada biz seçimi, sütun adı değişikliği gerçekleştirilen ve işlemleri bölme test için Amazon gözden geçirme kümesinden örneklenen İnceleme olabilir. Bellek subjectivity sözlüğü depolamak ve puan hesaplama işlemi hızlandırmak için bir karma paket kullanırız. Tam metin "tm" paketi tarafından simgeleştirilmiş ve düşünceleri sözlük Word'de ile karşılaştırılır. Son olarak, bir puan metinde öznel her sözcüğün ağırlığını ekleyerek hesaplanır. 

### <a name="experiment-flow"></a>Deneme akışı:
![Deneme akışı][2]

#### <a name="module-1"></a>Modül 1:
    # Map 1-based optional input ports to variables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a>Karma paketini yükle
    install.packages("src/hash_2.2.6.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("hash", lib.loc = ".", logical.return = TRUE, verbose = TRUE)
    library(tm)
    library(stringr)

    #create sentiment dictionary
    negation_word <- c("not","nor", "no")
    result <- c()
    sent_dict <- hash()
    sent_dict <- hash(sent_dict_data$word, sent_dict_data$polarity)

    #  Compute sentiment score for each document
    for (m in 1:nrow(dataset2)){
    polarity_ratio <- 0
    polarity_total <- 0
    not <- 0
    sentence <- tolower(dataset2[m,1])
    if (nchar(sentence) > 0){
        token_array <- scan_tokenizer(sentence)
        for (j in 1:length(token_array)){
            word = str_replace_all(token_array[j], "[^[:alnum:]]", "")
            for (k in 1:length(negation_word)){
              if (word == negation_word[k]){
                not <- (not+1) %% 2

              }
            }
            if (word != ""){
                if (!is.null(sent_dict[[word]])){
                  polarity_ratio <- polarity_ratio + (-2*not+1)*sent_dict[[word]]
                  polarity_total <- polarity_total + abs(sent_dict[[word]])
                }
            }

        }
    }
    if (polarity_total > 0){
        result <- c(result, polarity_ratio/polarity_total)
    }else{
        result<- c(result,0)
    }
    }

    # Sample operation
    data.set <- data.frame(result)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a>Sınırlamalar
Bir algoritma açısından sözlüğü tabanlı düşünceleri analiz sınıflandırma yöntemi belirli alanlar için daha iyi çalışmayabilir genel düşünceleri çözümleme aracı ' dir. Değilleme sorun, ile iyi ele değil. Biz stillerinizin birkaç değilleme sözcükleri bizim programında, ancak daha iyi bir yolu değilleme sözlüğünü kullanarak ve bazı kurallar oluşturun. Web hizmeti daha iyi tweet'leri ve Facebook gönderileri gibi kısa ve basit cümleler üzerinde daha uzun ve karmaşık cümleleri Amazon incelemeleri gibi gerçekleştirir. 

## <a name="faq"></a>SSS
Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


