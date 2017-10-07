---
title: "aaaCopy makine örnek denemeleri - Azure Öğrenme | Microsoft Docs"
description: "Nasıl toouse örnek makine öğrenme toocreate yeni denemeler Cortana Intelligence Galerisi ve Microsoft Azure Machine Learning denemelerini öğrenin."
keywords: "machine learning örnekleri, örnek deneme, machine learning örneği"
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 555f05cf9af2040d1703707f7583396d5da9f156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-example-experiments-toocreate-new-machine-learning-experiments"></a><span data-ttu-id="8bde5-104">Örnek denemeleri toocreate yeni machine learning denemeleri kopyalayın</span><span class="sxs-lookup"><span data-stu-id="8bde5-104">Copy example experiments toocreate new machine learning experiments</span></span>
<span data-ttu-id="8bde5-105">Nasıl örnekle toostart den denemelerini öğrenin [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/) makine öğrenimi denemelerine sıfırdan oluşturmak yerine.</span><span class="sxs-lookup"><span data-stu-id="8bde5-105">Learn how toostart with example experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="8bde5-106">Merhaba örnekler toobuild kendi machine learning çözüm kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bde5-106">You can use hello examples toobuild your own machine learning solution.</span></span>

<span data-ttu-id="8bde5-107">Merhaba Galerisi örnek denemeleri hello Machine Learning topluluğu tarafından paylaşılan örnekleri yanı sıra hello Microsoft Azure Machine Learning ekibi tarafından vardır.</span><span class="sxs-lookup"><span data-stu-id="8bde5-107">hello gallery has example experiments by hello Microsoft Azure Machine Learning team as well as examples shared by hello Machine Learning community.</span></span> <span data-ttu-id="8bde5-108">Ayrıca, denemeler hakkında soru sorabilir veya yorum yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bde5-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="8bde5-109">toosee toouse hello nasıl Galerisi, hello 3 dakikalık videoyu izleyin [diğer kişilerin çalışma toodo veri bilimi kopyalama](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) hello serisinden [yeni başlayanlar için veri bilimi](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="8bde5-109">toosee how toouse hello gallery, watch hello 3-minute video [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from hello series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-toocopy-in-cortana-intelligence-gallery"></a><span data-ttu-id="8bde5-110">Bir deneme toocopy Cortana Intelligence Galerisi'nde Bul</span><span class="sxs-lookup"><span data-stu-id="8bde5-110">Find an experiment toocopy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="8bde5-111">toosee hangi denemelerin kullanılabilir, Git toohello olan [galeri](https://gallery.cortanaintelligence.com/) tıklatıp **denemeler** hello sayfanın üst kısmındaki hello.</span><span class="sxs-lookup"><span data-stu-id="8bde5-111">toosee what experiments are available, go toohello [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at hello top of hello page.</span></span>

### <a name="find-hello-newest-or-most-popular-experiments"></a><span data-ttu-id="8bde5-112">Yeni veya en popüler denemeler Hello bulur</span><span class="sxs-lookup"><span data-stu-id="8bde5-112">Find hello newest or most popular experiments</span></span>
<span data-ttu-id="8bde5-113">Bu sayfada, gördüğünüz **en son eklenen** denemeler veya toolook aşağı **popüler olanlar** veya son hello **popüler Microsoft denemelerini**.</span><span class="sxs-lookup"><span data-stu-id="8bde5-113">On this page, you can see **Recently added** experiments, or scroll down toolook at **What's popular** or hello latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="8bde5-114">Belirli gereksinimleri karşılayan bir deneme arama</span><span class="sxs-lookup"><span data-stu-id="8bde5-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="8bde5-115">Tüm toobrowse denemelerini:</span><span class="sxs-lookup"><span data-stu-id="8bde5-115">toobrowse all experiments:</span></span>

1. <span data-ttu-id="8bde5-116">Tıklatın **tümüne Gözat** hello sayfanın üst kısmındaki hello.</span><span class="sxs-lookup"><span data-stu-id="8bde5-116">Click **Browse all** at hello top of hello page.</span></span>
2. <span data-ttu-id="8bde5-117">Merhaba sol taraftaki altında **tarafından daraltın** hello içinde **kategorileri** bölümünde, select **deneme** tüm hello alanındaki denemeler toosee hello Galerisi.</span><span class="sxs-lookup"><span data-stu-id="8bde5-117">On hello left-hand side, under **Refine by** in hello **Categories** section, select **Experiment** toosee all hello experiments in hello Gallery.</span></span>
3. <span data-ttu-id="8bde5-118">Gereksinimlerinize uyan denemeleri birkaç farklı yolla bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8bde5-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="8bde5-119">**Merhaba soldaki filtreleri seçin.**</span><span class="sxs-lookup"><span data-stu-id="8bde5-119">**Select filters on hello left.**</span></span> <span data-ttu-id="8bde5-120">Örneğin, PCA tabanlı anomali algılama algoritması kullanan toobrowse denemeler: ile **deneme** altında seçilen **kategorileri**, tıklatın **Tümünü Göster**.</span><span class="sxs-lookup"><span data-stu-id="8bde5-120">For example, toobrowse experiments that use a PCA-based anomaly detection algorithm: With **Experiment** selected under **Categories**, click **Show all**.</span></span> <span data-ttu-id="8bde5-121">Ardından, **Kullanılan Algoritmalar** altında **PCA Tabanlı Anomali Algılama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="8bde5-121">Then, under **Algorithms Used**, choose **PCA-Based Anomaly Detection**.</span></span> <br></br><span data-ttu-id="8bde5-122">
     ![Filtreleri seçin](./media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="8bde5-122">
![Select filters](./media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="8bde5-123">**Merhaba arama kutusunu kullanın.**</span><span class="sxs-lookup"><span data-stu-id="8bde5-123">**Use hello search box.**</span></span> <span data-ttu-id="8bde5-124">Örneğin, toofind denemeler katkıda ilgili Microsoft tarafından iki sınıflı destekli vektör makinesi algoritması kullanan toodigit tanıma hello arama kutusuna "rakam tanıma" girin.</span><span class="sxs-lookup"><span data-stu-id="8bde5-124">For example, toofind experiments contributed by Microsoft related toodigit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in hello search box.</span></span> <span data-ttu-id="8bde5-125">Sonra Seç hello filtreleri **deneme**, **yalnızca Microsoft içeriği**, ve **iki sınıflı destek vektör makinesi**:</span><span class="sxs-lookup"><span data-stu-id="8bde5-125">Then, select hello filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br><span data-ttu-id="8bde5-126">
     ![Merhaba arama kutusunu kullanın](./media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="8bde5-126">
![Use hello search box](./media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="8bde5-127">Bunun hakkında daha fazla bir deneme toolearn'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8bde5-127">Click an experiment toolearn more about it.</span></span>
5. <span data-ttu-id="8bde5-128">toorun ve/veya hello denemeyi değiştirmek, tıklatın **Studio'da Aç** hello deneme sayfasında.</span><span class="sxs-lookup"><span data-stu-id="8bde5-128">toorun and/or modify hello experiment, click **Open in Studio** on hello experiment's page.</span></span> <br></br>

    ![Örnek deneme](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="8bde5-130">Machine Learning Studio'da bir denemeyi ilk kez Merhaba açtığınızda ücretsiz deneyin veya bir Azure aboneliği satın alın.</span><span class="sxs-lookup"><span data-stu-id="8bde5-130">When you open an experiment in Machine Learning Studio for hello first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="8bde5-131">Merhaba Machine Learning Studio'nun Ücretli hizmeti karşılaştırması ücretsiz deneme sürümü hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="8bde5-131">Learn about hello Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="8bde5-132">Şablon olarak bir örnek kullanarak yeni deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="8bde5-132">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="8bde5-133">Ayrıca, bir Galeri örneğini bir şablon olarak kullanıp Machine Learning Studio'da yeni bir deneme oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bde5-133">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="8bde5-134">Oturum, Microsoft hesabı kimlik bilgileri toohello oturum [Studio](https://studio.azureml.net)ve ardından **yeni** toocreate bir deneme.</span><span class="sxs-lookup"><span data-stu-id="8bde5-134">Sign in with your Microsoft account credentials toohello [Studio](https://studio.azureml.net), and then click **New** toocreate an experiment.</span></span>
2. <span data-ttu-id="8bde5-135">Merhaba örnek içeriğine gözatın ve birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8bde5-135">Browse through hello example content and click one.</span></span>

<span data-ttu-id="8bde5-136">Merhaba örnek denemeyi şablon olarak kullanıp Machine Learning Studio çalışma alanınızda yeni bir deneme oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8bde5-136">A new experiment is created in your Machine Learning Studio workspace using hello example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bde5-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8bde5-137">Next steps</span></span>
* [<span data-ttu-id="8bde5-138">Çeşitli kaynaklardan veri alma</span><span class="sxs-lookup"><span data-stu-id="8bde5-138">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="8bde5-139">Machine Learning hello R dilde için hızlı başlangıç Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="8bde5-139">Quickstart tutorial for hello R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="8bde5-140">Machine Learning web hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="8bde5-140">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
