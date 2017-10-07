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
# <a name="deprecated-cluster-model"></a>(kullanım dışı) Küme modeli

> [!NOTE]
> Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Sipariş tooreduce hello ücret dışı riskini kredi kartı verenler kredi cardholders davranışlarının grupları'tahmin etmek nasıl biz? Nasıl biz performanslarını işyerindeki sipariş tooimprove kişilik nitelikler çalışanların grupları tanımlayabileceğiniz? Nasıl Doktorlar hastalar kendi diseases hello özelliklerine göre gruplar halinde sınıflandırabilirsiniz? Temelde, tüm Bu soruların yanıtları küme çözümlemesi yanıtlanması.   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Küme analiz gözlemleri gruplara değişkenleri birleşimlerini üzerinde temel iki veya daha fazla birbirini dışlayan bilinmeyen bir dizi sınıflandırır. Küme analiz Hello amacı, nereye hello gruplarının üyeleri özellikleri paylaşır toodiscover gözlemleri, genellikle kişiler veya kendi özellikleri gruplar halinde düzenleme sistem budur. Bu [hizmet](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) kullandığı hello K-ortalamaları yöntemi, yaygın olarak kullanılan bir kümeleme teknik gruplar halinde toocluster rastgele veriler. Bu web Hizmeti'nin hello verileri alır ve k hello sayısı giriş olarak kümeleri ve her gözlem ait hello k grupları toowhich biri tahminleri üretir. 

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi. Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.  
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Bu web Hizmeti'nin, her satır için k grupları ve çıkışları hello Grup ataması kümesine hello veri gruplandırır. Merhaba web hizmeti hello son kullanıcı tooinput veri burada satır (,) virgülle ayrılır ve sütunları noktalı virgülle (;) ayrılmış bir dize bekliyor. Merhaba web hizmeti, aynı anda 1 satır bekliyor. Bir örnek veri kümesini şöyle:

![Örnek veriler][1]

Merhaba isteyen kullanıcı tooseparate 3 birbirini dışlayan gruplar halinde bu verileri varsayalım. Merhaba dataset üzerinde hello hello aşağıdaki olacaktır için giriş verileri: değer = "10 5; 2,18; 1; 6,7; 5; 5,22; 3; 4,12; 2; 1,10; 3; 4"; k = "3". Merhaba çıkış olduğu hello tahmin edilen Grup üyeliği her hello satır.

> Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Web hizmet tüketimi için C# kodunu başlatılıyor:
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




## <a name="creation-of-web-service"></a>Web hizmeti oluşturma
> Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu. Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml). Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.
> 
> 

Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri çekilen hello çalışma. Merhaba veri şeması ile basit bir oluşturulduğu [R betiği yürütün][execute-r-script]. Ardından, bağlantılı toohello hello veri şeması olan küme modeli bölümünde, yeniden oluşturulan bir [R betiği yürütün][execute-r-script]. Merhaba, [R betiği yürütün] [ execute-r-script] hello küme modeli için kullanılan, hello web hizmet ardından hello önceden oluşturulmuş hello "k-ortalamaları" işlevi kullanan [R betiği yürütün] [ execute-r-script] Azure Machine Learning.    

![Deneme akışı][3]

#### <a name="module-1"></a>Modül 1:
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a>Modül 2:
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


## <a name="limitations"></a>Sınırlamalar
Bu, kümeleme web hizmetinin çok basit bir örnektir. Yukarıdaki Hello örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hello hizmeti her şeyi (izin verilen kategorik özellikleri yok), sürekli bir değişkeni, hello hizmeti yalnızca girişleri sayısal değer olarak bu web hello oluşturulmasını hello aynı anda varsayar hizmet. Ayrıca, hello Hizmet şu anda sınırlı veri boyutu işlediğinde, hello web hizmeti her çağrıldığında toohello istek/yanıt yapısını hello web hizmeti model hello çağrısı ve hello olgu uygun. 

## <a name="faq"></a>SSS
Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

