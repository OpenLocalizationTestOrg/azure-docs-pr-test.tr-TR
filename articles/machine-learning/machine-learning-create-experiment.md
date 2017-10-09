---
title: Machine Learning Studio'da basit deneme aaaA | Microsoft Docs
description: "Bu makine öğrenimi öğreticisi kolay bir veri bilimi deneyinde size kılavuzluk etmektedir. Biz hello regresyon algoritması kullanılarak bir araba fiyatını tahmin."
keywords: "deneme,doğrusal regresyon,makine öğrenimi algoritmaları,makine öğrenimi öğreticisi,tahmine dayalı modelleme teknikleri,veri bilimi deneyi"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="532ac-105">Makine öğrenimi öğreticisi: Azure Machine Learning Studio'da ilk veri bilimi denemenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="532ac-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="532ac-106">Daha önce **Azure Machine Learning Studio** kullanmadıysanız, bu öğretici sizin için hazırlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="532ac-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="532ac-107">Bu öğreticide, biz nasıl adım geçireceğiz toouse Studio hello için bir makine öğrenimi denemesinin ilk toocreate saat.</span><span class="sxs-lookup"><span data-stu-id="532ac-107">In this tutorial, we'll walk through how toouse Studio for hello first time toocreate a machine learning experiment.</span></span> <span data-ttu-id="532ac-108">Merhaba deneme hello marka ve teknik belirtimler gibi farklı değişkenleri alarak otomobil fiyatını tahmin analitik bir modeli test edeceğiz.</span><span class="sxs-lookup"><span data-stu-id="532ac-108">hello experiment will test an analytical model that predicts hello price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="532ac-109">Bu öğretici, denemenize üzerine nasıl toodrag ve bırak modülleri hello temelleri birbirine bağlamak, hello denemeyi çalıştırın ve hello sonuçlarına bakın gösterir.</span><span class="sxs-lookup"><span data-stu-id="532ac-109">This tutorial shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="532ac-110">Makine öğrenme genel konu veya nasıl tooselect ve kullanım Studio'daki 100 + yerleşik algoritmaları ve veri işleme modülleri hello toodiscuss hello yapacağız değil.</span><span class="sxs-lookup"><span data-stu-id="532ac-110">We're not going toodiscuss hello general topic of machine learning or how tooselect and use hello 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="532ac-111">Yeni toomachine öğrenme değilseniz, video serisi hello [yeni başlayanlar için veri bilimi](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) iyi toostart olabilir.</span><span class="sxs-lookup"><span data-stu-id="532ac-111">If you're new toomachine learning, hello video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place toostart.</span></span> <span data-ttu-id="532ac-112">Her gün dilini ve kavramları kullanarak harika giriş toomachine öğrenme bu video serisidir.</span><span class="sxs-lookup"><span data-stu-id="532ac-112">This video series is a great introduction toomachine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="532ac-113">Machine learning ile benzer, ancak Machine Learning Studio ve hello machine learning algoritmaları içerdiği hakkında daha fazla genel bilgi arıyorsanız, iyi bazı kaynaklar aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="532ac-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and hello machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="532ac-114">Machine Learning Studio nedir?</span><span class="sxs-lookup"><span data-stu-id="532ac-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="532ac-115">- Bu Studio’ya yönelik ileri seviye bir genel bakıştır.</span><span class="sxs-lookup"><span data-stu-id="532ac-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="532ac-116">[Makine öğrenme algoritmasını örneklerle temel](machine-learning-basics-infographic-with-algorithm-examples.md) -bu bilgi grafiği toolearn Machine Learning Studio ile dahil machine learning algoritmaları hello farklı türleri hakkında daha fazla bilgi istiyorsanız kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="532ac-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want toolearn more about hello different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="532ac-117">[Machine Learning Kılavuzu](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -bu kılavuz hello bilgi grafiği yukarıdaki, ancak etkileşimli bir biçimde benzer bilgileri kapsar.</span><span class="sxs-lookup"><span data-stu-id="532ac-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as hello infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="532ac-118">[Makine öğrenimi algoritması bilgi sayfası](machine-learning-algorithm-cheat-sheet.md) ve [nasıl Microsoft Azure Machine Learning için toochoose algoritmaları](machine-learning-algorithm-choice.md) -bu indirilebilir posteri ve eşlik eden makale hello Studio algoritmaları derinlemesine ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="532ac-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss hello Studio algorithms in depth.</span></span>
- <span data-ttu-id="532ac-119">[Machine Learning Studio: Algoritması ve modül Yardım](https://msdn.microsoft.com/library/azure/dn905974.aspx) -hello tam başvuru için makine öğrenimi algoritması da dahil olmak üzere tüm Studio modülleri budur</span><span class="sxs-lookup"><span data-stu-id="532ac-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is hello complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="532ac-120">Machine Learning Studio yardımı nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="532ac-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="532ac-121">Machine Learning Studio'da Tahmine dayalı modelleme teknikleri ile önceden programlanmış sürükle ve bırak modüllerini kullanan bir denemeyi yukarı kolay tooset kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="532ac-121">Machine Learning Studio makes it easy tooset up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="532ac-122">Etkileşimli, görsel bir çalışma alanı kullanarak ***veri kümeleri*** ve analiz ***modüllerini*** etkileşimli bir tuvale sürükleyip bırakın.</span><span class="sxs-lookup"><span data-stu-id="532ac-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="532ac-123">Birlikte tooform bağlanmak bir ***denemeler*** , Machine Learning Studio'da çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="532ac-123">You connect them together tooform an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="532ac-124">***Bir model oluşturmak***, ***hello modeli eğitmek***, ve ***puanı ve test hello modeli***.</span><span class="sxs-lookup"><span data-stu-id="532ac-124">You ***create a model***, ***train hello model***, and ***score and test hello model***.</span></span>

<span data-ttu-id="532ac-125">Model tasarımınızı hello deneme düzenleme yineleyebilirsiniz ve kadar verir çalıştıran Aradığınız sonuçları hello.</span><span class="sxs-lookup"><span data-stu-id="532ac-125">You can iterate on your model design, editing hello experiment and running it until it gives you hello results you're looking for.</span></span> <span data-ttu-id="532ac-126">Modeliniz hazır olduğunda, başkalarının yeni veriler göndererek tahminler alabilmesi için bir ***web hizmeti*** olarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532ac-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="532ac-127">Machine Learning Studio’yu açma</span><span class="sxs-lookup"><span data-stu-id="532ac-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="532ac-128">Studio ile çalışmaya tooget Git çok[https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="532ac-128">tooget started with Studio, go too[https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="532ac-129">Machine Learning Studio’da daha önce oturum açtıysanız **Oturum Aç**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532ac-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="532ac-130">Veya **Buradan kaydolun**’a tıklayıp ücretsiz ve ücretli seçenekler arasından seçim yapın.</span><span class="sxs-lookup"><span data-stu-id="532ac-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="532ac-131">![TooMachine Learning Studio'da oturum açın][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="532ac-131">![Sign in tooMachine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="532ac-132">
***TooMachine Learning Studio'da oturum açın***</span><span class="sxs-lookup"><span data-stu-id="532ac-132">
***Sign in tooMachine Learning Studio***</span></span>

## <a name="five-steps-toocreate-an-experiment"></a><span data-ttu-id="532ac-133">Beş adımı toocreate bir deneme</span><span class="sxs-lookup"><span data-stu-id="532ac-133">Five steps toocreate an experiment</span></span>

<span data-ttu-id="532ac-134">Bu makine öğrenimi öğreticisinde, beş temel adımı toobuild Machine Learning Studio toocreate, eğitme, bir deneme izleyin ve modelinizi puan:</span><span class="sxs-lookup"><span data-stu-id="532ac-134">In this machine learning tutorial, you'll follow five basic steps toobuild an experiment in Machine Learning Studio toocreate, train, and score your model:</span></span>

- <span data-ttu-id="532ac-135">**Bir model oluşturma**</span><span class="sxs-lookup"><span data-stu-id="532ac-135">**Create a model**</span></span>
    - <span data-ttu-id="532ac-136">[1. Adım: Verileri alma]</span><span class="sxs-lookup"><span data-stu-id="532ac-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="532ac-137">[2. adım: hello verileri hazırlama]</span><span class="sxs-lookup"><span data-stu-id="532ac-137">[Step 2: Prepare hello data]</span></span>
    - <span data-ttu-id="532ac-138">[3. Adım: Özellikleri tanımlama]</span><span class="sxs-lookup"><span data-stu-id="532ac-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="532ac-139">**Tren hello modeli**</span><span class="sxs-lookup"><span data-stu-id="532ac-139">**Train hello model**</span></span>
    - <span data-ttu-id="532ac-140">[4. Adım: Bir öğrenme algoritması seçme ve uygulama]</span><span class="sxs-lookup"><span data-stu-id="532ac-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="532ac-141">**Puan ve test modeli hello**</span><span class="sxs-lookup"><span data-stu-id="532ac-141">**Score and test hello model**</span></span>
    - <span data-ttu-id="532ac-142">[5. Adım: Yeni otomobil fiyatlarını tahmin etme]</span><span class="sxs-lookup"><span data-stu-id="532ac-142">[Step 5: Predict new automobile prices]</span></span>

[1. Adım: Verileri alma]: #step-1-get-data
[2. adım: hello verileri hazırlama]: #step-2-prepare-the-data
[3. Adım: Özellikleri tanımlama]: #step-3-define-features
[4. Adım: Bir öğrenme algoritması seçme ve uygulama]: #step-4-choose-and-apply-a-learning-algorithm
[5. Adım: Yeni otomobil fiyatlarını tahmin etme]: #step-5-predict-new-automobile-prices

> [!TIP] 
> <span data-ttu-id="532ac-148">Merhaba çalışan bir kopyasını bulabilirsiniz hello denemesinde aşağıdaki [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="532ac-148">You can find a working copy of hello following experiment in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="532ac-149">Çok Git**[ilk veri bilimi denemeler - otomobil fiyat tahmini](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  tıklatıp **Studio'da Aç** toodownload hello denemeyi Machine Learning içine bir kopyasını Studio çalışma alanı.</span><span class="sxs-lookup"><span data-stu-id="532ac-149">Go too**[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="532ac-150">1. Adım: Verileri alma</span><span class="sxs-lookup"><span data-stu-id="532ac-150">Step 1: Get data</span></span>

<span data-ttu-id="532ac-151">tooperform machine learning gereken ilk şey hello verilerdir.</span><span class="sxs-lookup"><span data-stu-id="532ac-151">hello first thing you need tooperform machine learning is data.</span></span>
<span data-ttu-id="532ac-152">Machine Learning Studio'da kullanabileceğiniz birçok örnek veri kümesi bulunur ve birçok kaynaktan verileri içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532ac-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="532ac-153">Bu örnekte, hello örnek veri kümesini kullanacağız **otomobil fiyat verileri (ham)**, çalışma alanınızda bulunur.</span><span class="sxs-lookup"><span data-stu-id="532ac-153">For this example, we'll use hello sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="532ac-154">Bu veri kümesi; marka, model, teknik belirtimler ve fiyat gibi bilgiler dahil olmak üzere birçok ayrı otomobil için giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="532ac-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="532ac-155">İşte nasıl tooget hello dataset denemenize.</span><span class="sxs-lookup"><span data-stu-id="532ac-155">Here's how tooget hello dataset into your experiment.</span></span>

1. <span data-ttu-id="532ac-156">Tıklayarak yeni bir deneme oluşturma **+ yeni** hello Machine Learning Studio penceresinin hello altında seçin **DENEMELER**ve ardından **boş denemeler**.</span><span class="sxs-lookup"><span data-stu-id="532ac-156">Create a new experiment by clicking **+NEW** at hello bottom of hello Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="532ac-157">Merhaba deneme hello tuvale hello üstünde görebilirsiniz varsayılan adı verilir.</span><span class="sxs-lookup"><span data-stu-id="532ac-157">hello experiment is given a default name that you can see at hello top of hello canvas.</span></span> <span data-ttu-id="532ac-158">Bu metin seçin ve toosomething anlamlı, örneğin, yeniden adlandırma **otomobil fiyat tahmini**.</span><span class="sxs-lookup"><span data-stu-id="532ac-158">Select this text and rename it toosomething meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="532ac-159">Merhaba adı toobe benzersiz gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="532ac-159">hello name doesn't need toobe unique.</span></span>

    ![Merhaba deneme yeniden adlandırma][rename-experiment]

2. <span data-ttu-id="532ac-161">Merhaba deneme tuvalinin toohello solundaki veri kümelerini ve modülleri paletini ' dir.</span><span class="sxs-lookup"><span data-stu-id="532ac-161">toohello left of hello experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="532ac-162">Tür **otomobil** hello arama kutusuna etiketli bu palet toofind hello dataset hello üstündeki **otomobil fiyat verileri (ham)**.</span><span class="sxs-lookup"><span data-stu-id="532ac-162">Type **automobile** in hello Search box at hello top of this palette toofind hello dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="532ac-163">Bu veri kümesi toohello deneme tuvaline sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="532ac-163">Drag this dataset toohello experiment canvas.</span></span>

    <span data-ttu-id="532ac-164">![Merhaba otomobil veri kümesi bulma ve hello deneme tuvaline sürükleyin][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-164">![Find hello automobile dataset and drag it onto hello experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="532ac-165">***Merhaba otomobil veri kümesi bulma ve hello deneme tuvaline sürükleyin***</span><span class="sxs-lookup"><span data-stu-id="532ac-165">***Find hello automobile dataset and drag it onto hello experiment canvas***</span></span>

<span data-ttu-id="532ac-166">toosee bu verileri hello otomobil veri kümesinin hello altındaki hello çıkış bağlantı noktasına tıklayın ve ardından gibi göründüğünü **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="532ac-166">toosee what this data looks like, click hello output port at hello bottom of hello automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="532ac-167">![Merhaba çıkış bağlantı noktasına tıklayın ve "Görselleştir" seçin][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="532ac-167">![Click hello output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="532ac-168">
***Merhaba çıkış bağlantı noktasına tıklayın ve "Görselleştir" seçin***</span><span class="sxs-lookup"><span data-stu-id="532ac-168">
***Click hello output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="532ac-169">Veri kümelerini ve modülleri giriş ve bağlantı noktaları hello altındaki çıkış bağlantı noktaları küçük daireler - hello üstünde, giriş bağlantı noktaları tarafından temsil edilen çıkış.</span><span class="sxs-lookup"><span data-stu-id="532ac-169">Datasets and modules have input and output ports represented by small circles - input ports at hello top, output ports at hello bottom.</span></span>
<span data-ttu-id="532ac-170">toocreate denemenizi üzerinden veri akışı, bir modül tooan giriş bağlantı noktası başka bir çıkış bağlantı noktasına bağlanırsınız.</span><span class="sxs-lookup"><span data-stu-id="532ac-170">toocreate a flow of data through your experiment, you'll connect an output port of one module tooan input port of another.</span></span>
<span data-ttu-id="532ac-171">Herhangi bir zamanda hello verileri bu noktada hello veri akışında benzer bir veri kümesi veya modülü toosee hello çıkış bağlantı noktasına tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532ac-171">At any time, you can click hello output port of a dataset or module toosee what hello data looks like at that point in hello data flow.</span></span>

<span data-ttu-id="532ac-172">Bu örnek veri kümesi her bir otomobil örneği de satır olarak görünür ve her otomobil ile ilişkili hello değişkenleri sütun olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="532ac-172">In this sample dataset, each instance of an automobile appears as a row, and hello variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="532ac-173">Merhaba değişkenleri için belirli bir otomobil verildiğinde, tootry toopredict hello fiyat sağdaki sütun (sütun başlıklı 26, "Fiyat") yapacağız.</span><span class="sxs-lookup"><span data-stu-id="532ac-173">Given hello variables for a specific automobile, we're going tootry toopredict hello price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="532ac-174">![Merhaba veri görselleştirme penceresinde Hello otomobil veri görüntüle][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="532ac-174">![View hello automobile data in hello data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="532ac-175">
***Merhaba veri görselleştirme penceresinde Hello otomobil veri görüntüle***</span><span class="sxs-lookup"><span data-stu-id="532ac-175">
***View hello automobile data in hello data visualization window***</span></span>

<span data-ttu-id="532ac-176">Merhaba tıklayarak görselleştirme penceresini kapat hello "**x**" Merhaba sağ üst köşedeki.</span><span class="sxs-lookup"><span data-stu-id="532ac-176">Close hello visualization window by clicking hello "**x**" in hello upper-right corner.</span></span>

## <a name="step-2-prepare-hello-data"></a><span data-ttu-id="532ac-177">2. adım: hello verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="532ac-177">Step 2: Prepare hello data</span></span>

<span data-ttu-id="532ac-178">Genellikle bir veri kümesi analiz edilmeden önce biraz ön işleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="532ac-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="532ac-179">Örneğin, değerleri hello çeşitli satırların sütunlarında mevcut eksik hello fark.</span><span class="sxs-lookup"><span data-stu-id="532ac-179">For example, you might have noticed hello missing values present in hello columns of various rows.</span></span> <span data-ttu-id="532ac-180">Bu eksik değerlerin toobe hello modeli hello verileri doğru şekilde analiz edebilmesi temizlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="532ac-180">These missing values need toobe cleaned so hello model can analyze hello data correctly.</span></span> <span data-ttu-id="532ac-181">Örneğimizde eksik değerleri olan satırları kaldıracağız.</span><span class="sxs-lookup"><span data-stu-id="532ac-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="532ac-182">Ayrıca, hello **normalleştirilmiş kayıplar** sütununda eksik değerleri büyük bir kısmının Biz bu sütun hello modelin tamamen dışında şekilde.</span><span class="sxs-lookup"><span data-stu-id="532ac-182">Also, hello **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from hello model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="532ac-183">Değerleri giriş verilerinden eksik temizleme hello hello modüllerin çoğu kullanmak için bir önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="532ac-183">Cleaning hello missing values from input data is a prerequisite for using most of hello modules.</span></span>

<span data-ttu-id="532ac-184">Merhaba kaldıran bir modül önce eklediğimiz **normalleştirilmiş kayıplar** sütun tamamen ve ardından eksik verileri olan herhangi bir satırın kaldırır başka bir modül ekleriz.</span><span class="sxs-lookup"><span data-stu-id="532ac-184">First we add a module that removes hello **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="532ac-185">Tür **sütunları seçin** hello arama kutusuna hello modül paleti toofind hello hello üstündeki [Select Columns in Dataset sütun] [ select-columns] modül toohello deneme tuvaline sürükleyin .</span><span class="sxs-lookup"><span data-stu-id="532ac-185">Type **select columns** in hello Search box at hello top of hello module palette toofind hello [Select Columns in Dataset][select-columns] module, then drag it toohello experiment canvas.</span></span> <span data-ttu-id="532ac-186">Bu modül bize modeli tooinclude istediğiniz veya dışarıda verilerin hangi sütunların hello tooselect sağlar.</span><span class="sxs-lookup"><span data-stu-id="532ac-186">This module allows us tooselect which columns of data we want tooinclude or exclude in hello model.</span></span>

2. <span data-ttu-id="532ac-187">Merhaba Hello çıkış bağlantı noktasına bağlanmak **otomobil fiyat verileri (ham)** dataset toohello giriş bağlantı noktası hello [Select Columns in Dataset sütun] [ select-columns] modülü.</span><span class="sxs-lookup"><span data-stu-id="532ac-187">Connect hello output port of hello **Automobile price data (Raw)** dataset toohello input port of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="532ac-188">![Merhaba "Sütun Dataset içinde seçin" modülü toohello deneme tuvalinin ekleyin ve bunu bağlayın][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-188">![Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="532ac-189">***Merhaba "Sütun Dataset içinde seçin" modülü toohello deneme tuvalinin ekleyin ve bunu bağlayın***</span><span class="sxs-lookup"><span data-stu-id="532ac-189">***Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it***</span></span>

3. <span data-ttu-id="532ac-190">Merhaba tıklatın [Select Columns in Dataset sütun] [ select-columns] modülü ve tıklatın **başlatma Sütun seçiciyi** hello içinde **özellikleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="532ac-190">Click hello [Select Columns in Dataset][select-columns] module and click **Launch column selector** in hello **Properties** pane.</span></span>

    - <span data-ttu-id="532ac-191">Hello solda tıklatın **kurallarla**</span><span class="sxs-lookup"><span data-stu-id="532ac-191">On hello left, click **With rules**</span></span>
    - <span data-ttu-id="532ac-192">**Şununla Başla** altında **Tüm sütunlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532ac-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="532ac-193">Bu yönlendirir [Select Columns in Dataset sütun] [ select-columns] tüm hello sütunlar (dışında hakkında tooexclude ki bu sütunları) aracılığıyla toopass.</span><span class="sxs-lookup"><span data-stu-id="532ac-193">This directs [Select Columns in Dataset][select-columns] toopass through all hello columns (except those columns we're about tooexclude).</span></span>
    - <span data-ttu-id="532ac-194">Merhaba aşağı açılan listeler, seçin **hariç** ve **sütun adları**ve ardından hello metin kutusunun içine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532ac-194">From hello drop-downs, select **Exclude** and **column names**, and then click inside hello text box.</span></span> <span data-ttu-id="532ac-195">Sütun listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="532ac-195">A list of columns is displayed.</span></span> <span data-ttu-id="532ac-196">Seçin **normalleştirilmiş kayıplar**, ve eklenen toohello metin kutusu olur.</span><span class="sxs-lookup"><span data-stu-id="532ac-196">Select **normalized-losses**, and it's added toohello text box.</span></span>
    - <span data-ttu-id="532ac-197">Merhaba onay işareti (Tamam) düğmesine tooclose hello Sütun seçiciyi (üzerinde hello sağ alt köşedeki) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532ac-197">Click hello check mark (OK) button tooclose hello column selector (on hello lower-right).</span></span>

    <span data-ttu-id="532ac-198">![Merhaba Sütun seçiciyi Başlat ve "normalleştirilmiş kayıplar" Merhaba sütununu hariç tutmak][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-198">![Launch hello column selector and exclude hello "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="532ac-199">***Merhaba Sütun seçiciyi Başlat ve "normalleştirilmiş kayıplar" Merhaba sütununu hariç tutmak***</span><span class="sxs-lookup"><span data-stu-id="532ac-199">***Launch hello column selector and exclude hello "normalized-losses" column***</span></span>

    <span data-ttu-id="532ac-200">Şimdi hello Özellikler bölmesi için **Select Columns in Dataset sütun** , tüm sütunlardan dışında hello kümesinden geçeceğini belirtir **normalleştirilmiş kayıplar**.</span><span class="sxs-lookup"><span data-stu-id="532ac-200">Now hello properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from hello dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="532ac-201">![Merhaba "normalleştirilmiş kayıplar" sütunun dışarıda Hello Özellikler bölmesi gösterir][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-201">![hello properties pane shows that hello "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="532ac-202">***Merhaba "normalleştirilmiş kayıplar" sütunun dışarıda Hello Özellikler bölmesi gösterir***</span><span class="sxs-lookup"><span data-stu-id="532ac-202">***hello properties pane shows that hello "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="532ac-203">Bir yorum tooa modülü bağlantısındaki hello modülü ve metin girme tarafından ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532ac-203">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="532ac-204">Bu, bir bakışta görmenize yardımcı hangi hello modülün denemenizde yapıyor.</span><span class="sxs-lookup"><span data-stu-id="532ac-204">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="532ac-205">Bu durumda, hello çift [Select Columns in Dataset sütun] [ select-columns] modülü ve türü hello Açıklama "Dışlama normalleştirilmiş kayıplar."</span><span class="sxs-lookup"><span data-stu-id="532ac-205">In this case double-click hello [Select Columns in Dataset][select-columns] module and type hello comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="532ac-206">![Bir modül tooadd yorum çift tıklatın][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-206">![Double-click a module tooadd a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="532ac-207">***Bir modül tooadd yorum çift tıklatın***</span><span class="sxs-lookup"><span data-stu-id="532ac-207">***Double-click a module tooadd a comment***</span></span>

3. <span data-ttu-id="532ac-208">Sürükleme hello [Clean Missing Data] [ clean-missing-data] modülü toohello tuvale denemek ve toohello bağlanmak [Select Columns in Dataset sütun] [ select-columns] modülü.</span><span class="sxs-lookup"><span data-stu-id="532ac-208">Drag hello [Clean Missing Data][clean-missing-data] module toohello experiment canvas and connect it toohello [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="532ac-209">Merhaba, **özellikleri** bölmesinde, **tüm satırı Kaldır** altında **temizleme modu**.</span><span class="sxs-lookup"><span data-stu-id="532ac-209">In hello **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="532ac-210">Bu yönlendirir [Clean Missing Data] [ clean-missing-data] tüm eksik değerleri olan satırları kaldırarak tooclean hello veri.</span><span class="sxs-lookup"><span data-stu-id="532ac-210">This directs [Clean Missing Data][clean-missing-data] tooclean hello data by removing rows that have any missing values.</span></span> <span data-ttu-id="532ac-211">Merhaba modüle çift tıklayın ve "eksik değerli satırları Kaldır" Merhaba yorum yazın</span><span class="sxs-lookup"><span data-stu-id="532ac-211">Double-click hello module and type hello comment "Remove missing value rows."</span></span>

    <span data-ttu-id="532ac-212">![Merhaba temizleme modunu ayarlama çok "Kaldır tüm satırı" hello "Clean Missing Data" modülü][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-212">![Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="532ac-213">***Merhaba temizleme modunu ayarlama çok "Kaldır tüm satırı" hello "Clean Missing Data" modülü***</span><span class="sxs-lookup"><span data-stu-id="532ac-213">***Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="532ac-214">Tıklayarak Hello denemeyi çalıştırın **çalıştırmak** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="532ac-214">Run hello experiment by clicking **RUN** at hello bottom of hello page.</span></span>

    <span data-ttu-id="532ac-215">Merhaba deneme çalışması sona erdi, tüm hello modülleri başarıyla tamamlandı yeşil onay işareti tooindicate vardır.</span><span class="sxs-lookup"><span data-stu-id="532ac-215">When hello experiment has finished running, all hello modules have a green check mark tooindicate that they finished successfully.</span></span> <span data-ttu-id="532ac-216">Ayrıca hello fark **çalıştırma tamamlandı** hello sağ üst köşesinde durumunda.</span><span class="sxs-lookup"><span data-stu-id="532ac-216">Notice also hello **Finished running** status in hello upper-right corner.</span></span>

<span data-ttu-id="532ac-217">![Çalıştırdıktan sonra hello deneme aşağıdakine benzer görünmelidir][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="532ac-217">![After running it, hello experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="532ac-218">
***Çalıştırdıktan sonra hello deneme aşağıdakine benzer görünmelidir***</span><span class="sxs-lookup"><span data-stu-id="532ac-218">
***After running it, hello experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="532ac-219">Neden hello denemeyi şimdi karşılaştınız?</span><span class="sxs-lookup"><span data-stu-id="532ac-219">Why did we run hello experiment now?</span></span> <span data-ttu-id="532ac-220">Çalışan hello deney tarafından hello aracılığıyla hello dataset hello sütun tanımları veri geçirmek [Select Columns in Dataset sütun] [ select-columns] modülü ile Merhaba [Clean Missing Data] [ clean-missing-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="532ac-220">By running hello experiment, hello column definitions for our data pass from hello dataset, through hello [Select Columns in Dataset][select-columns] module, and through hello [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="532ac-221">Biz bağlanmak çok herhangi bir modül buna[Clean Missing Data] [ clean-missing-data] aynı bilgiler da sahip olur.</span><span class="sxs-lookup"><span data-stu-id="532ac-221">This means that any modules we connect too[Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="532ac-222">Tüm hello deneme toothis noktası yukarı içinde yaptığınızdan temiz hello veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="532ac-222">All we have done in hello experiment up toothis point is clean hello data.</span></span> <span data-ttu-id="532ac-223">Tooview temizlenmesi hello dataset isterseniz, sol çıkış bağlantı noktasına hello hello tıklatın [Clean Missing Data] [ clean-missing-data] modülü ve select **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="532ac-223">If you want tooview hello cleaned dataset, click hello left output port of hello [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="532ac-224">Bu hello fark **normalleştirilmiş kayıplar** sütun dahil olduğunu artık ve eksik değerlerin yok.</span><span class="sxs-lookup"><span data-stu-id="532ac-224">Notice that hello **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="532ac-225">Merhaba veri temiz olduğunu, hangi özellikler biz hazır toospecify dileriz toouse hello Tahmine dayalı modelde oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="532ac-225">Now that hello data is clean, we're ready toospecify what features we're going toouse in hello predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="532ac-226">3. Adım: Özellikleri tanımlama</span><span class="sxs-lookup"><span data-stu-id="532ac-226">Step 3: Define features</span></span>

<span data-ttu-id="532ac-227">Machine learning'de *özellikler*, ilgilendiğiniz bir şeyin tek tek ölçülebilir özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="532ac-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="532ac-228">Veri kümemizde her bir satır bir otomobili temsil eder ve her bir sütun da bu otomobilin bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="532ac-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="532ac-229">Tahmine dayalı bir model oluşturmak için özellikleri iyi bir dizi deney ve hello sorun hakkında bilgi gerektirir bulma toosolve istiyor.</span><span class="sxs-lookup"><span data-stu-id="532ac-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about hello problem you want toosolve.</span></span> <span data-ttu-id="532ac-230">Bazı özellikleri diğerlerinden hello hedefi tahmin etmede daha uygundur.</span><span class="sxs-lookup"><span data-stu-id="532ac-230">Some features are better for predicting hello target than others.</span></span> <span data-ttu-id="532ac-231">Ayrıca, bazı özelliklerin diğer özelliklerle güçlü bir bağıntısı vardır ve kaldırılabilirler.</span><span class="sxs-lookup"><span data-stu-id="532ac-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="532ac-232">Biz bir tutmak ve hello tahmin önemli ölçüde etkilemeden hello diğer kaldırmak için örneğin, şehir-mpg ile otoban-mpg yakından ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="532ac-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove hello other without significantly affecting hello prediction.</span></span>

<span data-ttu-id="532ac-233">Şimdi kümemize hello özelliklerinin bir alt kümesi kullanan bir model oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="532ac-233">Let's build a model that uses a subset of hello features in our dataset.</span></span> <span data-ttu-id="532ac-234">Daha sonra dönmek ve farklı özellikler seçebilir, hello denemeyi tekrar çalıştırabilir ve daha iyi sonuçlar alırsanız bkz.</span><span class="sxs-lookup"><span data-stu-id="532ac-234">You can come back later and select different features, run hello experiment again, and see if you get better results.</span></span> <span data-ttu-id="532ac-235">Ancak toostart, özellikler aşağıdaki hello deneyelim:</span><span class="sxs-lookup"><span data-stu-id="532ac-235">But toostart, let's try hello following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="532ac-236">Başka bir sürükleyin [Select Columns in Dataset sütun] [ select-columns] modülü toohello deneme tuvaline.</span><span class="sxs-lookup"><span data-stu-id="532ac-236">Drag another [Select Columns in Dataset][select-columns] module toohello experiment canvas.</span></span> <span data-ttu-id="532ac-237">Merhaba çıkış bağlantı noktasına sol hello bağlanmak [Clean Missing Data] [ clean-missing-data] hello modülü toohello girişi [Select Columns in Dataset sütun] [ select-columns] modülü.</span><span class="sxs-lookup"><span data-stu-id="532ac-237">Connect hello left output port of hello [Clean Missing Data][clean-missing-data] module toohello input of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="532ac-238">![Merhaba "Sütun Dataset içinde seçin" modülü toohello "Clean Missing Data" modülünü bağlama][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-238">![Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="532ac-239">***Merhaba "Sütun Dataset içinde seçin" modülü toohello "Clean Missing Data" modülünü bağlama***</span><span class="sxs-lookup"><span data-stu-id="532ac-239">***Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="532ac-240">Merhaba modüle çift tıklayın ve "Tahmin için özellik seç." yazın</span><span class="sxs-lookup"><span data-stu-id="532ac-240">Double-click hello module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="532ac-241">Tıklatın **başlatma Sütun seçiciyi** hello içinde **özellikleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="532ac-241">Click **Launch column selector** in hello **Properties** pane.</span></span>

3. <span data-ttu-id="532ac-242">**Kurallar ile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532ac-242">Click **With rules**.</span></span>

4. <span data-ttu-id="532ac-243">**Şununla Başla** altında **Sütun yok**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532ac-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="532ac-244">Merhaba filtre satırını seçin **INCLUDE** ve **sütun adları** ve sütun adları listesi hello metin kutusunda seçin.</span><span class="sxs-lookup"><span data-stu-id="532ac-244">In hello filter row, select **Include** and **column names** and select our list of column names in hello text box.</span></span> <span data-ttu-id="532ac-245">Belirttiğimiz olanları hello dışında herhangi bir sütundan (Özellikler) hello modülü toonot geçiş yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="532ac-245">This directs hello module toonot pass through any columns (features) except hello ones that we specify.</span></span>

5. <span data-ttu-id="532ac-246">Merhaba onay işareti (Tamam) düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532ac-246">Click hello check mark (OK) button.</span></span>

    <span data-ttu-id="532ac-247">![Merhaba sütunlar (Özellikler) tooinclude hello öngörü seçin][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-247">![Select hello columns (features) tooinclude in hello prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="532ac-248">***Merhaba sütunlar (Özellikler) tooinclude hello öngörü seçin***</span><span class="sxs-lookup"><span data-stu-id="532ac-248">***Select hello columns (features) tooinclude in hello prediction***</span></span>

<span data-ttu-id="532ac-249">Bu öğrenme algoritmasının hello sonraki adımda kullanacağız toopass toohello istiyoruz yalnızca hello özellikleri içeren filtrelenmiş bir veri kümesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="532ac-249">This produces a filtered dataset containing only hello features we want toopass toohello learning algorithm we'll use in hello next step.</span></span> <span data-ttu-id="532ac-250">Daha sonra geri dönüp farklı özellikler seçerek yeniden deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532ac-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="532ac-251">4. Adım: Bir öğrenme algoritması seçme ve uygulama</span><span class="sxs-lookup"><span data-stu-id="532ac-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="532ac-252">Merhaba veriler hazır olduğuna göre Tahmine dayalı bir model oluşturmak eğitim ve sınama oluşur.</span><span class="sxs-lookup"><span data-stu-id="532ac-252">Now that hello data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="532ac-253">Veri tootrain hello modelimizi kullanacağız ve ardından biz hello modeli toosee test edeceksiniz ne kadar yakından mümkün toopredict fiyatlar değil.</span><span class="sxs-lookup"><span data-stu-id="532ac-253">We'll use our data tootrain hello model, and then we'll test hello model toosee how closely it's able toopredict prices.</span></span>
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

<span data-ttu-id="532ac-254">*Sınıflandırma* ve *regresyon*, denetimli makine öğrenimi algoritmasının iki türüdür.</span><span class="sxs-lookup"><span data-stu-id="532ac-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="532ac-255">Sınıflandırma; renk gibi (kırmızı, mavi veya yeşil) tanımlanmış bir kategori kümesinden yanıt tahmin eder.</span><span class="sxs-lookup"><span data-stu-id="532ac-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="532ac-256">Regresyon kullanılan toopredict bir sayı değil.</span><span class="sxs-lookup"><span data-stu-id="532ac-256">Regression is used toopredict a number.</span></span>

<span data-ttu-id="532ac-257">Bir sayıdır toopredict price istediğimiz çünkü bir regresyon algoritmasıdır. kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="532ac-257">Because we want toopredict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="532ac-258">Bu örnek için, basit bir *çizgisel regresyon* modeli kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="532ac-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="532ac-259">Machine learning algoritmaları farklı türleri hakkında daha fazla toolearn istiyorsanız ve ne zaman toouse onları, yeni başlayanlar seri için veri bilimi hello içinde hello ilk video görebileceği [hello beş veri bilimi yanıtlar sorular](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="532ac-259">If you want toolearn more about different types of machine learning algorithms and when toouse them, you might view hello first video in hello Data Science for Beginners series, [hello five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="532ac-260">Merhaba bilgi grafiği ayrıca görünebilir [makine öğrenme algoritmasını örneklerle temel](machine-learning-basics-infographic-with-algorithm-examples.md), veya hello denetleyin [makine öğrenimi algoritması bilgi sayfası](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="532ac-260">You might also look at hello infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out hello [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="532ac-261">Biz hello fiyatına dahildir veri kümesini vererek hello modeli eğitmek.</span><span class="sxs-lookup"><span data-stu-id="532ac-261">We train hello model by giving it a set of data that includes hello price.</span></span> <span data-ttu-id="532ac-262">Merhaba modeli hello veri ve otomobil ait özellikler ve onun fiyat arasındaki bağıntıları arayın tarar.</span><span class="sxs-lookup"><span data-stu-id="532ac-262">hello model scans hello data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="532ac-263">Ardından hello modeli test edeceksiniz - biz aşina ki otomobiller için bir özellikler kümesi sağlar ve ne kadar yakın hello modeli toopredicting hello bilinen fiyat geldiğini görmek.</span><span class="sxs-lookup"><span data-stu-id="532ac-263">Then we'll test hello model - we'll give it a set of features for automobiles we're familiar with and see how close hello model comes toopredicting hello known price.</span></span>

<span data-ttu-id="532ac-264">Merhaba model eğitim hem de ayrı eğitim ve test veri kümeleri halinde hello veri bölerek sınama için verilerimizi kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="532ac-264">We'll use our data for both training hello model and testing it by splitting hello data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="532ac-265">Seçin ve hello sürükleyin [bölünmüş veri] [ split] modülü toohello tuvale denemek ve son toohello bağlantı [Select Columns in Dataset sütun] [ select-columns] Modül.</span><span class="sxs-lookup"><span data-stu-id="532ac-265">Select and drag hello [Split Data][split] module toohello experiment canvas and connect it toohello last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="532ac-266">Merhaba tıklatın [bölünmüş veri] [ split] modülü tooselect.</span><span class="sxs-lookup"><span data-stu-id="532ac-266">Click hello [Split Data][split] module tooselect it.</span></span> <span data-ttu-id="532ac-267">Hello bulur **hello satırlar için kesir değerini ilk çıkış veri kümesi** (Merhaba içinde **özellikleri** bölmesinde toohello hello tuvalin sağındaki) ve too0.75 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="532ac-267">Find hello **Fraction of rows in hello first output dataset** (in hello **Properties** pane toohello right of hello canvas) and set it too0.75.</span></span> <span data-ttu-id="532ac-268">Bu şekilde, biz hello veri tootrain hello modeli yüzde 75'ini kullanın ve geri test etmek için yüzde 25 tutun (daha sonra farklı yüzdeleri kullanarak ile deneyebilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="532ac-268">This way, we'll use 75 percent of hello data tootrain hello model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="532ac-269">![Set hello hello "Böl verileri" modülü too0.75 kesir bölme][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-269">![Set hello split fraction of hello "Split Data" module too0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="532ac-270">***Set hello hello "Böl verileri" modülü too0.75 kesir bölme***</span><span class="sxs-lookup"><span data-stu-id="532ac-270">***Set hello split fraction of hello "Split Data" module too0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="532ac-271">Merhaba değiştirerek **rastgele doldurma** parametresi, eğitim ve test etme için farklı rastgele örnekler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532ac-271">By changing hello **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="532ac-272">Bu parametre hello hello sözde rastgele sayı üreticisinin doldurulmasını denetler.</span><span class="sxs-lookup"><span data-stu-id="532ac-272">This parameter controls hello seeding of hello pseudo-random number generator.</span></span>

2. <span data-ttu-id="532ac-273">Merhaba denemeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="532ac-273">Run hello experiment.</span></span> <span data-ttu-id="532ac-274">Merhaba deneme çalıştırdığınızda hello [Select Columns in Dataset sütun] [ select-columns] ve [bölünmüş veri] [ split] modüllerinin sütun tanımlarını toohello geçirin Modül biz sonraki ekleme.</span><span class="sxs-lookup"><span data-stu-id="532ac-274">When hello experiment is run, hello [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions toohello modules we'll be adding next.</span></span>  

3. <span data-ttu-id="532ac-275">algoritma, öğrenme tooselect hello hello genişletin **Machine Learning** hello modül paleti toohello sol kategorisinde hello tuvale ve ardından genişletin **modeli Başlat**.</span><span class="sxs-lookup"><span data-stu-id="532ac-275">tooselect hello learning algorithm, expand hello **Machine Learning** category in hello module palette toohello left of hello canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="532ac-276">Bu, kullanılan tooinitialize machine learning algoritmaları olabilir modülleri çeşitli kategorileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="532ac-276">This displays several categories of modules that can be used tooinitialize machine learning algorithms.</span></span> <span data-ttu-id="532ac-277">Bu deneme için hello seçin [doğrusal regresyon] [ linear-regression] hello altında Modülü **regresyon** kategori ve toohello deneme tuvaline sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="532ac-277">For this experiment, select hello [Linear Regression][linear-regression] module under hello **Regression** category, and drag it toohello experiment canvas.</span></span>
<span data-ttu-id="532ac-278">(Ayrıca hello modülü hello palet arama kutusuna "doğrusal regresyon" yazarak bulabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="532ac-278">(You can also find hello module by typing "linear regression" in hello palette Search box.)</span></span>

4. <span data-ttu-id="532ac-279">Bulma ve hello sürükleyin [Train Model] [ train-model] modülü toohello deneme tuvaline.</span><span class="sxs-lookup"><span data-stu-id="532ac-279">Find and drag hello [Train Model][train-model] module toohello experiment canvas.</span></span> <span data-ttu-id="532ac-280">Merhaba Hello çıkışına bağlayın [doğrusal regresyon] [ linear-regression] modülü toohello sol hello girişi [Train Model] [ train-model] modül ve hello bağlanın Eğitim verileri çıkışına (sol bağlantı noktası) hello [bölünmüş veri] [ split] modülü toohello sağ girişi hello [Train Model] [ train-model] Modül.</span><span class="sxs-lookup"><span data-stu-id="532ac-280">Connect hello output of hello [Linear Regression][linear-regression] module toohello left input of hello [Train Model][train-model] module, and connect hello training data output (left port) of hello [Split Data][split] module toohello right input of hello [Train Model][train-model] module.</span></span>

    <span data-ttu-id="532ac-281">!["Doğrusal regresyon" ve "Böl verileri" Hello "Train Model" modülü tooboth hello modülleri Bağlan][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-281">![Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="532ac-282">***"Doğrusal regresyon" ve "Böl verileri" Hello "Train Model" modülü tooboth hello modülleri Bağlan***</span><span class="sxs-lookup"><span data-stu-id="532ac-282">***Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="532ac-283">Merhaba tıklatın [Train Model] [ train-model] modülü,'ı tıklatın **başlatma Sütun seçiciyi** hello içinde **özellikleri** bölmesinde ve ardından hello **fiyat** sütun.</span><span class="sxs-lookup"><span data-stu-id="532ac-283">Click hello [Train Model][train-model] module, click **Launch column selector** in hello **Properties** pane, and then select hello **price** column.</span></span> <span data-ttu-id="532ac-284">Bu bizim modeli giderek toopredict olduğunu hello değerdir.</span><span class="sxs-lookup"><span data-stu-id="532ac-284">This is hello value that our model is going toopredict.</span></span>

    <span data-ttu-id="532ac-285">Merhaba seçin **fiyat** hello taşıyarak hello Sütun seçiciyi sütununda **kullanılabilir sütunlar** toohello listesinde **seçili sütunların** listesi.</span><span class="sxs-lookup"><span data-stu-id="532ac-285">You select hello **price** column in hello column selector by moving it from hello **Available columns** list toohello **Selected columns** list.</span></span>

    <span data-ttu-id="532ac-286">![Merhaba "Train Model" modülü için Hello fiyat sütun seçin][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-286">![Select hello price column for hello "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="532ac-287">***Merhaba "Train Model" modülü için Hello fiyat sütun seçin***</span><span class="sxs-lookup"><span data-stu-id="532ac-287">***Select hello price column for hello "Train Model" module***</span></span>

6. <span data-ttu-id="532ac-288">Merhaba denemeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="532ac-288">Run hello experiment.</span></span>

<span data-ttu-id="532ac-289">Şimdi kullanılan tooscore yeni otomobil veri toomake fiyat tahminleri olabilir eğitilen regresyon modeli sahibiz.</span><span class="sxs-lookup"><span data-stu-id="532ac-289">We now have a trained regression model that can be used tooscore new automobile data toomake price predictions.</span></span>

<span data-ttu-id="532ac-290">![Çalıştırdıktan sonra hello deneme aşağıdakine benzer görünmelidir][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="532ac-290">![After running, hello experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="532ac-291">
***Çalıştırdıktan sonra hello deneme aşağıdakine benzer görünmelidir***</span><span class="sxs-lookup"><span data-stu-id="532ac-291">
***After running, hello experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="532ac-292">5. Adım: Yeni otomobil fiyatlarını tahmin etme</span><span class="sxs-lookup"><span data-stu-id="532ac-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="532ac-293">Biz verilerimizi yüzde 75'ini kullanarak hello modeli eğittiğimize göre biz kullanabileceği tooscore hello diğer yüzde 25'i hello veri toosee ne kadar iyi verilerimizin.</span><span class="sxs-lookup"><span data-stu-id="532ac-293">Now that we've trained hello model using 75 percent of our data, we can use it tooscore hello other 25 percent of hello data toosee how well our model functions.</span></span>

1. <span data-ttu-id="532ac-294">Bulma ve hello sürükleyin [Score Model] [ score-model] modülü toohello deneme tuvaline.</span><span class="sxs-lookup"><span data-stu-id="532ac-294">Find and drag hello [Score Model][score-model] module toohello experiment canvas.</span></span> <span data-ttu-id="532ac-295">Merhaba Hello çıkışına bağlayın [Train Model] [ train-model] sol giriş bağlantı noktası modülü toohello [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="532ac-295">Connect hello output of hello [Train Model][train-model] module toohello left input port of [Score Model][score-model].</span></span> <span data-ttu-id="532ac-296">Merhaba test etme verileri çıkışına (sağ bağlantı noktası) hello bağlanmak [bölünmüş veri] [ split] modülü toohello sağ giriş bağlantı noktası [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="532ac-296">Connect hello test data output (right port) of hello [Split Data][split] module toohello right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="532ac-297">!["Train Model" ve "Böl verileri" Hello "Score Model" modülü tooboth hello modülleri Bağlan][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-297">![Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="532ac-298">***"Train Model" ve "Böl verileri" Hello "Score Model" modülü tooboth hello modülleri Bağlan***</span><span class="sxs-lookup"><span data-stu-id="532ac-298">***Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="532ac-299">Merhaba denemeyi çalıştırın ve hello hello çıktısını görüntüleyin [Score Model] [ score-model] Modülü (Merhaba çıkış bağlantı noktasına tıklayın [Score Model] [ score-model] ve seçin **Görselleştirmek**).</span><span class="sxs-lookup"><span data-stu-id="532ac-299">Run hello experiment and view hello output from hello [Score Model][score-model] module (click hello output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="532ac-300">Fiyat için tahmin edilen değerler hello ve hello test verileri bilinen değerleri hello Hello çıkış gösterir.</span><span class="sxs-lookup"><span data-stu-id="532ac-300">hello output shows hello predicted values for price and hello known values from hello test data.</span></span>  

    <span data-ttu-id="532ac-301">![Çıktı hello "Score Model" modülü][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="532ac-301">![Output of hello "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="532ac-302">***Çıktı hello "Score Model" modülü***</span><span class="sxs-lookup"><span data-stu-id="532ac-302">***Output of hello "Score Model" module***</span></span>

3. <span data-ttu-id="532ac-303">Son olarak, hello sonuçları hello kalitesini sınayın.</span><span class="sxs-lookup"><span data-stu-id="532ac-303">Finally, we test hello quality of hello results.</span></span> <span data-ttu-id="532ac-304">Seçin ve hello sürükleyin [Evaluate Model] [ evaluate-model] modülü toohello tuvale denemek ve hello hello çıkışına bağlayın [Score Model] [ score-model] girişi sol modülü toohello [Evaluate Model][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="532ac-304">Select and drag hello [Evaluate Model][evaluate-model] module toohello experiment canvas, and connect hello output of hello [Score Model][score-model] module toohello left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="532ac-305">Merhaba üzerinde iki giriş bağlantı noktaları olduğundan [Evaluate Model] [ evaluate-model] modülü kullanılan toocompare iki modeli yan yana olabileceğinden.</span><span class="sxs-lookup"><span data-stu-id="532ac-305">There are two input ports on hello [Evaluate Model][evaluate-model] module because it can be used toocompare two models side by side.</span></span> <span data-ttu-id="532ac-306">Daha sonra başka bir algoritma toohello deneme ekleyin ve kullanmak [Evaluate Model] [ evaluate-model] toosee hangisinin daha iyi sonuçlar verir.</span><span class="sxs-lookup"><span data-stu-id="532ac-306">Later, you can add another algorithm toohello experiment and use [Evaluate Model][evaluate-model] toosee which one gives better results.</span></span>

4. <span data-ttu-id="532ac-307">Merhaba denemeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="532ac-307">Run hello experiment.</span></span>

<span data-ttu-id="532ac-308">Merhaba tooview hello çıktısını [Evaluate Model] [ evaluate-model] modül hello çıkış bağlantı noktasına tıklayın ve ardından **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="532ac-308">tooview hello output from hello [Evaluate Model][evaluate-model] module, click hello output port, and then select **Visualize**.</span></span>

<span data-ttu-id="532ac-309">![Merhaba deneme değerlendirme sonuçları][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="532ac-309">![Evaluation results for hello experiment][evaluation-results]
</span></span><br/><span data-ttu-id="532ac-310">
***Merhaba deneme değerlendirme sonuçları***</span><span class="sxs-lookup"><span data-stu-id="532ac-310">
***Evaluation results for hello experiment***</span></span>

<span data-ttu-id="532ac-311">modelimiz için istatistikleri aşağıdaki hello gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="532ac-311">hello following statistics are shown for our model:</span></span>

- <span data-ttu-id="532ac-312">**Mutlak hata anlamına** (MAE): Merhaba mutlak hataların ortalaması (bir *hata* hello arasındaki farktır hello tahmin değeri ve hello gerçek değer).</span><span class="sxs-lookup"><span data-stu-id="532ac-312">**Mean Absolute Error** (MAE): hello average of absolute errors (an *error* is hello difference between hello predicted value and hello actual value).</span></span>
- <span data-ttu-id="532ac-313">**Kök ortalama karesi alınmış hata** (RMSE): hello karekökünü hello hello test veri kümesinde yapılan tahminlerin karesi alınmış hataların ortalaması.</span><span class="sxs-lookup"><span data-stu-id="532ac-313">**Root Mean Squared Error** (RMSE): hello square root of hello average of squared errors of predictions made on hello test dataset.</span></span>
- <span data-ttu-id="532ac-314">**Göreli mutlak hata**: Merhaba gerçek değerler ve hello tüm gerçek değerlerin ortalaması arasındaki mutlak hataların göreli toohello mutlak fark ortalaması.</span><span class="sxs-lookup"><span data-stu-id="532ac-314">**Relative Absolute Error**: hello average of absolute errors relative toohello absolute difference between actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="532ac-315">**Göreli karesi alınmış hata**: karesi göreli toohello hello Ortalama kare hello gerçek değerler ve tüm gerçek değerlerin ortalaması hello arasındaki fark.</span><span class="sxs-lookup"><span data-stu-id="532ac-315">**Relative Squared Error**: hello average of squared errors relative toohello squared difference between hello actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="532ac-316">**Katsayısı**: olarak da bilinen hello **R karesi alınmış değer**, bir model hello verileri ne kadar iyi uyumlu olduğunu gösteren istatistik ölçümleridir budur.</span><span class="sxs-lookup"><span data-stu-id="532ac-316">**Coefficient of Determination**: Also known as hello **R squared value**, this is a statistical metric indicating how well a model fits hello data.</span></span>

<span data-ttu-id="532ac-317">Her hello hata istatistikleri, daha küçük iyidir.</span><span class="sxs-lookup"><span data-stu-id="532ac-317">For each of hello error statistics, smaller is better.</span></span> <span data-ttu-id="532ac-318">Daha küçük bir değer hello tahminleri hello gerçek değerler daha yakından eşleştiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="532ac-318">A smaller value indicates that hello predictions more closely match hello actual values.</span></span> <span data-ttu-id="532ac-319">İçin **Coefficient of Determination**, hello yakın değeri tooone (1.0) hello daha iyi hello tahminleri'dır.</span><span class="sxs-lookup"><span data-stu-id="532ac-319">For **Coefficient of Determination**, hello closer its value is tooone (1.0), hello better hello predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="532ac-320">Son deneme</span><span class="sxs-lookup"><span data-stu-id="532ac-320">Final experiment</span></span>

<span data-ttu-id="532ac-321">Merhaba son deneme aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="532ac-321">hello final experiment should look something like this:</span></span>

<span data-ttu-id="532ac-322">![Merhaba son deneme][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="532ac-322">![hello final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="532ac-323">
***Merhaba son deneme***</span><span class="sxs-lookup"><span data-stu-id="532ac-323">
***hello final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="532ac-324">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="532ac-324">Next steps</span></span>

<span data-ttu-id="532ac-325">Merhaba ilk makine öğrenimi öğreticinizi tamamladığınıza ve denemenizi sahip olduğunuza tooimprove hello modeli devam et ve Tahmine dayalı web hizmeti olarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="532ac-325">Now that you've completed hello first machine learning tutorial and have your experiment set up, you can continue tooimprove hello model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="532ac-326">**Tootry tooimprove hello modeli yinelemek** -Örneğin, tahmin kullandığınız hello özelliklerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532ac-326">**Iterate tootry tooimprove hello model** - For example, you can change hello features you use in your prediction.</span></span> <span data-ttu-id="532ac-327">Veya hello hello özelliklerini değiştirebilirsiniz [doğrusal regresyon] [ linear-regression] algoritması veya tamamen farklı bir algoritma deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532ac-327">Or you can modify hello properties of hello [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="532ac-328">Hatta birden çok makine öğrenimi algoritmaları tooyour denemesinin aynı anda eklemek ve ikisi hello kullanarak karşılaştırın [Evaluate Model] [ evaluate-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="532ac-328">You can even add multiple machine learning algorithms tooyour experiment at one time and compare two of them by using hello [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="532ac-329">Bir örneği nasıl toocompare tek bir deneme birden çok modellerinde görmek için [karşılaştırmak Regresör](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) hello içinde [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="532ac-329">For an example of how toocompare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="532ac-330">toocopy kullanım hello denemenizi herhangi bir yinelemesini **SAVE AS** hello altındaki hello sayfasının düğmesini.</span><span class="sxs-lookup"><span data-stu-id="532ac-330">toocopy any iteration of your experiment, use hello **SAVE AS** button at hello bottom of hello page.</span></span> <span data-ttu-id="532ac-331">Tıklayarak denemenizin tüm hello yinelemelerini görebilirsiniz **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="532ac-331">You can see all hello iterations of your experiment by clicking **VIEW RUN HISTORY** at hello bottom of hello page.</span></span> <span data-ttu-id="532ac-332">Daha fazla ayrıntı için bkz. [Azure Machine Learning Studio'da deneme yinelemelerini yönetme][runhistory].</span><span class="sxs-lookup"><span data-stu-id="532ac-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="532ac-333">**Merhaba modeli tahmine dayalı web hizmeti olarak dağıtma** - modelinizi ile memnun kaldığınızda yeni verileri kullanarak bir web hizmeti toobe toopredict otomobil fiyatlarını kullanılan olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="532ac-333">**Deploy hello model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service toobe used toopredict automobile prices by using new data.</span></span> <span data-ttu-id="532ac-334">Daha fazla ayrıntı için bkz. [Bir Azure Machine Learning web hizmetini dağıtma][publish].</span><span class="sxs-lookup"><span data-stu-id="532ac-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="532ac-335">Daha fazla toolearn istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="532ac-335">Want toolearn more?</span></span> <span data-ttu-id="532ac-336">Oluşturma, eğitim, Puanlama ve model dağıtma hello işleminin daha kapsamlı ve Ayrıntılı Kılavuzu için bkz: [Azure Machine Learning kullanarak Tahmine dayalı bir çözüm geliştirmek][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="532ac-336">For a more extensive and detailed walkthrough of hello process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
