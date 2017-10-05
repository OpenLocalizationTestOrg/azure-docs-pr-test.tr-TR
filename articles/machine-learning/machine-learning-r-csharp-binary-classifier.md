---
title: "(kullanım dışı) İkili sınıflandırıcı - Azure | Microsoft Docs"
description: "(kullanım dışı) İkili sınıflandırıcı"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
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
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a>(kullanım dışı) İkili sınıflandırıcı

> [!NOTE]
> Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Bir veri kümeniz ve bağımsız değişkenlere bağlı bir ikili bağımlı değişken tahmin etmek istediğiniz varsayalım. 'Lojistik regresyon', bu tür tahminleri için kullanılan yaygın bir istatistik tekniğidir. Bağımlı Değişken İkili veya dichotomous işte ve p ilgi karakteristiğini varlığını olasılıktır. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Basit bir senaryoyu olası Öğrenci (yüksek okul, aile gelir, yerleşik durumu GPA cinsiyet) bilgilerine dayalı bir üniversite için bir giriş teklifini kabul etmek büyük olasılıkla olup olmadığını tahmin etmek bir araştırmacı nerede çalışıyor olabilir. Tahmin edilen sonucu giriş teklifini kabul olası Öğrenci olasılıktır. Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/log_regression) verilere Lojistik regresyon modeli sığar ve her veri gözlemleri (y) olasılık değeri çıkarır.  

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi. Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.  
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Bu web hizmeti tüm gözlemleri bağımsız değişkenleri göre bağımlı değişkenin tahmin edilen değerler sağlar. Web hizmeti burada satırları virgül (,) tarafından ayrılır ve sütunları noktalı virgül (;) ayrılmış bir dize olarak veri girişi için son kullanıcı bekliyor. Web hizmeti, aynı anda 1 satır bekler ve ilk sütun bağımlı değişkenin olmasını bekler. Bir örnek veri kümesini şöyle:

![Örnek veriler][1]

Bağımlı bir değişken olmadan gözlemleri "NA" için y girmelisiniz. Yukarıdaki veri kümesi aşağıdaki dize şöyle için giriş verileri: "1; 5; 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, BELİRTİLMEYEN; 3; 4". Çıktı, her bağımsız değişkenleri esas alarak satır için tahmin edilen değerdir. 

> Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).

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

Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri çekilen çalışma. Bu web hizmeti bir Azure Machine Learning deneme ile temel bir R betiği çalıştırır. Bu deneme 2 bölümü vardır: şema tanımı ve eğitim modeli + Puanlama. İlk modülü burada ilk değişkenin bağımlı değişken ve kalan değişkenleri bağımsız girdi veri kümesi, beklenen yapısını tanımlar. İkinci modül giriş verileri için bir genel Lojistik regresyon modeli sığar.    

![Deneme akışı][2]

#### <a name="module-1"></a>Modül 1:
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a>Modül 2:
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a>Sınırlamalar
Bu ikili sınıflandırma web hizmeti çok basit bir örnektir. Yukarıdaki örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hizmetin her şeyi ikili/sürekli bir değişken (izin verilen kategorik özellikleri yok), hizmet girişleri sayısal değerler yalnızca bu web hizmeti oluşturma zamanında olduğunu varsayar . Ayrıca, hizmet şu anda sınırlı veri boyutu son web hizmeti çağrısı ve model web hizmeti adlı her zaman uygun olduğunu olgu istek/yanıt yapısı işler. 

## <a name="faq"></a>SSS
Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

