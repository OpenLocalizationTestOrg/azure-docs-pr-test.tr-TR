---
title: "(kullanım dışı) Machine learning web hizmetleri R - Azure ile oluşturulmuş örnekleri | Microsoft Docs"
description: "(kullanım dışı) Web yararlı bir dizi R kodu ve Machine Learning ile oluşturulan ve Azure Marketi yayımlanan hizmetleri örnekleri bulun."
keywords: "CSharp, r kodu, web Hizmetleri örnekleri"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
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
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a>(kullanım dışı) Web üzerinde Azure Machine Learning kullanarak R kodu örnekleri Hizmetleri ve Microsoft Azure Market'e yayımlanan

> [!NOTE]
> Microsoft DataMarket kullanımdan kaldırıldı ve bu API'leri kullanım dışı bırakıldı. 
> 
> Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com). Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).

Bu makaledeki örnek web hizmetleri Azure Machine Learning kullanarak oluşturulan ve Azure Marketi yayımlanan ' dir. Her web hizmeti örnek Hizmetleri test etmek ve kullanıcı benzer bir hizmet kendilerini nasıl oluşturabileceğinizi açıklayan için örnek veri kümelerini katıştırma bağlı, kapsamlı bir belge sahiptir. 

Azure Machine Learning Studio'da kullanıcılar R kodu yazma ve birkaç tıklama ile uygulama ve cihazlar dünyanın kullanmak web hizmeti olarak yayımlayın. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Bir özel metin araştırma düşünceleri analiz bir göstergesi olduğu oluşturma için istatistik işlevleri sağlayan basit hesaplayıcıları oluşturan öğesinden hem yeni hem de deneyimli R kullanıcılar Azure Machine Learning kullanıcılarının R faaliyete geçirebilirsiniz kolaylığı yararlanabilir kod. Machine Learning nasıl faaliyete geçirebilirsiniz göstermek için bu web hizmetleri olası bir mobil uygulama veya bir Web sitesi, bu web hizmetleri örnekler amacı aracılığıyla kullanıcılar tarafından kullanılabilecek iken R analitik amaçlarla ve komut dosyaları üstte web hizmetleri oluşturmak için kullanılır R kodu.

Her örneğin bir C# örnek web hizmet tüketimi için içerir.

![Azure Machine Learning R kodu diyagramı: kullanın veya Azure Marketi yayımlanan özel R çözümleri.][1]

Aşağıdaki senaryoları göz önünde bulundurun.

## <a name="scenario-1-generic-model"></a>Senaryo 1: Genel modeli
Bir kullanıcı bir temel zaman serisi veri veya gelişmiş analizler özel olarak geliştirilmiş bir R yöntemiyle tahmin gibi yeni kullanıcının verilere uygulanan genel bir modeli ile çalışır. Bu kullanıcı model başkalarının kendi verileri ile kullanmak bir web hizmeti olarak yayımlar.

* [İkili Dosya Sınıflandırıcı](machine-learning-r-csharp-binary-classifier.md)
* [Küme Modeli](machine-learning-r-csharp-cluster-model.md)
* [Çok Değişkenli Doğrusal Regresyon](machine-learning-r-csharp-multivariate-linear-regression.md)
* [Tahmin - Üstel Düzeltme](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [Madde işaretleri + STL tahmin](machine-learning-r-csharp-retail-demand-forecasting.md)
* [Tahmin - Autoregressive tümleşik hareketli ortalama (ARIMA)](machine-learning-r-csharp-arima.md)
* [Yaşam Analizi](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a>Senaryo 2: Eğitilmiş model – belirli veri
Bir kullanıcı gibi büyük bir örnek kullanıcının kişilik türü veya bir kişinin riskini tahmin etmek için kullanılan sistem durumu anket veri tahmin etmek için bir k-ortalamaları algoritması kümelenmiş kişilik formlarının R kodlarda yararlı tahminleri sağlar veriler var. acil ihtiyaç analiz R paketi ile Akciğer kanseri için. Kullanıcı verileri yeni bir kullanıcının sonuç tahmin bir web hizmeti aracılığıyla yayımlar.

## <a name="scenario-3-trained-model--generic-data"></a>Senaryo 3: Eğitilmiş model – genel veriler
Kullanıcı yerleşik ve kullanım örnekleri ve senaryoları farklı türlerde arasında genel olarak uygulanan bir web hizmeti sağlayan genel veriler de (örneğin, bir metin gövde) sahiptir.

* [Sözlüğe Dayalı Yaklaşım Analizi](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a>Senaryo 4: Gelişmiş hesaplayıcısı
Bir kullanıcı, Gelişmiş hesaplamalar veya herhangi bir eğitilen model veya kullanıcının verileri için bir modelin sığdırma gerektirmeyen benzetimleri sağlar.

* [Oran Farkı Testi](machine-learning-r-csharp-difference-in-two-proportions.md)
* [Normal Dağıtım Paketi](machine-learning-r-csharp-normal-distribution.md)
* [İki Terimli Dağıtım Paketi](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a>SSS
Web hizmeti veya Market yayımlamayı tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



