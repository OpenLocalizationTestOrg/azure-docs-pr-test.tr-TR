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
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a><span data-ttu-id="655b4-104">(kullanım dışı) Web üzerinde Azure Machine Learning kullanarak R kodu örnekleri Hizmetleri ve Microsoft Azure Market'e yayımlanan</span><span class="sxs-lookup"><span data-stu-id="655b4-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="655b4-105">Microsoft DataMarket kullanımdan kaldırıldı ve bu API'leri kullanım dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="655b4-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="655b4-106">Çok sayıda kullanışlı örnek denemeleri ve API'leri bulabilirsiniz [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="655b4-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="655b4-107">Galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="655b4-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="655b4-108">Bu makaledeki örnek web hizmetleri Azure Machine Learning kullanarak oluşturulan ve Azure Marketi yayımlanan ' dir.</span><span class="sxs-lookup"><span data-stu-id="655b4-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span></span> <span data-ttu-id="655b4-109">Her web hizmeti örnek Hizmetleri test etmek ve kullanıcı benzer bir hizmet kendilerini nasıl oluşturabileceğinizi açıklayan için örnek veri kümelerini katıştırma bağlı, kapsamlı bir belge sahiptir.</span><span class="sxs-lookup"><span data-stu-id="655b4-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span></span> 

<span data-ttu-id="655b4-110">Azure Machine Learning Studio'da kullanıcılar R kodu yazma ve birkaç tıklama ile uygulama ve cihazlar dünyanın kullanmak web hizmeti olarak yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="655b4-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="655b4-111">Bir özel metin araştırma düşünceleri analiz bir göstergesi olduğu oluşturma için istatistik işlevleri sağlayan basit hesaplayıcıları oluşturan öğesinden hem yeni hem de deneyimli R kullanıcılar Azure Machine Learning kullanıcılarının R faaliyete geçirebilirsiniz kolaylığı yararlanabilir kod.</span><span class="sxs-lookup"><span data-stu-id="655b4-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="655b4-112">Machine Learning nasıl faaliyete geçirebilirsiniz göstermek için bu web hizmetleri olası bir mobil uygulama veya bir Web sitesi, bu web hizmetleri örnekler amacı aracılığıyla kullanıcılar tarafından kullanılabilecek iken R analitik amaçlarla ve komut dosyaları üstte web hizmetleri oluşturmak için kullanılır R kodu.</span><span class="sxs-lookup"><span data-stu-id="655b4-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span></span>

<span data-ttu-id="655b4-113">Her örneğin bir C# örnek web hizmet tüketimi için içerir.</span><span class="sxs-lookup"><span data-stu-id="655b4-113">Each example includes a C# example for web service consumption.</span></span>

![Azure Machine Learning R kodu diyagramı: kullanın veya Azure Marketi yayımlanan özel R çözümleri.][1]

<span data-ttu-id="655b4-115">Aşağıdaki senaryoları göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="655b4-115">Consider the following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="655b4-116">Senaryo 1: Genel modeli</span><span class="sxs-lookup"><span data-stu-id="655b4-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="655b4-117">Bir kullanıcı bir temel zaman serisi veri veya gelişmiş analizler özel olarak geliştirilmiş bir R yöntemiyle tahmin gibi yeni kullanıcının verilere uygulanan genel bir modeli ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="655b4-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="655b4-118">Bu kullanıcı model başkalarının kendi verileri ile kullanmak bir web hizmeti olarak yayımlar.</span><span class="sxs-lookup"><span data-stu-id="655b4-118">This user publishes the model as a web service for others to consume with their data.</span></span>

* [<span data-ttu-id="655b4-119">İkili Dosya Sınıflandırıcı</span><span class="sxs-lookup"><span data-stu-id="655b4-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="655b4-120">Küme Modeli</span><span class="sxs-lookup"><span data-stu-id="655b4-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="655b4-121">Çok Değişkenli Doğrusal Regresyon</span><span class="sxs-lookup"><span data-stu-id="655b4-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="655b4-122">Tahmin - Üstel Düzeltme</span><span class="sxs-lookup"><span data-stu-id="655b4-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="655b4-123">Madde işaretleri + STL tahmin</span><span class="sxs-lookup"><span data-stu-id="655b4-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="655b4-124">Tahmin - Autoregressive tümleşik hareketli ortalama (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="655b4-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="655b4-125">Yaşam Analizi</span><span class="sxs-lookup"><span data-stu-id="655b4-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="655b4-126">Senaryo 2: Eğitilmiş model – belirli veri</span><span class="sxs-lookup"><span data-stu-id="655b4-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="655b4-127">Bir kullanıcı gibi büyük bir örnek kullanıcının kişilik türü veya bir kişinin riskini tahmin etmek için kullanılan sistem durumu anket veri tahmin etmek için bir k-ortalamaları algoritması kümelenmiş kişilik formlarının R kodlarda yararlı tahminleri sağlar veriler var. acil ihtiyaç analiz R paketi ile Akciğer kanseri için.</span><span class="sxs-lookup"><span data-stu-id="655b4-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="655b4-128">Kullanıcı verileri yeni bir kullanıcının sonuç tahmin bir web hizmeti aracılığıyla yayımlar.</span><span class="sxs-lookup"><span data-stu-id="655b4-128">The user publishes the data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="655b4-129">Senaryo 3: Eğitilmiş model – genel veriler</span><span class="sxs-lookup"><span data-stu-id="655b4-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="655b4-130">Kullanıcı yerleşik ve kullanım örnekleri ve senaryoları farklı türlerde arasında genel olarak uygulanan bir web hizmeti sağlayan genel veriler de (örneğin, bir metin gövde) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="655b4-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="655b4-131">Sözlüğe Dayalı Yaklaşım Analizi</span><span class="sxs-lookup"><span data-stu-id="655b4-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="655b4-132">Senaryo 4: Gelişmiş hesaplayıcısı</span><span class="sxs-lookup"><span data-stu-id="655b4-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="655b4-133">Bir kullanıcı, Gelişmiş hesaplamalar veya herhangi bir eğitilen model veya kullanıcının verileri için bir modelin sığdırma gerektirmeyen benzetimleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="655b4-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span></span>

* [<span data-ttu-id="655b4-134">Oran Farkı Testi</span><span class="sxs-lookup"><span data-stu-id="655b4-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="655b4-135">Normal Dağıtım Paketi</span><span class="sxs-lookup"><span data-stu-id="655b4-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="655b4-136">İki Terimli Dağıtım Paketi</span><span class="sxs-lookup"><span data-stu-id="655b4-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="655b4-137">SSS</span><span class="sxs-lookup"><span data-stu-id="655b4-137">FAQ</span></span>
<span data-ttu-id="655b4-138">Web hizmeti veya Market yayımlamayı tüketimi hakkında sık sorulan sorular için bkz: [burada](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="655b4-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



