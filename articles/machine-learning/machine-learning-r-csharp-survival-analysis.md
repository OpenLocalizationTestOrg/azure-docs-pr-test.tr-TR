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
# <a name="deprecated-survival-analysis"></a>(kullanım dışı) Acil ihtiyaç çözümleme

> [!NOTE]
> Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Birçok senaryolarda hello ana sonucu değerlendirme altında hello zaman tooan ilgi etkinliğidir. "Bu olay meydana gelir?," başka bir deyişle, hello soru istedi. Örnek olarak, burada hello verileri tanımlayan hello geçen süre (gün, yıl, mesafe, vb.) durumlarda hello kadar göz önünde bulundurun (Hastalık relapse, alınan Doktora derece, Fren paneli hatası) ilgi olayı oluşur. Merhaba veri her örnek, belirli bir nesneye (bir süre bekleyin, öğrencinin, bir araba, vb.) temsil eder.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) "ne olay ilgi hello hello olasılık zaman n nesnesinin x tarafından gerçekleştirilecek?" Merhaba soru yanıtlar Acil ihtiyaç çözümleme modeli sağlayarak, bu web hizmeti kullanıcıların toosupply veri tootrain hello modeli sağlar ve test. Merhaba olay ilgi gerçekleşene kadar hello deneme hello ana temasını toomodel hello hello geçen süre uzunluğu olabilir. 

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi. Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.  
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Merhaba giriş verisi şeması hello web hizmeti, aşağıdaki tablonun hello gösterilir. Altı bilgi parçalarını hello giriş olarak gerekiyor: eğitim verileri, test verileri, ilgilendiğiniz zaman, "saat" boyutun başlangıç dizini, "olay" boyut ve hello değişken türleri hello dizini (sürekli veya faktörü). Merhaba eğitim verilerini burada hello satırları virgülle ayrılmış ve hello sütunları noktalı virgülle ayrılmış bir dize ile temsil edilir. Merhaba hello veri özelliklerini esnek sayısıdır. Merhaba giriş dizesi tüm hello öğeler sayısal olmalıdır. Merhaba başlangıç noktası hello araştırmak bu yana (alma uyuşturucu işleme programları, Öğrenci başlangıç Doktora incelemesi, bir araba toobe başlayarak bir Hasta geçen zaman birimleri (gün, yıl, mesafe, vb.) hello sayısı hello "zaman" boyutu Hello eğitim verileri gösterir güdümlü, vs.) Merhaba (Merhaba hasta döndürme toodrug kullanımı, hello Öğrenci alma hello Doktora derece, hello araba sahip Fren paneli hatası, vb.) ilgi olay gerçekleşene kadar. Merhaba "olay" boyut hello olay ilgi hello hello incelemesi sonunda olup olmadığını belirtir. Değerini "olay = 1" olay ilgi hello anlamına gelir oluşur hello "zaman" boyuta göre; belirtilen hello zaman "olay = 0" olay ilgi hello anlamına gelir hello "zaman" boyutu tarafından belirtilen hello zamana göre değil oluştu.

* trainingdata - bir karakter dizesi. Satır virgülle ayrılır ve sütunları noktalı virgülle ayrılır. Her satır, "saat" boyut, "olay" boyut ve bir göstergesi olduğu değişkenleri içerir.
* testingdata - belirli bir nesne için bir göstergesi olduğu değişkenleri içeren veri bir satır.
* time_of_interest - faiz n hello geçen süre.
* index_time - hello sütun dizini hello "zaman" boyutunun (1'den başlayarak).
* index_event - hello sütun dizini hello "olay" boyutun (1'den başlayarak).
* variable_types - noktalı virgül, ayırıcı olarak bir karakter dizesi. 0 sürekli değişkenleri ve 1 faktörü değişkenleri gösterir.

Merhaba çıktı tarafından belirli bir zamanda gerçekleşen bir olay hello olasılıktır. 

> Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Web hizmet tüketimi için C# kodunu başlatılıyor:
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




Bu test Hello yorumu aşağıdaki gibidir. Merhaba veri Hello amacı toomodel hello geçen süre kadar hello olduğunu varsayarak hello iki işleme programları birini alınan hello hastalar için toodrug kullanım döndürür. Merhaba hello web hizmeti okuma çıktısını: hastalar 35 yaşında olan, önceki sahip Uyuşturucu işleme 2 kez hello uzun konut işleme programı, alma ve heroin ve cocaine kullanımı ile toohello Uyuşturucu kullanım döndürme hello %95.64 olasılıktır günü 500.

## <a name="creation-of-web-service"></a>Web hizmeti oluşturma
> Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu. Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml). Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.
> 
> 

Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri hello çalışma çekilen. Merhaba veri şeması ile basit bir oluşturulmuş [R betiği yürütün][execute-r-script], hello giriş veri şeması hello web hizmeti tanımlar. Bu modül ise toohello ikinci bağlantılı [R betiği yürütün] [ execute-r-script] iş ana modülü. Bu modül veri ön işleme, model oluşturmanın ve tahminleri yapar. Merhaba veri önişlem adımda, uzun bir dize tarafından temsil edilen hello giriş veri dönüştürülen ve veri çerçeveye dönüştürülür. Hello modeli oluşturma adımında, dış R paketi "survival_2.37-7.zip" acil ihtiyaç analizi yürütmek için önce yüklenir. Merhaba "coxph" işlevi serisi veri işleme görevlerini sonra yürütülür. Merhaba "coxph" işlevi için acil ihtiyaç analiz Hello ayrıntılarını hello R belgelerinden okuyabilir. Merhaba tahmin adımda, bir test örneği hello eğitilen modelini hello "surfit" işlevi ile sağlanan ve hello hayatta eğri bu test örneği için "eğri" değişken olarak üretilir. Son olarak, ilgi hello süreyi hello olasılık elde edilir. 

### <a name="experiment-flow"></a>Deneme akışı:
![Deneme akışı][1]

#### <a name="module-1"></a>Modül 1:
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

#### <a name="module-2"></a>Modül 2:
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




## <a name="limitations"></a>Sınırlamalar
Bu web hizmeti yalnızca sayısal değerler özellik değişkenleri (sütunları) olarak alabilir. Merhaba "olay" sütunu yalnızca değer 0 veya 1 alabilir. Merhaba "zaman" sütununu toobe pozitif bir tamsayı olmalıdır.

## <a name="faq"></a>SSS
Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

