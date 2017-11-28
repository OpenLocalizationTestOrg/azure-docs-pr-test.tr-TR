---
title: "Machine Learning Studio'da deneme yinelemelerini yönetme | Microsoft Docs"
description: "Azure Machine Learning Studio'da deneme yinelemelerini yönetme"
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
ms.openlocfilehash: 0e32a02358d1901bb80f356b0289b02b8e98afdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a><span data-ttu-id="7282e-103">Azure Machine Learning Studio’da deneme yinelemelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="7282e-103">Manage experiment iterations in Azure Machine Learning Studio</span></span>
<span data-ttu-id="7282e-104">Tahmine dayalı analiz modeli geliştirmek olduğu yinelemeli süreç - memnun olana kadar sonuçlarınız yakınsanır çeşitli işlevleri ve denemenizi parametrelerini değiştirirken, eğitilmiş ve verimli bir model sahip.</span><span class="sxs-lookup"><span data-stu-id="7282e-104">Developing a predictive analysis model is an iterative process - as you modify the various functions and parameters of your experiment, your results converge until you are satisfied that you have a trained, effective model.</span></span> <span data-ttu-id="7282e-105">Bu işlem anahtarına deneme parametreleri ve yapılandırmaları çeşitli yinelemelerini izlemektir.</span><span class="sxs-lookup"><span data-stu-id="7282e-105">Key to this process is tracking the various iterations of your experiment parameters and configurations.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="7282e-106">Sınama, yeniden ziyaret ve sonuçta onaylayın ya da önceki varsayımlar iyileştirmek için herhangi bir zamanda denemelerinizi önceki çalışmalarını gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7282e-106">You can review previous runs of your experiments at any time in order to challenge, revisit, and ultimately either confirm or refine previous assumptions.</span></span> <span data-ttu-id="7282e-107">Bir deneme çalıştırdığınızda, Machine Learning Studio veri kümesi, modül ve bağlantı noktası bağlantıları ve parametreleri de dahil olmak üzere çalışma geçmişini tutar.</span><span class="sxs-lookup"><span data-stu-id="7282e-107">When you run an experiment, Machine Learning Studio keeps a history of the run, including dataset, module, and port connections and parameters.</span></span> <span data-ttu-id="7282e-108">Bu geçmiş ayrıca sonuçları, başlatma ve durdurma sürelerini, günlük iletilerini ve yürütme durumu gibi çalışma zamanı bilgileri yakalar.</span><span class="sxs-lookup"><span data-stu-id="7282e-108">This history also captures results, runtime information such as start and stop times, log messages, and execution status.</span></span> <span data-ttu-id="7282e-109">Bu çalıştırır hiçbirini uygulanmasına geçmişi deneme ve Ara sonuçlarını gözden geçirmek için herhangi bir zamanda geri bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7282e-109">You can look back at any of these runs at any time to review the chronology of your experiment and intermediate results.</span></span> <span data-ttu-id="7282e-110">Denemenizi, önceki bir çalışmasında bile yolunda basit, karmaşık veya hatta ensemble modelleme çözümleri oluşturmak için yeni bir soru ve bulma aşaması başlatmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7282e-110">You can even use a previous run of your experiment to launch into a new phase of inquiry and discovery on your path to creating simple, complex, or even ensemble modeling solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="7282e-111">Önceki bir çalışmasında bir deneme görüntülediğinizde, bu deneme sürümünün kilitli ve düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="7282e-111">When you view a previous run of an experiment, that version of the experiment is locked and can't be edited.</span></span> <span data-ttu-id="7282e-112">Ancak, bir kopyasını tıklayarak kaydedebileceğiniz **SAVE AS** ve kopya için yeni bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="7282e-112">You can, however, save a copy of it by clicking **SAVE AS** and providing a new name for the copy.</span></span> <span data-ttu-id="7282e-113">Machine Learning Studio'da daha sonra Düzenle ve çalıştırmak yeni bir kopyası açılır.</span><span class="sxs-lookup"><span data-stu-id="7282e-113">Machine Learning Studio opens the new copy, which you can then edit and run.</span></span> <span data-ttu-id="7282e-114">Bu kopyası denemenizi kullanılabilir **DENEMELER** diğer tüm denemelerinizi birlikte listesi.</span><span class="sxs-lookup"><span data-stu-id="7282e-114">This copy of your experiment is available in the **EXPERIMENTS** list along with all your other experiments.</span></span>
> 
> 

## <a name="viewing-the-prior-run"></a><span data-ttu-id="7282e-115">Önceki çalışma görüntüleme</span><span class="sxs-lookup"><span data-stu-id="7282e-115">Viewing the Prior Run</span></span>
<span data-ttu-id="7282e-116">En az bir kez çalıştır bir deneme açık olduğunda tıklayarak denemeyi önceki yürütülmesi görüntüleyebilirsiniz **önceki Çalıştır** Özellikler bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="7282e-116">When you have an experiment open that you have run at least once, you can view the preceding run of the experiment by clicking **Prior Run** in the properties pane.</span></span>

<span data-ttu-id="7282e-117">Örneğin, bir deneme oluşturmak ve 11: 23'te bu sürümlerini çalıştıran varsayalım 11:42 ve 11:55.</span><span class="sxs-lookup"><span data-stu-id="7282e-117">For example, suppose you create an experiment and run versions of it at 11:23, 11:42, and 11:55.</span></span> <span data-ttu-id="7282e-118">Deneme (11:55)'ın son çalıştırılmasındaki açın ve'ı tıklatırsanız **önceki Çalıştır**, 11:42 çalıştırdığınız sürümü açılır.</span><span class="sxs-lookup"><span data-stu-id="7282e-118">If you open the last run of the experiment (11:55) and click **Prior Run**, the version you ran at 11:42 is opened.</span></span>

## <a name="viewing-the-run-history"></a><span data-ttu-id="7282e-119">Çalıştırma geçmişini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="7282e-119">Viewing the Run History</span></span>
<span data-ttu-id="7282e-120">Bir deneme önceki tüm çalışmalarınızı tıklayarak görüntüleyebilirsiniz **çalıştırma geçmişini görüntüle** açık bir deney olarak.</span><span class="sxs-lookup"><span data-stu-id="7282e-120">You can view all the previous runs of an experiment by clicking **View Run History** in an open experiment.</span></span>

<span data-ttu-id="7282e-121">Örneğin, bir deneme ile oluşturduğunuz varsayalım [doğrusal regresyon] [ linear-regression] modülü ve değerinin değiştirilmesi etkisini izlemek istediğinizde **öğrenme oranı** üzerinde Deneme sonuçları.</span><span class="sxs-lookup"><span data-stu-id="7282e-121">For example, suppose you create an experiment with the [Linear Regression][linear-regression] module and you want to observe the effect of changing the value of **Learning rate** on your experiment results.</span></span> <span data-ttu-id="7282e-122">Denemeyi birden çok kez bu parametre için farklı değerler ile aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="7282e-122">You run the experiment multiple times with different values for this parameter, as follows:</span></span>

| <span data-ttu-id="7282e-123">Öğrenme hızı değeri</span><span class="sxs-lookup"><span data-stu-id="7282e-123">Learning Rate value</span></span> | <span data-ttu-id="7282e-124">Çalıştırma başlangıç zamanı</span><span class="sxs-lookup"><span data-stu-id="7282e-124">Run start time</span></span> |
| --- | --- |
| <span data-ttu-id="7282e-125">0.1</span><span class="sxs-lookup"><span data-stu-id="7282e-125">0.1</span></span> |<span data-ttu-id="7282e-126">11/9/2014 4:18:58 pm</span><span class="sxs-lookup"><span data-stu-id="7282e-126">9/11/2014 4:18:58 pm</span></span> |
| <span data-ttu-id="7282e-127">0.2</span><span class="sxs-lookup"><span data-stu-id="7282e-127">0.2</span></span> |<span data-ttu-id="7282e-128">11/9/2014 4:24:33 pm</span><span class="sxs-lookup"><span data-stu-id="7282e-128">9/11/2014 4:24:33 pm</span></span> |
| <span data-ttu-id="7282e-129">0.4</span><span class="sxs-lookup"><span data-stu-id="7282e-129">0.4</span></span> |<span data-ttu-id="7282e-130">11/9/2014 4:28:36 pm</span><span class="sxs-lookup"><span data-stu-id="7282e-130">9/11/2014 4:28:36 pm</span></span> |
| <span data-ttu-id="7282e-131">0.5</span><span class="sxs-lookup"><span data-stu-id="7282e-131">0.5</span></span> |<span data-ttu-id="7282e-132">11/9/2014 4:33:31 pm</span><span class="sxs-lookup"><span data-stu-id="7282e-132">9/11/2014 4:33:31 pm</span></span> |

<span data-ttu-id="7282e-133">Tıklatırsanız **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE**, bu çalıştırır listesi Bkz:</span><span class="sxs-lookup"><span data-stu-id="7282e-133">If you click **VIEW RUN HISTORY**, you see a list of all these runs:</span></span>

![Örnek çalıştırma geçmişi][runhistory]

<span data-ttu-id="7282e-135">Herhangi bir anlık görüntüsünü çalıştırdığınızda, deneme görüntülemek için bu çalıştırır birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7282e-135">Click any of these runs to view a snapshot of the experiment at the time you ran it.</span></span> <span data-ttu-id="7282e-136">Yapılandırma, parametre değerleri, açıklamalar ve sonuçları tüm denemenizi bu yürütülmesi tamamlandı kaydını vermek için korunur.</span><span class="sxs-lookup"><span data-stu-id="7282e-136">The configuration, parameter values, comments, and results are all preserved to give you a complete record of that run of your experiment.</span></span>

> [!TIP]
> <span data-ttu-id="7282e-137">Deneme yinelemelerini belgelemek için her zaman başlığını değiştirebilirsiniz. Bunu çalıştırmanız, güncelleştirebilirsiniz **Özet** deneme özelliklerinde, bölmesinde ve ekleyebilir ya da güncelleştirebilirsiniz kaydetmek için tek tek modülleri yorumları, değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7282e-137">To document your iterations of the experiment, you can modify the title each time you run it, you can update the **Summary** of the experiment in the properties pane, and you can add or update comments on individual modules to record your changes.</span></span> <span data-ttu-id="7282e-138">Başlık, özetini ve modül açıklamaları her denemeyi çalıştırma ile kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="7282e-138">The title, summary, and module comments are saved with each run of the experiment.</span></span>
> 
> 

<span data-ttu-id="7282e-139">Alanındaki denemeler listesi **DENEMELER** sekmesi Machine Learning Studio'da her zaman en son bir deneme sürümünü görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7282e-139">The list of experiments in the **EXPERIMENTS** tab in Machine Learning Studio always displays the latest version of an experiment.</span></span> <span data-ttu-id="7282e-140">Denemeyi, önceki bir çalışmasında açarsanız (kullanarak **önceki Çalıştır** veya **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE**), tıklatarak taslak sürüm dönebilirsiniz **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** ve seçme sahip yineleme bir **durumu** , **düzenlenebilir**.</span><span class="sxs-lookup"><span data-stu-id="7282e-140">If you open a previous run of the experiment (using **Prior Run** or **VIEW RUN HISTORY**), you can return to the draft version by clicking **VIEW RUN HISTORY** and selecting the iteration that has a **STATE** of **Editable**.</span></span>

## <a name="iterating-on-a-previous-run"></a><span data-ttu-id="7282e-141">Önceki bir çalışmasında üzerinde yineleme</span><span class="sxs-lookup"><span data-stu-id="7282e-141">Iterating on a Previous Run</span></span>
<span data-ttu-id="7282e-142">Tıkladığınızda **önceki Çalıştır** veya **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** ve önceki bir çalışmasında açın, tamamlanmış bir deneme salt okunur modunda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7282e-142">When you click **Prior Run** or **VIEW RUN HISTORY** and open a previous run, you can view a finished experiment in read-only mode.</span></span>

<span data-ttu-id="7282e-143">Denemenizi, yapılandırma, bir önceki çalıştırma için yönteminiz ile başlayarak, bir yinelemeye başlamak isterseniz, Çalıştır açıp tıklatarak bunu yapabilirsiniz **SAVE AS**.</span><span class="sxs-lookup"><span data-stu-id="7282e-143">If you want to begin an iteration of your experiment starting with the way you configured it for a previous run, you can do this by opening the run and clicking **SAVE AS**.</span></span> <span data-ttu-id="7282e-144">Bu yeni bir deneme çalıştırma geçmişi, boş bir yeni başlık oluşturur ve tüm bileşenleri ve parametre değerlerini önceki çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7282e-144">This creates a new experiment, with a new title, an empty run history, and all the components and parameter values of the previous run.</span></span> <span data-ttu-id="7282e-145">Bu yeni bir deneme listelenen **DENEMELERİNİ** Machine Learning Studio giriş sayfası ve sekmede değiştirebilirsiniz ve bu, yeni bir başlatma run denemenizi bu yinelemesi geçmişini.</span><span class="sxs-lookup"><span data-stu-id="7282e-145">This new experiment is listed in the **EXPERIMENTS** tab in the Machine Learning Studio home page, and you can modify and run it, initiating a new run history for this iteration of your experiment.</span></span> 

<span data-ttu-id="7282e-146">Örneğin, önceki bölümde gösterilen geçmişi çalıştırmak deneme olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7282e-146">For example, suppose you have the experiment run history shown in the previous section.</span></span> <span data-ttu-id="7282e-147">Ayarladığınız zaman neler gözlemlemek istediğiniz **öğrenme oranı** parametresi 0.4 ve için farklı değerler deneyin **eğitim dönemlerinde sayısı** parametresi.</span><span class="sxs-lookup"><span data-stu-id="7282e-147">You want to observe what happens when you set the **Learning rate** parameter to 0.4, and try different values for the **Number of training epochs** parameter.</span></span>

1. <span data-ttu-id="7282e-148">Tıklatın **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** ve 4:28:36 (hangi parametre değerine ayarlamanız için 0.4) pm adresindeki çalıştırdığınız deneme yinelemesi açın.</span><span class="sxs-lookup"><span data-stu-id="7282e-148">Click **VIEW RUN HISTORY** and open the iteration of the experiment that you ran at 4:28:36 pm (in which you set the parameter value to 0.4).</span></span>
2. <span data-ttu-id="7282e-149">Tıklatın **SAVE AS**.</span><span class="sxs-lookup"><span data-stu-id="7282e-149">Click **SAVE AS**.</span></span>
3. <span data-ttu-id="7282e-150">Yeni bir başlık girin ve tıklayın **Tamam** onay işareti.</span><span class="sxs-lookup"><span data-stu-id="7282e-150">Enter a new title and click the **OK** checkmark.</span></span> <span data-ttu-id="7282e-151">Yeni bir deneme kopyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7282e-151">A new copy of the experiment is created.</span></span>
4. <span data-ttu-id="7282e-152">Değiştirme **eğitim dönemlerinde sayısı** parametresi.</span><span class="sxs-lookup"><span data-stu-id="7282e-152">Modify the **Number of training epochs** parameter.</span></span>
5. <span data-ttu-id="7282e-153">Tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="7282e-153">Click **RUN**.</span></span>

<span data-ttu-id="7282e-154">Şimdi bu sürümü, denemeyi çalıştırmak ve değiştirmek, çalışmanızı kaydetmek için yeni bir çalıştırma geçmişi oluşturmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7282e-154">You can now continue to modify and run this version of your experiment, building a new run history to record your work.</span></span>

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
