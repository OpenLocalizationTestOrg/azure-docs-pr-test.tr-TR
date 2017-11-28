---
title: Azure Machine Learning ile hayatta analiz AAA(deprecated) | Microsoft Docs
description: "(kullanım dışı) Acil ihtiyaç analiz olay oluşumu olasılık"
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="a5e3a-103">(kullanım dışı) Acil ihtiyaç çözümleme</span><span class="sxs-lookup"><span data-stu-id="a5e3a-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="a5e3a-104">Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="a5e3a-105">Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="a5e3a-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="a5e3a-106">Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="a5e3a-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="a5e3a-107">Birçok senaryolarda hello ana sonucu değerlendirme altında hello zaman tooan ilgi etkinliğidir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-107">Under many scenarios, hello main outcome under assessment is hello time tooan event of interest.</span></span> <span data-ttu-id="a5e3a-108">"Bu olay meydana gelir?," başka bir deyişle, hello soru</span><span class="sxs-lookup"><span data-stu-id="a5e3a-108">In other words, hello question “when this event will occur?”</span></span> <span data-ttu-id="a5e3a-109">istedi.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-109">is asked.</span></span> <span data-ttu-id="a5e3a-110">Örnek olarak, burada hello verileri tanımlayan hello geçen süre (gün, yıl, mesafe, vb.) durumlarda hello kadar göz önünde bulundurun (Hastalık relapse, alınan Doktora derece, Fren paneli hatası) ilgi olayı oluşur.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-110">As examples, consider situations where hello data describes hello elapsed time (days, years, mileage, etc.) until hello event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="a5e3a-111">Merhaba veri her örnek, belirli bir nesneye (bir süre bekleyin, öğrencinin, bir araba, vb.) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-111">Each instance in hello data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="a5e3a-112">Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) "ne olay ilgi hello hello olasılık zaman n nesnesinin x tarafından gerçekleştirilecek?" Merhaba soru yanıtlar</span><span class="sxs-lookup"><span data-stu-id="a5e3a-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers hello question “what is hello probability that hello event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="a5e3a-113">Acil ihtiyaç çözümleme modeli sağlayarak, bu web hizmeti kullanıcıların toosupply veri tootrain hello modeli sağlar ve test.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-113">By providing a survival analysis model, this web service enables users toosupply data tootrain hello model and test it.</span></span> <span data-ttu-id="a5e3a-114">Merhaba olay ilgi gerçekleşene kadar hello deneme hello ana temasını toomodel hello hello geçen süre uzunluğu olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-114">hello main theme of hello experiment is toomodel hello length of hello elapsed time until hello event of interest occurs.</span></span> 

> <span data-ttu-id="a5e3a-115">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="a5e3a-116">Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="a5e3a-117">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="a5e3a-118">Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="a5e3a-119">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="a5e3a-119">Consumption of web service</span></span>
<span data-ttu-id="a5e3a-120">Merhaba giriş verisi şeması hello web hizmeti, aşağıdaki tablonun hello gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-120">hello input data schema of hello web service is shown in hello following table.</span></span> <span data-ttu-id="a5e3a-121">Altı bilgi parçalarını hello giriş olarak gerekiyor: eğitim verileri, test verileri, ilgilendiğiniz zaman, "saat" boyutun başlangıç dizini, "olay" boyut ve hello değişken türleri hello dizini (sürekli veya faktörü).</span><span class="sxs-lookup"><span data-stu-id="a5e3a-121">Six pieces of information are needed as hello input: training data, testing data, time of interest, hello index of "time" dimension, hello index of "event" dimension, and hello variable types (continuous or factor).</span></span> <span data-ttu-id="a5e3a-122">Merhaba eğitim verilerini burada hello satırları virgülle ayrılmış ve hello sütunları noktalı virgülle ayrılmış bir dize ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-122">hello training data is represented with a string, where hello rows are separated by comma, and hello columns are separated by semicolon.</span></span> <span data-ttu-id="a5e3a-123">Merhaba hello veri özelliklerini esnek sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-123">hello number of features of hello data is flexible.</span></span> <span data-ttu-id="a5e3a-124">Merhaba giriş dizesi tüm hello öğeler sayısal olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-124">All hello elements in hello input string must be numeric.</span></span> <span data-ttu-id="a5e3a-125">Merhaba başlangıç noktası hello araştırmak bu yana (alma uyuşturucu işleme programları, Öğrenci başlangıç Doktora incelemesi, bir araba toobe başlayarak bir Hasta geçen zaman birimleri (gün, yıl, mesafe, vb.) hello sayısı hello "zaman" boyutu Hello eğitim verileri gösterir güdümlü, vs.) Merhaba (Merhaba hasta döndürme toodrug kullanımı, hello Öğrenci alma hello Doktora derece, hello araba sahip Fren paneli hatası, vb.) ilgi olay gerçekleşene kadar.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-125">In hello training data, hello “time” dimension indicates hello number of time units (days, years, mileage, etc.) elapsed since hello starting point of hello study (a patient receiving drug treatment programs, a student starting PhD study, a car starting toobe driven, etc.) until hello event of interest (hello patient returning toodrug usage, hello student obtaining hello PhD degree, hello car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="a5e3a-126">Merhaba "olay" boyut hello olay ilgi hello hello incelemesi sonunda olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-126">hello “event” dimension indicates whether hello event of interest occurs at hello end of hello study.</span></span> <span data-ttu-id="a5e3a-127">Değerini "olay = 1" olay ilgi hello anlamına gelir oluşur hello "zaman" boyuta göre; belirtilen hello zaman "olay = 0" olay ilgi hello anlamına gelir hello "zaman" boyutu tarafından belirtilen hello zamana göre değil oluştu.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-127">A value of “event=1” means that hello event of interest occurs at hello time indicated by hello “time” dimension; “event=0” means that hello event of interest has not occurred by hello time indicated by hello “time” dimension.</span></span>

* <span data-ttu-id="a5e3a-128">trainingdata - bir karakter dizesi.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-128">trainingdata - A character string.</span></span> <span data-ttu-id="a5e3a-129">Satır virgülle ayrılır ve sütunları noktalı virgülle ayrılır.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="a5e3a-130">Her satır, "saat" boyut, "olay" boyut ve bir göstergesi olduğu değişkenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="a5e3a-131">testingdata - belirli bir nesne için bir göstergesi olduğu değişkenleri içeren veri bir satır.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="a5e3a-132">time_of_interest - faiz n hello geçen süre.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-132">time_of_interest - hello elapsed time of interest n.</span></span>
* <span data-ttu-id="a5e3a-133">index_time - hello sütun dizini hello "zaman" boyutunun (1'den başlayarak).</span><span class="sxs-lookup"><span data-stu-id="a5e3a-133">index_time - hello column index of hello “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="a5e3a-134">index_event - hello sütun dizini hello "olay" boyutun (1'den başlayarak).</span><span class="sxs-lookup"><span data-stu-id="a5e3a-134">index_event - hello column index of hello “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="a5e3a-135">variable_types - noktalı virgül, ayırıcı olarak bir karakter dizesi.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="a5e3a-136">0 sürekli değişkenleri ve 1 faktörü değişkenleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="a5e3a-137">Merhaba çıktı tarafından belirli bir zamanda gerçekleşen bir olay hello olasılıktır.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-137">hello output is hello probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="a5e3a-138">Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-138">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="a5e3a-139">Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="a5e3a-139">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="a5e3a-140">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="a5e3a-140">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




<span data-ttu-id="a5e3a-141">Bu test Hello yorumu aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-141">hello interpretation of this test is as follows.</span></span> <span data-ttu-id="a5e3a-142">Merhaba veri Hello amacı toomodel hello geçen süre kadar hello olduğunu varsayarak hello iki işleme programları birini alınan hello hastalar için toodrug kullanım döndürür.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-142">Assuming hello goal of hello data is toomodel hello elapsed time until hello return toodrug usage for hello patients who received one of hello two treatment programs.</span></span> <span data-ttu-id="a5e3a-143">Merhaba hello web hizmeti okuma çıktısını: hastalar 35 yaşında olan, önceki sahip Uyuşturucu işleme 2 kez hello uzun konut işleme programı, alma ve heroin ve cocaine kullanımı ile toohello Uyuşturucu kullanım döndürme hello %95.64 olasılıktır günü 500.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-143">hello output of hello web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking hello long residential treatment program, and with both heroin and cocaine usage, hello probability of returning toohello drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="a5e3a-144">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5e3a-144">Creation of web service</span></span>
> <span data-ttu-id="a5e3a-145">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="a5e3a-146">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="a5e3a-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="a5e3a-147">Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-147">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="a5e3a-148">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri hello çalışma çekilen.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="a5e3a-149">Merhaba veri şeması ile basit bir oluşturulmuş [R betiği yürütün][execute-r-script], hello giriş veri şeması hello web hizmeti tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-149">hello data schema was created with a simple [Execute R Script][execute-r-script], which defines hello input data schema for hello web service.</span></span> <span data-ttu-id="a5e3a-150">Bu modül ise toohello ikinci bağlantılı [R betiği yürütün] [ execute-r-script] iş ana modülü.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-150">This module is then linked toohello second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="a5e3a-151">Bu modül veri ön işleme, model oluşturmanın ve tahminleri yapar.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="a5e3a-152">Merhaba veri önişlem adımda, uzun bir dize tarafından temsil edilen hello giriş veri dönüştürülen ve veri çerçeveye dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-152">In hello data preprocessing step, hello input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="a5e3a-153">Hello modeli oluşturma adımında, dış R paketi "survival_2.37-7.zip" acil ihtiyaç analizi yürütmek için önce yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-153">In hello model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="a5e3a-154">Merhaba "coxph" işlevi serisi veri işleme görevlerini sonra yürütülür.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-154">Then hello “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="a5e3a-155">Merhaba "coxph" işlevi için acil ihtiyaç analiz Hello ayrıntılarını hello R belgelerinden okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-155">hello details of hello “coxph” function for survival analysis can be read from hello R documentation.</span></span> <span data-ttu-id="a5e3a-156">Merhaba tahmin adımda, bir test örneği hello eğitilen modelini hello "surfit" işlevi ile sağlanan ve hello hayatta eğri bu test örneği için "eğri" değişken olarak üretilir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-156">In hello prediction step, a testing instance is supplied into hello trained model with hello “surfit” function, and hello survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="a5e3a-157">Son olarak, ilgi hello süreyi hello olasılık elde edilir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-157">Finally, hello probability of hello time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="a5e3a-158">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="a5e3a-158">Experiment flow:</span></span>
![Deneme akışı][1]

#### <a name="module-1"></a><span data-ttu-id="a5e3a-160">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="a5e3a-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="a5e3a-161">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="a5e3a-161">Module 2:</span></span>
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="a5e3a-162">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="a5e3a-162">Limitations</span></span>
<span data-ttu-id="a5e3a-163">Bu web hizmeti yalnızca sayısal değerler özellik değişkenleri (sütunları) olarak alabilir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="a5e3a-164">Merhaba "olay" sütunu yalnızca değer 0 veya 1 alabilir.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-164">hello “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="a5e3a-165">Merhaba "zaman" sütununu toobe pozitif bir tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a5e3a-165">hello “time” column needs toobe a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="a5e3a-166">SSS</span><span class="sxs-lookup"><span data-stu-id="a5e3a-166">FAQ</span></span>
<span data-ttu-id="a5e3a-167">Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a5e3a-167">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

