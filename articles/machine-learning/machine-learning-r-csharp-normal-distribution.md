---
title: "AAA(deprecated) Normal dağıtım Web hizmeti Suite - Azure | Microsoft Docs"
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
redirect_document_id: True
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="80433-103">(kullanım dışı) Normal dağıtım paketi</span><span class="sxs-lookup"><span data-stu-id="80433-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="80433-104">Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="80433-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="80433-105">Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="80433-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="80433-106">Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="80433-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="80433-107">Merhaba Normal dağıtım paketi örnek web hizmetleri kümesidir ([Oluşturucu](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile hesaplayıcı](https://datamarket.azure.com/dataset/aml_labs/ndq5), [olasılık hesaplayıcı](https://datamarket.azure.com/dataset/aml_labs/ndp5)) oluşturma ve işleme Yardım Normal dağıtımları.</span><span class="sxs-lookup"><span data-stu-id="80433-107">hello Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="80433-108">normal dağıtım sırası quantiles verilen olasılık gelen hesaplama ve verilen quantile gelen olasılık hesaplama herhangi uzunluğu oluşturma Hello hizmetler sağlar.</span><span class="sxs-lookup"><span data-stu-id="80433-108">hello services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="80433-109">Merhaba hizmetlerinin her biri farklı çıkışları seçili hello hizmetini temel alan yayar (Açıklama aşağıya bakın).</span><span class="sxs-lookup"><span data-stu-id="80433-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="80433-110">Merhaba Normal dağıtım paketi hello R işlevleri qnorm rnorm ve pnorm, hangi R istatistikleri paketindeki temel alır.</span><span class="sxs-lookup"><span data-stu-id="80433-110">hello Normal Distribution Suite is based on hello R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="80433-111">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="80433-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="80433-112">Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve.</span><span class="sxs-lookup"><span data-stu-id="80433-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="80433-113">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="80433-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="80433-114">Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="80433-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="80433-115">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="80433-115">Consumption of web service</span></span>
<span data-ttu-id="80433-116">Merhaba Normal dağıtım paketi 3 Hizmetleri aşağıdaki hello içerir.</span><span class="sxs-lookup"><span data-stu-id="80433-116">hello Normal Distribution Suite includes hello following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="80433-117">Normal dağıtım Quantile hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="80433-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="80433-118">Bu hizmet normal dağıtım 4 bağımsız değişkenlerini kabul eder ve ilişkili hello quantile hesaplar.</span><span class="sxs-lookup"><span data-stu-id="80433-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>

<span data-ttu-id="80433-119">Merhaba giriş bağımsız değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="80433-119">hello input arguments are:</span></span>

* <span data-ttu-id="80433-120">p - normal dağıtım olayla tek bir olasılık.</span><span class="sxs-lookup"><span data-stu-id="80433-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="80433-121">Ortalama - hello normal dağıtım ortalaması.</span><span class="sxs-lookup"><span data-stu-id="80433-121">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="80433-122">SD - hello normal dağıtım standart sapması.</span><span class="sxs-lookup"><span data-stu-id="80433-122">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="80433-123">Yan - hello alt tarafı hello dağıtım için m ve U hello dağıtım hello üst tarafı için.</span><span class="sxs-lookup"><span data-stu-id="80433-123">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="80433-124">Merhaba hello hizmet olasılık verilen hello ile ilişkili hesaplanan hello quantile çıkışıdır.</span><span class="sxs-lookup"><span data-stu-id="80433-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="80433-125">Normal dağıtım olasılık hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="80433-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="80433-126">Bu hizmet normal dağıtım 4 bağımsız değişkenlerini kabul eder ve ilişkili hello olasılık hesaplar.</span><span class="sxs-lookup"><span data-stu-id="80433-126">This service accepts 4 arguments of a normal distribution and calculates hello associated probability.</span></span>

<span data-ttu-id="80433-127">Merhaba giriş bağımsız değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="80433-127">hello input arguments are:</span></span>

* <span data-ttu-id="80433-128">q bir olayın normal dağıtım ile tek quantile.</span><span class="sxs-lookup"><span data-stu-id="80433-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="80433-129">Ortalama - hello normal dağıtım ortalaması.</span><span class="sxs-lookup"><span data-stu-id="80433-129">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="80433-130">SD - hello normal dağıtım standart sapması.</span><span class="sxs-lookup"><span data-stu-id="80433-130">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="80433-131">Yan - hello alt tarafı hello dağıtım için m ve U hello dağıtım hello üst tarafı için.</span><span class="sxs-lookup"><span data-stu-id="80433-131">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="80433-132">Merhaba çıktı hello hizmetinin quantile verilen hello ile ilişkili hesaplanan hello olasılıktır.</span><span class="sxs-lookup"><span data-stu-id="80433-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="80433-133">Normal dağıtım Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="80433-133">Normal Distribution Generator</span></span>
<span data-ttu-id="80433-134">Bu hizmet normal dağıtım 3 bağımsız değişkenlerini kabul eder ve normal olarak dağıtılmış numaraları rastgele bir dizi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80433-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="80433-135">Merhaba şu bağımsız değişkenleri tooit hello istek içinde sağlanmış olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="80433-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="80433-136">n - hello gözlemleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="80433-136">n - hello number of observations.</span></span> 
* <span data-ttu-id="80433-137">Ortalama - hello normal dağıtım ortalaması.</span><span class="sxs-lookup"><span data-stu-id="80433-137">mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="80433-138">SD - hello normal dağıtım standart sapması.</span><span class="sxs-lookup"><span data-stu-id="80433-138">sd - hello normal distribution standard deviation.</span></span> 

<span data-ttu-id="80433-139">Merhaba çıktı hello hizmetinin hello ortalama ve sd bağımsız değişkenler üzerinde temel normal dağıtım uzunluğu n dizisidir.</span><span class="sxs-lookup"><span data-stu-id="80433-139">hello output of hello service is a sequence of length n with a normal distribution based on hello mean and sd arguments.</span></span>

> <span data-ttu-id="80433-140">Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="80433-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="80433-141">Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (örneğin uygulamalardır burada: [Oluşturucu](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [olasılık hesaplayıcı](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile hesaplayıcı](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="80433-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="80433-142">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="80433-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="80433-143">Normal dağıtım Quantile hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="80433-143">Normal Distribution Quantile Calculator</span></span>
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


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="80433-144">Normal dağıtım olasılık hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="80433-144">Normal Distribution Probability Calculator</span></span>
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

### <a name="normal-distribution-generator"></a><span data-ttu-id="80433-145">Normal dağıtım Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="80433-145">Normal Distribution Generator</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="80433-146">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="80433-146">Creation of web service</span></span>
> <span data-ttu-id="80433-147">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="80433-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="80433-148">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="80433-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="80433-149">Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="80433-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="80433-150">Normal dağıtım Quantile hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="80433-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="80433-151">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="80433-151">Experiment flow:</span></span>

![Deneme akışı][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="80433-153">Normal dağıtım olasılık hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="80433-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="80433-154">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="80433-154">Experiment flow:</span></span>

![Deneme akışı][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="80433-156">Normal dağıtım Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="80433-156">Normal Distribution Generator</span></span>
<span data-ttu-id="80433-157">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="80433-157">Experiment flow:</span></span>

![Deneme akışı][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="80433-159">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="80433-159">Limitations</span></span>
<span data-ttu-id="80433-160">Bunlar hello normal dağıtım çevreleyen çok basit örnektir.</span><span class="sxs-lookup"><span data-stu-id="80433-160">These are very simple examples surrounding hello normal distribution.</span></span> <span data-ttu-id="80433-161">Yukarıdaki Hello örnek koddan görüldüğü gibi küçük hata yakalama uygulanır.</span><span class="sxs-lookup"><span data-stu-id="80433-161">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="80433-162">SSS</span><span class="sxs-lookup"><span data-stu-id="80433-162">FAQ</span></span>
<span data-ttu-id="80433-163">Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="80433-163">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

