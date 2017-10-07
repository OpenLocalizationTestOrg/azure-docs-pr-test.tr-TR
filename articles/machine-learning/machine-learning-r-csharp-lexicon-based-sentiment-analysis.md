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
# <a name="deprecated-lexicon-based-sentiment-analysis"></a><span data-ttu-id="5a476-103">(kullanım dışı) Düşünceleri çözümleme sözlüğü dayalı</span><span class="sxs-lookup"><span data-stu-id="5a476-103">(deprecated) Lexicon Based Sentiment Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="5a476-104">Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="5a476-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="5a476-105">Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="5a476-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="5a476-106">Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="5a476-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="5a476-107">Nasıl, ölçüm kullanıcıların görüşlerini ve alışkanlıklarınızı markalar veya çevrimiçi sosyal ağlar konularında doğru Facebook yazılarını gibi tweet'leri, incelemeler vb..?</span><span class="sxs-lookup"><span data-stu-id="5a476-107">How can you measure users’ opinions and attitudes toward brands or topics in online social networks, such as Facebook posts, tweets, reviews, etc.?</span></span> <span data-ttu-id="5a476-108">Düşünceleri analiz gibi soruları çözümlemek için bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a476-108">Sentiment analysis provides a method for analyzing such questions.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="5a476-109">Genellikle düşünceleri analiz için iki yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="5a476-109">There are generally two methods for sentiment analysis.</span></span> <span data-ttu-id="5a476-110">Bir denetimli öğrenme algoritmasını kullanıyor ve Denetimsiz öğrenme olarak hello diğer işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="5a476-110">One is using a supervised learning algorithm, and hello other can be treated as unsupervised learning.</span></span> <span data-ttu-id="5a476-111">Denetimli öğrenme algoritmasını genellikle büyük bir açıklama gövde üzerinde bir sınıflandırma modeli oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5a476-111">A supervised learning algorithm generally builds a classification model on a large annotated corpus.</span></span> <span data-ttu-id="5a476-112">Doğruluğunu çoğunlukla hello ek açıklama hello kalitesini temel alır ve genellikle hello Eğitim işlemini bir uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="5a476-112">Its accuracy is mainly based on hello quality of hello annotation, and usually hello training process will take a long time.</span></span> <span data-ttu-id="5a476-113">Biz hello algoritması tooanother etki alanı, uyguladığınızda, yanı sıra hello sonuç genellikle iyi değil.</span><span class="sxs-lookup"><span data-stu-id="5a476-113">Besides that, when we apply hello algorithm tooanother domain, hello result is usually not good.</span></span> <span data-ttu-id="5a476-114">Toosupervised öğrenme, sözlüğü tabanlı büyük veri gövde depolama gerektirmeyen bir düşünceleri sözlük Denetimsiz öğrenme kullanır ve yapar eğitim - hello tüm işlem çok daha hızlı karşılaştırılan.</span><span class="sxs-lookup"><span data-stu-id="5a476-114">Compared toosupervised learning, lexicon-based unsupervised learning uses a sentiment dictionary, which doesn’t require storing a large data corpus and training - which makes hello whole process much faster.</span></span> 

<span data-ttu-id="5a476-115">Bizim [hizmet](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) hello en yaygın olarak kullanılan hello subjectivity sözlüklerinin biri olan MPQA Subjectivity sözlüğü (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/) üzerinde oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="5a476-115">Our [service](https://datamarket.azure.com/dataset/aml_labs/lexicon_based_sentiment_analysis) is built on hello MPQA Subjectivity Lexicon (http://mpqa.cs.pitt.edu/lexicons/subj_lexicon/), which is one of hello most commonly used subjectivity lexicons.</span></span> <span data-ttu-id="5a476-116">İçinde MPQA 5097 negatif ve 2533 pozitif sözcükleri vardır.</span><span class="sxs-lookup"><span data-stu-id="5a476-116">There are 5097 negative and 2533 positive words in MPQA.</span></span> <span data-ttu-id="5a476-117">Ve tüm bu sözcüklerin güçlü veya zayıf polarite açıklama.</span><span class="sxs-lookup"><span data-stu-id="5a476-117">And all of these words are annotated as strong or weak polarity.</span></span> <span data-ttu-id="5a476-118">Merhaba tüm gövde GNU Genel Kamu Lisansı altında olur.</span><span class="sxs-lookup"><span data-stu-id="5a476-118">hello whole corpus is under GNU General Public License.</span></span> <span data-ttu-id="5a476-119">Merhaba web hizmeti tweet'leri ve Facebook gönderileri gibi uygulanan tooany kısa tümce olabilir.</span><span class="sxs-lookup"><span data-stu-id="5a476-119">hello web service can be applied tooany short sentences, such as tweets and Facebook posts.</span></span> 

> <span data-ttu-id="5a476-120">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla veya yerel bilgisayarda bile örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="5a476-120">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer for example.</span></span> <span data-ttu-id="5a476-121">Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve.</span><span class="sxs-lookup"><span data-stu-id="5a476-121">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="5a476-122">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="5a476-122">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="5a476-123">Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="5a476-123">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="5a476-124">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="5a476-124">Consumption of web service</span></span>
<span data-ttu-id="5a476-125">Merhaba giriş verileri herhangi bir metin olabilir, ancak hello web hizmeti ile kısa tümce daha iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a476-125">hello input data can be any text, but hello web service works better with short sentences.</span></span> <span data-ttu-id="5a476-126">Merhaba çıktı, -1 ile 1 arasında sayısal bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="5a476-126">hello output is a numeric value between -1 and 1.</span></span> <span data-ttu-id="5a476-127">0 altındaki herhangi bir değer hello düşünceleri hello metnin negatif olduğunu gösterir; pozitif 0 ise yukarıda.</span><span class="sxs-lookup"><span data-stu-id="5a476-127">Any value below 0 denotes that hello sentiment of hello text is negative; positive if above 0.</span></span> <span data-ttu-id="5a476-128">Merhaba mutlak değeri hello sonucunun ilişkili hello düşünceleri hello gücünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="5a476-128">hello absolute value of hello result denotes hello strength of hello associated sentiment.</span></span> 

> <span data-ttu-id="5a476-129">Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a476-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="5a476-130">Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/)).</span><span class="sxs-lookup"><span data-stu-id="5a476-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="5a476-131">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="5a476-131">Starting C# code for web service consumption:</span></span>
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



<span data-ttu-id="5a476-132">"Bugün bir iyi günüdür." Merhaba giriş olabilir</span><span class="sxs-lookup"><span data-stu-id="5a476-132">hello input is “Today is a good day.”</span></span> <span data-ttu-id="5a476-133">Merhaba çıktı hello giriş cümlesi ile ilişkili bir pozitif düşünceleri gösterir "1" şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="5a476-133">hello output is “1”, which indicates a positive sentiment associated with hello input sentence.</span></span> 

## <a name="creation-of-web-service"></a><span data-ttu-id="5a476-134">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a476-134">Creation of web service</span></span>
> <span data-ttu-id="5a476-135">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="5a476-135">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="5a476-136">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="5a476-136">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="5a476-137">Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="5a476-137">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="5a476-138">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu.</span><span class="sxs-lookup"><span data-stu-id="5a476-138">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="5a476-139">Aşağıdaki şekilde Hello sözlüğü tabanlı düşünceleri analiz hello deneme akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5a476-139">hello figure below shows hello experiment flow of lexicon-based sentiment analysis.</span></span> <span data-ttu-id="5a476-140">Merhaba "sent_dict.csv" dosya hello MPQA subjectivity sözlüğü ve hello girişleri biri olarak ayarlandığından [R betiği yürütün][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="5a476-140">hello “sent_dict.csv” file is hello MPQA subjectivity lexicon, and is set as one of hello inputs of [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="5a476-141">Başka bir giriş kümesinden hello Amazon gözden geçirme burada biz seçimi, sütun adı değişikliği gerçekleştirilen ve işlemleri bölme test için örneklenen İnceleme olabilir.</span><span class="sxs-lookup"><span data-stu-id="5a476-141">Another input is a sampled review from hello Amazon review dataset for test, where we performed selection, column name modification, and split operations.</span></span> <span data-ttu-id="5a476-142">Bir karma paket toostore hello subjectivity sözlüğü hello bellekte kullanır ve hello puan hesaplama işlemi hızlandırmak.</span><span class="sxs-lookup"><span data-stu-id="5a476-142">We use a hash package toostore hello subjectivity lexicon in hello memory and accelerate hello score computation process.</span></span> <span data-ttu-id="5a476-143">Merhaba tam metin "tm" paketi tarafından simgeleştirilmiş ve hello düşünceleri sözlükte hello word ile karşılaştırılır.</span><span class="sxs-lookup"><span data-stu-id="5a476-143">hello whole text will be tokenized by “tm” package and compared with hello word in hello sentiment dictionary.</span></span> <span data-ttu-id="5a476-144">Son olarak, bir puan hello metinde hello ağırlık öznel her sözcüğün ekleyerek hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="5a476-144">Finally, a score will be calculated by adding hello weight of each subjective word in hello text.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="5a476-145">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="5a476-145">Experiment flow:</span></span>
![Deneme akışı][2]

#### <a name="module-1"></a><span data-ttu-id="5a476-147">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="5a476-147">Module 1:</span></span>
    # Map 1-based optional input ports toovariables
    sent_dict_data<- maml.mapInputPort(1) # class: data.frame
    dataset2 <- maml.mapInputPort(2) # class: data.frame

# <a name="install-hash-package"></a><span data-ttu-id="5a476-148">Karma paketini yükle</span><span class="sxs-lookup"><span data-stu-id="5a476-148">Install hash package</span></span>
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



## <a name="limitations"></a><span data-ttu-id="5a476-149">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="5a476-149">Limitations</span></span>
<span data-ttu-id="5a476-150">Bir algoritma açısından sözlüğü tabanlı düşünceleri analiz hello sınıflandırma yöntemi belirli alanlar için daha iyi çalışmayabilir genel düşünceleri çözümleme aracı ' dir.</span><span class="sxs-lookup"><span data-stu-id="5a476-150">From an algorithm perspective, lexicon-based sentiment analysis is a general sentiment analysis tool, which may not perform better than hello classification method for specific fields.</span></span> <span data-ttu-id="5a476-151">Merhaba değilleme sorun, ile iyi ele değil.</span><span class="sxs-lookup"><span data-stu-id="5a476-151">hello negation problem is not well dealt with.</span></span> <span data-ttu-id="5a476-152">Biz stillerinizin birkaç değilleme sözcükleri bizim programında, ancak daha iyi bir yolu değilleme sözlüğünü kullanarak ve bazı kurallar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5a476-152">We hardcode several negation words in our program, but a better way is using a negation dictionary and build some rules.</span></span> <span data-ttu-id="5a476-153">Merhaba web hizmeti daha iyi tweet'leri ve Facebook gönderileri gibi kısa ve basit cümleler üzerinde daha uzun ve karmaşık cümleleri Amazon incelemeleri gibi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5a476-153">hello web service performs better on short and simple sentences, such as tweets and Facebook posts, than on long and complex sentences such as Amazon reviews.</span></span> 

## <a name="faq"></a><span data-ttu-id="5a476-154">SSS</span><span class="sxs-lookup"><span data-stu-id="5a476-154">FAQ</span></span>
<span data-ttu-id="5a476-155">Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="5a476-155">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_1.png
[2]: ./media/machine-learning-r-csharp-lexicon-based-sentiment-analysis/sentiment_analysis_2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


