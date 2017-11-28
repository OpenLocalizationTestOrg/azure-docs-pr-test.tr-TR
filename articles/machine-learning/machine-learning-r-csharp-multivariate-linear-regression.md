---
title: "AAA(deprecated) Multivariate doğrusal regresyon - Azure | Microsoft Docs"
description: "(kullanım dışı) Multivariate doğrusal regresyon"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="32b3a-103">(kullanım dışı) Multivariate doğrusal regresyon</span><span class="sxs-lookup"><span data-stu-id="32b3a-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="32b3a-104">Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="32b3a-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="32b3a-105">Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="32b3a-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="32b3a-106">Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="32b3a-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="32b3a-107">Bağımsız değişkenleri esas alarak her kişi (i) için bir veri kümeniz ve tooquickly gibi bağımlı bir değişken (y) tahmin etmek varsayalım.</span><span class="sxs-lookup"><span data-stu-id="32b3a-107">Suppose you have a dataset and would like tooquickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="32b3a-108">Doğrusal regresyon, bu tür tahminleri için kullanılan yaygın bir istatistik tekniğidir.</span><span class="sxs-lookup"><span data-stu-id="32b3a-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="32b3a-109">Burada hello bağımlı değişken y toobe sürekli bir değeri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="32b3a-109">Here hello dependent variable y is assumed toobe a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="32b3a-110">Basit bir senaryoyu hello araştırmacı toopredict hello kendi yüksekliği (x) dayalı bir kişinin (y) ağırlığını nerede çalışıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="32b3a-110">A simple scenario could be where hello researcher is trying toopredict hello weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="32b3a-111">Daha gelişmiş bir senaryo burada hello araştırmacı hello (gibi ağırlık, cinsiyetiniz, yarış) tek tek ek bilgi ve toopredict hello hello tek ağırlığını çalışır olabilir.</span><span class="sxs-lookup"><span data-stu-id="32b3a-111">A more advanced scenario could be where hello researcher has additional information for hello individual (such as weight, gender, race) and attempts toopredict hello weight of hello individual.</span></span> <span data-ttu-id="32b3a-112">Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) sığar hello doğrusal regresyon modeli toohello veri ve çıkışları her hello gözlemleri hello veri için tahmin edilen bir değer (y) hello.</span><span class="sxs-lookup"><span data-stu-id="32b3a-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits hello linear regression model toohello data and outputs hello predicted value (y) for each of hello observations in hello data.</span></span>

> <span data-ttu-id="32b3a-113">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="32b3a-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="32b3a-114">Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve.</span><span class="sxs-lookup"><span data-stu-id="32b3a-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="32b3a-115">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="32b3a-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="32b3a-116">Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="32b3a-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="32b3a-117">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="32b3a-117">Consumption of web service</span></span>
<span data-ttu-id="32b3a-118">Bu web hizmeti verir hello hello bağımlı tüm hello gözlemleri hello bağımsız değişkenleri göre değişken değerleri tahmin.</span><span class="sxs-lookup"><span data-stu-id="32b3a-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="32b3a-119">Merhaba web hizmeti hello son kullanıcı tooinput veri burada satır (,) virgülle ayrılır ve sütunları noktalı virgülle (;) ayrılmış bir dize bekliyor.</span><span class="sxs-lookup"><span data-stu-id="32b3a-119">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="32b3a-120">Merhaba web hizmeti, aynı anda 1 satır bekler ve hello ilk sütun toobe hello bağımlı değişken bekliyor.</span><span class="sxs-lookup"><span data-stu-id="32b3a-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="32b3a-121">Bir örnek veri kümesini şöyle:</span><span class="sxs-lookup"><span data-stu-id="32b3a-121">An example dataset could look like this:</span></span>

![Örnek veriler][1]

<span data-ttu-id="32b3a-123">Bağımlı bir değişken olmadan gözlemleri "NA" için y girmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="32b3a-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="32b3a-124">Merhaba verileri dataset üzerinde hello için olması hello aşağıdaki dizesi girin: "10 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1, ad 3; 4".</span><span class="sxs-lookup"><span data-stu-id="32b3a-124">hello data input for hello above dataset would be hello following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="32b3a-125">Merhaba hello her hello satır için tahmin edilen değer hello bağımsız değişkenlerine bağlı olduğu çıktı.</span><span class="sxs-lookup"><span data-stu-id="32b3a-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="32b3a-126">Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="32b3a-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="32b3a-127">Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="32b3a-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="32b3a-128">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="32b3a-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="32b3a-129">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="32b3a-129">Creation of web service</span></span>
> <span data-ttu-id="32b3a-130">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="32b3a-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="32b3a-131">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="32b3a-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="32b3a-132">Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="32b3a-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="32b3a-133">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri hello çalışma çekilen.</span><span class="sxs-lookup"><span data-stu-id="32b3a-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="32b3a-134">Bu web hizmeti bir Azure Machine Learning deneme ile temel bir R betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="32b3a-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="32b3a-135">2 bölümleri toothis denemeler vardır: şema tanımı ve eğitim modeli + Puanlama.</span><span class="sxs-lookup"><span data-stu-id="32b3a-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="32b3a-136">Merhaba ilk modülü burada hello ilk değişken hello bağımlı değişken ve hello kalan değişkenleri bağımsız hello girdi veri kümesi, beklenen hello yapısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="32b3a-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="32b3a-137">Merhaba ikinci modül hello giriş verileri için bir genel doğrusal regresyon modeli sığar.</span><span class="sxs-lookup"><span data-stu-id="32b3a-137">hello second module fits a generic linear regression model for hello input data.</span></span>  

![Deneme akışı][3]

#### <a name="module-1"></a><span data-ttu-id="32b3a-139">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="32b3a-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="32b3a-140">Şema tanımı</span><span class="sxs-lookup"><span data-stu-id="32b3a-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="32b3a-141">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="32b3a-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="32b3a-142">LM modelleme</span><span class="sxs-lookup"><span data-stu-id="32b3a-142">LM modeling</span></span>
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a><span data-ttu-id="32b3a-143">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="32b3a-143">Limitations</span></span>
<span data-ttu-id="32b3a-144">Bu, birden çok doğrusal regresyon web hizmeti, çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="32b3a-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="32b3a-145">Yukarıdaki Hello örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hello hizmeti her şeyi (izin verilen kategorik özellikleri yok), sürekli bir değişkeni, hello hizmeti yalnızca girişleri sayısal değer olarak bu web hello oluşturulmasını hello aynı anda varsayar hizmet.</span><span class="sxs-lookup"><span data-stu-id="32b3a-145">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="32b3a-146">Ayrıca, hello Hizmet şu anda sınırlı veri boyutu işlediğinde, hello web hizmeti her çağrıldığında toohello istek/yanıt yapısını hello web hizmeti model hello çağrısı ve hello olgu uygun.</span><span class="sxs-lookup"><span data-stu-id="32b3a-146">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="32b3a-147">SSS</span><span class="sxs-lookup"><span data-stu-id="32b3a-147">FAQ</span></span>
<span data-ttu-id="32b3a-148">Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="32b3a-148">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

