---
title: "(kullanım dışı) Terimli dağıtım paketi - Azure | Microsoft Docs"
description: "(kullanım dışı) Terimli dağıtım paketi"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 6f0a6d06e7401c8360a92a707a0552f41ff3657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="0952b-103">(kullanım dışı) Terimli dağıtım paketi</span><span class="sxs-lookup"><span data-stu-id="0952b-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="0952b-104">Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="0952b-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="0952b-105">Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="0952b-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="0952b-106">Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0952b-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="0952b-107">Örnek web hizmetleri kümesi terimli dağıtım paketidir ([terimli Oluşturucu](https://datamarket.azure.com/dataset/aml_labs/bdg5), [olasılık hesaplayıcı](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile hesaplayıcı](https://datamarket.azure.com/dataset/aml_labs/bdq5)) Yardım oluşturmak ve terimli dağıtımları postalarla.</span><span class="sxs-lookup"><span data-stu-id="0952b-107">The Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="0952b-108">Quantiles hesaplama herhangi bir uzunlukta terimli dağıtım dizisini oluşturma hizmetleri izin dışında verilen quantile olasılık ve hesaplama olasılık verilen.</span><span class="sxs-lookup"><span data-stu-id="0952b-108">The services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="0952b-109">Hizmetlerinin her biri farklı çıkışları seçili hizmetini temel alan yayar (Açıklama aşağıya bakın).</span><span class="sxs-lookup"><span data-stu-id="0952b-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="0952b-110">R işlevleri qbinom rbinom ve pbinom, R istatistikleri paketinde bulunan terimli Dağıtım paketine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0952b-110">The Binomial Distribution Suite is based on the R functions qbinom, rbinom, and pbinom, which are included in the R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="0952b-111">Bu web hizmetleri kullanıcılar tarafından – olası bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, bir mobil uygulama aracılığıyla, doğrudan Market'te örneğin kullanılabilecek.</span><span class="sxs-lookup"><span data-stu-id="0952b-111">These web services could be consumed by users – potentially directly on the marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="0952b-112">Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek.</span><span class="sxs-lookup"><span data-stu-id="0952b-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="0952b-113">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="0952b-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="0952b-114">Web hizmeti daha sonra Azure Marketi yayımlanan ve dünya genelindeki kullanıcılar ve cihazlar tarafından tüketilen – web hizmeti yazarı tarafından hiçbir altyapı Kurulumu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0952b-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world – no infrastructure setup by the author of the web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="0952b-115">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="0952b-115">Consumption of web service</span></span>
<span data-ttu-id="0952b-116">Terimli dağıtım paketi, aşağıdaki 3 Hizmetleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0952b-116">The Binomial Distribution Suite includes the following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="0952b-117">Terimli dağıtım Quantile hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="0952b-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="0952b-118">Bu hizmet normal dağıtım 4 bağımsız değişkenlerini kabul eder ve ilişkili quantile hesaplar.</span><span class="sxs-lookup"><span data-stu-id="0952b-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>
<span data-ttu-id="0952b-119">Giriş bağımsız değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0952b-119">The input arguments are:</span></span>

* <span data-ttu-id="0952b-120">p - birden çok deneme olasılığını tek bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="0952b-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="0952b-121">boyutu - deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="0952b-121">size - The number of trials.</span></span>
* <span data-ttu-id="0952b-122">olasılık - bir deneme başarı olasılığı.</span><span class="sxs-lookup"><span data-stu-id="0952b-122">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="0952b-123">Yan - M dağıtımın, dağıtım üst tarafındaki U alt tarafı için.</span><span class="sxs-lookup"><span data-stu-id="0952b-123">Side - L for the lower side of the distribution, U for the upper side of the distribution.</span></span> 

<span data-ttu-id="0952b-124">Hizmet verilen olasılık ile ilişkili hesaplanan quantile çıkışıdır.</span><span class="sxs-lookup"><span data-stu-id="0952b-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="0952b-125">Terimli dağıtım olasılık hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="0952b-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="0952b-126">Bu hizmet terimli dağıtım 4 bağımsız değişkenlerini kabul eder ve ilişkili olasılık hesaplar.</span><span class="sxs-lookup"><span data-stu-id="0952b-126">This service accepts 4 arguments of a binomial distribution and calculates the associated probability.</span></span>
<span data-ttu-id="0952b-127">Giriş bağımsız değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0952b-127">The input arguments are:</span></span>

* <span data-ttu-id="0952b-128">q bir olayın terimli dağılımı ile tek quantile.</span><span class="sxs-lookup"><span data-stu-id="0952b-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="0952b-129">boyutu - deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="0952b-129">size - The number of trials.</span></span>
* <span data-ttu-id="0952b-130">olasılık - bir deneme başarı olasılığı.</span><span class="sxs-lookup"><span data-stu-id="0952b-130">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="0952b-131">yan - M dağıtımın, dağıtım veya başarıları tek bir dizi eşittir E üst tarafındaki U alt tarafı için.</span><span class="sxs-lookup"><span data-stu-id="0952b-131">side - L for the lower side of the distribution, U for the upper side of the distribution, or E that is equal to a single number of successes.</span></span>

<span data-ttu-id="0952b-132">Hizmet çıktısını verilen quantile ile ilişkili hesaplanan olasılıktır.</span><span class="sxs-lookup"><span data-stu-id="0952b-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="0952b-133">Terimli dağıtım Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="0952b-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="0952b-134">Bu hizmet terimli dağıtım 3 bağımsız değişkenlerini kabul eder ve rastgele bir dizi binomially dağıtılmış sayı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0952b-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="0952b-135">Şu bağımsız değişkenleri için isteği içinde sağlanmasını:</span><span class="sxs-lookup"><span data-stu-id="0952b-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="0952b-136">n - gözlemleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="0952b-136">n - Number of observations.</span></span> 
* <span data-ttu-id="0952b-137">boyutu - deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="0952b-137">size - Number of trials.</span></span>
* <span data-ttu-id="0952b-138">olasılık - başarı olasılığı.</span><span class="sxs-lookup"><span data-stu-id="0952b-138">prob - Probability of success.</span></span>

<span data-ttu-id="0952b-139">Hizmet çıktısını uzunluğu n terimli boyutu ve olasılık bağımsız değişkenler üzerinde tabanlı bir dağıtım ile dizisidir.</span><span class="sxs-lookup"><span data-stu-id="0952b-139">The output of the service is a sequence of length n with a binomial distribution based on the size and prob arguments.</span></span>

> <span data-ttu-id="0952b-140">Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="0952b-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="0952b-141">Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (örneğin uygulamalardır burada: [Oluşturucu](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [olasılık hesaplayıcı](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile hesaplayıcı](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="0952b-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="0952b-142">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="0952b-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="0952b-143">Terimli dağıtım Quantile hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="0952b-143">Binomial Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="0952b-144">Terimli dağıtım olasılık hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="0952b-144">Binomial Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a><span data-ttu-id="0952b-145">Terimli dağıtım Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="0952b-145">Binomial Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }





## <a name="creation-of-web-service"></a><span data-ttu-id="0952b-146">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="0952b-146">Creation of web service</span></span>
> <span data-ttu-id="0952b-147">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="0952b-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="0952b-148">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="0952b-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="0952b-149">Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="0952b-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="0952b-150">Terimli dağıtım Quantile hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="0952b-150">Binomial Distribution Quantile Calculator</span></span>
![Çalışma alanı oluşturma][4]

#### <a name="module-1"></a><span data-ttu-id="0952b-152">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="0952b-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port
#### <a name="module-2"></a><span data-ttu-id="0952b-153">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="0952b-153">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="0952b-154">Terimli dağıtım olasılık hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="0952b-154">Binomial Distribution Probability Calculator</span></span>
![Çalışma alanı oluşturma][5]

#### <a name="module-1"></a><span data-ttu-id="0952b-156">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="0952b-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port


#### <a name="module-2"></a><span data-ttu-id="0952b-157">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="0952b-157">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="0952b-158">Terimli dağıtım Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="0952b-158">Binomial Distribution Generator</span></span>
![Çalışma alanı oluşturma][6]

#### <a name="module-1"></a><span data-ttu-id="0952b-160">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="0952b-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="0952b-161">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="0952b-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="0952b-162">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="0952b-162">Limitations</span></span>
<span data-ttu-id="0952b-163">Bunlar terimli dağıtım çevreleyen çok basit örnektir.</span><span class="sxs-lookup"><span data-stu-id="0952b-163">These are very simple examples surrounding the binomial distribution.</span></span> <span data-ttu-id="0952b-164">Yukarıdaki örnek koddan görüldüğü gibi küçük hata yakalama uygulanır.</span><span class="sxs-lookup"><span data-stu-id="0952b-164">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="0952b-165">SSS</span><span class="sxs-lookup"><span data-stu-id="0952b-165">FAQ</span></span>
<span data-ttu-id="0952b-166">Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="0952b-166">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

