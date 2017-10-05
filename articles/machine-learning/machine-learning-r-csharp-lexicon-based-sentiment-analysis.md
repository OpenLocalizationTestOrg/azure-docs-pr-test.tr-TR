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
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="c07f4-103">(kullanım dışı) Düşünceleri çözümleme sözlüğü dayalı</span><span class="sxs-lookup"><span data-stu-id="c07f4-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="c07f4-104">Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="c07f4-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="c07f4-105">Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="c07f4-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="c07f4-106">Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="c07f4-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="c07f4-107">Nasıl, ölçüm kullanıcıların görüşlerini ve alışkanlıklarınızı markalar veya çevrimiçi sosyal ağlar konularında doğru Facebook yazılarını gibi tweet'leri, incelemeler vb..?</span><span class="sxs-lookup"><span data-stu-id="c07f4-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="c07f4-108">Düşünceleri analiz gibi soruları çözümlemek için bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="c07f4-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="c07f4-109">Genellikle düşünceleri analiz için iki yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="c07f4-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="c07f4-110">Bir denetimli öğrenme algoritmasını kullanıyor ve diğer Denetimsiz öğrenme olarak işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-110">One is using a supervised learning algorithm, and the other can be treated as unsupervised learning.</span></span> <span data-ttu-id="c07f4-111">Denetimli öğrenme algoritmasını genellikle büyük bir açıklama gövde üzerinde bir sınıflandırma modeli oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c07f4-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="c07f4-112">Doğruluğunu çoğunlukla ek açıklamanın kalitesinden temel alır ve genellikle Eğitim işlemini bir uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="c07f4-112">Its accuracy is mainly based on the quality of the annotation, and usually the training process will take a long time.</span></span> <span data-ttu-id="c07f4-113">Biz başka bir etki alanı için algoritma uyguladığınızda, yanı sıra, sonuç genellikle iyi değil.</span><span class="sxs-lookup"><span data-stu-id="c07f4-113">Besides that, when we apply the algorithm to another domain, the result is usually not good.</span></span> <span data-ttu-id="c07f4-114">Denetimli öğrenme, sözlüğü tabanlı Denetimsiz öğrenme kullanan bir büyük veri gövde depolamak ve eğitim gerektirmeyen bir düşünceleri sözlük karşılaştırılan - hangi tüm çok daha hızlı hale getirir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-114">Compared to supervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes the whole process much faster.</span></span> 

<span data-ttu-id="c07f4-115">Bizim [hizmet](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) MPQA Subjectivity en yaygın kullanılan subjectivity sözlüklerinin biri olan sözlüğü üzerinde (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="c07f4-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on the MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of the most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="c07f4-116">İçinde MPQA 5097 negatif ve 2533 pozitif sözcükleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c07f4-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="c07f4-117">Ve tüm bu sözcüklerin güçlü veya zayıf polarite açıklama.</span><span class="sxs-lookup"><span data-stu-id="c07f4-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="c07f4-118">Tüm gövde GNU Genel Kamu Lisansı altında olur.</span><span class="sxs-lookup"><span data-stu-id="c07f4-118">The whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="c07f4-119">Web hizmeti tweet'leri ve Facebook gönderileri gibi kısa bir cümle uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-119">The web service can be applied to any short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="c07f4-120">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla veya yerel bilgisayarda bile örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="c07f4-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="c07f4-121">Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek.</span><span class="sxs-lookup"><span data-stu-id="c07f4-121">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="c07f4-122">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="c07f4-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="c07f4-123">Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="c07f4-123">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="c07f4-124">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="c07f4-124">Consumption of web service</span></span>
<span data-ttu-id="c07f4-125">Giriş verisi herhangi bir metin olabilir, ancak web hizmeti ile kısa tümce daha iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="c07f4-125">The input data can be any text, but the web service works better with short sentences.</span></span> <span data-ttu-id="c07f4-126">Çıkış, -1 ile 1 arasında sayısal bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-126">The output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="c07f4-127">Herhangi bir değer 0 aşağıda metni düşünceleri negatif olduğunu gösterir; pozitif 0 ise yukarıda.</span><span class="sxs-lookup"><span data-stu-id="c07f4-127">Any value below 0 denotes that the sentiment of the text is negative; positive if above 0.</span></span> <span data-ttu-id="c07f4-128">Sonuç mutlak değerini ilişkili düşünceleri gücünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-128">The absolute value of the result denotes the strength of the associated sentiment.</span></span> 

> <span data-ttu-id="c07f4-129">Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="c07f4-130">Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="c07f4-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="c07f4-131">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="c07f4-131">Starting C# code for web service consumption:</span></span>
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



<span data-ttu-id="c07f4-132">Giriş "Bugün iyi gün" metnidir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-132">The input is “Today is a good day.”</span></span> <span data-ttu-id="c07f4-133">Çıktı, giriş cümlesi ile ilişkili bir pozitif düşünceleri gösterir "1" şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-133">The output is “1”, which indicates a positive sentiment associated with the input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="c07f4-134">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="c07f4-134">Creation of web service</span></span>
> <span data-ttu-id="c07f4-135">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="c07f4-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="c07f4-136">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="c07f4-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="c07f4-137">Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="c07f4-137">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="c07f4-138">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu.</span><span class="sxs-lookup"><span data-stu-id="c07f4-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="c07f4-139">Aşağıdaki şekilde sözlüğü tabanlı düşünceleri analiz deneme akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-139">The figure below shows the experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="c07f4-140">"Sent_dict.csv" dosya MPQA subjectivity sözlüğü ve girişleri biri olarak ayarlandığından [R betiği yürütün][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="c07f4-140">The “sent_dict.csv” file is the MPQA subjectivity lexicon, and is set as one of the inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="c07f4-141">Başka bir giriş burada biz seçimi, sütun adı değişikliği gerçekleştirilen ve işlemleri bölme test için Amazon gözden geçirme kümesinden örneklenen İnceleme olabilir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-141">Another input is a sampled review from the Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="c07f4-142">Bellek subjectivity sözlüğü depolamak ve puan hesaplama işlemi hızlandırmak için bir karma paket kullanırız.</span><span class="sxs-lookup"><span data-stu-id="c07f4-142">We use a hash package to store the subjectivity lexicon in the memory and accelerate the score computation process.</span></span> <span data-ttu-id="c07f4-143">Tam metin "tm" paketi tarafından simgeleştirilmiş ve düşünceleri sözlük Word'de ile karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="c07f4-143">The whole text will be tokenized by “tm” package and compared with the word in the sentiment dictionary.</span></span> <span data-ttu-id="c07f4-144">Son olarak, bir puan metinde öznel her sözcüğün ağırlığını ekleyerek hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="c07f4-144">Finally, a score will be calculated by adding the weight of each subjective word in the text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="c07f4-145">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="c07f4-145">Experiment flow:</span></span>
![Deneme akışı][2]

#### <a name="module-1"></a><span data-ttu-id="c07f4-147">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="c07f4-147">Module 1:</span></span>
    # Map 1-based optional input ports to variables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="c07f4-148">Karma paketini yükle</span><span class="sxs-lookup"><span data-stu-id="c07f4-148">Install hash package</span></span>
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



## <a name="limitations"></a><span data-ttu-id="c07f4-149">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="c07f4-149">Limitations</span></span>
<span data-ttu-id="c07f4-150">Bir algoritma açısından sözlüğü tabanlı düşünceleri analiz sınıflandırma yöntemi belirli alanlar için daha iyi çalışmayabilir genel düşünceleri çözümleme aracı ' dir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than the classification method for specific fields.</span></span> <span data-ttu-id="c07f4-151">Değilleme sorun, ile iyi ele değil.</span><span class="sxs-lookup"><span data-stu-id="c07f4-151">The negation problem is not well dealt with.</span></span> <span data-ttu-id="c07f4-152">Biz stillerinizin birkaç değilleme sözcükleri bizim programında, ancak daha iyi bir yolu değilleme sözlüğünü kullanarak ve bazı kurallar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c07f4-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="c07f4-153">Web hizmeti daha iyi tweet'leri ve Facebook gönderileri gibi kısa ve basit cümleler üzerinde daha uzun ve karmaşık cümleleri Amazon incelemeleri gibi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="c07f4-153">The web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="c07f4-154">SSS</span><span class="sxs-lookup"><span data-stu-id="c07f4-154">FAQ</span></span>
<span data-ttu-id="c07f4-155">Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="c07f4-155">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


