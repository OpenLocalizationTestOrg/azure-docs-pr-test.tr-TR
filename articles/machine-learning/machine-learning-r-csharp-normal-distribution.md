---
title: "(kullanım dışı) Normal dağıtım Web hizmeti Suite - Azure | Microsoft Docs"
description: "(kullanım dışı) Normal dağıtım Web hizmet paketi"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
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
ms.openlocfilehash: 79d1621330ad56b0c62ca46cfac424c2306e371f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="99243-103">(kullanım dışı) Normal dağıtım paketi</span><span class="sxs-lookup"><span data-stu-id="99243-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="99243-104">Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="99243-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="99243-105">Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="99243-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="99243-106">Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="99243-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="99243-107">Normal dağıtım paketi örnek web hizmetleri kümesidir ([Oluşturucu](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile hesaplayıcı](https://datamarket.azure.com/dataset/aml_labs/ndq5), [olasılık hesaplayıcı](https://datamarket.azure.com/dataset/aml_labs/ndp5)) oluşturmak ve normal dağıtım işleme Yardım.</span><span class="sxs-lookup"><span data-stu-id="99243-107">The Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="99243-108">Hizmet verilen olasılık gelen quantiles hesaplama ve verilen quantile gelen olasılık hesaplama herhangi bir uzunlukta, normal dağıtım dizisini oluşturma sağlar.</span><span class="sxs-lookup"><span data-stu-id="99243-108">The services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="99243-109">Hizmetlerinin her biri farklı çıkışları seçili hizmetini temel alan yayar (Açıklama aşağıya bakın).</span><span class="sxs-lookup"><span data-stu-id="99243-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="99243-110">Normal dağıtım paketi R işlevleri qnorm rnorm ve pnorm, hangi R istatistikleri paketindeki temel alır.</span><span class="sxs-lookup"><span data-stu-id="99243-110">The Normal Distribution Suite is based on the R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="99243-111">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="99243-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="99243-112">Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek.</span><span class="sxs-lookup"><span data-stu-id="99243-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="99243-113">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="99243-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="99243-114">Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="99243-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="99243-115">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="99243-115">Consumption of web service</span></span>
<span data-ttu-id="99243-116">Normal dağıtım paketi, aşağıdaki 3 Hizmetleri içerir.</span><span class="sxs-lookup"><span data-stu-id="99243-116">The Normal Distribution Suite includes the following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="99243-117">Normal dağıtım Quantile hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="99243-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="99243-118">Bu hizmet normal dağıtım 4 bağımsız değişkenlerini kabul eder ve ilişkili quantile hesaplar.</span><span class="sxs-lookup"><span data-stu-id="99243-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>

<span data-ttu-id="99243-119">Giriş bağımsız değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="99243-119">The input arguments are:</span></span>

* <span data-ttu-id="99243-120">p - normal dağıtım olayla tek bir olasılık.</span><span class="sxs-lookup"><span data-stu-id="99243-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="99243-121">Ortalama - normal dağıtım ortalaması.</span><span class="sxs-lookup"><span data-stu-id="99243-121">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="99243-122">SD - normal dağıtım standart sapması.</span><span class="sxs-lookup"><span data-stu-id="99243-122">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="99243-123">Yan - dağıtım alt tarafında m ve U dağıtım üst tarafındaki için.</span><span class="sxs-lookup"><span data-stu-id="99243-123">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="99243-124">Hizmet verilen olasılık ile ilişkili hesaplanan quantile çıkışıdır.</span><span class="sxs-lookup"><span data-stu-id="99243-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="99243-125">Normal dağıtım olasılık hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="99243-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="99243-126">Bu hizmet normal dağıtım 4 bağımsız değişkenlerini kabul eder ve ilişkili olasılık hesaplar.</span><span class="sxs-lookup"><span data-stu-id="99243-126">This service accepts 4 arguments of a normal distribution and calculates the associated probability.</span></span>

<span data-ttu-id="99243-127">Giriş bağımsız değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="99243-127">The input arguments are:</span></span>

* <span data-ttu-id="99243-128">q bir olayın normal dağıtım ile tek quantile.</span><span class="sxs-lookup"><span data-stu-id="99243-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="99243-129">Ortalama - normal dağıtım ortalaması.</span><span class="sxs-lookup"><span data-stu-id="99243-129">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="99243-130">SD - normal dağıtım standart sapması.</span><span class="sxs-lookup"><span data-stu-id="99243-130">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="99243-131">Yan - dağıtım alt tarafında m ve U dağıtım üst tarafındaki için.</span><span class="sxs-lookup"><span data-stu-id="99243-131">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="99243-132">Hizmet çıktısını verilen quantile ile ilişkili hesaplanan olasılıktır.</span><span class="sxs-lookup"><span data-stu-id="99243-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="99243-133">Normal dağıtım Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="99243-133">Normal Distribution Generator</span></span>
<span data-ttu-id="99243-134">Bu hizmet normal dağıtım 3 bağımsız değişkenlerini kabul eder ve normal olarak dağıtılmış numaraları rastgele bir dizi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99243-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="99243-135">Şu bağımsız değişkenleri için isteği içinde sağlanmasını:</span><span class="sxs-lookup"><span data-stu-id="99243-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="99243-136">n - gözlemleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="99243-136">n - The number of observations.</span></span> 
* <span data-ttu-id="99243-137">Ortalama - normal dağıtım ortalaması.</span><span class="sxs-lookup"><span data-stu-id="99243-137">mean - The normal distribution mean.</span></span>
* <span data-ttu-id="99243-138">SD - normal dağıtım standart sapması.</span><span class="sxs-lookup"><span data-stu-id="99243-138">sd - The normal distribution standard deviation.</span></span> 

<span data-ttu-id="99243-139">Hizmet çıktısı, ortalama ve sd bağımsız değişkenler üzerinde temel normal dağıtım uzunluğu n dizisidir.</span><span class="sxs-lookup"><span data-stu-id="99243-139">The output of the service is a sequence of length n with a normal distribution based on the mean and sd arguments.</span></span>

> <span data-ttu-id="99243-140">Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="99243-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="99243-141">Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (örneğin uygulamalardır burada: [Oluşturucu](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [olasılık hesaplayıcı](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile hesaplayıcı](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="99243-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="99243-142">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="99243-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="99243-143">Normal dağıtım Quantile hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="99243-143">Normal Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="99243-144">Normal dağıtım olasılık hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="99243-144">Normal Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a><span data-ttu-id="99243-145">Normal dağıtım Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="99243-145">Normal Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="99243-146">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="99243-146">Creation of web service</span></span>
> <span data-ttu-id="99243-147">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="99243-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="99243-148">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="99243-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="99243-149">Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="99243-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="99243-150">Normal dağıtım Quantile hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="99243-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="99243-151">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="99243-151">Experiment flow:</span></span>

![Deneme akışı][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="99243-153">Normal dağıtım olasılık hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="99243-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="99243-154">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="99243-154">Experiment flow:</span></span>

![Deneme akışı][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="99243-156">Normal dağıtım Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="99243-156">Normal Distribution Generator</span></span>
<span data-ttu-id="99243-157">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="99243-157">Experiment flow:</span></span>

![Deneme akışı][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="99243-159">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="99243-159">Limitations</span></span>
<span data-ttu-id="99243-160">Bu, normal dağıtım çevreleyen çok basit örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="99243-160">These are very simple examples surrounding the normal distribution.</span></span> <span data-ttu-id="99243-161">Yukarıdaki örnek koddan görüldüğü gibi küçük hata yakalama uygulanır.</span><span class="sxs-lookup"><span data-stu-id="99243-161">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="99243-162">SSS</span><span class="sxs-lookup"><span data-stu-id="99243-162">FAQ</span></span>
<span data-ttu-id="99243-163">Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="99243-163">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

