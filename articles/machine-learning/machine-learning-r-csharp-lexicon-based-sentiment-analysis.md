---
title: "AAA(deprecated) sözlüğü düşünceleri analiz temel - Azure | Microsoft Docs"
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
redirect_document_id: True
ms.openlocfilehash: 1ed7e19441c6a8ad270a0c0f567b4aea588a583e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-lexicon-based-sentiment-analysis"></a>(kullanım dışı) Düşünceleri çözümleme sözlüğü dayalı

> [!NOTE]
> Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Nasıl, ölçüm kullanıcıların görüşlerini ve alışkanlıklarınızı markalar veya çevrimiçi sosyal ağlar konularında doğru Facebook yazılarını gibi tweet'leri, incelemeler vb..? Düşünceleri analiz gibi soruları çözümlemek için bir yöntem sağlar.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Genellikle düşünceleri analiz için iki yöntem vardır. Bir denetimli öğrenme algoritmasını kullanıyor ve Denetimsiz öğrenme olarak hello diğer işlenebilir. Denetimli öğrenme algoritmasını genellikle büyük bir açıklama gövde üzerinde bir sınıflandırma modeli oluşturur. Doğruluğunu çoğunlukla hello ek açıklama hello kalitesini temel alır ve genellikle hello Eğitim işlemini bir uzun sürer. Biz hello algoritması tooanother etki alanı, uyguladığınızda, yanı sıra hello sonuç genellikle iyi değil. Toosupervised öğrenme, sözlüğü tabanlı büyük veri gövde depolama gerektirmeyen bir düşünceleri sözlük Denetimsiz öğrenme kullanır ve yapar eğitim - hello tüm işlem çok daha hızlı karşılaştırılan. 

Bizim [hizmet](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) hello en yaygın olarak kullanılan hello subjectivity sözlüklerinin biri olan MPQA Subjectivity sözlüğü (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/) üzerinde oluşturulmuştur. İçinde MPQA 5097 negatif ve 2533 pozitif sözcükleri vardır. Ve tüm bu sözcüklerin güçlü veya zayıf polarite açıklama. Merhaba tüm gövde GNU Genel Kamu Lisansı altında olur. Merhaba web hizmeti tweet'leri ve Facebook gönderileri gibi uygulanan tooany kısa tümce olabilir. 

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla veya yerel bilgisayarda bile örneğin tüketilmesi. Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Merhaba giriş verileri herhangi bir metin olabilir, ancak hello web hizmeti ile kısa tümce daha iyi çalışır. Merhaba çıktı, -1 ile 1 arasında sayısal bir değerdir. 0 altındaki herhangi bir değer hello düşünceleri hello metnin negatif olduğunu gösterir; pozitif 0 ise yukarıda. Merhaba mutlak değeri hello sonucunun ilişkili hello düşünceleri hello gücünü gösterir. 

> Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/)).

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



"Bugün bir iyi günüdür." Merhaba giriş olabilir Merhaba çıktı hello giriş cümlesi ile ilişkili bir pozitif düşünceleri gösterir "1" şeklindedir. 

## <a name="creation-of-web-service"></a>Web hizmeti oluşturma
> Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu. Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml). Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.
> 
> 

Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu. Aşağıdaki şekilde Hello sözlüğü tabanlı düşünceleri analiz hello deneme akışı gösterilmektedir. Merhaba "sent_dict.csv" dosya hello MPQA subjectivity sözlüğü ve hello girişleri biri olarak ayarlandığından [R betiği yürütün][execute-r-script]. Başka bir giriş kümesinden hello Amazon gözden geçirme burada biz seçimi, sütun adı değişikliği gerçekleştirilen ve işlemleri bölme test için örneklenen İnceleme olabilir. Bir karma paket toostore hello subjectivity sözlüğü hello bellekte kullanır ve hello puan hesaplama işlemi hızlandırmak. Merhaba tam metin "tm" paketi tarafından simgeleştirilmiş ve hello düşünceleri sözlükte hello word ile karşılaştırılır. Son olarak, bir puan hello metinde hello ağırlık öznel her sözcüğün ekleyerek hesaplanır. 

### <a name="experiment-flow"></a>Deneme akışı:
![Deneme akışı][2]

#### <a name="module-1"></a>Modül 1:
    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("data.set")



## <a name="limitations"></a>Sınırlamalar
Bir algoritma açısından sözlüğü tabanlı düşünceleri analiz hello sınıflandırma yöntemi belirli alanlar için daha iyi çalışmayabilir genel düşünceleri çözümleme aracı ' dir. Merhaba değilleme sorun, ile iyi ele değil. Biz stillerinizin birkaç değilleme sözcükleri bizim programında, ancak daha iyi bir yolu değilleme sözlüğünü kullanarak ve bazı kurallar oluşturun. Merhaba web hizmeti daha iyi tweet'leri ve Facebook gönderileri gibi kısa ve basit cümleler üzerinde daha uzun ve karmaşık cümleleri Amazon incelemeleri gibi gerçekleştirir. 

## <a name="faq"></a>SSS
Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


