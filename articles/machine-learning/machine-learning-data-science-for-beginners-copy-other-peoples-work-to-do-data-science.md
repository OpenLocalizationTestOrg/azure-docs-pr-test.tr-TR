---
title: "Başkalarının veri bilimi örnekler – Azure Machine Learning kopyalama | Microsoft Docs"
description: "Veri bilimi, ticari sır: çalışmanızı bunu başkalarına alın. Machine learning örnekler Cortana Analytics Galerisi'nden alın."
keywords: "Veri bilimi örnekler, algoritma örnek kümeleme algoritması, kümeleme machine learning örnek"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: ec2be823-c325-4ad8-b8b2-3e664f1a44b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: a67d9ccb9d9e6074bee7e1429ede96bd508945c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="copy-other-peoples-work-to-do-data-science"></a><span data-ttu-id="fb896-105">Veri bilimi için başkalarının çalışmalarını kopyalama</span><span class="sxs-lookup"><span data-stu-id="fb896-105">Copy other people's work to do data science</span></span>
## <a name="video-5-data-science-for-beginners-series"></a><span data-ttu-id="fb896-106">Video 5: Yeni başlayanlar seri için veri bilimi</span><span class="sxs-lookup"><span data-stu-id="fb896-106">Video 5: Data Science for Beginners series</span></span>
<span data-ttu-id="fb896-107">Veri bilimi, ticari sır birini iş yaptığınız için diğer kişileri almaktır.</span><span class="sxs-lookup"><span data-stu-id="fb896-107">One of the trade secrets of data science is getting other people to do your work for you.</span></span> <span data-ttu-id="fb896-108">Cortana Analytics galerisinde kendi makine öğrenimi denemesinin için kullanılacak bir kümeleme algoritması örnek bulun.</span><span class="sxs-lookup"><span data-stu-id="fb896-108">Find a clustering algorithm example in Cortana Analytics Gallery to use for your own machine learning experiment.</span></span>

<span data-ttu-id="fb896-109">Serinin en dışında almak için tümünü izleyin.</span><span class="sxs-lookup"><span data-stu-id="fb896-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="fb896-110">[Videolar listesine Git](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="fb896-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-copy-other-peoples-work-to-do-data-science/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="fb896-111">Bu serideki diğer videolar</span><span class="sxs-lookup"><span data-stu-id="fb896-111">Other videos in this series</span></span>
<span data-ttu-id="fb896-112">*Yeni başlayanlar için veri bilimi* veri bilimi beş kısa videolar içindeki bir giriş değil.</span><span class="sxs-lookup"><span data-stu-id="fb896-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="fb896-113">Video 1: [5 veri bilimi yanıtlar sorular](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 dakika 14 saniye)*</span><span class="sxs-lookup"><span data-stu-id="fb896-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="fb896-114">Video 2: [verileriniz için veri bilimi hazır?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="fb896-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="fb896-115">*(4 min 56 sn)*</span><span class="sxs-lookup"><span data-stu-id="fb896-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="fb896-116">Video 3: [verilerle yanıt soru](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sn)*</span><span class="sxs-lookup"><span data-stu-id="fb896-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="fb896-117">Video 4: [basit bir modelle bir yanıt tahmin](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sn)*</span><span class="sxs-lookup"><span data-stu-id="fb896-117">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="fb896-118">Video 5: veri bilimi yapmak için diğer kişilerin çalışma kopyalayın</span><span class="sxs-lookup"><span data-stu-id="fb896-118">Video 5: Copy other people's work to do data science</span></span>

## <a name="transcript-copy-other-peoples-work-to-do-data-science"></a><span data-ttu-id="fb896-119">Dökümü: veri bilimi yapmak için diğer kişilerin iş kopyalama</span><span class="sxs-lookup"><span data-stu-id="fb896-119">Transcript: Copy other people's work to do data science</span></span>
<span data-ttu-id="fb896-120">Serideki beşinci video "Yeni başlayanlar için veri bilimi." Hoş Geldiniz</span><span class="sxs-lookup"><span data-stu-id="fb896-120">Welcome to the fifth video in the series "Data Science for Beginners."</span></span>

<span data-ttu-id="fb896-121">Bu tek bir yerde, gelen bir başlangıç noktası olarak kendi iş için kullanırım Bul örnekler için öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="fb896-121">In this one, you’ll discover a place to find examples that you can borrow from as a starting point for your own work.</span></span> <span data-ttu-id="fb896-122">Bu serideki önceki videoları ilk izleyin, en iyi bu videoyu alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb896-122">You might get the most out of this video if you first watch the earlier videos in this series.</span></span>

<span data-ttu-id="fb896-123">Veri bilimi, ticari sır birini iş yaptığınız için diğer kişileri almaktır.</span><span class="sxs-lookup"><span data-stu-id="fb896-123">One of the trade secrets of data science is getting other people to do your work for you.</span></span>

## <a name="find-examples-in-the-cortana-intelligence-gallery"></a><span data-ttu-id="fb896-124">Cortana Intelligence Galerisi'nde örnekleri Bul</span><span class="sxs-lookup"><span data-stu-id="fb896-124">Find examples in the Cortana Intelligence Gallery</span></span>
<span data-ttu-id="fb896-125">Microsoft adlı bulut tabanlı bir hizmete sahip [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) ücretsiz deneyin Hoş Geldiniz.</span><span class="sxs-lookup"><span data-stu-id="fb896-125">Microsoft has a cloud-based service called [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) that you're welcome to try for free.</span></span> <span data-ttu-id="fb896-126">Bu, bir çalışma alanıyla farklı machine learning algoritmaları ile deneyebilirsiniz ve yerdir, çalışılan çözümünüzün var olduğunda sağlar, web hizmeti olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="fb896-126">It provides you with a workspace where you can experiment with different machine learning algorithms, and, when you've got your solution worked out, you can launch it as a web service.</span></span>

<span data-ttu-id="fb896-127">Bu hizmetin parçası olan bir şey adlı  **[Cortana Intelligence Galerisi](http://aka.ms/CortanaIntelligenceGallery)**.</span><span class="sxs-lookup"><span data-stu-id="fb896-127">Part of this service is something called the **[Cortana Intelligence Gallery](http://aka.ms/CortanaIntelligenceGallery)**.</span></span> <span data-ttu-id="fb896-128">Azure Machine Learning denemeleri veya kişiler yerleşik ve diğerleri için kullanılacak katkıda modelleri koleksiyonu gibi kaynakları içerir.</span><span class="sxs-lookup"><span data-stu-id="fb896-128">It contains resources, including a collection of Azure Machine Learning experiments, or models, that people have built and contributed for others to use.</span></span> <span data-ttu-id="fb896-129">Bu denemeler düşünce ve diğer kendi çözümlerini başlamanıza yardımcı olmak için sabit iş yararlanmak için harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="fb896-129">These experiments are a great way to leverage the thought and hard work of others to get you started on your own solutions.</span></span>

<span data-ttu-id="fb896-130">' Daki galeri bulabilirsiniz [aka.ms/CortanaIntelligenceGallery](http://aka.ms/CortanaIntelligenceGallery).</span><span class="sxs-lookup"><span data-stu-id="fb896-130">You can find the gallery at [aka.ms/CortanaIntelligenceGallery](http://aka.ms/CortanaIntelligenceGallery).</span></span> <span data-ttu-id="fb896-131">Herkes üzerinden Gözat Hoş Geldiniz.</span><span class="sxs-lookup"><span data-stu-id="fb896-131">Everyone is welcome to browse through it.</span></span>

![Cortana Intelligence Galerisi](./media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/cortana-intelligence-gallery.png)

<span data-ttu-id="fb896-133">Tıklatırsanız **denemeler** en üstte en son ve popüler denemeler galerideki sayısı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fb896-133">If you click **Experiments** at the top, you'll see a number of the most recent and popular experiments in the gallery.</span></span> <span data-ttu-id="fb896-134">Tıklatarak denemeler kullanılmadıkları arayabilirsiniz **tümüne Gözat** ekranın üstünde ve orada girdiğiniz arama terimleri ve arama filtrelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="fb896-134">You can search through the rest of experiments by clicking **Browse All** at the top of the screen, and there you can enter search terms and choose search filters.</span></span>

## <a name="find-and-use-a-clustering-algorithm-example"></a><span data-ttu-id="fb896-135">Bulma ve kümeleme algoritması örneği kullanın</span><span class="sxs-lookup"><span data-stu-id="fb896-135">Find and use a clustering algorithm example</span></span>
<span data-ttu-id="fb896-136">Bu nedenle, örneğin, arama için kümeleme nasıl çalıştığını, bir örnek görmek istediğiniz diyelim ki **"Tarama Kümeleme"** denemeler.</span><span class="sxs-lookup"><span data-stu-id="fb896-136">So, for instance, let's say you want to see an example of how clustering works, so you search for **"clustering sweep"** experiments.</span></span>

![Denemeler kümeleme için arama](./media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/search-for-clustering-experiments.png)

<span data-ttu-id="fb896-138">Birisi Galeriye katkıda ilginç bir İşte.</span><span class="sxs-lookup"><span data-stu-id="fb896-138">Here's an interesting one that someone contributed to the gallery.</span></span>

![Deneme kümeleme](./media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/clustering-experiment.png)

<span data-ttu-id="fb896-140">Üzerinde deneme ve bazı sonuçları yanı sıra bu katkıda bulunan, yaptığınız iş açıklayan bir web sayfası Al'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="fb896-140">Click on that experiment and you get a web page that describes the work that this contributor did, along with some of their results.</span></span>

![Deneme açıklama sayfa kümeleme](./media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/clustering-experiment-description-page.png)

<span data-ttu-id="fb896-142">Bildirim bağlantısını **Studio'da Aç**.</span><span class="sxs-lookup"><span data-stu-id="fb896-142">Notice the link that says **Open in Studio**.</span></span>

![Studio düğmesi Aç](./media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/open-in-studio.png)

<span data-ttu-id="fb896-144">Üzerinde tıklayabilir ve bana sağdan sürdüğünü **Azure Machine Learning Studio**.</span><span class="sxs-lookup"><span data-stu-id="fb896-144">I can click on that and it takes me right to **Azure Machine Learning Studio**.</span></span> <span data-ttu-id="fb896-145">Denemeyi bir kopyasını oluşturur ve çalışma Alanım kendi yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="fb896-145">It creates a copy of the experiment and puts it in my own workspace.</span></span> <span data-ttu-id="fb896-146">Bu, Katkıda Bulunanlar veri kümesi, yaptıkları işlemin, tüm işlemler tüm kullandıkları algoritmaları ve sonuçları kaydedilme içerir.</span><span class="sxs-lookup"><span data-stu-id="fb896-146">This includes the contributor's dataset, all the processing that they did, all of the algorithms that they used, and how they saved out the results.</span></span>

![Machine Learning Studio - kümeleme algoritması örnek bir galeri deneme açın](./media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/cluster-experiment-open-in-studio.png)

<span data-ttu-id="fb896-148">Ve bir başlangıç noktası şimdi sahibim.</span><span class="sxs-lookup"><span data-stu-id="fb896-148">And now I have a starting point.</span></span> <span data-ttu-id="fb896-149">I için kendi verilerini takas ve kendi modelini uyguladıkça yapın.</span><span class="sxs-lookup"><span data-stu-id="fb896-149">I can swap out their data for my own and do my own tweaking of the model.</span></span> <span data-ttu-id="fb896-150">Bu bana bir çalışan başlangıç verir ve bana bilen gerçekten ne yaptıklarını kişilerin çalışmalarını yapı olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="fb896-150">This gives me a running start, and it lets me build on the work of people who really know what they’re doing.</span></span>

## <a name="find-experiments-that-demonstrate-machine-learning-techniques"></a><span data-ttu-id="fb896-151">Machine learning teknikleri göstermek denemeler Bul</span><span class="sxs-lookup"><span data-stu-id="fb896-151">Find experiments that demonstrate machine learning techniques</span></span>
<span data-ttu-id="fb896-152">Diğer denemeler vardır [Cortana Intelligence Galerisi](http://aka.ms/CortanaIntelligenceGallery) , katkıda bulunan özellikle veri bilimi yeni kişiler için nasıl yapılır örnekler sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="fb896-152">There are other experiments in the [Cortana Intelligence Gallery](http://aka.ms/CortanaIntelligenceGallery) that were contributed specifically to provide how-to examples for people new to data science.</span></span> <span data-ttu-id="fb896-153">Örneğin, bir deneme eksik değerleri nasıl ele alınacağını gösteren galerisinde yoktur ([eksik değerleri işlemek için yöntemleri](https://gallery.cortanaintelligence.com/Experiment/Methods-for-handling-missing-values-1)).</span><span class="sxs-lookup"><span data-stu-id="fb896-153">For instance, there's an experiment in the gallery that demonstrates how to handle missing values ([Methods for handling missing values](https://gallery.cortanaintelligence.com/Experiment/Methods-for-handling-missing-values-1)).</span></span> <span data-ttu-id="fb896-154">Boş değerleri değiştirerek 15 farklı yöntemler size yol gösterir ve her yöntem ve ne zaman kullanılmalı avantajları hakkında ettiği.</span><span class="sxs-lookup"><span data-stu-id="fb896-154">It walks you through 15 different ways of substituting empty values, and talks about the benefits of each method and when to use it.</span></span>

![Machine Learning Studio'da - eksik değerleri için yöntemleri galeri denemeler açın](./media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/experiment-methods-for-handling-missing-values.png)

<span data-ttu-id="fb896-156">[Cortana Intelligence Galerisi](http://aka.ms/CortanaIntelligenceGallery) kendi çözümleri için bir başlangıç noktası olarak kullanabileceğiniz çalışma denemeleri bulmak için bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="fb896-156">[Cortana Intelligence Gallery](http://aka.ms/CortanaIntelligenceGallery) is a place to find working experiments that you can use as a starting point for your own solutions.</span></span>

<span data-ttu-id="fb896-157">"Veri bilimi için yeni başlayanlar" Microsoft Azure Machine learning'in diğer videoları kullanıma emin olun.</span><span class="sxs-lookup"><span data-stu-id="fb896-157">Be sure to check out the other videos in “Data Science for Beginners” from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb896-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb896-158">Next steps</span></span>
* [<span data-ttu-id="fb896-159">Azure Machine Learning ile ilk veri bilimi denemenizi deneyin</span><span class="sxs-lookup"><span data-stu-id="fb896-159">Try your first data science experiment with Azure Machine Learning</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="fb896-160">Microsoft Azure Machine Learning giriş Al</span><span class="sxs-lookup"><span data-stu-id="fb896-160">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
