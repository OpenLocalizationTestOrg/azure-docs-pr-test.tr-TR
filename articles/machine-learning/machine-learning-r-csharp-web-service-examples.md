---
title: "AAA(deprecated) Machine learning web hizmetleri R - Azure ile oluşturulmuş örnekleri | Microsoft Docs"
description: "(kullanım dışı) Web hizmetleri örnekler yararlı bir dizi R kodu ve Machine Learning ile oluşturulan ve yayımlanan toohello Azure Marketi bulun."
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
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a><span data-ttu-id="e8ba1-104">(kullanım dışı) Azure Machine Learning ve yayımlanan tooMicrosoft Azure Marketi R kodu kullanılarak örnekler Web Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="e8ba1-104">(deprecated) Web services examples using R code on Azure Machine Learning and published tooMicrosoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="e8ba1-105">Merhaba Microsoft DataMarket kullanımdan kaldırıldı ve bu API'leri kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-105">hello Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="e8ba1-106">Çok sayıda kullanışlı örnek denemeleri ve API hello bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="e8ba1-106">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="e8ba1-107">Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="e8ba1-107">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="e8ba1-108">Bu makaledeki örnek web hizmetleri Azure Machine Learning kullanılarak oluşturulan ve yayımlanan toohello Azure Marketi ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-108">In this article are example web services were created using Azure Machine Learning and published toohello Azure Marketplace.</span></span> <span data-ttu-id="e8ba1-109">Her web hizmeti örnek hello Hizmetleri test ve hello kullanıcı benzer bir hizmet kendilerini nasıl oluşturabileceğinizi açıklayan için örnek veri kümelerini katıştırma bağlı, kapsamlı bir belge sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing hello services and explaining how hello user can create a similar service themselves.</span></span> 

<span data-ttu-id="e8ba1-110">Kullanıcılar Azure Machine Learning Studio'da R kodu yazın ve uygulamalar ve cihazlar tooconsume Merhaba Dünya için web hizmeti olarak yayımlama birkaç tıklama ile.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices tooconsume around hello world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e8ba1-111">Bir özel metin araştırma düşünceleri analiz bir göstergesi olduğu istatistik işlevleri toocreating sağlayan basit hesaplayıcıları oluşturan öğesinden hem yeni hem de deneyimli R kullanıcılar Azure Machine Learning kullanıcılarının R faaliyete geçirebilirsiniz hello kolaylığı yararlanabilir kod.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-111">From producing simple calculators that provide statistical functionality toocreating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from hello ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="e8ba1-112">Bu web hizmetleri olası bir mobil uygulama veya bir Web sitesi aracılığıyla kullanıcılar tarafından kullanılabilecek hello amacı örnekleri olan Machine Learning nasıl faaliyete geçirebilirsiniz tooshow bu web Hizmetleri, R analitik amacıyla komut dosyaları ve web hizmetleri kullanılan toocreate olması R kodu üstündeki.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-112">While these web services could be consumed by users, potentially through a mobile app or a website, hello purpose of these web services examples is tooshow how Machine Learning can operationalize R scripts for analytical purposes and be used toocreate web services on top of R code.</span></span>

<span data-ttu-id="e8ba1-113">Her örneğin bir C# örnek web hizmet tüketimi için içerir.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-113">Each example includes a C# example for web service consumption.</span></span>

![Azure Machine Learning R kodu diyagramı: özel kullanmak veya yayımlanan toohello Azure Marketi R çözümler.][1]

<span data-ttu-id="e8ba1-115">Hello aşağıdaki senaryoları göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-115">Consider hello following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="e8ba1-116">Senaryo 1: Genel modeli</span><span class="sxs-lookup"><span data-stu-id="e8ba1-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="e8ba1-117">Bir kullanıcı bir temel zaman serisi veri veya gelişmiş analizler özel olarak geliştirilmiş bir R yöntemiyle tahmin gibi uygulanan tooa yeni kullanıcının verileri olabilir genel bir model çalışır.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-117">A user works with a generic model that can be applied tooa new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="e8ba1-118">Bu kullanıcı hello yayımlar verileriyle tooconsume model başkalarının bir web hizmeti olarak.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-118">This user publishes hello model as a web service for others tooconsume with their data.</span></span>

* [<span data-ttu-id="e8ba1-119">İkili Dosya Sınıflandırıcı</span><span class="sxs-lookup"><span data-stu-id="e8ba1-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="e8ba1-120">Küme Modeli</span><span class="sxs-lookup"><span data-stu-id="e8ba1-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="e8ba1-121">Çok Değişkenli Doğrusal Regresyon</span><span class="sxs-lookup"><span data-stu-id="e8ba1-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="e8ba1-122">Tahmin - Üstel Düzeltme</span><span class="sxs-lookup"><span data-stu-id="e8ba1-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="e8ba1-123">Madde işaretleri + STL tahmin</span><span class="sxs-lookup"><span data-stu-id="e8ba1-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="e8ba1-124">Tahmin - Autoregressive tümleşik hareketli ortalama (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="e8ba1-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="e8ba1-125">Yaşam Analizi</span><span class="sxs-lookup"><span data-stu-id="e8ba1-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="e8ba1-126">Senaryo 2: Eğitilmiş model – belirli veri</span><span class="sxs-lookup"><span data-stu-id="e8ba1-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="e8ba1-127">Bir kullanıcı, büyük bir örnek kişilik soru k-ortalamaları algoritması toopredict hello kullanıcının kişilik türünü kümelenmiş veya sistem durumu, bir kişinin kullanılan toopredict olabilir veri anket gibi yararlı tahminleri R kodlarda sağlayan veri sahip acil ihtiyaç analiz R paketi ile Akciğer kanseri için risk.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm toopredict hello user’s personality type, or health survey data that can be used toopredict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="e8ba1-128">Merhaba kullanıcı yeni bir kullanıcının sonuç tahmin bir web hizmeti ile Merhaba veri yayımlar.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-128">hello user publishes hello data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="e8ba1-129">Senaryo 3: Eğitilmiş model – genel veriler</span><span class="sxs-lookup"><span data-stu-id="e8ba1-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="e8ba1-130">Kullanıcı yerleşik ve kullanım örnekleri ve senaryoları farklı türlerde arasında genel olarak uygulanan bir web hizmeti toobe izin veren genel verileri (örneğin, bir metin gövde) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-130">A user has generic data (such as a text corpus) that allows a web service toobe built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="e8ba1-131">Sözlüğe Dayalı Yaklaşım Analizi</span><span class="sxs-lookup"><span data-stu-id="e8ba1-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="e8ba1-132">Senaryo 4: Gelişmiş hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="e8ba1-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="e8ba1-133">Bir kullanıcı, Gelişmiş hesaplamalar veya herhangi bir eğitilen model veya bir model toohello kullanıcının verileri sığdırma gerektirmeyen benzetimleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8ba1-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model toohello user’s data.</span></span>

* [<span data-ttu-id="e8ba1-134">Oran Farkı Testi</span><span class="sxs-lookup"><span data-stu-id="e8ba1-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="e8ba1-135">Normal Dağıtım Paketi</span><span class="sxs-lookup"><span data-stu-id="e8ba1-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="e8ba1-136">İki Terimli Dağıtım Paketi</span><span class="sxs-lookup"><span data-stu-id="e8ba1-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="e8ba1-137">SSS</span><span class="sxs-lookup"><span data-stu-id="e8ba1-137">FAQ</span></span>
<span data-ttu-id="e8ba1-138">Merhaba web hizmetinin veya yayımlama toohello Market tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="e8ba1-138">For frequently asked questions on consumption of hello web service or publishing toohello Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



