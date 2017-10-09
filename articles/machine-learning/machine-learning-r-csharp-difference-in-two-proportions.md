---
title: "AAA(deprecated) oranları Test - Azure fark | Microsoft Docs"
description: "(kullanım dışı) Oranları Test fark"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="bdc1d-103">(kullanım dışı) Oranları Test fark</span><span class="sxs-lookup"><span data-stu-id="bdc1d-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="bdc1d-104">Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="bdc1d-105">Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="bdc1d-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="bdc1d-106">Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="bdc1d-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="bdc1d-107">İki oranları istatistiksel olarak fark nedir?</span><span class="sxs-lookup"><span data-stu-id="bdc1d-107">Are two proportions statistically different?</span></span> <span data-ttu-id="bdc1d-108">Bir kullanıcı bir filmi önemli ölçüde daha büyük bir kısmının varsa toocompare iki filmler toodetermine 'yöntemlerine' ne zaman istediğini varsayın toohello diğer karşılaştırılan.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="bdc1d-109">Büyük bir örnekle hello oranları 0,50 ve 0.51 arasında istatistiksel olarak önemli bir fark olabilir.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="bdc1d-110">Küçük bir örnekle değil yeterli veri toodetermine bu oranları gerçekte farklı durumunda olabilir.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="bdc1d-111">Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/prop_test) Merhaba, ancak başarı hello toplam sayısını ve denemeler hello 2 karşılaştırma grupları için kullanıcı girişi göre iki oranları hello fark varsayımınızın sınamasını gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="bdc1d-112">Bir olası senaryoda, bu web Hizmeti'nin hello filmler birini gerçekten 'hello diğer, daha sık film derecelendirmelerine dayalı ilişkilendirilmiş olup olmadığını' hello kullanıcıya söyleyen bir filmi karşılaştırma uygulamada çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="bdc1d-113">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="bdc1d-114">Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="bdc1d-115">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="bdc1d-116">Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="bdc1d-117">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="bdc1d-117">Consumption of web service</span></span>
<span data-ttu-id="bdc1d-118">Bu hizmet 4 bağımsız değişkenleri kabul eder ve bir varsayım oranlarını test yapar.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="bdc1d-119">Merhaba giriş bağımsız değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bdc1d-119">hello input arguments are:</span></span>

* <span data-ttu-id="bdc1d-120">Successes1 - 1 örnekteki başarı olayların sayısı.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="bdc1d-121">Successes2 - örnek 2 başarı olayları sayısı.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="bdc1d-122">Total1 - 1 örnek boyutu.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="bdc1d-123">Total2 - örnek 2 boyutu.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="bdc1d-124">Merhaba hello hizmet çıkışıdır hello varsayımınızın hello sonucunu test hello chi-square istatistiği, df, p-değeri ile birlikte ve oran örnek 1/2 ve güvenilirlik aralığını sınırları içinde.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="bdc1d-125">Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="bdc1d-126">Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="bdc1d-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="bdc1d-127">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="bdc1d-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="bdc1d-128">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdc1d-128">Creation of web service</span></span>
> <span data-ttu-id="bdc1d-129">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="bdc1d-130">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="bdc1d-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="bdc1d-131">Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="bdc1d-132">Azure Machine Learning içinde yeni bir boş deneme iki oluşturulduğu [R betiği yürütün] [ execute-r-script] modüller.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="bdc1d-133">Merhaba ikinci Modül 2 oranlarını R tooperform hello varsayımınızın test içindeki hello prop.test komut kullanırken hello ilk modülünde hello veri şeması, tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="bdc1d-134">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="bdc1d-134">Experiment flow:</span></span>
![Deneme akışı][2]

#### <a name="module-1"></a><span data-ttu-id="bdc1d-136">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="bdc1d-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="bdc1d-137">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="bdc1d-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="bdc1d-138">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="bdc1d-138">Limitations</span></span>
<span data-ttu-id="bdc1d-139">Bu, 2 oranları fark testi için çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="bdc1d-140">Yukarıdaki Hello örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve tüm hello değişkenleri sürekli hello hizmeti varsayar.</span><span class="sxs-lookup"><span data-stu-id="bdc1d-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="bdc1d-141">SSS</span><span class="sxs-lookup"><span data-stu-id="bdc1d-141">FAQ</span></span>
<span data-ttu-id="bdc1d-142">Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="bdc1d-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

