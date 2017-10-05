---
title: "(kullanım dışı) İkili sınıflandırıcı - Azure | Microsoft Docs"
description: "(kullanım dışı) İkili sınıflandırıcı"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
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
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="0d76f-103">(kullanım dışı) İkili sınıflandırıcı</span><span class="sxs-lookup"><span data-stu-id="0d76f-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="0d76f-104">Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="0d76f-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="0d76f-105">Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="0d76f-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="0d76f-106">Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0d76f-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="0d76f-107">Bir veri kümeniz ve bağımsız değişkenlere bağlı bir ikili bağımlı değişken tahmin etmek istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="0d76f-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span></span> <span data-ttu-id="0d76f-108">'Lojistik regresyon', bu tür tahminleri için kullanılan yaygın bir istatistik tekniğidir.</span><span class="sxs-lookup"><span data-stu-id="0d76f-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="0d76f-109">Bağımlı Değişken İkili veya dichotomous işte ve p ilgi karakteristiğini varlığını olasılıktır.</span><span class="sxs-lookup"><span data-stu-id="0d76f-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="0d76f-110">Basit bir senaryoyu olası Öğrenci (yüksek okul, aile gelir, yerleşik durumu GPA cinsiyet) bilgilerine dayalı bir üniversite için bir giriş teklifini kabul etmek büyük olasılıkla olup olmadığını tahmin etmek bir araştırmacı nerede çalışıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="0d76f-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="0d76f-111">Tahmin edilen sonucu giriş teklifini kabul olası Öğrenci olasılıktır.</span><span class="sxs-lookup"><span data-stu-id="0d76f-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span></span> <span data-ttu-id="0d76f-112">Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/log_regression) verilere Lojistik regresyon modeli sığar ve her veri gözlemleri (y) olasılık değeri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="0d76f-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span></span>  

> <span data-ttu-id="0d76f-113">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="0d76f-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="0d76f-114">Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek.</span><span class="sxs-lookup"><span data-stu-id="0d76f-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="0d76f-115">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="0d76f-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="0d76f-116">Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="0d76f-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="0d76f-117">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="0d76f-117">Consumption of web service</span></span>
<span data-ttu-id="0d76f-118">Bu web hizmeti tüm gözlemleri bağımsız değişkenleri göre bağımlı değişkenin tahmin edilen değerler sağlar.</span><span class="sxs-lookup"><span data-stu-id="0d76f-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="0d76f-119">Web hizmeti burada satırları virgül (,) tarafından ayrılır ve sütunları noktalı virgül (;) ayrılmış bir dize olarak veri girişi için son kullanıcı bekliyor.</span><span class="sxs-lookup"><span data-stu-id="0d76f-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="0d76f-120">Web hizmeti, aynı anda 1 satır bekler ve ilk sütun bağımlı değişkenin olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="0d76f-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="0d76f-121">Bir örnek veri kümesini şöyle:</span><span class="sxs-lookup"><span data-stu-id="0d76f-121">An example dataset could look like this:</span></span>

![Örnek veriler][1]

<span data-ttu-id="0d76f-123">Bağımlı bir değişken olmadan gözlemleri "NA" için y girmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="0d76f-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="0d76f-124">Yukarıdaki veri kümesi aşağıdaki dize şöyle için giriş verileri: "1; 5; 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, BELİRTİLMEYEN; 3; 4".</span><span class="sxs-lookup"><span data-stu-id="0d76f-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="0d76f-125">Çıktı, her bağımsız değişkenleri esas alarak satır için tahmin edilen değerdir.</span><span class="sxs-lookup"><span data-stu-id="0d76f-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="0d76f-126">Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="0d76f-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="0d76f-127">Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0d76f-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="0d76f-128">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="0d76f-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="0d76f-129">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d76f-129">Creation of web service</span></span>
> <span data-ttu-id="0d76f-130">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="0d76f-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="0d76f-131">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="0d76f-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="0d76f-132">Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="0d76f-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="0d76f-133">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri çekilen çalışma.</span><span class="sxs-lookup"><span data-stu-id="0d76f-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="0d76f-134">Bu web hizmeti bir Azure Machine Learning deneme ile temel bir R betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="0d76f-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="0d76f-135">Bu deneme 2 bölümü vardır: şema tanımı ve eğitim modeli + Puanlama.</span><span class="sxs-lookup"><span data-stu-id="0d76f-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="0d76f-136">İlk modülü burada ilk değişkenin bağımlı değişken ve kalan değişkenleri bağımsız girdi veri kümesi, beklenen yapısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0d76f-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="0d76f-137">İkinci modül giriş verileri için bir genel Lojistik regresyon modeli sığar.</span><span class="sxs-lookup"><span data-stu-id="0d76f-137">The second module fits a generic logistic regression model for the input data.</span></span>    

![Deneme akışı][2]

#### <a name="module-1"></a><span data-ttu-id="0d76f-139">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="0d76f-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="0d76f-140">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="0d76f-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="0d76f-141">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="0d76f-141">Limitations</span></span>
<span data-ttu-id="0d76f-142">Bu ikili sınıflandırma web hizmeti çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="0d76f-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="0d76f-143">Yukarıdaki örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hizmetin her şeyi ikili/sürekli bir değişken (izin verilen kategorik özellikleri yok), hizmet girişleri sayısal değerler yalnızca bu web hizmeti oluşturma zamanında olduğunu varsayar .</span><span class="sxs-lookup"><span data-stu-id="0d76f-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="0d76f-144">Ayrıca, hizmet şu anda sınırlı veri boyutu son web hizmeti çağrısı ve model web hizmeti adlı her zaman uygun olduğunu olgu istek/yanıt yapısı işler.</span><span class="sxs-lookup"><span data-stu-id="0d76f-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="0d76f-145">SSS</span><span class="sxs-lookup"><span data-stu-id="0d76f-145">FAQ</span></span>
<span data-ttu-id="0d76f-146">Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="0d76f-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

