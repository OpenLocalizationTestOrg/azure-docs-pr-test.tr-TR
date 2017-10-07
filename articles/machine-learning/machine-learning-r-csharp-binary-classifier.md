---
title: "AAA(deprecated) ikili sınıflandırıcı - Azure | Microsoft Docs"
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
redirect_document_id: True
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="2192b-103">(kullanım dışı) İkili sınıflandırıcı</span><span class="sxs-lookup"><span data-stu-id="2192b-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="2192b-104">Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="2192b-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="2192b-105">Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="2192b-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="2192b-106">Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="2192b-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="2192b-107">Bir veri kümeniz ve toopredict ikili bağımlı hello bağımsız değişkenlere bağlı bir değişken istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="2192b-107">Suppose you have a dataset and would like toopredict a binary dependent variable based on hello independent variables.</span></span> <span data-ttu-id="2192b-108">'Lojistik regresyon', bu tür tahminleri için kullanılan yaygın bir istatistik tekniğidir.</span><span class="sxs-lookup"><span data-stu-id="2192b-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="2192b-109">Merhaba bağımlı değişken ikili veya dichotomous işte ve p hello hello karakteristiğini ilgi varlığını olasılığı.</span><span class="sxs-lookup"><span data-stu-id="2192b-109">Here hello dependent variable is binary or dichotomous, and p is hello probability of presence of hello characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="2192b-110">Basit bir senaryoyu olası Öğrenci büyük olasılıkla tooaccept (yüksek okul, aile gelir, yerleşik durumu GPA cinsiyet) bilgilere göre bir giriş teklif tooa university olup bir araştırmacı toopredict nerede çalışıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="2192b-110">A simple scenario could be where a researcher is trying toopredict whether a prospective student is likely tooaccept an admission offer tooa university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="2192b-111">Merhaba tahmin edilen sonucu, hello olası öğrencinin hello Giriş teklifi kabul hello olasılıktır.</span><span class="sxs-lookup"><span data-stu-id="2192b-111">hello predicted outcome is hello probability of hello prospective student accepting hello admission offer.</span></span> <span data-ttu-id="2192b-112">Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/log_regression) sığar hello Lojistik regresyon modeli toohello veri ve çıkışları her hello gözlemleri hello verilerdeki olasılık değeri (y) hello.</span><span class="sxs-lookup"><span data-stu-id="2192b-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits hello logistic regression model toohello data and outputs hello probability value (y) for each of hello observations in hello data.</span></span>  

> <span data-ttu-id="2192b-113">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="2192b-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="2192b-114">Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve.</span><span class="sxs-lookup"><span data-stu-id="2192b-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="2192b-115">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="2192b-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="2192b-116">Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="2192b-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="2192b-117">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="2192b-117">Consumption of web service</span></span>
<span data-ttu-id="2192b-118">Bu web hizmeti verir hello hello bağımlı tüm hello gözlemleri hello bağımsız değişkenleri göre değişken değerleri tahmin.</span><span class="sxs-lookup"><span data-stu-id="2192b-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="2192b-119">Merhaba web hizmeti hello son kullanıcı tooinput veri burada satırları virgül (,) tarafından ayrılır ve sütunları noktalı virgül (;) ayrılmış bir dize bekliyor.</span><span class="sxs-lookup"><span data-stu-id="2192b-119">hello web service expects hello end user tooinput data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="2192b-120">Merhaba web hizmeti, aynı anda 1 satır bekler ve hello ilk sütun toobe hello bağımlı değişken bekliyor.</span><span class="sxs-lookup"><span data-stu-id="2192b-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="2192b-121">Bir örnek veri kümesini şöyle:</span><span class="sxs-lookup"><span data-stu-id="2192b-121">An example dataset could look like this:</span></span>

![Örnek veriler][1]

<span data-ttu-id="2192b-123">Bağımlı bir değişken olmadan gözlemleri "NA" için y girmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="2192b-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="2192b-124">Merhaba verileri dataset üzerinde hello için olması hello aşağıdaki dizesi girin: "1; 5; 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, BELİRTİLMEYEN; 3; 4".</span><span class="sxs-lookup"><span data-stu-id="2192b-124">hello data input for hello above dataset would be hello following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="2192b-125">Merhaba hello her hello satır için tahmin edilen değer hello bağımsız değişkenlerine bağlı olduğu çıktı.</span><span class="sxs-lookup"><span data-stu-id="2192b-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="2192b-126">Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="2192b-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="2192b-127">Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="2192b-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="2192b-128">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="2192b-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="2192b-129">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="2192b-129">Creation of web service</span></span>
> <span data-ttu-id="2192b-130">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="2192b-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="2192b-131">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="2192b-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="2192b-132">Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="2192b-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="2192b-133">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri çekilen hello çalışma.</span><span class="sxs-lookup"><span data-stu-id="2192b-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="2192b-134">Bu web hizmeti bir Azure Machine Learning deneme ile temel bir R betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="2192b-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="2192b-135">2 bölümleri toothis denemeler vardır: şema tanımı ve eğitim modeli + Puanlama.</span><span class="sxs-lookup"><span data-stu-id="2192b-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="2192b-136">Merhaba ilk modülü burada hello ilk değişken hello bağımlı değişken ve hello kalan değişkenleri bağımsız hello girdi veri kümesi, beklenen hello yapısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2192b-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="2192b-137">Merhaba ikinci modül hello giriş verileri için bir genel Lojistik regresyon modeli sığar.</span><span class="sxs-lookup"><span data-stu-id="2192b-137">hello second module fits a generic logistic regression model for hello input data.</span></span>    

![Deneme akışı][2]

#### <a name="module-1"></a><span data-ttu-id="2192b-139">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="2192b-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="2192b-140">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="2192b-140">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="2192b-141">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="2192b-141">Limitations</span></span>
<span data-ttu-id="2192b-142">Bu ikili sınıflandırma web hizmeti çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="2192b-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="2192b-143">Yukarıdaki Hello örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hello hizmeti her şeyi (izin verilen kategorik özellikleri yok), ikili/sürekli bir değişkeni, hello hizmeti yalnızca girişleri sayısal değer olarak bu hello oluşturulmasını hello aynı anda varsayar Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="2192b-143">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a binary/continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="2192b-144">Ayrıca, hello Hizmet şu anda sınırlı veri boyutu işlediğinde, hello web hizmeti her çağrıldığında toohello istek/yanıt yapısını hello web hizmeti model hello çağrısı ve hello olgu uygun.</span><span class="sxs-lookup"><span data-stu-id="2192b-144">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="2192b-145">SSS</span><span class="sxs-lookup"><span data-stu-id="2192b-145">FAQ</span></span>
<span data-ttu-id="2192b-146">Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="2192b-146">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

