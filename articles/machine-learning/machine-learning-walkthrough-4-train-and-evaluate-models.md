---
title: "4. adım: Eğitmek ve Tahmine dayalı analitik modelleri değerlendirme | Microsoft Docs"
description: "4. adımını geliştirme Tahmine dayalı bir çözüm izlenecek yol: eğitme, Puanlama ve Azure Machine Learning Studio'da birden fazla modeli değerlendirin."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 58d46dd1464ec0a3fc9639f78d4429e0e778c2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-the-predictive-analytic-models"></a><span data-ttu-id="cc0db-103">Kılavuz Adımı 4: Öngörücü analiz modelleri hakkında eğitim ve değerlendirme</span><span class="sxs-lookup"><span data-stu-id="cc0db-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span></span>
<span data-ttu-id="cc0db-104">Bu konu, izlenecek dördüncü adımı içerir [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="cc0db-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="cc0db-105">Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc0db-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="cc0db-106">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="cc0db-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="cc0db-107">Yeni bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc0db-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="cc0db-108">**Modelleri eğitme ve değerlendirme**</span><span class="sxs-lookup"><span data-stu-id="cc0db-108">**Train and evaluate the models**</span></span>
5. [<span data-ttu-id="cc0db-109">Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="cc0db-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="cc0db-110">Web hizmetine erişim</span><span class="sxs-lookup"><span data-stu-id="cc0db-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="cc0db-111">Machine learning modellerini oluşturmak için Azure Machine Learning Studio'da kullanmanın avantajlarından biri tek bir deneme zamanında birden fazla türde bir model deneyin ve sonuçları karşılaştırmak için yeteneğidir.</span><span class="sxs-lookup"><span data-stu-id="cc0db-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span></span> <span data-ttu-id="cc0db-112">Bu tür bir deney sorununuzu için en iyi çözüm bulmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cc0db-112">This type of experimentation helps you find the best solution for your problem.</span></span>

<span data-ttu-id="cc0db-113">Bu kılavuzda geliştirme yapıyorsanız denemesinde biz modelleri iki farklı türde oluşturacak ve bizim son deneme şu kullanmak istediğiniz algoritmayı karar vermek için Puanlama sonuçlarını karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="cc0db-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span></span>  

<span data-ttu-id="cc0db-114">Biz arasından seçim çeşitli modellerin vardır.</span><span class="sxs-lookup"><span data-stu-id="cc0db-114">There are various models we could choose from.</span></span> <span data-ttu-id="cc0db-115">Kullanılabilir modelleri görmek için genişletin **Machine Learning** modül paletindeki düğümünü genişletin ve ardından **modeli Başlat** ve altındaki düğümleri.</span><span class="sxs-lookup"><span data-stu-id="cc0db-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span></span> <span data-ttu-id="cc0db-116">Bu deneme amaçları doğrultusunda, biz seçersiniz [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] (SVM) ve [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modüller.</span><span class="sxs-lookup"><span data-stu-id="cc0db-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="cc0db-117">Çözmeye çalıştığınız belirli sorun Machine Learning algoritmayı en iyi uyan karar vermeyle ilgili Yardım almak için bkz: [için Microsoft Azure Machine Learning algoritmaları seçme](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="cc0db-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-the-models"></a><span data-ttu-id="cc0db-118">Modelleri eğitme</span><span class="sxs-lookup"><span data-stu-id="cc0db-118">Train the models</span></span>

<span data-ttu-id="cc0db-119">Her ikisi de ekleyeceğiz [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modülü ve [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] bu deneme modülünde.</span><span class="sxs-lookup"><span data-stu-id="cc0db-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="cc0db-120">İki sınıflı artırılmış karar ağacı</span><span class="sxs-lookup"><span data-stu-id="cc0db-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="cc0db-121">İlk olarak, şimdi artırılmış karar ağacı modelini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cc0db-121">First, let's set up the boosted decision tree model.</span></span>

1. <span data-ttu-id="cc0db-122">Bul [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modül paletindeki modülünü tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="cc0db-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="cc0db-123">Bul [Train Model] [ train-model] modülünü tuvale sürükleyin ve çıkışına bağlayın [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] Modül sol giriş bağlantı noktası [Train Model] [ train-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="cc0db-124">[İki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modülü genel model başlatır ve [modeli eğitmek] [ train-model] eğitmek için eğitim verileri kullanır Model.</span><span class="sxs-lookup"><span data-stu-id="cc0db-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span></span> 

3. <span data-ttu-id="cc0db-125">Sol sol çıkışına bağlayın [R betiği yürütün] [ execute-r-script] modülü sağ giriş bağlantı noktası [Train Model] [ train-model] (karar içinde Modülü [Adım 3](machine-learning-walkthrough-3-create-new-experiment.md) bölünmüş veri modülünün eğitim sol taraftan gelen veriler kullanmak için bu kılavuzun).</span><span class="sxs-lookup"><span data-stu-id="cc0db-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="cc0db-126">İki girişleri ve çıkışları birini gerekmez [R betiği yürütün] [ execute-r-script] biz bunları eklenmemiş bırakabilirsiniz, bu nedenle bu deneme için modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="cc0db-127">Bu bölümü denemeyi şimdi şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="cc0db-127">This portion of the experiment now looks something like this:</span></span>  

![Bir model eğitimi][1]

<span data-ttu-id="cc0db-129">Bildirmek ihtiyacımız artık [Train Model] [ train-model] modülü modelin kredi riski değer tahmin etmek istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="cc0db-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span></span>

1. <span data-ttu-id="cc0db-130">Seçin [Train Model] [ train-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-130">Select the [Train Model][train-model] module.</span></span> <span data-ttu-id="cc0db-131">İçinde **özellikleri** bölmesinde tıklatın **başlatma Sütun seçiciyi**.</span><span class="sxs-lookup"><span data-stu-id="cc0db-131">In the **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="cc0db-132">İçinde **tek bir sütun seçin** iletişim kutusunda, türü "Kredi riski" altındaki arama alanında **kullanılabilir sütunlar**, aşağıda "Kredi riski"'ı seçin ve sağ ok düğmesine tıklayın ( **>** ) "Kredi riski" taşımak için **seçili sütun**.</span><span class="sxs-lookup"><span data-stu-id="cc0db-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span></span> 

    ![Train Model modülü için kredi riski sütun seçin][0]

3. <span data-ttu-id="cc0db-134">Tıklatın **Tamam** onay işareti.</span><span class="sxs-lookup"><span data-stu-id="cc0db-134">Click the **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="cc0db-135">Çift Sınıflı Destek Vektör Makinesi</span><span class="sxs-lookup"><span data-stu-id="cc0db-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="cc0db-136">Ardından, SVM modelini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cc0db-136">Next, we set up the SVM model.</span></span>  

<span data-ttu-id="cc0db-137">Öncelikle, SVM hakkında biraz açıklama.</span><span class="sxs-lookup"><span data-stu-id="cc0db-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="cc0db-138">Artırılmış karar ağaçları iyi herhangi bir türde özellikleri ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="cc0db-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="cc0db-139">Doğrusal bir sınıflandırıcı SVM modülü oluşturur olduğundan, tüm sayısal özellikleri aynı ölçeğini varsa ancak ürettiği modeli en iyi test hata var.</span><span class="sxs-lookup"><span data-stu-id="cc0db-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span></span> <span data-ttu-id="cc0db-140">Bir "Tanh" dönüştürmesi kullanırız tüm sayısal özellikleri aynı ölçek dönüştürmek için (ile [normalleştirin veri] [ normalize-data] Modülü).</span><span class="sxs-lookup"><span data-stu-id="cc0db-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="cc0db-141">Bu bizim numaraları [0,1] aralığına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="cc0db-141">This transforms our numbers into the [0,1] range.</span></span> <span data-ttu-id="cc0db-142">Biz dize özellikleri el ile dönüştürme gerek kalmaması SVM modülü kategorik özellikleri ve ardından ikili 0/1 özellikleri, dize özellikleri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="cc0db-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span></span> <span data-ttu-id="cc0db-143">Ayrıca, kredi riski sütun (sütun 21) dönüştürmek istemediğiniz - sayısal ancak tek başına bırakmak ihtiyacımız şekilde tahmin etmek için model eğitim değerdir.</span><span class="sxs-lookup"><span data-stu-id="cc0db-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span></span>  

<span data-ttu-id="cc0db-144">SVM modeli kurmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="cc0db-144">To set up the SVM model, do the following:</span></span>

1. <span data-ttu-id="cc0db-145">Bul [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] modül paletindeki modülünü tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="cc0db-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="cc0db-146">Sağ [Train Model] [ train-model] modülü, select **kopya**, seçin ve tuvale sağ tıklatın **Yapıştır**.</span><span class="sxs-lookup"><span data-stu-id="cc0db-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span></span> <span data-ttu-id="cc0db-147">Kopyasını [Train Model] [ train-model] modül aynı sütun seçimi özgün olarak sahiptir.</span><span class="sxs-lookup"><span data-stu-id="cc0db-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span></span>

3. <span data-ttu-id="cc0db-148">Çıkışına bağlayın [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] modülü sol giriş bağlantı noktası saniye [Train Model] [ train-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="cc0db-149">Bul [normalleştirin veri] [ normalize-data] modülünü tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="cc0db-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span></span>

5. <span data-ttu-id="cc0db-150">Sol sol çıkışına bağlayın [R betiği yürütün] [ execute-r-script] giriş (bildirim için birden fazla modülü modülünün çıkış bağlantı noktasına bağlı olduğunu) Bu modülün modül.</span><span class="sxs-lookup"><span data-stu-id="cc0db-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span></span>

6. <span data-ttu-id="cc0db-151">Sol çıkış bağlantı noktasına bağlanmak [normalleştirin veri] [ normalize-data] modülü sağ giriş bağlantı noktası saniye [Train Model] [ train-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span></span>

<span data-ttu-id="cc0db-152">Bu bizim deneme kısmı bu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="cc0db-152">This portion of our experiment should now look something like this:</span></span>  

![Eğitim ikinci modeli][2]  

<span data-ttu-id="cc0db-154">Şimdi yapılandırmak [normalleştirin veri] [ normalize-data] Modülü:</span><span class="sxs-lookup"><span data-stu-id="cc0db-154">Now configure the [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="cc0db-155">Seçmek için tıklatın [normalleştirin veri] [ normalize-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-155">Click to select the [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="cc0db-156">İçinde **özellikleri** bölmesinde, **Tanh** için **dönüştürme yöntemi** parametresi.</span><span class="sxs-lookup"><span data-stu-id="cc0db-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span></span>

2. <span data-ttu-id="cc0db-157">Tıklatın **başlatma Sütun seçiciyi**, "Hiçbir sütun" seçin **şununla Başla**seçin **INCLUDE** ilk açılır menüde seçin **sütun türü** ikinci açılır ve seçin **sayısal** üçüncü açılır.</span><span class="sxs-lookup"><span data-stu-id="cc0db-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span></span> <span data-ttu-id="cc0db-158">Bu, tüm sayısal sütunlar (ve yalnızca sayısal) dönüştürüldüğünden belirtir.</span><span class="sxs-lookup"><span data-stu-id="cc0db-158">This specifies that all the numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="cc0db-159">Bu satır sağındaki artı (+) tıklayın - bu bırakmalar satırının oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cc0db-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="cc0db-160">Seçin **hariç** ilk açılır menüde seçin **sütun adları** ikinci açılır ve "metin alanında risk kredi" girin.</span><span class="sxs-lookup"><span data-stu-id="cc0db-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span></span> <span data-ttu-id="cc0db-161">Bu kredi riski sütun yoksayılmalıdır belirtir (Bu sütunu sayısal olduğundan ve biz bunu siz bıraksanız dönüştürülmesi böylece bunun ihtiyacımız).</span><span class="sxs-lookup"><span data-stu-id="cc0db-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="cc0db-162">Tıklatın **Tamam** onay işareti.</span><span class="sxs-lookup"><span data-stu-id="cc0db-162">Click the **OK** check mark.</span></span>  

    ![Veri normalleştirin modülü sütunlarını seçin][5]

<span data-ttu-id="cc0db-164">[Normalleştirin veri] [ normalize-data] modülü kredi riski sütun dışında tüm sayısal sütunlarda Tanh dönüştürme gerçekleştirmek için şimdi ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="cc0db-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span></span>  

## <a name="score-and-evaluate-the-models"></a><span data-ttu-id="cc0db-165">Puanlama ve modelleri değerlendir</span><span class="sxs-lookup"><span data-stu-id="cc0db-165">Score and evaluate the models</span></span>

<span data-ttu-id="cc0db-166">Tarafından ayrıldı çıkışı test verilerinin kullanırız [bölünmüş veri] [ split] bizim eğitilmiş modeller Puanlama modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span></span> <span data-ttu-id="cc0db-167">Biz, ardından, daha iyi sonuçlar oluşturulan görmek için iki model sonuçlarını karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc0db-167">We can then compare the results of the two models to see which generated better results.</span></span>  

### <a name="add-the-score-model-modules"></a><span data-ttu-id="cc0db-168">Score Model modülleri ekleme</span><span class="sxs-lookup"><span data-stu-id="cc0db-168">Add the Score Model modules</span></span>

1. <span data-ttu-id="cc0db-169">Bul [Score Model] [ score-model] modülünü tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="cc0db-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="cc0db-170">Bağlantı [Train Model] [ train-model] bağlı Modülü [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modülü sol giriş bağlantı noktası [Score Model] [ score-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="cc0db-171">Sağa bağlanmak [R betiği yürütün] [ execute-r-script] Modülü (test verilerimizi) sağ giriş bağlantı noktası [Score Model] [ score-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span></span>

    ![Score Model modülünün bağlı][6]
   
   <span data-ttu-id="cc0db-173">[Score Model] [ score-model] modülü artık test verilerinin kredi bilgileri alın, modeli aracılığıyla çalıştırmak ve modeli oluşturur gerçek kredi riski sütuna tahminleri Karşılaştır verileri test etme.</span><span class="sxs-lookup"><span data-stu-id="cc0db-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span></span>

4. <span data-ttu-id="cc0db-174">Kopyalama ve yapıştırma [Score Model] [ score-model] modülü ikinci bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc0db-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span></span>

5. <span data-ttu-id="cc0db-175">SVM modeli çıkışına bağlayın (diğer bir deyişle, çıkış bağlantı [Train Model] [ train-model] bağlı Modülü [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] Modülü) ikinci giriş noktasına [Score Model] [ score-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="cc0db-176">SVM modeli için eğitim verileri yaptığımız gibi test verileri için aynı dönüştürme yapmak sahibiz.</span><span class="sxs-lookup"><span data-stu-id="cc0db-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span></span> <span data-ttu-id="cc0db-177">Bu nedenle kopyalama ve yapıştırma [normalleştirin veri] [ normalize-data] ikinci bir kopyasını oluşturmak ve sağa bağlanmak için Modülü [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="cc0db-178">İkinci sol çıkışına bağlayın [normalleştirin veri] [ normalize-data] modülü sağ giriş bağlantı noktası saniye [Score Model] [ score-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span></span>

    ![Bağlı her iki Score Model modülleri][7]

### <a name="add-the-evaluate-model-module"></a><span data-ttu-id="cc0db-180">Evaluate Model Modül Ekle</span><span class="sxs-lookup"><span data-stu-id="cc0db-180">Add the Evaluate Model module</span></span>

<span data-ttu-id="cc0db-181">İki Puanlama sonuçları değerlendirin ve bunları karşılaştırmak için kullanırız bir [Evaluate Model] [ evaluate-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="cc0db-182">Bul [Evaluate Model] [ evaluate-model] modülünü tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="cc0db-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="cc0db-183">Çıkış bağlantı noktasına bağlanmak [Score Model] [ score-model] sol giriş bağlantı noktası için artırılmış karar ağacı modeli ile ilişkili Modülü [Evaluate Model] [ evaluate-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="cc0db-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="cc0db-184">Diğer bağlanmak [Score Model] [ score-model] modülü sağ giriş bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="cc0db-184">Connect the other [Score Model][score-model] module to the right input port.</span></span>  

    ![Modeli değerlendirin bağlı Modülü][8]

### <a name="run-the-experiment-and-check-the-results"></a><span data-ttu-id="cc0db-186">Denemeyi çalıştırmak ve sonuçları denetleyin</span><span class="sxs-lookup"><span data-stu-id="cc0db-186">Run the experiment and check the results</span></span>

<span data-ttu-id="cc0db-187">Denemeyi çalıştırmak için tıklatın **çalıştırmak** tuvale aşağıdaki düğmesine.</span><span class="sxs-lookup"><span data-stu-id="cc0db-187">To run the experiment, click the **RUN** button below the canvas.</span></span> <span data-ttu-id="cc0db-188">Birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="cc0db-188">It may take a few minutes.</span></span> <span data-ttu-id="cc0db-189">Dönen göstergesi her modül çalışıp çalışmadığını ve ardından modülünün tamamladığında yeşil bir onay işareti gösterir gösterir.</span><span class="sxs-lookup"><span data-stu-id="cc0db-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span></span> <span data-ttu-id="cc0db-190">Tüm modülleri bir onay işareti varsa, deneme çalışması sona erdi.</span><span class="sxs-lookup"><span data-stu-id="cc0db-190">When all the modules have a check mark, the experiment has finished running.</span></span>

<span data-ttu-id="cc0db-191">Denemeyi bu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="cc0db-191">The experiment should now look something like this:</span></span>  

![Her iki modeli değerlendirme][3]

<span data-ttu-id="cc0db-193">Sonuçları denetlemek için çıkış bağlantı noktasına tıklayın [Evaluate Model] [ evaluate-model] modülü ve select **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="cc0db-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="cc0db-194">[Evaluate Model] [ evaluate-model] modülü eğriler ve iki puanlanmış modelleri sonuçları karşılaştırmak izin ölçümleri çifti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cc0db-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span></span> <span data-ttu-id="cc0db-195">Alıcı işleci karakteristiğini (ROC) Eğriler, duyarlık/geri çağırma Eğriler ya da yükseltme Eğriler olarak sonuçlarını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc0db-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="cc0db-196">Görüntülenen ek verileri karışıklığı matrisi, eğri (AUC) ve diğer ölçümleri alanında toplu değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="cc0db-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span></span> <span data-ttu-id="cc0db-197">Kaydırıcıyı sola veya sağa hareket ettirerek eşik değerini değiştirin ve ölçümleri kümesi nasıl etkilediği bakın.</span><span class="sxs-lookup"><span data-stu-id="cc0db-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span></span>  

<span data-ttu-id="cc0db-198">Grafik sağında tıklatın **veri kümesi belirtmek** veya **karşılaştırmak için veri kümesi belirtmek** ilişkili eğri vurgulayın ve aşağıdaki ilişkili ölçümleri görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="cc0db-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span></span> <span data-ttu-id="cc0db-199">Eğriler göstergede "veri kümesi belirtmek" sol giriş bağlantı noktasına karşılık gelen [Evaluate Model] [ evaluate-model] modül - Örneğimizde, artırılmış karar ağacı modeli budur.</span><span class="sxs-lookup"><span data-stu-id="cc0db-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span></span> <span data-ttu-id="cc0db-200">"Karşılaştırmak için veri kümesi belirtmek" sağ giriş bağlantı noktasını - bu örnekte SVM modeli karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="cc0db-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span></span> <span data-ttu-id="cc0db-201">Bu etiketler birine tıkladığınızda, bu model için eğri vurgulanır ve aşağıdaki grafikte gösterildiği gibi ilgili ölçümleri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cc0db-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span></span>  

![Modelleri için ROC Eğriler][4]

<span data-ttu-id="cc0db-203">Bu değerleri inceleyerek, hangi model Aradığınız sonuçları vermiş, en yakın olan karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc0db-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span></span> <span data-ttu-id="cc0db-204">Geri dönün ve farklı modellerde parametre değerlerini değiştirerek denemenizi üzerinde yineleme.</span><span class="sxs-lookup"><span data-stu-id="cc0db-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span></span> 

<span data-ttu-id="cc0db-205">Bilim bu sonuçları yorumlayarak ve model performans ayarlama resim ise bu kılavuzun kapsamı dışındadır.</span><span class="sxs-lookup"><span data-stu-id="cc0db-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span></span> <span data-ttu-id="cc0db-206">Ek Yardım için aşağıdaki makaleler okuyun:</span><span class="sxs-lookup"><span data-stu-id="cc0db-206">For additional help, you might read the following articles:</span></span>
- [<span data-ttu-id="cc0db-207">Azure Machine Learning modeli performansını değerlendirmek nasıl</span><span class="sxs-lookup"><span data-stu-id="cc0db-207">How to evaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="cc0db-208">Azure Machine Learning algoritmaları en iyi duruma getirmek için parametreleri seçin</span><span class="sxs-lookup"><span data-stu-id="cc0db-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="cc0db-209">Azure Machine Learning modeli sonuçlarında yorumlama</span><span class="sxs-lookup"><span data-stu-id="cc0db-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="cc0db-210">Denemeyi bu yineleme kaydını her çalıştırdığınızda çalıştırma geçmişi korunur.</span><span class="sxs-lookup"><span data-stu-id="cc0db-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span></span> <span data-ttu-id="cc0db-211">Bu yineleme görüntülemek ve tıklayarak herhangi biri, geri dönüp **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** tuvale aşağıda.</span><span class="sxs-lookup"><span data-stu-id="cc0db-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span></span> <span data-ttu-id="cc0db-212">Tıklatabilirsiniz **önceki Çalıştır** içinde **özellikleri** hemen bir önceki yineleme dönmek için bölmeniz Aç.</span><span class="sxs-lookup"><span data-stu-id="cc0db-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span></span>
> 
> <span data-ttu-id="cc0db-213">Tıklayarak denemenizin herhangi bir yinelemesini kopyasını yapabilirsiniz **SAVE AS** tuvale aşağıda.</span><span class="sxs-lookup"><span data-stu-id="cc0db-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span></span> 
> <span data-ttu-id="cc0db-214">Deneme kullanmak **Özet** ve **açıklama** özellikleri, deneme yinelemelerini çalıştınız kaydını tutun.</span><span class="sxs-lookup"><span data-stu-id="cc0db-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="cc0db-215">Daha fazla ayrıntı için bkz: [Azure Machine Learning Studio'da deneme yinelemelerini yönetme](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="cc0db-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="cc0db-216">**Sonraki: [web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="cc0db-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
