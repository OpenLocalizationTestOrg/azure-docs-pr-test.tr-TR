---
title: aaaManage yineleme Machine Learning Studio'da deneme | Microsoft Docs
description: "Nasıl toomanage denemeler Azure Machine Learning Studio'da yineleme"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a><span data-ttu-id="bf80e-103">Azure Machine Learning Studio’da deneme yinelemelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="bf80e-103">Manage experiment iterations in Azure Machine Learning Studio</span></span>
<span data-ttu-id="bf80e-104">Tahmine dayalı analiz modeli geliştirmek olduğu yinelemeli süreç - hello değiştirme gibi çeşitli işlevleri ve denemenizi parametrelerinin memnun olana kadar sonuçlarınız yakınsanır eğitilmiş ve verimli bir model sahip.</span><span class="sxs-lookup"><span data-stu-id="bf80e-104">Developing a predictive analysis model is an iterative process - as you modify hello various functions and parameters of your experiment, your results converge until you are satisfied that you have a trained, effective model.</span></span> <span data-ttu-id="bf80e-105">Anahtar toothis işlem izleme hello çeşitli yinelemelerini deneme parametreleri ve yapılandırmaları olduğu.</span><span class="sxs-lookup"><span data-stu-id="bf80e-105">Key toothis process is tracking hello various iterations of your experiment parameters and configurations.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="bf80e-106">Önceki çalışmalarını gözden geçirebilirsiniz denemelerinizi sipariş toochallenge herhangi bir zamanda, yeniden ziyaret ve sonuçta onaylayın ya da önceki varsayımlar daraltın.</span><span class="sxs-lookup"><span data-stu-id="bf80e-106">You can review previous runs of your experiments at any time in order toochallenge, revisit, and ultimately either confirm or refine previous assumptions.</span></span> <span data-ttu-id="bf80e-107">Bir deneme çalıştırdığınızda, Machine Learning Studio Çalıştır hello veri kümesi, modül ve bağlantı noktası bağlantıları ve parametreleri de dahil olmak üzere geçmişini tutar.</span><span class="sxs-lookup"><span data-stu-id="bf80e-107">When you run an experiment, Machine Learning Studio keeps a history of hello run, including dataset, module, and port connections and parameters.</span></span> <span data-ttu-id="bf80e-108">Bu geçmiş ayrıca sonuçları, başlatma ve durdurma sürelerini, günlük iletilerini ve yürütme durumu gibi çalışma zamanı bilgileri yakalar.</span><span class="sxs-lookup"><span data-stu-id="bf80e-108">This history also captures results, runtime information such as start and stop times, log messages, and execution status.</span></span> <span data-ttu-id="bf80e-109">Geri hiçbir zaman tooreview hello uygulanmasına deneme ve Ara sonuçların Geçmişi'de bu çalışır hiçbirini bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf80e-109">You can look back at any of these runs at any time tooreview hello chronology of your experiment and intermediate results.</span></span> <span data-ttu-id="bf80e-110">Deneme toolaunch, önceki bir çalışmasında yeni bir soru ve bulma aşaması çözümleri modelleme, yol toocreating basit, karmaşık veya hatta ensemble üzerinde bile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf80e-110">You can even use a previous run of your experiment toolaunch into a new phase of inquiry and discovery on your path toocreating simple, complex, or even ensemble modeling solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="bf80e-111">Önceki bir çalışmasında bir deneme görüntülediğinizde hello deneme sürümünün kilitli ve düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="bf80e-111">When you view a previous run of an experiment, that version of hello experiment is locked and can't be edited.</span></span> <span data-ttu-id="bf80e-112">Ancak, bir kopyasını tıklayarak kaydedebileceğiniz **SAVE AS** ve hello kopya için yeni bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf80e-112">You can, however, save a copy of it by clicking **SAVE AS** and providing a new name for hello copy.</span></span> <span data-ttu-id="bf80e-113">Machine Learning Studio, ardından çalıştırın ve düzenleyebileceği hello yeni kopya, açılır.</span><span class="sxs-lookup"><span data-stu-id="bf80e-113">Machine Learning Studio opens hello new copy, which you can then edit and run.</span></span> <span data-ttu-id="bf80e-114">Bu kopyası denemenizi hello kullanılabilir **DENEMELER** diğer tüm denemelerinizi birlikte listesi.</span><span class="sxs-lookup"><span data-stu-id="bf80e-114">This copy of your experiment is available in hello **EXPERIMENTS** list along with all your other experiments.</span></span>
> 
> 

## <a name="viewing-hello-prior-run"></a><span data-ttu-id="bf80e-115">Görüntüleme hello önceki Çalıştır</span><span class="sxs-lookup"><span data-stu-id="bf80e-115">Viewing hello Prior Run</span></span>
<span data-ttu-id="bf80e-116">En az bir kez çalıştır bir deneme açık olduğunda hello deneme yürütülmesi tıklatarak yukarıdaki hello görüntüleyebilirsiniz **önceki Çalıştır** hello Özellikler bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="bf80e-116">When you have an experiment open that you have run at least once, you can view hello preceding run of hello experiment by clicking **Prior Run** in hello properties pane.</span></span>

<span data-ttu-id="bf80e-117">Örneğin, bir deneme oluşturmak ve 11: 23'te bu sürümlerini çalıştıran varsayalım 11:42 ve 11:55.</span><span class="sxs-lookup"><span data-stu-id="bf80e-117">For example, suppose you create an experiment and run versions of it at 11:23, 11:42, and 11:55.</span></span> <span data-ttu-id="bf80e-118">Merhaba son çalışması hello deneme (11:55) açın ve'ı tıklatırsanız **önceki Çalıştır**, 11:42 çalıştırdığınız hello sürümü açılır.</span><span class="sxs-lookup"><span data-stu-id="bf80e-118">If you open hello last run of hello experiment (11:55) and click **Prior Run**, hello version you ran at 11:42 is opened.</span></span>

## <a name="viewing-hello-run-history"></a><span data-ttu-id="bf80e-119">Görüntüleme hello çalıştırma geçmişi</span><span class="sxs-lookup"><span data-stu-id="bf80e-119">Viewing hello Run History</span></span>
<span data-ttu-id="bf80e-120">Merhaba önceki çalışmalarını deneme tıklatarak görüntüleyebileceğiniz **çalıştırma geçmişini görüntüle** açık bir deney olarak.</span><span class="sxs-lookup"><span data-stu-id="bf80e-120">You can view all hello previous runs of an experiment by clicking **View Run History** in an open experiment.</span></span>

<span data-ttu-id="bf80e-121">Örneğin, hello ile bir deneme oluşturduğunuzu varsayalım [doğrusal regresyon] [ linear-regression] modülü ve tooobserve hello etkisini, hello değerini değiştirmek istiyorsanız **öğrenme oranı** üzerinde Deneme sonuçlarınızı.</span><span class="sxs-lookup"><span data-stu-id="bf80e-121">For example, suppose you create an experiment with hello [Linear Regression][linear-regression] module and you want tooobserve hello effect of changing hello value of **Learning rate** on your experiment results.</span></span> <span data-ttu-id="bf80e-122">Hello denemeyi birden çok kez bu parametre için farklı değerler ile aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bf80e-122">You run hello experiment multiple times with different values for this parameter, as follows:</span></span>

| <span data-ttu-id="bf80e-123">Öğrenme hızı değeri</span><span class="sxs-lookup"><span data-stu-id="bf80e-123">Learning Rate value</span></span> | <span data-ttu-id="bf80e-124">Çalıştırma başlangıç zamanı</span><span class="sxs-lookup"><span data-stu-id="bf80e-124">Run start time</span></span> |
| --- | --- |
| <span data-ttu-id="bf80e-125">0.1</span><span class="sxs-lookup"><span data-stu-id="bf80e-125">0.1</span></span> |<span data-ttu-id="bf80e-126">11/9/2014 4:18:58 pm</span><span class="sxs-lookup"><span data-stu-id="bf80e-126">9/11/2014 4:18:58 pm</span></span> |
| <span data-ttu-id="bf80e-127">0.2</span><span class="sxs-lookup"><span data-stu-id="bf80e-127">0.2</span></span> |<span data-ttu-id="bf80e-128">11/9/2014 4:24:33 pm</span><span class="sxs-lookup"><span data-stu-id="bf80e-128">9/11/2014 4:24:33 pm</span></span> |
| <span data-ttu-id="bf80e-129">0.4</span><span class="sxs-lookup"><span data-stu-id="bf80e-129">0.4</span></span> |<span data-ttu-id="bf80e-130">11/9/2014 4:28:36 pm</span><span class="sxs-lookup"><span data-stu-id="bf80e-130">9/11/2014 4:28:36 pm</span></span> |
| <span data-ttu-id="bf80e-131">0.5</span><span class="sxs-lookup"><span data-stu-id="bf80e-131">0.5</span></span> |<span data-ttu-id="bf80e-132">11/9/2014 4:33:31 pm</span><span class="sxs-lookup"><span data-stu-id="bf80e-132">9/11/2014 4:33:31 pm</span></span> |

<span data-ttu-id="bf80e-133">Tıklatırsanız **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE**, bu çalıştırır listesi Bkz:</span><span class="sxs-lookup"><span data-stu-id="bf80e-133">If you click **VIEW RUN HISTORY**, you see a list of all these runs:</span></span>

![Örnek çalıştırma geçmişi][runhistory]

<span data-ttu-id="bf80e-135">Herhangi bir anlık görüntüsünü hello denemeler, çalıştırdığınız hello aynı anda bu çalıştırır tooview birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bf80e-135">Click any of these runs tooview a snapshot of hello experiment at hello time you ran it.</span></span> <span data-ttu-id="bf80e-136">Merhaba yapılandırma, parametre değerleri, açıklamalar ve sonuçları tüm korunan toogive olan, eksiksiz bir kaydı denemenizi bu çalışması ile.</span><span class="sxs-lookup"><span data-stu-id="bf80e-136">hello configuration, parameter values, comments, and results are all preserved toogive you a complete record of that run of your experiment.</span></span>

> [!TIP]
> <span data-ttu-id="bf80e-137">toodocument, hello deneme yinelemelerini her çalıştırdığınızda hello başlık değiştirebilirsiniz, hello güncelleştirebilirsiniz **Özet** hello hello Özellikler bölmesinde denemeler ve ekleme veya güncelleştirme tek tek modülleri açıklamaları toorecord değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="bf80e-137">toodocument your iterations of hello experiment, you can modify hello title each time you run it, you can update hello **Summary** of hello experiment in hello properties pane, and you can add or update comments on individual modules toorecord your changes.</span></span> <span data-ttu-id="bf80e-138">Merhaba başlık, özetini ve modül açıklamaları hello deneme her yürütülmesi kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="bf80e-138">hello title, summary, and module comments are saved with each run of hello experiment.</span></span>
> 
> 

<span data-ttu-id="bf80e-139">Merhaba denemeler Hello listesi **DENEMELER** sekmesi Machine Learning Studio'da bir denemeyi en son sürümünü hello her zaman görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bf80e-139">hello list of experiments in hello **EXPERIMENTS** tab in Machine Learning Studio always displays hello latest version of an experiment.</span></span> <span data-ttu-id="bf80e-140">Merhaba deneme, önceki bir çalışmasında açarsanız (kullanarak **önceki Çalıştır** veya **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE**), tıklatarak toohello taslak sürüm dönebilirsiniz **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** ve seçme Merhaba sahip yineleme bir **durumu** , **düzenlenebilir**.</span><span class="sxs-lookup"><span data-stu-id="bf80e-140">If you open a previous run of hello experiment (using **Prior Run** or **VIEW RUN HISTORY**), you can return toohello draft version by clicking **VIEW RUN HISTORY** and selecting hello iteration that has a **STATE** of **Editable**.</span></span>

## <a name="iterating-on-a-previous-run"></a><span data-ttu-id="bf80e-141">Önceki bir çalışmasında üzerinde yineleme</span><span class="sxs-lookup"><span data-stu-id="bf80e-141">Iterating on a Previous Run</span></span>
<span data-ttu-id="bf80e-142">Tıkladığınızda **önceki Çalıştır** veya **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** ve önceki bir çalışmasında açın, tamamlanmış bir deneme salt okunur modunda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf80e-142">When you click **Prior Run** or **VIEW RUN HISTORY** and open a previous run, you can view a finished experiment in read-only mode.</span></span>

<span data-ttu-id="bf80e-143">Toobegin denemenizi hello şekilde yapılandırdığınız, bir önceki çalıştırma için başlayarak, bir yinelemeye istiyorsanız açma hello çalıştırın ve tıklayarak bunu yapabilirsiniz **SAVE AS**.</span><span class="sxs-lookup"><span data-stu-id="bf80e-143">If you want toobegin an iteration of your experiment starting with hello way you configured it for a previous run, you can do this by opening hello run and clicking **SAVE AS**.</span></span> <span data-ttu-id="bf80e-144">Yeni bir başlık, boş bir çalıştırma geçmişi ve tüm hello bileşenleri ve parametre değerlerini önceki hello çalıştırmak ile yeni bir deneme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bf80e-144">This creates a new experiment, with a new title, an empty run history, and all hello components and parameter values of hello previous run.</span></span> <span data-ttu-id="bf80e-145">Bu yeni bir deneme hello listelenen **DENEMELERİNİ** hello Machine Learning Studio giriş sayfasının ve sekmede değiştirebilirsiniz ve bu, yeni bir başlatma run denemenizi bu yinelemesi geçmişini.</span><span class="sxs-lookup"><span data-stu-id="bf80e-145">This new experiment is listed in hello **EXPERIMENTS** tab in hello Machine Learning Studio home page, and you can modify and run it, initiating a new run history for this iteration of your experiment.</span></span> 

<span data-ttu-id="bf80e-146">Örneğin, hello deneme çalıştırma geçmişi hello önceki bölümde gösterilen olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="bf80e-146">For example, suppose you have hello experiment run history shown in hello previous section.</span></span> <span data-ttu-id="bf80e-147">Merhaba neler tooobserve istediğiniz **öğrenme oranı** parametresi too0.4 ve hello için farklı değerler deneyin **eğitim dönemlerinde sayısı** parametresi.</span><span class="sxs-lookup"><span data-stu-id="bf80e-147">You want tooobserve what happens when you set hello **Learning rate** parameter too0.4, and try different values for hello **Number of training epochs** parameter.</span></span>

1. <span data-ttu-id="bf80e-148">Tıklatın **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** ve 4:28:36 (hangi ayarladığınız hello parametre değeri too0.4) pm çalıştırdığınız hello deneme hello yinelemesi açın.</span><span class="sxs-lookup"><span data-stu-id="bf80e-148">Click **VIEW RUN HISTORY** and open hello iteration of hello experiment that you ran at 4:28:36 pm (in which you set hello parameter value too0.4).</span></span>
2. <span data-ttu-id="bf80e-149">Tıklatın **SAVE AS**.</span><span class="sxs-lookup"><span data-stu-id="bf80e-149">Click **SAVE AS**.</span></span>
3. <span data-ttu-id="bf80e-150">Yeni bir başlık girin ve hello tıklayın **Tamam** onay işareti.</span><span class="sxs-lookup"><span data-stu-id="bf80e-150">Enter a new title and click hello **OK** checkmark.</span></span> <span data-ttu-id="bf80e-151">Merhaba deneme yeni bir kopyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bf80e-151">A new copy of hello experiment is created.</span></span>
4. <span data-ttu-id="bf80e-152">Merhaba değiştirme **eğitim dönemlerinde sayısı** parametresi.</span><span class="sxs-lookup"><span data-stu-id="bf80e-152">Modify hello **Number of training epochs** parameter.</span></span>
5. <span data-ttu-id="bf80e-153">Tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="bf80e-153">Click **RUN**.</span></span>

<span data-ttu-id="bf80e-154">Şimdi toomodify devam etmek ve yeni bir çalıştırma geçmişi toorecord çalışmanızı oluşturma denemenizi, bu sürümü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bf80e-154">You can now continue toomodify and run this version of your experiment, building a new run history toorecord your work.</span></span>

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
