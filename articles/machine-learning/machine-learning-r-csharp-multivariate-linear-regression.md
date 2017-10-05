---
title: "(kullanım dışı) Multivariate doğrusal regresyon - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 65a8005139e920cd19593e954fc1bf836354bdf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="d20e3-103">(kullanım dışı) Multivariate doğrusal regresyon</span><span class="sxs-lookup"><span data-stu-id="d20e3-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="d20e3-104">Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="d20e3-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="d20e3-105">Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="d20e3-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="d20e3-106">Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d20e3-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="d20e3-107">Bağımsız değişkenleri esas alarak her kişi (i) için bir veri kümeniz ve hızlı bir şekilde bağımlı bir değişken (y) tahmin etmek istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d20e3-107">Suppose you have a dataset and would like to quickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="d20e3-108">Doğrusal regresyon, bu tür tahminleri için kullanılan yaygın bir istatistik tekniğidir.</span><span class="sxs-lookup"><span data-stu-id="d20e3-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="d20e3-109">Burada bağımlı değişken y sürekli bir değeri olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="d20e3-109">Here the dependent variable y is assumed to be a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="d20e3-110">Basit bir senaryoyu araştırmacı kendi yüksekliği (x) dayalı bir kişinin (y) ağırlığını tahmin etmek nerede çalışıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="d20e3-110">A simple scenario could be where the researcher is trying to predict the weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="d20e3-111">Daha gelişmiş bir senaryo araştırmacı burada ek bilgi için (örneğin, ağırlık, cinsiyetiniz, yarış) tek tek ve tek tek ağırlığını tahmin etmek çalışır olabilir.</span><span class="sxs-lookup"><span data-stu-id="d20e3-111">A more advanced scenario could be where the researcher has additional information for the individual (such as weight, gender, race) and attempts to predict the weight of the individual.</span></span> <span data-ttu-id="d20e3-112">Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) veriler için doğrusal regresyon modeli sığar ve tahmin edilen bir değer (y) her veri gözlemleri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="d20e3-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits the linear regression model to the data and outputs the predicted value (y) for each of the observations in the data.</span></span>

> <span data-ttu-id="d20e3-113">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="d20e3-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="d20e3-114">Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek.</span><span class="sxs-lookup"><span data-stu-id="d20e3-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="d20e3-115">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="d20e3-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="d20e3-116">Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="d20e3-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="d20e3-117">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="d20e3-117">Consumption of web service</span></span>
<span data-ttu-id="d20e3-118">Bu web hizmeti tüm gözlemleri bağımsız değişkenleri göre bağımlı değişkenin tahmin edilen değerler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d20e3-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="d20e3-119">Web hizmeti burada satır (,) virgülle ayrılır ve sütunları noktalı virgülle (;) ayrılmış bir dize olarak veri girişi için son kullanıcı bekliyor.</span><span class="sxs-lookup"><span data-stu-id="d20e3-119">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="d20e3-120">Web hizmeti, aynı anda 1 satır bekler ve ilk sütun bağımlı değişkenin olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="d20e3-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="d20e3-121">Bir örnek veri kümesini şöyle:</span><span class="sxs-lookup"><span data-stu-id="d20e3-121">An example dataset could look like this:</span></span>

![Örnek veriler][1]

<span data-ttu-id="d20e3-123">Bağımlı bir değişken olmadan gözlemleri "NA" için y girmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="d20e3-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="d20e3-124">Yukarıdaki veri kümesi aşağıdaki dize şöyle için giriş verileri: "10 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1, ad 3; 4".</span><span class="sxs-lookup"><span data-stu-id="d20e3-124">The data input for the above dataset would be the following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="d20e3-125">Çıktı, her bağımsız değişkenleri esas alarak satır için tahmin edilen değerdir.</span><span class="sxs-lookup"><span data-stu-id="d20e3-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="d20e3-126">Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="d20e3-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="d20e3-127">Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d20e3-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="d20e3-128">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="d20e3-128">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="d20e3-129">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="d20e3-129">Creation of web service</span></span>
> <span data-ttu-id="d20e3-130">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d20e3-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="d20e3-131">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="d20e3-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="d20e3-132">Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="d20e3-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="d20e3-133">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri çalışma çekilen.</span><span class="sxs-lookup"><span data-stu-id="d20e3-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="d20e3-134">Bu web hizmeti bir Azure Machine Learning deneme ile temel bir R betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="d20e3-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="d20e3-135">Bu deneme 2 bölümü vardır: şema tanımı ve eğitim modeli + Puanlama.</span><span class="sxs-lookup"><span data-stu-id="d20e3-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="d20e3-136">İlk modülü burada ilk değişkenin bağımlı değişken ve kalan değişkenleri bağımsız girdi veri kümesi, beklenen yapısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d20e3-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="d20e3-137">İkinci modül giriş verileri için bir genel doğrusal regresyon modeli sığar.</span><span class="sxs-lookup"><span data-stu-id="d20e3-137">The second module fits a generic linear regression model for the input data.</span></span>  

![Deneme akışı][3]

#### <a name="module-1"></a><span data-ttu-id="d20e3-139">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="d20e3-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="d20e3-140">Şema tanımı</span><span class="sxs-lookup"><span data-stu-id="d20e3-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="d20e3-141">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="d20e3-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="d20e3-142">LM modelleme</span><span class="sxs-lookup"><span data-stu-id="d20e3-142">LM modeling</span></span>
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

## <a name="limitations"></a><span data-ttu-id="d20e3-143">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="d20e3-143">Limitations</span></span>
<span data-ttu-id="d20e3-144">Bu, birden çok doğrusal regresyon web hizmeti, çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="d20e3-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="d20e3-145">Yukarıdaki örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hizmetin her şeyi sürekli bir değişken (izin verilen kategorik özellikleri yok), hizmet girişleri sayısal değerler yalnızca bu web hizmeti oluşturma zamanında olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d20e3-145">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="d20e3-146">Ayrıca, hizmet şu anda sınırlı veri boyutu son web hizmeti çağrısı ve model web hizmeti adlı her zaman uygun olduğunu olgu istek/yanıt yapısı işler.</span><span class="sxs-lookup"><span data-stu-id="d20e3-146">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="d20e3-147">SSS</span><span class="sxs-lookup"><span data-stu-id="d20e3-147">FAQ</span></span>
<span data-ttu-id="d20e3-148">Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d20e3-148">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

