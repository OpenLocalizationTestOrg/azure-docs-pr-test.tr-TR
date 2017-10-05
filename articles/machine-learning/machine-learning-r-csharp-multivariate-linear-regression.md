---
title: "(kullanım dışı) Multivariate doğrusal regresyon - Azure | Microsoft Docs"
description: "(kullanım dışı) Multivariate doğrusal regresyon"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
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
ms.openlocfilehash: 65a8005139e920cd19593e954fc1bf836354bdf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-multivariate-linear-regression"></a>(kullanım dışı) Multivariate doğrusal regresyon

> [!NOTE]
> Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Bağımsız değişkenleri esas alarak her kişi (i) için bir veri kümeniz ve hızlı bir şekilde bağımlı bir değişken (y) tahmin etmek istediğiniz varsayalım. Doğrusal regresyon, bu tür tahminleri için kullanılan yaygın bir istatistik tekniğidir. Burada bağımlı değişken y sürekli bir değeri olduğu varsayılır.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Basit bir senaryoyu araştırmacı kendi yüksekliği (x) dayalı bir kişinin (y) ağırlığını tahmin etmek nerede çalışıyor olabilir. Daha gelişmiş bir senaryo araştırmacı burada ek bilgi için (örneğin, ağırlık, cinsiyetiniz, yarış) tek tek ve tek tek ağırlığını tahmin etmek çalışır olabilir. Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) veriler için doğrusal regresyon modeli sığar ve tahmin edilen bir değer (y) her veri gözlemleri çıkarır.

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi. Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.  
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Bu web hizmeti tüm gözlemleri bağımsız değişkenleri göre bağımlı değişkenin tahmin edilen değerler sağlar. Web hizmeti burada satır (,) virgülle ayrılır ve sütunları noktalı virgülle (;) ayrılmış bir dize olarak veri girişi için son kullanıcı bekliyor. Web hizmeti, aynı anda 1 satır bekler ve ilk sütun bağımlı değişkenin olmasını bekler. Bir örnek veri kümesini şöyle:

![Örnek veriler][1]

Bağımlı bir değişken olmadan gözlemleri "NA" için y girmelisiniz. Yukarıdaki veri kümesi aşağıdaki dize şöyle için giriş verileri: "10 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1, ad 3; 4". Çıktı, her bağımsız değişkenleri esas alarak satır için tahmin edilen değerdir. 

> Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Web hizmet tüketimi için C# kodunu başlatılıyor:
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




## <a name="creation-of-web-service"></a>Web hizmeti oluşturma
> Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu. Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml). Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.
> 
> 

Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri çalışma çekilen. Bu web hizmeti bir Azure Machine Learning deneme ile temel bir R betiği çalıştırır. Bu deneme 2 bölümü vardır: şema tanımı ve eğitim modeli + Puanlama. İlk modülü burada ilk değişkenin bağımlı değişken ve kalan değişkenleri bağımsız girdi veri kümesi, beklenen yapısını tanımlar. İkinci modül giriş verileri için bir genel doğrusal regresyon modeli sığar.  

![Deneme akışı][3]

#### <a name="module-1"></a>Modül 1:
#### <a name="schema-definition"></a>Şema tanımı
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a>Modül 2:
#### <a name="lm-modeling"></a>LM modelleme
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a>Sınırlamalar
Bu, birden çok doğrusal regresyon web hizmeti, çok basit bir örnektir. Yukarıdaki örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hizmetin her şeyi sürekli bir değişken (izin verilen kategorik özellikleri yok), hizmet girişleri sayısal değerler yalnızca bu web hizmeti oluşturma zamanında olduğunu varsayar. Ayrıca, hizmet şu anda sınırlı veri boyutu son web hizmeti çağrısı ve model web hizmeti adlı her zaman uygun olduğunu olgu istek/yanıt yapısı işler. 

## <a name="faq"></a>SSS
Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

