---
title: "Tahmine dayalı bir çözüm aaaA Machine Learning ile kredi riski için | Microsoft Docs"
description: "Gösteren ayrıntılı bir kılavuz nasıl toocreate kredi için Tahmine dayalı analiz çözümü risk değerlendirmesi Azure Machine Learning Studio'da."
keywords: "kredi riski, tahmine dayalı analiz çözümü, risk değerlendirmesi"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="071f6-104">Kılavuz: Azure Machine Learning Studio'da kredi riski değerlendirmesi için tahmine dayalı bir analiz çözümü geliştirme</span><span class="sxs-lookup"><span data-stu-id="071f6-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="071f6-105">Bu kılavuzda, biz Machine Learning Studio'da Tahmine dayalı analiz çözümü geliştirme sürecini hello genişletilmiş bir göz atın.</span><span class="sxs-lookup"><span data-stu-id="071f6-105">In this walkthrough, we take an extended look at hello process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="071f6-106">Biz Machine Learning Studio'da basit bir modeli geliştirmek ve hello modeli yeni verileri kullanarak tahminleri burada yapabilirsiniz bir Azure Machine Learning web hizmeti olarak dağıtabilir.</span><span class="sxs-lookup"><span data-stu-id="071f6-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where hello model can make predictions using new data.</span></span> 

<span data-ttu-id="071f6-107">Bu kılavuzda Machine Learning Studio'yu daha önce en az bir kere kullandığınız ve makine öğrenimi kavramlarıyla ilgili bir fikriniz olduğu kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="071f6-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="071f6-108">Bununla birlikte, bir uzman olduğunuz da varsayılmaz.</span><span class="sxs-lookup"><span data-stu-id="071f6-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="071f6-109">Hiç kullanmadıysanız **Azure Machine Learning Studio** toostart hello öğretici ile isteyebilirsiniz önce [ilk veri bilimi Azure Machine Learning Studio'da deneme oluşturma](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="071f6-109">If you've never used **Azure Machine Learning Studio** before, you might want toostart with hello tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="071f6-110">Bu öğretici Machine Learning Studio ilk kez Merhaba gösterir.</span><span class="sxs-lookup"><span data-stu-id="071f6-110">That tutorial takes you through Machine Learning Studio for hello first time.</span></span> <span data-ttu-id="071f6-111">Size nasıl toodrag ve bırak modülleri, denemenize üzerine hello temelleri birbirine bağlamak, hello denemeyi çalıştırın ve hello sonuçlarına bakın gösterir.</span><span class="sxs-lookup"><span data-stu-id="071f6-111">It shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="071f6-112">Başlarken için yararlı olabilecek başka bir Machine Learning Studio'nun hello özelliklerine genel bakış sağlayan bir diyagram aracıdır.</span><span class="sxs-lookup"><span data-stu-id="071f6-112">Another tool that may be helpful for getting started is a diagram that gives an overview of hello capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="071f6-113">Diyagramı şu sayfadan indirip yazdırabilirsiniz: [Azure Machine Learning Studio özelliklerine genel bakış diyagramı](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="071f6-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="071f6-114">Machine learning genel yeni toohello alanına değilseniz, yararlı tooyou olabilecek bir video serisi yok.</span><span class="sxs-lookup"><span data-stu-id="071f6-114">If you're new toohello field of machine learning in general, there's a video series that might be helpful tooyou.</span></span> <span data-ttu-id="071f6-115">Çağrılır [yeni başlayanlar için veri bilimi](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) ve onu, gündelik dil ve kavramları kullanarak harika giriş toomachine öğrenme verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="071f6-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction toomachine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a><span data-ttu-id="071f6-116">Merhaba sorunu</span><span class="sxs-lookup"><span data-stu-id="071f6-116">hello problem</span></span>

<span data-ttu-id="071f6-117">Bir kişinin kredi riski kredi uygulamasında verdiği hello bilgileri temel alarak toopredict gerektiğini varsayalım.</span><span class="sxs-lookup"><span data-stu-id="071f6-117">Suppose you need toopredict an individual's credit risk based on hello information they gave on a credit application.</span></span>  

<span data-ttu-id="071f6-118">Kredi riski değerlendirmesi karmaşık bir sorun olsa da bu kılavuz için biraz basitleştirebiliriz.</span><span class="sxs-lookup"><span data-stu-id="071f6-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="071f6-119">Microsoft Azure Machine Learning’i kullanarak nasıl tahmine dayalı analiz çözümü oluşturabileceğinizi gösteren bir örnek olarak kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="071f6-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="071f6-120">toodo Bu, Azure Machine Learning Studio ve Machine Learning web hizmeti kullanırız.</span><span class="sxs-lookup"><span data-stu-id="071f6-120">toodo this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="hello-solution"></a><span data-ttu-id="071f6-121">Merhaba çözümü</span><span class="sxs-lookup"><span data-stu-id="071f6-121">hello solution</span></span>

<span data-ttu-id="071f6-122">Bu ayrıntılı kılavuzda, herkesin erişebileceği kredi riski verileriyle çalışmaya başlayarak bu verileri temel alan tahmine dayalı bir model geliştireceğiz ve modeli eğiteceğiz.</span><span class="sxs-lookup"><span data-stu-id="071f6-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="071f6-123">Bunu başkaları tarafından kredi riski değerlendirmesi için kullanılacak şekilde ardından biz hello modeli bir web hizmeti olarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="071f6-123">Then we deploy hello model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="071f6-124">toocreate bu kredi riski değerlendirme çözümü şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="071f6-124">toocreate this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="071f6-125">Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="071f6-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="071f6-126">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="071f6-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="071f6-127">Deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="071f6-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="071f6-128">Eğitmek ve hello modelleri değerlendir</span><span class="sxs-lookup"><span data-stu-id="071f6-128">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="071f6-129">Merhaba web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="071f6-129">Deploy hello web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="071f6-130">Erişim hello web hizmeti</span><span class="sxs-lookup"><span data-stu-id="071f6-130">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="071f6-131">Bu kılavuzda hello biz geliştirmek hello deneme çalışan bir kopyasını bulabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="071f6-131">You can find a working copy of hello experiment that we develop in this walkthrough in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="071f6-132">Çok Git**[izlenecek - kredi riski tahmini](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  tıklatıp **Studio'da Aç** toodownload hello denemeyi Machine Learning Studio çalışma alanına bir kopyası.</span><span class="sxs-lookup"><span data-stu-id="071f6-132">Go too**[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="071f6-133">Bu kılavuzda hello örnek denemesinin basitleştirilmiş bir sürümünü temel [ikili sınıflandırma: Kredi riski tahmini](http://go.microsoft.com/fwlink/?LinkID=525270), hello bulunan [galeri](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="071f6-133">This walkthrough is based on a simplified version of hello sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in hello [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
