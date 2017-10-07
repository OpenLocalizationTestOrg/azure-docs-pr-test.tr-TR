---
title: "AAA(deprecated) tahmin - Üstel Düzeltme - Azure | Microsoft Docs"
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
redirect_document_id: True
ms.openlocfilehash: ebc732d3a47943405b0cb26a373f529a50de9005
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a><span data-ttu-id="6990f-103">(kullanım dışı) Tahmin - Üstel Düzeltme</span><span class="sxs-lookup"><span data-stu-id="6990f-103">(deprecated) Forecasting - Exponential Smoothing</span></span>

> [!NOTE]
> <span data-ttu-id="6990f-104">Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="6990f-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="6990f-105">Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="6990f-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="6990f-106">Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="6990f-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="6990f-107">Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/ets) uygulayan hello Üstel Düzeltme modeli (madde işaretleri) tooproduce tahminleri hello kullanıcı tarafından sağlanan hello geçmiş verileri temel alan.</span><span class="sxs-lookup"><span data-stu-id="6990f-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/ets) implements hello Exponential Smoothing model (ETS) tooproduce predictions based on hello historical data provided by hello user.</span></span> <span data-ttu-id="6990f-108">İsteğe bağlı bir ürünle artış bu yıl için hello?</span><span class="sxs-lookup"><span data-stu-id="6990f-108">Will hello demand for a specific product increase this year?</span></span> <span data-ttu-id="6990f-109">Böylece envanterim planlama etkili miyim Noel sezonu hello my ürün satışlarının tahmin edebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="6990f-109">Can I predict my product sales for hello Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="6990f-110">Tahmin modelleri apt tooaddress gibi sorular vardır.</span><span class="sxs-lookup"><span data-stu-id="6990f-110">Forecasting models are apt tooaddress such questions.</span></span> <span data-ttu-id="6990f-111">Merhaba verilen gizli eğilimleri ve mevsimselliğin toopredict gelecekteki eğilimleri verileri, bu modeller inceleyin.</span><span class="sxs-lookup"><span data-stu-id="6990f-111">Given hello past data, these models examine hidden trends and seasonality toopredict future trends.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="6990f-112">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="6990f-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="6990f-113">Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve.</span><span class="sxs-lookup"><span data-stu-id="6990f-113">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="6990f-114">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="6990f-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="6990f-115">Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="6990f-115">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="6990f-116">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="6990f-116">Consumption of web service</span></span>
<span data-ttu-id="6990f-117">Bu hizmet 4 bağımsız değişkenleri kabul eder ve hello madde işaretleri tahminleri hesaplar.</span><span class="sxs-lookup"><span data-stu-id="6990f-117">This service accepts 4 arguments and calculates hello ETS forecasts.</span></span>
<span data-ttu-id="6990f-118">Merhaba giriş bağımsız değişkenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6990f-118">hello input arguments are:</span></span>

* <span data-ttu-id="6990f-119">Sıklık - hello ham verileri (Günlük/Haftalık/ay/üç aylık/Yıllık) hello sıklığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6990f-119">Frequency - Indicates hello frequency of hello raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="6990f-120">Yatay - gelecekteki zaman çerçevesi tahmin.</span><span class="sxs-lookup"><span data-stu-id="6990f-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="6990f-121">Tarih - hello yeni zaman serisi veri süredir ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6990f-121">Date - Add in hello new time series data for time.</span></span>
* <span data-ttu-id="6990f-122">Değer - hello yeni zaman serisi veri değerlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6990f-122">Value - Add in hello new time series data values.</span></span>

<span data-ttu-id="6990f-123">Merhaba hello hizmet hello tahmin değerler hesaplanan çıkışıdır.</span><span class="sxs-lookup"><span data-stu-id="6990f-123">hello output of hello service is hello calculated forecast values.</span></span>

<span data-ttu-id="6990f-124">Örnek giriş aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="6990f-124">Sample input could be:</span></span> 

* <span data-ttu-id="6990f-125">Sıklık - 12</span><span class="sxs-lookup"><span data-stu-id="6990f-125">Frequency - 12</span></span>
* <span data-ttu-id="6990f-126">Yatay - 12</span><span class="sxs-lookup"><span data-stu-id="6990f-126">Horizon - 12</span></span>
* <span data-ttu-id="6990f-127">Tarih - 15/1/2012; 15/2/2012 3/15/2012; 15/4/2012; 15/5/2012; 15/6/2012; 15/7/2012; 8 / 15/2012; 15/9/2012; 15/10/2012; 15/11/2012; 12/15/2012; 15/1/2013 15/2/2013 15/3/2013; 15/4/2013; 15/5/2013; 15/6/2013; 15/7/2013; 8 / 15/2013 15/9/2013 15/10/2013; 15/11/2013; 12/15/2013; 15/1/2014 15/2/2014; 15/3/2014; 15/4/2014; 15/5/2014; 15/6/2014; 15/7/2014; 8 / 15/2014; 15/9/2014</span><span class="sxs-lookup"><span data-stu-id="6990f-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="6990f-128">Değer - 3.479; 3.68; 3.832; 3.941; 3.797; 3.586; 3.508; 3.731; 3.915; 3.844; 3.634; 3.549; 3.557; 3.785; 3.782; 3.601; 3.544; 3.556; 3.65; 3.709; 3.682; 3.511; 3.429 3.51; 3.523; 3.525; 3.626; 3.695; 3.711; 3.711; 3.693; 3.571; 3.509</span><span class="sxs-lookup"><span data-stu-id="6990f-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="6990f-129">Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="6990f-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="6990f-130">Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="6990f-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="6990f-131">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="6990f-131">Starting C# code for web service consumption:</span></span>
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



## <a name="creation-of-web-service"></a><span data-ttu-id="6990f-132">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="6990f-132">Creation of web service</span></span>
> <span data-ttu-id="6990f-133">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="6990f-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="6990f-134">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="6990f-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="6990f-135">Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="6990f-135">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="6990f-136">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu.</span><span class="sxs-lookup"><span data-stu-id="6990f-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="6990f-137">Örnek giriş verilerini önceden tanımlanmış veri şeması ile karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="6990f-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="6990f-138">Bağlantılı toohello veri şeması bir [R betiği yürütün] [ execute-r-script] oluşturur modülü hello r 'madde işaretleri' ve 'tahmin' işlevlerden kullanarak modeli tahmin madde işaretleri</span><span class="sxs-lookup"><span data-stu-id="6990f-138">Linked toohello data schema is an [Execute R Script][execute-r-script] module that generates hello ETS forecasting model by using ‘ets’ and ‘forecast’ functions from R.</span></span> 

![Deneme akışı][2]

#### <a name="module-1"></a><span data-ttu-id="6990f-140">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="6990f-140">Module 1:</span></span>
    # Add in hello CSV file with hello data in hello format shown below 
![Veri örneği][3]    

#### <a name="module-2"></a><span data-ttu-id="6990f-142">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="6990f-142">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="6990f-143">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="6990f-143">Limitations</span></span>
<span data-ttu-id="6990f-144">Madde işaretleri tahmin için çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="6990f-144">This is a very simple example for ETS forecasting.</span></span> <span data-ttu-id="6990f-145">Yukarıdaki Hello örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hello hizmeti varsayar tüm hello değişkenleri sürekli/pozitif değerler ve hello sıklığı 1'den büyük bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6990f-145">As can be seen from hello example code above, no error catching is implemented, and hello service assumes that all hello variables are continuous/positive values and hello frequency should be an integer greater than 1.</span></span> <span data-ttu-id="6990f-146">Başlangıç tarihi ve değer vektörlerinin Hello uzunluğu olması hello aynı.</span><span class="sxs-lookup"><span data-stu-id="6990f-146">hello length of hello date and value vectors should be hello same.</span></span> <span data-ttu-id="6990f-147">Merhaba tarih değişkeni toohello biçimi 'aa/gg/yyyy' uyması.</span><span class="sxs-lookup"><span data-stu-id="6990f-147">hello date variable should adhere toohello format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="6990f-148">SSS</span><span class="sxs-lookup"><span data-stu-id="6990f-148">FAQ</span></span>
<span data-ttu-id="6990f-149">Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="6990f-149">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

