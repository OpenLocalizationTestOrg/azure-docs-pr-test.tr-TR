---
title: "AAA(deprecated) ikili sınıflandırıcı - Azure | Microsoft Docs"
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
redirect_document_id: True
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a>(kullanım dışı) İkili sınıflandırıcı

> [!NOTE]
> Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Bir veri kümeniz ve toopredict ikili bağımlı hello bağımsız değişkenlere bağlı bir değişken istediğiniz varsayalım. 'Lojistik regresyon', bu tür tahminleri için kullanılan yaygın bir istatistik tekniğidir. Merhaba bağımlı değişken ikili veya dichotomous işte ve p hello hello karakteristiğini ilgi varlığını olasılığı. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Basit bir senaryoyu olası Öğrenci büyük olasılıkla tooaccept (yüksek okul, aile gelir, yerleşik durumu GPA cinsiyet) bilgilere göre bir giriş teklif tooa university olup bir araştırmacı toopredict nerede çalışıyor olabilir. Merhaba tahmin edilen sonucu, hello olası öğrencinin hello Giriş teklifi kabul hello olasılıktır. Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/log_regression) sığar hello Lojistik regresyon modeli toohello veri ve çıkışları her hello gözlemleri hello verilerdeki olasılık değeri (y) hello.  

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi. Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.  
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Bu web hizmeti verir hello hello bağımlı tüm hello gözlemleri hello bağımsız değişkenleri göre değişken değerleri tahmin. Merhaba web hizmeti hello son kullanıcı tooinput veri burada satırları virgül (,) tarafından ayrılır ve sütunları noktalı virgül (;) ayrılmış bir dize bekliyor. Merhaba web hizmeti, aynı anda 1 satır bekler ve hello ilk sütun toobe hello bağımlı değişken bekliyor. Bir örnek veri kümesini şöyle:

![Örnek veriler][1]

Bağımlı bir değişken olmadan gözlemleri "NA" için y girmelisiniz. Merhaba verileri dataset üzerinde hello için olması hello aşağıdaki dizesi girin: "1; 5; 2,1; 1; 6,0; 5.3; 2.1,0; 5; 5,0; 3; 4,1; 2; 1, BELİRTİLMEYEN; 3; 4". Merhaba hello her hello satır için tahmin edilen değer hello bağımsız değişkenlerine bağlı olduğu çıktı. 

> Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).

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

Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu ve iki [R betiği yürütün] [ execute-r-script] modülleri çekilen hello çalışma. Bu web hizmeti bir Azure Machine Learning deneme ile temel bir R betiği çalıştırır. 2 bölümleri toothis denemeler vardır: şema tanımı ve eğitim modeli + Puanlama. Merhaba ilk modülü burada hello ilk değişken hello bağımlı değişken ve hello kalan değişkenleri bağımsız hello girdi veri kümesi, beklenen hello yapısını tanımlar. Merhaba ikinci modül hello giriş verileri için bir genel Lojistik regresyon modeli sığar.    

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
Bu ikili sınıflandırma web hizmeti çok basit bir örnektir. Yukarıdaki Hello örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hello hizmeti her şeyi (izin verilen kategorik özellikleri yok), ikili/sürekli bir değişkeni, hello hizmeti yalnızca girişleri sayısal değer olarak bu hello oluşturulmasını hello aynı anda varsayar Web hizmeti. Ayrıca, hello Hizmet şu anda sınırlı veri boyutu işlediğinde, hello web hizmeti her çağrıldığında toohello istek/yanıt yapısını hello web hizmeti model hello çağrısı ve hello olgu uygun. 

## <a name="faq"></a>SSS
Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

