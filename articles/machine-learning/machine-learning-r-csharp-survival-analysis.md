---
title: "(kullanım dışı) Azure Machine Learning ile hayatta çözümleme | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7d4066d5f15a39c428d8035257c4841f9b3cc775
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="d3ee8-103">(kullanım dışı) Acil ihtiyaç çözümleme</span><span class="sxs-lookup"><span data-stu-id="d3ee8-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="d3ee8-104">Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="d3ee8-105">Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="d3ee8-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="d3ee8-106">Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d3ee8-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="d3ee8-107">Birçok senaryolarda değerlendirme altında ana sonucu olaya ilgi saattir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span></span> <span data-ttu-id="d3ee8-108">Diğer bir deyişle, "Bu olay meydana gelir?" olduğunda soru</span><span class="sxs-lookup"><span data-stu-id="d3ee8-108">In other words, the question “when this event will occur?”</span></span> <span data-ttu-id="d3ee8-109">istedi.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-109">is asked.</span></span> <span data-ttu-id="d3ee8-110">Örnek olarak, burada verileri tanımlayan geçen süre (gün, yıl, mesafe, vb.) durumlarda faiz (Hastalık relapse, alınan Doktora derece, Fren paneli hatası) olay kadar göz önünde bulundurun oluşur.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="d3ee8-111">Her örnek verileri belirli bir nesneye (bir süre bekleyin, öğrencinin, bir araba, vb.) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="d3ee8-112">Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) "ilgi olay zaman n nesnesinin x tarafından gerçekleşir olasılık nedir?" sorusunu yanıtlar</span><span class="sxs-lookup"><span data-stu-id="d3ee8-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="d3ee8-113">Acil ihtiyaç çözümleme modeli sağlayarak, modeli eğitmek ve test için veri sağlamak kullanıcıların bu web hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span></span> <span data-ttu-id="d3ee8-114">Denemeyi ana temasını ilgi olay gerçekleşene kadar geçen süre modellemektir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span></span> 

> <span data-ttu-id="d3ee8-115">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="d3ee8-116">Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="d3ee8-117">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="d3ee8-118">Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="d3ee8-119">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="d3ee8-119">Consumption of web service</span></span>
<span data-ttu-id="d3ee8-120">Web hizmetinin giriş veri şeması aşağıdaki tabloda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-120">The input data schema of the web service is shown in the following table.</span></span> <span data-ttu-id="d3ee8-121">Altı bilgi parçalarını giriş olarak gerekiyor: verileri eğitim verileri test etme, ilgi, "saat" dizinini zaman boyut, "olay" boyut ve değişken türleri dizini (sürekli veya faktörü).</span><span class="sxs-lookup"><span data-stu-id="d3ee8-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span></span> <span data-ttu-id="d3ee8-122">Eğitim verileri burada satırları virgülle ayrılır ve sütunları noktalı virgülle ayrılmış bir dize ile temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span></span> <span data-ttu-id="d3ee8-123">Veri özellikleri sayısı esnektir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-123">The number of features of the data is flexible.</span></span> <span data-ttu-id="d3ee8-124">Giriş dizisinde tüm öğeler sayısal olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-124">All the elements in the input string must be numeric.</span></span> <span data-ttu-id="d3ee8-125">Eğitim verileri (Uyuşturucu kullanımı, Doktora derece, Fren paneli hataya neden araba alma Öğrenci döndürme hasta ilgi olay kadar (hasta alma uyuşturucu işleme programları, Öğrenci başlangıç Doktora incelemesi, başlangıç güdümlü, vb. bir araba) incelemesi başlangıç noktası itibaren geçen zaman birimleri (gün, yıl, mesafe, vb.) sayısı "zaman" boyutu belirtir. VS.) oluşur.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="d3ee8-126">"Olay" boyut ilgi olay incelemesinde sonunda oluşup oluşmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span></span> <span data-ttu-id="d3ee8-127">Değerini "olay = 1", "saat" boyuta göre; belirtilen saatte ilgi olayı meydana anlamına gelir "olay = 0", "saat" boyutu tarafından belirtilen zaman tarafından ilgi olay gerçekleşmedi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span></span>

* <span data-ttu-id="d3ee8-128">trainingdata - bir karakter dizesi.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-128">trainingdata - A character string.</span></span> <span data-ttu-id="d3ee8-129">Satır virgülle ayrılır ve sütunları noktalı virgülle ayrılır.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="d3ee8-130">Her satır, "saat" boyut, "olay" boyut ve bir göstergesi olduğu değişkenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="d3ee8-131">testingdata - belirli bir nesne için bir göstergesi olduğu değişkenleri içeren veri bir satır.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="d3ee8-132">time_of_interest - faiz n geçen süre.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-132">time_of_interest - The elapsed time of interest n.</span></span>
* <span data-ttu-id="d3ee8-133">index_time - (1'den başlayarak) "saat" boyutun sütun dizini.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-133">index_time - The column index of the “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="d3ee8-134">index_event - (1'den başlayarak) "olay" boyutun sütun dizini.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-134">index_event - The column index of the “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="d3ee8-135">variable_types - noktalı virgül, ayırıcı olarak bir karakter dizesi.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="d3ee8-136">0 sürekli değişkenleri ve 1 faktörü değişkenleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="d3ee8-137">Çıktı tarafından belirli bir zamanda gerçekleşen bir olay olasılıktır.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-137">The output is the probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="d3ee8-138">Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="d3ee8-139">Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d3ee8-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="d3ee8-140">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="d3ee8-140">Starting C# code for web service consumption:</span></span>
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




<span data-ttu-id="d3ee8-141">Bu test yorumu aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-141">The interpretation of this test is as follows.</span></span> <span data-ttu-id="d3ee8-142">Veri amacı varsayılarak Uyuşturucu kullanım için dönüş iki işleme programları birini alınan hastalar için kadar geçen süre model sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span></span> <span data-ttu-id="d3ee8-143">Web hizmeti okuma çıktısı: hastalar 35 yaşında olan, önceki sahip Uyuşturucu işleme 2 kez uzun konut işleme program alma ve heroin ve cocaine kullanımı ile Uyuşturucu kullanım döndürme olasılığı %95.64 gün 500.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="d3ee8-144">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3ee8-144">Creation of web service</span></span>
> <span data-ttu-id="d3ee8-145">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="d3ee8-146">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="d3ee8-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="d3ee8-147">Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="d3ee8-148">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri çalışma çekilen.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="d3ee8-149">Veri şeması ile basit bir oluşturulmuş [R betiği yürütün][execute-r-script], web hizmeti için giriş veri şeması tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span></span> <span data-ttu-id="d3ee8-150">Bu modül sonra ikinci bağlantılı [R betiği yürütün] [ execute-r-script] iş ana modülü.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="d3ee8-151">Bu modül veri ön işleme, model oluşturmanın ve tahminleri yapar.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="d3ee8-152">Veri önişlem adımda, uzun bir dize tarafından temsil edilen giriş verileri dönüştürülen ve veri çerçeveye dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="d3ee8-153">Model oluşturma adımda dış R paketi "survival_2.37-7.zip" acil ihtiyaç analizi yürütmek için önce yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="d3ee8-154">"Coxph" işlevi serisi veri işleme görevlerini sonra yürütülür.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-154">Then the “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="d3ee8-155">"Coxph" işlevi için acil ihtiyaç analiz ayrıntılarını R belgelerinden okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span></span> <span data-ttu-id="d3ee8-156">Tahmin adımda, bir test örneği eğitilen modelini "surfit" işlevi ile sağlanan ve acil ihtiyaç eğri bu test örneği için "eğri" değişken olarak üretilir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="d3ee8-157">Son olarak, ilgilendiğiniz zaman olasılığını elde edilir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-157">Finally, the probability of the time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="d3ee8-158">Deneme akışı:</span><span class="sxs-lookup"><span data-stu-id="d3ee8-158">Experiment flow:</span></span>
![Deneme akışı][1]

#### <a name="module-1"></a><span data-ttu-id="d3ee8-160">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="d3ee8-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="d3ee8-161">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="d3ee8-161">Module 2:</span></span>
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

    # Prepare to build model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct the execution string
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

    # Fit a Cox proportional hazards model and get the predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find the event occurrence probability
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

    #Pull out results to send to web service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="d3ee8-162">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="d3ee8-162">Limitations</span></span>
<span data-ttu-id="d3ee8-163">Bu web hizmeti yalnızca sayısal değerler özellik değişkenleri (sütunları) olarak alabilir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="d3ee8-164">"Olay" sütunu yalnızca değer 0 veya 1 alabilir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-164">The “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="d3ee8-165">"Zaman" sütununu pozitif bir tamsayı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3ee8-165">The “time” column needs to be a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="d3ee8-166">SSS</span><span class="sxs-lookup"><span data-stu-id="d3ee8-166">FAQ</span></span>
<span data-ttu-id="d3ee8-167">Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d3ee8-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

