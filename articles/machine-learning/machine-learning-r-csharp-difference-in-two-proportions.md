---
title: "(kullanım dışı) Oranları Test - Azure fark | Microsoft Docs"
description: "(kullanım dışı) Oranları Test fark"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a08f91ca76eef2562caeb9eb64cec5e549ed2f5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-difference-in-proportions-test"></a>(kullanım dışı) Oranları Test fark

> [!NOTE]
> Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

İki oranları istatistiksel olarak fark nedir? Karşılaştırılacak kullanıcının istediğini varsayın bir filmi önemli ölçüde daha büyük bir kısmının olup olmadığını belirlemek için iki filmler 'yöntemlerine' ne zaman diğer karşılaştırılan. Büyük bir örnekle 0,50 ve 0.51 oranları arasında istatistiksel olarak önemli bir fark olabilir. Küçük bir örnekle olmayabilir bu oranları gerçekte farklı olup olmadığını belirlemek için yeterli veri. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/prop_test) iki oranları başarı sayısını ve 2 karşılaştırma grupları için deneme sayısı toplam kullanıcı girişi temel fark, bir varsayım sınaması yürütür. Bir olası senaryoda, bu web Hizmeti'nin filmler birini gerçekten 'diğerini kıyasla daha sık film derecelendirmelerine dayalı ilişkilendirilmiş olup olmadığını' kullanıcıya söyleyen bir filmi karşılaştırma uygulamada çağrılabilir.

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi. Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Bu hizmet 4 bağımsız değişkenleri kabul eder ve bir varsayım oranlarını test yapar.

Giriş bağımsız değişkenleri şunlardır:

* Successes1 - 1 örnekteki başarı olayların sayısı.
* Successes2 - örnek 2 başarı olayları sayısı.
* Total1 - 1 örnek boyutu.
* Total2 - örnek 2 boyutu.

Hizmet çıktısını varsayımını sonucudur test chi-square istatistik, df, p değeri ile birlikte ve oran örnek 1/2 ve güvenilirlik aralığını sınırları içinde.

> Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Web hizmet tüketimi için C# kodunu başlatılıyor:
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
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
> Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu. Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml). Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.
> 
> 

Azure Machine Learning içinde yeni bir boş deneme iki oluşturulduğu [R betiği yürütün] [ execute-r-script] modüller. Veri şeması tanımlanan ilk modülünde ikinci 2 oranlarını varsayım testi gerçekleştirmek için R içindeki prop.test komut modülü kullanır. 

### <a name="experiment-flow"></a>Deneme akışı:
![Deneme akışı][2]

#### <a name="module-1"></a>Modül 1:
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data to output port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a>Modül 2:
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"The proportions are different!",
    "The proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a>Sınırlamalar
Bu, 2 oranları fark testi için çok basit bir örnektir. Yukarıdaki örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hizmetin tüm değişkenleri sürekli olduğunu varsayar.

## <a name="faq"></a>SSS
Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

