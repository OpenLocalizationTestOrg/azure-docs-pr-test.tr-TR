---
title: "(kullanım dışı) Tahmin: Autoregressive hareketli ortalama (ARIMA) - Azure tümleşik | Microsoft Docs"
description: "(kullanım dışı) Tahmin - Autoregressive tümleşik hareketli ortalama (ARIMA)"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: 1e0d525f-8a9e-4b42-87e0-c9423f059f8c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 6be76618c8ce5917f8fdfdea851c3ca65f9fddd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-forecasting---autoregressive-integrated-moving-average-arima"></a>(kullanım dışı) Tahmin - Autoregressive tümleşik hareketli ortalama (ARIMA)

> [!NOTE]
> Microsoft DataMarket kullanımdan kaldırıldı ve bu API kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).


Bu [hizmet](https://datamarket.azure.com/dataset/aml_labs/arima) Autoregressive tümleşik hareketli ortalama (kullanıcı tarafından sağlanan geçmiş verilere dayalı Öngörüler üretmek için ARIMA) uygular. Belirli bir ürün için isteğe bağlı bu yıl artmasına neden olur? Böylece envanterim planlama etkili miyim Noel sezonu için my ürün satış tahmin edebilirsiniz? Tahmin modelleri gibi soruları apt. Geçmiş verileri verildiğinde, bu modeller gizli eğilimleri ve gelecekteki eğilimleri öngörmek için mevsimselliğin inceleyin. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Bu web hizmeti tarafından kullanıcılara – potansiyel olarak mobil uygulama, bir Web sitesi aracılığıyla ya da bile yerel bir bilgisayarda, örneğin tüketilmesi. Ancak web hizmetinin amacı, ayrıca Azure Machine Learning web hizmetleri R kodu üstünde oluşturmak için nasıl kullanılabileceği bir örnek olarak hizmet verecek. Yalnızca birkaç satırlık bir R kodu ve Azure Machine Learning Studio içinde bir düğmeye tıklama ile bir deneme R kodu ile oluşturulan ve bir web hizmeti olarak yayımlanan. Web hizmeti için Azure Marketi yayımlanan ve kullanıcılar ve aygıtlar için herhangi bir altyapı Kurulumu yazarı tarafından oluşturulan web hizmeti ile dünya genelindeki tüketilen.
> 
> 

## <a name="consumption-of-web-service"></a>Web hizmetinin tüketim
Bu hizmet 4 bağımsız değişkenleri kabul eder ve ARIMA tahminleri hesaplar.
Giriş bağımsız değişkenleri şunlardır:

* Sıklık - ham verileri (Günlük/Haftalık/ay/üç aylık/Yıllık) sıklığını belirtir.
* Yatay - gelecekteki zaman çerçevesi tahmin.
* Tarih - saat için yeni zaman serisi verilerde ekleme.
* Değer - yeni zaman serisi veri değerlerini ekleyin.

Hesaplanan tahmin değerleri hizmet çıkışıdır. 

Örnek giriş aşağıdakilerden biri olabilir: 

* Sıklık - 12
* Yatay - 12
* Tarih - 15/1/2012; 15/2/2012 3/15/2012; 15/4/2012; 15/5/2012; 15/6/2012; 15/7/2012; 8 / 15/2012; 15/9/2012; 15/10/2012; 15/11/2012; 12/15/2012; 15/1/2013 15/2/2013 15/3/2013; 15/4/2013; 15/5/2013; 15/6/2013; 15/7/2013; 8 / 15/2013 15/9/2013 15/10/2013; 15/11/2013; 12/15/2013; 15/1/2014 15/2/2014; 15/3/2014; 15/4/2014; 15/5/2014; 15/6/2014; 15/7/2014; 8 / 15/2014; 15/9/2014
* Değer - 3.479; 3.68; 3.832; 3.941; 3.797; 3.586; 3.508; 3.731; 3.915; 3.844; 3.634; 3.549; 3.557; 3.785; 3.782; 3.601; 3.544; 3.556; 3.65; 3.709; 3.682; 3.511; 3.429 3.51; 3.523; 3.525; 3.626; 3.695; 3.711; 3.711; 3.693; 3.571; 3.509

> Bu hizmet Azure Marketi üzerinde barındırılan bir OData hizmeti aynıdır; Bu POST veya GET yöntemleri ile çağrılabilir. 
> 
> 

Otomatik bir şekilde hizmetinde tüketen birkaç yolu vardır (bir örnek uygulaması [burada](http://microsoftazuremachinelearning.azurewebsites.net/ArimaForecasting.aspx)).

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
          var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri =  "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";

          var httpClient = new HttpClient();
           httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere","ChangeToAPIKey");
           httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
          var query = httpClient.PostAsync(acitionUri,new StringContent(json));
          var result = query.Result.Content;
          var scoreResult = result.ReadAsStringAsync().Result;
      }

## <a name="creation-of-web-service"></a>Web hizmeti oluşturma
> Bu web hizmeti, Azure Machine Learning kullanılarak oluşturuldu. Denemeler oluşturma tanıtım videoları yanı sıra, ücretsiz deneme için ve [web hizmetleri yayımlama](machine-learning-publish-a-machine-learning-web-service.md), lütfen bkz [azure.com/ml](http://azure.com/ml). Bir ekran görüntüsünü her denemenin içinde modülü için web hizmeti ve örnek kod oluşturulan deneme aşağıdadır.
> 
> 

Azure Machine Learning içinde yeni bir boş deneme oluşturulduğu. Örnek giriş verilerini önceden tanımlanmış veri şeması ile karşıya yüklendi. Verilere bağlı şeması bir [R betiği yürütün] [ execute-r-script] r 'auto.arima' ve 'tahmin' işlevlerden kullanarak modeli tahmin ARIMA oluşturur Modülü 

### <a name="experiment-flow"></a>Deneme akışı:
![Çalışma alanı oluşturma][2]

#### <a name="module-1"></a>Modül 1:
    # Add in the CSV file with the data in the format shown below 
![Çalışma alanı oluşturma][3]    

#### <a name="module-2"></a>Modül 2:
    # data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- auto.arima(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # produce forecasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a>Sınırlamalar
Bu, ARIMA tahmin için çok basit bir örnektir. Yukarıdaki örnek koddan görüldüğü gibi hiçbir hata yakalama uygulanır ve hizmeti varsayar tüm değişkenleri sürekli/pozitif değerler ve sıklığı 1'den büyük bir tamsayı olmalıdır. Tarih ve değer vektörlerinin uzunluğu aynı olmalıdır. Tarih değişkeni ' aa/gg/yyyy' biçimine uyması.

## <a name="faq"></a>SSS
Web hizmeti veya Market yayımlamayı tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-arima/arima-img1.png
[2]: ./media/machine-learning-r-csharp-arima/arima-img2.png
[3]: ./media/machine-learning-r-csharp-arima/arima-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

