---
title: "AAA(deprecated) tahmin - madde işaretleri + STL - Azure | Microsoft Docs"
description: "(kullanım dışı) Tahmin - madde işaretleri + STL"
services: machine-learning
documentationcenter: 
author: xueshanz
manager: jhubbard
editor: cgronlun
ms.assetid: 153eab4d-6293-45e1-9871-ec339e810dd9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 550d423898d46564936fdcfbf05b7c88d2e292c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---ets--stl"></a>(kullanım dışı) Tahmin - madde işaretleri + STL

> [!NOTE]
> Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Bu [web hizmeti](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) hello kullanıcı tarafından sağlanan hello geçmiş verileri temel Mevsimlik eğilimi ayrıştırma (STL) ve üstel yumuşatma (madde işaretleri) modelleri tooproduce tahminleri uygular. İsteğe bağlı bir ürünle artış bu yıl için hello? Böylece envanterim planlama etkili miyim Noel sezonu hello my ürün satışlarının tahmin edebilirsiniz? Tahmin modelleri apt tooaddress gibi sorular vardır. Merhaba verilen gizli eğilimleri ve mevsimselliğin toopredict gelecekteki eğilimleri verileri, bu modeller inceleyin. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi. Ancak hello amacı hello web hizmeti, ayrıca Azure Machine Learning kullanılan toocreate web hizmetleri R kodu en üstünde nasıl olabilir bir örnek olarak tooserve. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Merhaba web hizmeti sonra yayımlanan toohello Azure Marketi olabilir ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu hello web hizmeti hello yazarı tarafından ile Merhaba dünya genelindeki tüketilen.  
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Bu hizmet 4 bağımsız değişkenleri kabul eder ve hello tahminleri hesaplar.
Merhaba giriş bağımsız değişkenleri şunlardır:

* Sıklık - hello ham verileri (Günlük/Haftalık/ay/üç aylık/Yıllık) hello sıklığını belirtir.
* Yatay - gelecekteki zaman çerçevesi tahmin.
* Tarih - hello yeni zaman serisi veri süredir ekleyin.
* Değer - hello yeni zaman serisi veri değerlerini ekleyin.

Merhaba hello hizmet hello tahmin değerler hesaplanan çıkışıdır.

Örnek giriş aşağıdakilerden biri olabilir: 

* Sıklık - 12
* Yatay - 12
* Tarih - 15/1/2012; 15/2/2012 3/15/2012; 15/4/2012; 15/5/2012; 15/6/2012; 15/7/2012; 8 / 15/2012; 15/9/2012; 15/10/2012; 15/11/2012; 12/15/2012; 15/1/2013 15/2/2013 15/3/2013; 15/4/2013; 15/5/2013; 15/6/2013; 15/7/2013; 8 / 15/2013 15/9/2013 15/10/2013; 15/11/2013; 12/15/2013; 15/1/2014 15/2/2014; 15/3/2014; 15/4/2014; 15/5/2014; 15/6/2014; 15/7/2014; 8 / 15/2014; 15/9/2014
* Değer - 3.479; 3.68; 3.832; 3.941; 3.797; 3.586; 3.508; 3.731; 3.915; 3.844; 3.634; 3.549; 3.557; 3.785; 3.782; 3.601; 3.544; 3.556; 3.65; 3.709; 3.682; 3.511; 3.429 3.51; 3.523; 3.525; 3.626; 3.695; 3.711; 3.711; 3.693; 3.571; 3.509

> Bu hizmet Azure Marketi hello üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hello hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Web hizmet tüketimi için C# kodunu başlatılıyor:
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };         var json = JsonConvert.SerializeObject(input);
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

Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu. Örnek giriş verilerini önceden tanımlanmış veri şeması ile karşıya yüklendi. Bağlantılı toohello veri şeması bir [R betiği yürütün] [ execute-r-script] modülü, STL ve madde işaretleri 'stl', 'madde işaretleri' kullanarak tahmin modelleri oluşturur ve 'tahmin' r işlevleri 

### <a name="experiment-flow"></a>Deneme akışı:
![Deneme akışı][2]

#### <a name="module-1"></a>Modül 1:
    # Add in hello CSV file with hello data in hello format shown below 
![Örnek veriler][3]    

#### <a name="module-2"></a>Modül 2:
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- stl(train_ts,  s.window="periodic")
    train_model <- forecast(fit1, h = data$horizon, method = 'ets')
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");

## <a name="limitations"></a>Sınırlamalar
Madde işaretleri + STL için çok basit bir örnek budur tahmin. Yukarıdaki Hello örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hello hizmeti varsayar tüm hello değişkenleri sürekli/pozitif değerler ve hello sıklığı 1'den büyük bir tamsayı olmalıdır. Merhaba uzunluğu başlangıç tarihi ve değer vektörlerinin aynı hello ve hello zaman serisi hello uzunluğu 2'den büyük olmalıdır * sıklığı. Merhaba tarih değişkeni toohello biçimi 'aa/gg/yyyy' uyması.

## <a name="faq"></a>SSS
Merhaba web hizmetinin veya yayımlama toohello Azure Marketi tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img1.png
[2]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img2.png
[3]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

