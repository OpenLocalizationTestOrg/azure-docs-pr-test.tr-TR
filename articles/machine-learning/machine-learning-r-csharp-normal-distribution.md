---
title: "(kullanım dışı) Normal dağıtım Web hizmeti Suite - Azure | Microsoft Docs"
description: "(kullanım dışı) Normal dağıtım Web hizmet paketi"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 79d1621330ad56b0c62ca46cfac424c2306e371f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-normal-distribution-suite"></a>(kullanım dışı) Normal dağıtım paketi

> [!NOTE]
> Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Normal dağıtım paketi örnek web hizmetleri kümesidir ([Oluşturucu](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile hesaplayıcı](https://datamarket.azure.com/dataset/aml_labs/ndq5), [olasılık hesaplayıcı](https://datamarket.azure.com/dataset/aml_labs/ndp5)) oluşturmak ve normal dağıtım işleme Yardım. Hizmet verilen olasılık gelen quantiles hesaplama ve verilen quantile gelen olasılık hesaplama herhangi bir uzunlukta, normal dağıtım dizisini oluşturma sağlar. Hizmetlerinin her biri farklı çıkışları seçili hizmetini temel alan yayar (Açıklama aşağıya bakın). Normal dağıtım paketi R işlevleri qnorm rnorm ve pnorm, hangi R istatistikleri paketindeki temel alır.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi. Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.  
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Normal dağıtım paketi, aşağıdaki 3 Hizmetleri içerir.

### <a name="normal-distribution-quantile-calculator"></a>Normal dağıtım Quantile hesaplayıcısı
Bu hizmet normal dağıtım 4 bağımsız değişkenlerini kabul eder ve ilişkili quantile hesaplar.

Giriş bağımsız değişkenleri şunlardır:

* p - normal dağıtım olayla tek bir olasılık. 
* Ortalama - normal dağıtım ortalaması.
* SD - normal dağıtım standart sapması. 
* Yan - dağıtım alt tarafında m ve U dağıtım üst tarafındaki için.

Hizmet verilen olasılık ile ilişkili hesaplanan quantile çıkışıdır.

### <a name="normal-distribution-probability-calculator"></a>Normal dağıtım olasılık hesaplayıcısı
Bu hizmet normal dağıtım 4 bağımsız değişkenlerini kabul eder ve ilişkili olasılık hesaplar.

Giriş bağımsız değişkenleri şunlardır:

* q bir olayın normal dağıtım ile tek quantile. 
* Ortalama - normal dağıtım ortalaması.
* SD - normal dağıtım standart sapması. 
* Yan - dağıtım alt tarafında m ve U dağıtım üst tarafındaki için.

Hizmet çıktısını verilen quantile ile ilişkili hesaplanan olasılıktır.

### <a name="normal-distribution-generator"></a>Normal dağıtım Oluşturucusu
Bu hizmet normal dağıtım 3 bağımsız değişkenlerini kabul eder ve normal olarak dağıtılmış numaraları rastgele bir dizi oluşturur. Şu bağımsız değişkenleri için isteği içinde sağlanmasını:

* n - gözlemleri sayısı. 
* Ortalama - normal dağıtım ortalaması.
* SD - normal dağıtım standart sapması. 

Hizmet çıktısı, ortalama ve sd bağımsız değişkenler üzerinde temel normal dağıtım uzunluğu n dizisidir.

> Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (örneğin uygulamalardır burada: [Oluşturucu](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [olasılık hesaplayıcı](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile hesaplayıcı](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Web hizmet tüketimi için C# kodunu başlatılıyor:
### <a name="normal-distribution-quantile-calculator"></a>Normal dağıtım Quantile hesaplayıcısı
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a>Normal dağıtım olasılık hesaplayıcısı
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a>Normal dağıtım Oluşturucusu
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
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
> Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu. Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml). 
> 
> 

Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.

### <a name="normal-distribution-quantile-calculator"></a>Normal dağıtım Quantile hesaplayıcısı
Deneme akışı:

![Deneme akışı][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a>Normal dağıtım olasılık hesaplayıcısı
Deneme akışı:

![Deneme akışı][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a>Normal dağıtım Oluşturucusu
Deneme akışı:

![Deneme akışı][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a>Sınırlamalar
Bu, normal dağıtım çevreleyen çok basit örnek verilmiştir. Yukarıdaki örnek koddan görüldüğü gibi küçük hata yakalama uygulanır.

## <a name="faq"></a>SSS
Web hizmeti veya Azure Marketi'nde yayımlama tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

