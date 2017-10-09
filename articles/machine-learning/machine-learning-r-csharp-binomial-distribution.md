---
title: "AAA(deprecated) terimli dağıtım paketi - Azure | Microsoft Docs"
description: "(kullanım dışı) Terimli dağıtım paketi"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a>(kullanım dışı) Terimli dağıtım paketi

> [!NOTE]
> Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Merhaba terimli dağıtım paketi örnek web hizmetleri kümesidir ([terimli Oluşturucu](https://datamarket.azure.com/dataset/aml_labs/bdg5), [olasılık hesaplayıcı](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile hesaplayıcı](https://datamarket.azure.com/dataset/aml_labs/bdq5)) Yardım oluşturmak ve terimli dağıtımları postalarla. Merhaba Hizmetleri quantiles hesaplama herhangi bir uzunlukta terimli dağıtım dizisini oluşturma izin dışında verilen quantile olasılık ve hesaplama olasılık verilen. Merhaba hizmetlerinin her biri farklı çıkışları seçili hello hizmetini temel alan yayar (Açıklama aşağıya bakın). Merhaba terimli dağıtım paketi hello R işlevleri qbinom rbinom ve pbinom, hangi hello R istatistikleri paketine dahil edilen temel alır. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Bu web hizmetleri kullanıcılar tarafından – potansiyel olarak doğrudan bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, bir mobil uygulama üzerinden hello Market üzerinde örneğin kullanılabilecek. Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve Merhaba dünya genelindeki – kullanıcılar ve cihazlar tarafından tüketilen hello web hizmeti hello yazarı tarafından hiçbir altyapı Kurulumu gerekmez.
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Merhaba terimli dağıtım paketi 3 Hizmetleri aşağıdaki hello içerir.

### <a name="binomial-distribution-quantile-calculator"></a>Terimli dağıtım Quantile hesaplayıcısı
Bu hizmet normal dağıtım 4 bağımsız değişkenlerini kabul eder ve ilişkili hello quantile hesaplar.
Merhaba giriş bağımsız değişkenleri şunlardır:

* p - birden çok deneme olasılığını tek bir araya getirilir.  
* boyutu - hello deneme sayısı.
* olasılık - başarı bir deneme hello olasılık.
* Yan - M hello dağıtımının hello dağıtım üst tarafındaki hello U hello alt tarafı için. 

Merhaba hello hizmet olasılık verilen hello ile ilişkili hesaplanan hello quantile çıkışıdır.

### <a name="binomial-distribution-probability-calculator"></a>Terimli dağıtım olasılık hesaplayıcısı
Bu hizmet terimli dağıtım 4 bağımsız değişkenlerini kabul eder ve ilişkili hello olasılık hesaplar.
Merhaba giriş bağımsız değişkenleri şunlardır:

* q bir olayın terimli dağılımı ile tek quantile. 
* boyutu - hello deneme sayısı.
* olasılık - başarı bir deneme hello olasılık.
* yan - M hello dağıtım, U hello üst tarafı hello dağıtım için ya da eşit tooa tek sayısı eşiğidir E hello alt tarafı için.

Merhaba çıktı hello hizmetinin quantile verilen hello ile ilişkili hesaplanan hello olasılıktır.

### <a name="binomial-distribution-generator"></a>Terimli dağıtım Oluşturucusu
Bu hizmet terimli dağıtım 3 bağımsız değişkenlerini kabul eder ve rastgele bir dizi binomially dağıtılmış sayı oluşturur. Merhaba şu bağımsız değişkenleri tooit hello istek içinde sağlanmış olmalıdır:

* n - gözlemleri sayısı. 
* boyutu - deneme sayısı.
* olasılık - başarı olasılığı.

Merhaba çıktı hello hizmetinin uzunluğu n terimli hello boyutu ve olasılık bağımsız değişkenler üzerinde tabanlı bir dağıtım ile dizisidir.

> Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (örneğin uygulamalardır burada: [Oluşturucu](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [olasılık hesaplayıcı](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile hesaplayıcı](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Web hizmet tüketimi için C# kodunu başlatılıyor:
### <a name="binomial-distribution-quantile-calculator"></a>Terimli dağıtım Quantile hesaplayıcısı
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a>Terimli dağıtım olasılık hesaplayıcısı
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a>Terimli dağıtım Oluşturucusu
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
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

### <a name="binomial-distribution-quantile-calculator"></a>Terimli dağıtım Quantile hesaplayıcısı
![Çalışma alanı oluşturma][4]

#### <a name="module-1"></a>Modül 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a>Modül 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a>Terimli dağıtım olasılık hesaplayıcısı
![Çalışma alanı oluşturma][5]

#### <a name="module-1"></a>Modül 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a>Modül 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a>Terimli dağıtım Oluşturucusu
![Çalışma alanı oluşturma][6]

#### <a name="module-1"></a>Modül 1:
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a>Modül 2:
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a>Sınırlamalar
Bunlar hello terimli dağıtım çevreleyen çok basit örnektir. Yukarıdaki Hello örnek koddan görüldüğü gibi küçük hata yakalama uygulanır.

## <a name="faq"></a>SSS
Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

