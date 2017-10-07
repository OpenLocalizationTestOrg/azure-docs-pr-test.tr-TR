---
title: "4. adım: Eğitmek ve hello Tahmine dayalı analitik modelleri değerlendirme | Microsoft Docs"
description: "4. adımını hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: eğitme, Puanlama ve Azure Machine Learning Studio'da birden fazla modeli değerlendirin."
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
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="ae6ba-103">Gözden geçirme adım 4: Eğitmek ve hello Tahmine dayalı analitik modelleri değerlendir</span><span class="sxs-lookup"><span data-stu-id="ae6ba-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="ae6ba-104">Bu konu, hello izlenecek hello dördüncü adımı içerir [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="ae6ba-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="ae6ba-105">Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ae6ba-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="ae6ba-106">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="ae6ba-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="ae6ba-107">Yeni bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="ae6ba-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="ae6ba-108">**Eğitmek ve hello modelleri değerlendir**</span><span class="sxs-lookup"><span data-stu-id="ae6ba-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="ae6ba-109">Merhaba Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="ae6ba-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="ae6ba-110">Merhaba Web hizmetine erişim</span><span class="sxs-lookup"><span data-stu-id="ae6ba-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="ae6ba-111">Biri makine öğrenimi modellerini oluşturmak için Azure Machine Learning Studio'da kullanmanın yararları hello hello özelliği tootry birden fazla türde bir model tek bir deneme zamanında ve hello sonucu karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="ae6ba-112">Bu tür bir deney sorununuzu için hello en iyi çözüm bulmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="ae6ba-113">Biz bu kılavuzda geliştirmekte hello denemesinde, biz modelleri iki farklı türde oluşturacak ve sonra bunların Puanlama sonuçları toodecide algoritmayı karşılaştırmak bizim son deneme toouse istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="ae6ba-114">Biz arasından seçim çeşitli modellerin vardır.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-114">There are various models we could choose from.</span></span> <span data-ttu-id="ae6ba-115">toosee hello modelleri kullanılabilir genişletin hello **Machine Learning** hello modül paletindeki düğümünü genişletin ve ardından **modeli Başlat** ve hello düğümü altındaki.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="ae6ba-116">Bu deneme Hello amaçları doğrultusunda, biz hello seçersiniz [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] (SVM) ve hello [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modüller.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="ae6ba-117">Machine Learning algoritmayı en iyi karar tooget Yardım uygun hello belirli sorun toosolve çalıştığınız için bkz: [nasıl Microsoft Azure Machine Learning için toochoose algoritmaları](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="ae6ba-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="ae6ba-118">Merhaba modelleri eğitme</span><span class="sxs-lookup"><span data-stu-id="ae6ba-118">Train hello models</span></span>

<span data-ttu-id="ae6ba-119">Her iki hello ekleyeceğiz [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modülü ve [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] bu modülü denemeler yapın.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="ae6ba-120">İki sınıflı artırılmış karar ağacı</span><span class="sxs-lookup"><span data-stu-id="ae6ba-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="ae6ba-121">İlk olarak, şirketinizdeki boosted hello karar ağacı modelini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="ae6ba-122">Hello bulur [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] hello modül paleti modülünde hello tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="ae6ba-123">Hello bulur [Train Model] [ train-model] modülü, hello tuvale sürükleyin ve ardından hello hello çıkışına bağlayın [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree]modülü toohello sol giriş bağlantı noktası hello [Train Model] [ train-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="ae6ba-124">Merhaba [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modülü hello genel modeli, başlatır ve [Train Model] [ train-model] eğitim verileri kullanır tootrain hello modeli.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="ae6ba-125">Merhaba sol hello sol çıkışına bağlayın [R betiği yürütün] [ execute-r-script] modülü toohello sağ giriş bağlantı noktası hello [Train Model] [ train-model] (biz Modülü içinde karar [adım 3](machine-learning-walkthrough-3-create-new-experiment.md) yan hello bölünmüş veri modülünün eğitim sol hello gelen bu izlenecek yol toouse hello veri).</span><span class="sxs-lookup"><span data-stu-id="ae6ba-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ae6ba-126">İki hello girdi ve hello hello çıkışları biri gerekmez [R betiği yürütün] [ execute-r-script] biz bunları eklenmemiş bırakabilirsiniz, bu nedenle bu deneme için modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="ae6ba-127">Bu kısmı hello denemeyi şimdi şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="ae6ba-127">This portion of hello experiment now looks something like this:</span></span>  

![Bir model eğitimi][1]

<span data-ttu-id="ae6ba-129">Tootell hello ihtiyacımız artık [Train Model] [ train-model] modülü hello model toopredict hello kredi riski değeri istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="ae6ba-130">Select hello [Train Model] [ train-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="ae6ba-131">Merhaba, **özellikleri** bölmesinde tıklatın **başlatma Sütun seçiciyi**.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="ae6ba-132">Merhaba, **tek bir sütun seçin** iletişim kutusunda, türü "Kredi riski" Merhaba arama alanında altında **kullanılabilir sütunlar**, aşağıda "Kredi riski"'ı seçin ve hello sağ ok düğmesine tıklayın ( **>** ) toomove "çok kredi riski"**seçili sütun**.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![Merhaba Train Model modülü için Hello kredi riski sütun seçin][0]

3. <span data-ttu-id="ae6ba-134">Merhaba tıklatın **Tamam** onay işareti.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="ae6ba-135">Çift Sınıflı Destek Vektör Makinesi</span><span class="sxs-lookup"><span data-stu-id="ae6ba-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="ae6ba-136">Ardından, hello SVM modelini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="ae6ba-137">Öncelikle, SVM hakkında biraz açıklama.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="ae6ba-138">Artırılmış karar ağaçları iyi herhangi bir türde özellikleri ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="ae6ba-139">Doğrusal bir sınıflandırıcı Hello SVM modülü oluşturur olduğundan, tüm sayısal özellikleri hello olduğunda ancak ürettiği hello modeli hello en iyi test hatalı aynı ölçek.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="ae6ba-140">tüm sayısal tooconvert özellikleri toohello aynı ölçeklendirme, bir "Tanh" dönüştürmesi kullanıyoruz (Merhaba ile [normalleştirin veri] [ normalize-data] Modülü).</span><span class="sxs-lookup"><span data-stu-id="ae6ba-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="ae6ba-141">Bu bizim numaraları hello [0,1] aralığına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="ae6ba-142">dize özellikleri toocategorical Özellikler'i ve ardından toobinary 0/1 özellikler Hello SVM modülü dönüştürür, biz olmayan şekilde toomanually dize özellikleri dönüştürme.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="ae6ba-143">Ayrıca, biz tootransform hello kredi riski sütun (sütun 21) istemediğiniz - sayısal ancak bu eğitim hello değeri hello modeli toopredict tooleave ihtiyacımız şekilde, tek başına.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="ae6ba-144">Merhaba SVM modeli yukarı tooset hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="ae6ba-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="ae6ba-145">Hello bulur [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] hello modül paleti modülünde hello tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="ae6ba-146">Sağ hello [Train Model] [ train-model] modülü, select **kopyalama**ve ardından hello tuvale sağ tıklatın ve seçin **Yapıştır**.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="ae6ba-147">Merhaba hello kopyasını [Train Model] [ train-model] modülüne sahip hello hello özgün olarak aynı sütun seçimi.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="ae6ba-148">Merhaba Hello çıkışına bağlayın [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] modülü toohello sol giriş bağlantı noktası Merhaba, ikinci [Train Model] [ train-model] Modül.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="ae6ba-149">Hello bulur [normalleştirin veri] [ normalize-data] modülü ve hello tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="ae6ba-150">Merhaba sol hello sol çıkışına bağlayın [R betiği yürütün] [ execute-r-script] modül toohello girişi Bu modülün (bildirim hello çıkış bağlantı noktasına bir modülün başka bir modül'den bağlı toomore olabilir).</span><span class="sxs-lookup"><span data-stu-id="ae6ba-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="ae6ba-151">Merhaba çıkış bağlantı noktasına sol hello bağlanmak [normalleştirin veri] [ normalize-data] modülü toohello sağ giriş bağlantı noktası hello ikinci [Train Model] [ train-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="ae6ba-152">Bu bizim deneme kısmı bu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="ae6ba-152">This portion of our experiment should now look something like this:</span></span>  

![Eğitim hello ikinci modeli][2]  

<span data-ttu-id="ae6ba-154">Şimdi hello yapılandırmak [normalleştirin veri] [ normalize-data] Modülü:</span><span class="sxs-lookup"><span data-stu-id="ae6ba-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="ae6ba-155">Tooselect hello tıklatın [normalleştirin veri] [ normalize-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="ae6ba-156">Merhaba, **özellikleri** bölmesinde, **Tanh** hello için **dönüştürme yöntemi** parametresi.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="ae6ba-157">Tıklatın **başlatma Sütun seçiciyi**, "Hiçbir sütun" seçin **şununla Başla**seçin **INCLUDE** hello ilk açılır menüde seçin **sütun türü**ikinci açılır hello ve seçin **sayısal** içinde hello üçüncü açılır.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="ae6ba-158">Bu, tüm hello sayısal sütunlar (ve yalnızca sayısal) dönüştürüldüğünden belirtir.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="ae6ba-159">Tıklatın artı (+) toohello bu satırın sağ hello - bu bırakmalar satırının oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="ae6ba-160">Seçin **hariç** hello ilk açılır menüde seçin **sütun adları** ikinci açılır hello ve "Merhaba metin alanında risk kredi" girin.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="ae6ba-161">Bu, hello kredi riski sütuna dikkate belirtir (Bu olduğundan bu sütun sayısal ve bunu dönüştürülmüş biz bunu siz bıraksanız toodo ihtiyacımız).</span><span class="sxs-lookup"><span data-stu-id="ae6ba-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="ae6ba-162">Merhaba tıklatın **Tamam** onay işareti.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-162">Click hello **OK** check mark.</span></span>  

    ![Merhaba normalleştirin veri modülü sütunlarını seçin][5]

<span data-ttu-id="ae6ba-164">Merhaba [normalleştirin veri] [ normalize-data] modülüdür şimdi kümesi tooperform hello kredi riski sütun dışında tüm sayısal sütunlarda Tanh dönüştürme.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="ae6ba-165">Puanlama ve hello modelleri değerlendir</span><span class="sxs-lookup"><span data-stu-id="ae6ba-165">Score and evaluate hello models</span></span>

<span data-ttu-id="ae6ba-166">Merhaba tarafından ayrıldı verileri test etme hello kullanırız [bölünmüş veri] [ split] modülü tooscore bizim eğitilmiş modeller.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="ae6ba-167">Biz, ardından daha iyi sonuçlar oluşturulan hello iki modelleri toosee hello sonuçlarını karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="ae6ba-168">Merhaba Score Model modülleri ekleme</span><span class="sxs-lookup"><span data-stu-id="ae6ba-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="ae6ba-169">Hello bulur [Score Model] [ score-model] modülü ve hello tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="ae6ba-170">Merhaba bağlanmak [Train Model] [ train-model] toohello bağlandı Modülü [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modülü toohello sol giriş başlangıç bağlantı noktası [Score Model] [ score-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="ae6ba-171">Merhaba sağ bağlanmak [R betiği yürütün] [ execute-r-script] Modülü (test verilerimizi) toohello sağ giriş bağlantı noktası hello [Score Model] [ score-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![Score Model modülünün bağlı][6]
   
   <span data-ttu-id="ae6ba-173">Merhaba [Score Model] [ score-model] modülü şimdi veri hello modeli aracılığıyla çalıştırmak, test hello hello kredi bilgileri alın ve karşılaştırma hello tahminleri hello modeli oluşturur hello gerçek ile kredi riski verileri test etme hello sütun.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="ae6ba-174">Kopyalama ve yapıştırma hello [Score Model] [ score-model] modülü toocreate ikinci bir kopyası.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="ae6ba-175">Merhaba SVM modeli Hello çıkışına bağlayın (diğer bir deyişle, başlangıç bağlantı noktası hello çıktı [Train Model] [ train-model] toohello bağlandı Modülü [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] Modülü) toohello giriş bağlantı noktası hello ikinci [Score Model] [ score-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="ae6ba-176">Merhaba SVM modeli için aynı dönüşüm toohello test verileri toohello eğitim verilerini yaptığımız gibi hello toodo sahip.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="ae6ba-177">Merhaba şekilde kopyalayıp [normalleştirin veri] [ normalize-data] modülü toocreate ikinci kopya ve toohello sağ bağlamak [R betiği yürütün] [ execute-r-script] modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="ae6ba-178">Merhaba sol hello çıktısını ikinci bağlanmak [normalleştirin veri] [ normalize-data] modülü toohello sağ giriş bağlantı noktası hello ikinci [Score Model] [ score-model] Modül.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![Bağlı her iki Score Model modülleri][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="ae6ba-180">Merhaba Evaluate Model Modül Ekle</span><span class="sxs-lookup"><span data-stu-id="ae6ba-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="ae6ba-181">tooevaluate iki Puanlama sonuçları hello ve bunları karşılaştırır, kullandığımız bir [Evaluate Model] [ evaluate-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="ae6ba-182">Hello bulur [Evaluate Model] [ evaluate-model] modülü ve hello tuvale sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="ae6ba-183">Merhaba Hello çıkış bağlantı noktasına bağlanmak [Score Model] [ score-model] hello ile ilişkilendirilmiş modül boosted karar ağacı modeli sol toohello giriş hello bağlantı noktası [Evaluate Model] [ evaluate-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="ae6ba-184">Merhaba diğer bağlanmak [Score Model] [ score-model] modülü toohello sağ giriş bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![Modeli değerlendirin bağlı Modülü][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="ae6ba-186">Merhaba denemeyi çalıştırın ve hello sonuçlarını kontrol edin</span><span class="sxs-lookup"><span data-stu-id="ae6ba-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="ae6ba-187">toorun Merhaba deneme, hello tıklatın **çalıştırmak** hello tuvale aşağıdaki düğmesine.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="ae6ba-188">Birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-188">It may take a few minutes.</span></span> <span data-ttu-id="ae6ba-189">Dönen göstergesi her modül çalışıp çalışmadığını ve ardından hello modülünün tamamladığında yeşil bir onay işareti gösterir gösterir.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="ae6ba-190">Tüm hello modülleri bir onay işareti varsa, hello deneme çalışması sona erdi.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="ae6ba-191">Merhaba deneme bu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="ae6ba-191">hello experiment should now look something like this:</span></span>  

![Her iki modeli değerlendirme][3]

<span data-ttu-id="ae6ba-193">toocheck hello sonuçları hello hello çıkış bağlantı noktasına tıklayın [Evaluate Model] [ evaluate-model] modülü ve select **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="ae6ba-194">Merhaba [Evaluate Model] [ evaluate-model] modülü eğriler ve toocompare hello hello iki puanlanmış modelleri sonuçlarını izin ölçümleri çifti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="ae6ba-195">Alıcı işleci karakteristiğini (ROC) Eğriler, duyarlık/geri çağırma Eğriler ya da yükseltme Eğriler olarak hello sonuçlarını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="ae6ba-196">Görüntülenen ek verileri karışıklığı matrisi, hello eğri (AUC) hello alanında toplu değerlerini ve diğer ölçümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="ae6ba-197">Taşıma hello kaydırıcı tarafından sola veya sağa hello eşik değerini değiştirin ve ölçümleri hello kümesi nasıl etkilediği bakın.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="ae6ba-198">toohello hello grafiğin sağına tıklayın **veri kümesi belirtmek** veya **dataset toocompare skoru** toohighlight hello ilişkili eğrisi ve toodisplay hello ilişkili aşağıdaki ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="ae6ba-199">Merhaba Eğriler Hello göstergede "veri kümesi belirtmek" hello, giriş bağlantı noktası sol toohello karşılık gelen [Evaluate Model] [ evaluate-model] modül - Örneğimizde, bu boosted hello karar ağacı modelidir.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="ae6ba-200">"Veri kümesi toocompare skoru" toohello sağ giriş bağlantı noktasını - hello SVM modeli Bu örnekte karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="ae6ba-201">Bu etiketler birine tıkladığınızda, bu model için hello eğri vurgulanır ve hello grafiği aşağıdaki gösterildiği gibi hello karşılık gelen ölçümleri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![Modelleri için ROC Eğriler][4]

<span data-ttu-id="ae6ba-203">Bu değerleri inceleyerek, aradığınız sonuçları hello en yakın toogiving modeldir karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="ae6ba-204">Geri dönün ve parametre değerlerini hello farklı modellerde değiştirerek denemenizi üzerinde yineleme.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="ae6ba-205">Merhaba Bilim ve bu sonuçları yorumlayarak ve hello modeli performans ayarlama resim, bu kılavuzda dış hello kapsamını olur.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="ae6ba-206">Ek Yardım için aşağıdaki makaleler hello okuyun:</span><span class="sxs-lookup"><span data-stu-id="ae6ba-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="ae6ba-207">Nasıl tooevaluate model Azure Machine Learning performansı</span><span class="sxs-lookup"><span data-stu-id="ae6ba-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="ae6ba-208">Azure Machine Learning, algoritmaları parametreleri toooptimize seçin</span><span class="sxs-lookup"><span data-stu-id="ae6ba-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="ae6ba-209">Azure Machine Learning modeli sonuçlarında yorumlama</span><span class="sxs-lookup"><span data-stu-id="ae6ba-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="ae6ba-210">Merhaba deneme bu yineleme kaydını her çalıştırdığınızda hello çalıştırma geçmişi korunur.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="ae6ba-211">Bu yinelemeleri görüntülemek ve tıklayarak tooany, geri dönüp **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** hello tuvale aşağıda.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="ae6ba-212">De tıklayabilirsiniz **önceki Çalıştır** hello içinde **özellikleri** hemen önceki bölmesinde tooreturn toohello yineleme hello bir açık olması.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="ae6ba-213">Tıklayarak denemenizin herhangi bir yinelemesini kopyasını yapabilirsiniz **SAVE AS** hello tuvale aşağıda.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="ae6ba-214">Merhaba deneme kullanmak **Özet** ve **açıklama** özellikleri tookeep, deneme yinelemelerini çalıştınız kaydını.</span><span class="sxs-lookup"><span data-stu-id="ae6ba-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="ae6ba-215">Daha fazla ayrıntı için bkz: [Azure Machine Learning Studio'da deneme yinelemelerini yönetme](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="ae6ba-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="ae6ba-216">**Sonraki: [hello web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="ae6ba-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

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
