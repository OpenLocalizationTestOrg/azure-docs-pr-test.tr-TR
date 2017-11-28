---
title: "AAA(deprecated) küme modeli - Azure | Microsoft Docs"
description: "(kullanım dışı) Küme modeli"
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="9a871-103">(kullanım dışı) Küme modeli</span><span class="sxs-lookup"><span data-stu-id="9a871-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="9a871-104">Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="9a871-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="9a871-105">Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="9a871-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="9a871-106">Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="9a871-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="9a871-107">Sipariş tooreduce hello ücret dışı riskini kredi kartı verenler kredi cardholders davranışlarının grupları'tahmin etmek nasıl biz?</span><span class="sxs-lookup"><span data-stu-id="9a871-107">How can we predict groups of credit cardholders’ behaviors in order tooreduce hello charge-off risk of credit card issuers?</span></span> <span data-ttu-id="9a871-108">Nasıl biz performanslarını işyerindeki sipariş tooimprove kişilik nitelikler çalışanların grupları tanımlayabileceğiniz?</span><span class="sxs-lookup"><span data-stu-id="9a871-108">How can we define groups of personality traits of employees in order tooimprove their performance at work?</span></span> <span data-ttu-id="9a871-109">Nasıl Doktorlar hastalar kendi diseases hello özelliklerine göre gruplar halinde sınıflandırabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="9a871-109">How can doctors classify patients into groups based on hello characteristics of their diseases?</span></span> <span data-ttu-id="9a871-110">Temelde, tüm Bu soruların yanıtları küme çözümlemesi yanıtlanması.</span><span class="sxs-lookup"><span data-stu-id="9a871-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="9a871-111">Küme analiz gözlemleri gruplara değişkenleri birleşimlerini üzerinde temel iki veya daha fazla birbirini dışlayan bilinmeyen bir dizi sınıflandırır.</span><span class="sxs-lookup"><span data-stu-id="9a871-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="9a871-112">Küme analiz Hello amacı, nereye hello gruplarının üyeleri özellikleri paylaşır toodiscover gözlemleri, genellikle kişiler veya kendi özellikleri gruplar halinde düzenleme sistem budur.</span><span class="sxs-lookup"><span data-stu-id="9a871-112">hello purpose of cluster analysis is toodiscover a system of organizing observations, usually people or their characteristics, into groups, where members of hello groups share properties in common.</span></span> <span data-ttu-id="9a871-113">Bu [hizmet](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) kullandığı hello K-ortalamaları yöntemi, yaygın olarak kullanılan bir kümeleme teknik gruplar halinde toocluster rastgele veriler.</span><span class="sxs-lookup"><span data-stu-id="9a871-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses hello K-Means methodology, a commonly used clustering technique, toocluster arbitrary data into groups.</span></span> <span data-ttu-id="9a871-114">Bu web Hizmeti'nin hello verileri alır ve k hello sayısı giriş olarak kümeleri ve her gözlem ait hello k grupları toowhich biri tahminleri üretir.</span><span class="sxs-lookup"><span data-stu-id="9a871-114">This web service takes hello data and hello number of k clusters as input, and produces predictions of which of hello k groups toowhich each observations belongs.</span></span> 

> <span data-ttu-id="9a871-115">Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi.</span><span class="sxs-lookup"><span data-stu-id="9a871-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="9a871-116">Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve.</span><span class="sxs-lookup"><span data-stu-id="9a871-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="9a871-117">Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="9a871-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="9a871-118">Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.</span><span class="sxs-lookup"><span data-stu-id="9a871-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="9a871-119">Web hizmetinin tüketim</span><span class="sxs-lookup"><span data-stu-id="9a871-119">Consumption of web service</span></span>
<span data-ttu-id="9a871-120">Bu web Hizmeti'nin, her satır için k grupları ve çıkışları hello Grup ataması kümesine hello veri gruplandırır.</span><span class="sxs-lookup"><span data-stu-id="9a871-120">This web service groups hello data into a set of k groups and outputs hello group assignment for each row.</span></span> <span data-ttu-id="9a871-121">Merhaba web hizmeti hello son kullanıcı tooinput veri burada satır (,) virgülle ayrılır ve sütunları noktalı virgülle (;) ayrılmış bir dize bekliyor.</span><span class="sxs-lookup"><span data-stu-id="9a871-121">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="9a871-122">Merhaba web hizmeti, aynı anda 1 satır bekliyor.</span><span class="sxs-lookup"><span data-stu-id="9a871-122">hello web service expects 1 row at a time.</span></span> <span data-ttu-id="9a871-123">Bir örnek veri kümesini şöyle:</span><span class="sxs-lookup"><span data-stu-id="9a871-123">An example dataset could look like this:</span></span>

![Örnek veriler][1]

<span data-ttu-id="9a871-125">Merhaba isteyen kullanıcı tooseparate 3 birbirini dışlayan gruplar halinde bu verileri varsayalım.</span><span class="sxs-lookup"><span data-stu-id="9a871-125">Suppose hello user wanted tooseparate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="9a871-126">Merhaba dataset üzerinde hello hello aşağıdaki olacaktır için giriş verileri: değer = "10 5; 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4"; k = "3".</span><span class="sxs-lookup"><span data-stu-id="9a871-126">hello data input for hello above dataset would be hello following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="9a871-127">Merhaba çıkış olduğu hello tahmin edilen Grup üyeliği her hello satır.</span><span class="sxs-lookup"><span data-stu-id="9a871-127">hello output is hello predicted group membership for each of hello rows.</span></span>

> <span data-ttu-id="9a871-128">Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="9a871-128">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="9a871-129">Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="9a871-129">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="9a871-130">Web hizmet tüketimi için C# kodunu başlatılıyor:</span><span class="sxs-lookup"><span data-stu-id="9a871-130">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="9a871-131">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a871-131">Creation of web service</span></span>
> <span data-ttu-id="9a871-132">Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="9a871-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="9a871-133">Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="9a871-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="9a871-134">Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="9a871-134">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="9a871-135">Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri çekilen hello çalışma.</span><span class="sxs-lookup"><span data-stu-id="9a871-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="9a871-136">Merhaba veri şeması ile basit bir oluşturulduğu [R betiği yürütün][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="9a871-136">hello data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="9a871-137">Ardından, bağlantılı toohello hello veri şeması olan küme modeli bölümünde, yeniden oluşturulan bir [R betiği yürütün][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="9a871-137">Then, hello data schema was linked toohello cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="9a871-138">Merhaba, [R betiği yürütün] [ execute-r-script] hello küme modeli için kullanılan, hello web hizmet ardından hello önceden oluşturulmuş hello "k-ortalamaları" işlevi kullanan [R betiği yürütün] [ execute-r-script] Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9a871-138">In hello [Execute R Script][execute-r-script] used for hello cluster model, hello web service then utilizes hello “k-means” function, which is prebuilt into hello [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Deneme akışı][3]

#### <a name="module-1"></a><span data-ttu-id="9a871-140">Modül 1:</span><span class="sxs-lookup"><span data-stu-id="9a871-140">Module 1:</span></span>
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="9a871-141">Modül 2:</span><span class="sxs-lookup"><span data-stu-id="9a871-141">Module 2:</span></span>
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="9a871-142">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="9a871-142">Limitations</span></span>
<span data-ttu-id="9a871-143">Bu, kümeleme web hizmetinin çok basit bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="9a871-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="9a871-144">Yukarıdaki Hello örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hello hizmeti her şeyi (izin verilen kategorik özellikleri yok), sürekli bir değişkeni, hello hizmeti yalnızca girişleri sayısal değer olarak bu web hello oluşturulmasını hello aynı anda varsayar hizmet.</span><span class="sxs-lookup"><span data-stu-id="9a871-144">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="9a871-145">Ayrıca, hello Hizmet şu anda sınırlı veri boyutu işlediğinde, hello web hizmeti her çağrıldığında toohello istek/yanıt yapısını hello web hizmeti model hello çağrısı ve hello olgu uygun.</span><span class="sxs-lookup"><span data-stu-id="9a871-145">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="9a871-146">SSS</span><span class="sxs-lookup"><span data-stu-id="9a871-146">FAQ</span></span>
<span data-ttu-id="9a871-147">Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9a871-147">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

