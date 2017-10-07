---
title: "AAA(deprecated) Multivariate doğrusal regresyon - Azure | Microsoft Docs"
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
redirect_document_id: True
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a>(kullanım dışı) Multivariate doğrusal regresyon

> [!NOTE]
> Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Bağımsız değişkenleri esas alarak her kişi (i) için bir veri kümeniz ve tooquickly gibi bağımlı bir değişken (y) tahmin etmek varsayalım. Doğrusal regresyon, bu tür tahminleri için kullanılan yaygın bir istatistik tekniğidir. Burada hello bağımlı değişken y toobe sürekli bir değeri kabul edilir.  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Basit bir senaryoyu hello araştırmacı toopredict hello kendi yüksekliği (x) dayalı bir kişinin (y) ağırlığını nerede çalışıyor olabilir. Daha gelişmiş bir senaryo burada hello araştırmacı hello (gibi ağırlık, cinsiyetiniz, yarış) tek tek ek bilgi ve toopredict hello hello tek ağırlığını çalışır olabilir. Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) sığar hello doğrusal regresyon modeli toohello veri ve çıkışları her hello gözlemleri hello veri için tahmin edilen bir değer (y) hello.

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi. Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.  
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Bu web hizmeti verir hello hello bağımlı tüm hello gözlemleri hello bağımsız değişkenleri göre değişken değerleri tahmin. Merhaba web hizmeti hello son kullanıcı tooinput veri burada satır (,) virgülle ayrılır ve sütunları noktalı virgülle (;) ayrılmış bir dize bekliyor. Merhaba web hizmeti, aynı anda 1 satır bekler ve hello ilk sütun toobe hello bağımlı değişken bekliyor. Bir örnek veri kümesini şöyle:

![Örnek veriler][1]

Bağımlı bir değişken olmadan gözlemleri "NA" için y girmelisiniz. Merhaba verileri dataset üzerinde hello için olması hello aşağıdaki dizesi girin: "10 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1, ad 3; 4". Merhaba hello her hello satır için tahmin edilen değer hello bağımsız değişkenlerine bağlı olduğu çıktı. 

> Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).

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
> Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu. Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml). Bir ekran görüntüsünü her hello deneyin içinde hello modüllerin hello web hizmeti ve örnek kod oluşturulan hello deneme aşağıdadır.
> 
> 

Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri hello çalışma çekilen. Bu web hizmeti bir Azure Machine Learning deneme ile temel bir R betiği çalıştırır. 2 bölümleri toothis denemeler vardır: şema tanımı ve eğitim modeli + Puanlama. Merhaba ilk modülü burada hello ilk değişken hello bağımlı değişken ve hello kalan değişkenleri bağımsız hello girdi veri kümesi, beklenen hello yapısını tanımlar. Merhaba ikinci modül hello giriş verileri için bir genel doğrusal regresyon modeli sığar.  

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
Bu, birden çok doğrusal regresyon web hizmeti, çok basit bir örnektir. Yukarıdaki Hello örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hello hizmeti her şeyi (izin verilen kategorik özellikleri yok), sürekli bir değişkeni, hello hizmeti yalnızca girişleri sayısal değer olarak bu web hello oluşturulmasını hello aynı anda varsayar hizmet. Ayrıca, hello Hizmet şu anda sınırlı veri boyutu işlediğinde, hello web hizmeti her çağrıldığında toohello istek/yanıt yapısını hello web hizmeti model hello çağrısı ve hello olgu uygun. 

## <a name="faq"></a>SSS
Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

