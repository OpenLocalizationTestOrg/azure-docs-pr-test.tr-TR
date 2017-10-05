---
title: "(kullanım dışı) -Üstel Düzeltme - Azure tahmin | Microsoft Docs"
description: "(kullanım dışı) Web hizmeti: tahmin-üstel düzgünleştirme"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: a4150681-6eac-4145-9eca-0cdf60781dde
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 736d5d4adb8ecfd1e3372d273b64917f4a2e76ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a><span data-ttu-id="f97c3-103">(kullanım dışı) Tahmin - Üstel Düzeltme</span><span class="sxs-lookup"><span data-stu-id="f97c3-103">(deprecated) Forecasting - Exponential Smoothing</span></span>

> [!NOTE]
> <span data-ttu-id="f97c3-104">Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="f97c3-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="f97c3-105">Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="f97c3-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f97c3-106">Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f97c3-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="f97c3-107">Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/ets) Üstel Düzeltme modelini (kullanıcı tarafından sağlanan geçmiş verilere dayalı Öngörüler üretmek için madde işaretleri) uygular.</span><span class="sxs-lookup"><span data-stu-id="f97c3-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/ets) implements the Exponential Smoothing model (ETS) to produce predictions based on the historical data provided by the user.</span></span> <span data-ttu-id="f97c3-108">Belirli bir ürün için isteğe bağlı bu yıl artmasına neden olur?</span><span class="sxs-lookup"><span data-stu-id="f97c3-108">Will the demand for a specific product increase this year?</span></span> <span data-ttu-id="f97c3-109">Böylece envanterim planlama etkili miyim Noel sezonu için my ürün satış tahmin edebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="f97c3-109">Can I predict my product sales for the Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="f97c3-110">Tahmin modelleri gibi soruları apt.</span><span class="sxs-lookup"><span data-stu-id="f97c3-110">Forecasting models are apt to address such questions.</span></span> <span data-ttu-id="f97c3-111">Geçmiş verileri verildiğinde, bu modeller gizli eğilimleri ve gelecekteki eğilimleri öngörmek için mevsimselliğin inceleyin.</span><span class="sxs-lookup"><span data-stu-id="f97c3-111">Given the past data, these models examine hidden trends and seasonality to predict future trends.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="f97c3-112">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="f97c3-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="f97c3-113">Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek.</span><span class="sxs-lookup"><span data-stu-id="f97c3-113">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="f97c3-114">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="f97c3-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="f97c3-115">Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="f97c3-115">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="f97c3-116">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="f97c3-116">Consumption of web service</span></span>
<span data-ttu-id="f97c3-117">Bu hizmet 4 bağımsız değişkenleri kabul eder ve madde işaretleri tahminleri hesaplar.</span><span class="sxs-lookup"><span data-stu-id="f97c3-117">This service accepts 4 arguments and calculates the ETS forecasts.</span></span>
<span data-ttu-id="f97c3-118">Giriş bağımsız değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f97c3-118">The input arguments are:</span></span>

* <span data-ttu-id="f97c3-119">Sıklık - ham verileri (Günlük/Haftalık/ay/üç aylık/Yıllık) sıklığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f97c3-119">Frequency - Indicates the frequency of the raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="f97c3-120">Yatay - gelecekteki zaman çerçevesi tahmin.</span><span class="sxs-lookup"><span data-stu-id="f97c3-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="f97c3-121">Tarih - saat için yeni zaman serisi verilerde ekleme.</span><span class="sxs-lookup"><span data-stu-id="f97c3-121">Date - Add in the new time series data for time.</span></span>
* <span data-ttu-id="f97c3-122">Değer - yeni zaman serisi veri değerlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f97c3-122">Value - Add in the new time series data values.</span></span>

<span data-ttu-id="f97c3-123">Hesaplanan tahmin değerleri hizmet çıkışıdır.</span><span class="sxs-lookup"><span data-stu-id="f97c3-123">The output of the service is the calculated forecast values.</span></span>

<span data-ttu-id="f97c3-124">Örnek giriş aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="f97c3-124">Sample input could be:</span></span> 

* <span data-ttu-id="f97c3-125">Sıklık - 12</span><span class="sxs-lookup"><span data-stu-id="f97c3-125">Frequency - 12</span></span>
* <span data-ttu-id="f97c3-126">Yatay - 12</span><span class="sxs-lookup"><span data-stu-id="f97c3-126">Horizon - 12</span></span>
* <span data-ttu-id="f97c3-127">Tarih - 15/1/2012; 15/2/2012 3/15/2012; 15/4/2012; 15/5/2012; 15/6/2012; 15/7/2012; 8 / 15/2012; 15/9/2012; 15/10/2012; 15/11/2012; 12/15/2012; 15/1/2013 15/2/2013 15/3/2013; 15/4/2013; 15/5/2013; 15/6/2013; 15/7/2013; 8 / 15/2013 15/9/2013 15/10/2013; 15/11/2013; 12/15/2013; 15/1/2014 15/2/2014; 15/3/2014; 15/4/2014; 15/5/2014; 15/6/2014; 15/7/2014; 8 / 15/2014; 15/9/2014</span><span class="sxs-lookup"><span data-stu-id="f97c3-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="f97c3-128">Değer - 3.479; 3.68; 3.832; 3.941; 3.797; 3.586; 3.508; 3.731; 3.915; 3.844; 3.634; 3.549; 3.557; 3.785; 3.782; 3.601; 3.544; 3.556; 3.65; 3.709; 3.682; 3.511; 3.429 3.51; 3.523; 3.525; 3.626; 3.695; 3.711; 3.711; 3.693; 3.571; 3.509</span><span class="sxs-lookup"><span data-stu-id="f97c3-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="f97c3-129">Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="f97c3-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="f97c3-130">Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="f97c3-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="f97c3-131">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="f97c3-131">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }



## <a name="creation-of-web-service"></a><span data-ttu-id="f97c3-132">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="f97c3-132">Creation of web service</span></span>
> <span data-ttu-id="f97c3-133">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="f97c3-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="f97c3-134">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="f97c3-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="f97c3-135">Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="f97c3-135">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="f97c3-136">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu.</span><span class="sxs-lookup"><span data-stu-id="f97c3-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="f97c3-137">Örnek giriş verilerini önceden tanımlanmış veri şeması ile karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="f97c3-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="f97c3-138">Verilere bağlı şeması bir [R betiği yürütün] [ execute-r-script] r 'madde işaretleri' ve 'tahmin' işlevlerden kullanarak modeli tahmin madde işaretleri oluşturur Modülü</span><span class="sxs-lookup"><span data-stu-id="f97c3-138">Linked to the data schema is an [Execute R Script][execute-r-script] module that generates the ETS forecasting model by using ‘ets’ and ‘forecast’ functions from R.</span></span> 

![Deneme akışı][2]

#### <a name="module-1"></a><span data-ttu-id="f97c3-140">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="f97c3-140">Module 1:</span></span>
    # Add in the CSV file with the data in the format shown below 
![Veri örneği][3]    

#### <a name="module-2"></a><span data-ttu-id="f97c3-142">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="f97c3-142">Module 2:</span></span>
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- ets(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a><span data-ttu-id="f97c3-143">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="f97c3-143">Limitations</span></span>
<span data-ttu-id="f97c3-144">Madde işaretleri tahmin için çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="f97c3-144">This is a very simple example for ETS forecasting.</span></span> <span data-ttu-id="f97c3-145">Yukarıdaki örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hizmeti varsayar tüm değişkenleri sürekli/pozitif değerler ve sıklığı 1'den büyük bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f97c3-145">As can be seen from the example code above, no error catching is implemented, and the service assumes that all the variables are continuous/positive values and the frequency should be an integer greater than 1.</span></span> <span data-ttu-id="f97c3-146">Tarih ve değer vektörlerinin uzunluğu aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f97c3-146">The length of the date and value vectors should be the same.</span></span> <span data-ttu-id="f97c3-147">Tarih değişkeni ' aa/gg/yyyy' biçimine uyması.</span><span class="sxs-lookup"><span data-stu-id="f97c3-147">The date variable should adhere to the format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="f97c3-148">SSS</span><span class="sxs-lookup"><span data-stu-id="f97c3-148">FAQ</span></span>
<span data-ttu-id="f97c3-149">Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f97c3-149">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

