---
title: "Azure Machine Learning modelinizde hata ayıklama | Microsoft Docs"
description: "Azure Machine Learning Train Model ve Score Model modülleri tarafından oluşturulan hataları ayıklamak üzere nasıl."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: d4cc94a6395ea45bccf65d9a9f3118ec98cb258d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="fd2dd-103">Azure Machine Learning’de Model Hatalarını Ayıklama</span><span class="sxs-lookup"><span data-stu-id="fd2dd-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="fd2dd-104">Bu makalede neden aşağıdaki iki hataların ya da bir model çalıştırırken karşılaşılabilecek olası nedenleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="fd2dd-104">This article explains the potential reasons why either of the following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="fd2dd-105">[Train Model] [ train-model] modülünde bir hata oluşturur</span><span class="sxs-lookup"><span data-stu-id="fd2dd-105">the [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="fd2dd-106">[Score Model] [ score-model] modülü hatalı sonuçlar üretir</span><span class="sxs-lookup"><span data-stu-id="fd2dd-106">the [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="fd2dd-107">Train Model modülünün bir hata oluşturur</span><span class="sxs-lookup"><span data-stu-id="fd2dd-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="fd2dd-109">[Train Model] [ train-model] modülü iki girdi bekliyor:</span><span class="sxs-lookup"><span data-stu-id="fd2dd-109">The [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="fd2dd-110">Azure Machine Learning tarafından sağlanan modelleri koleksiyonundan makine öğrenimi modeline türü.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-110">The type of machine learning model from the collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="fd2dd-111">Eğitim verileri tahmin etmek için değişken belirten belirtilen etiket sütunu (diğer sütunların özellikleri olduğu varsayılır).</span><span class="sxs-lookup"><span data-stu-id="fd2dd-111">The training data with a specified Label column which specifies the variable to predict (the other columns are assumed to be Features).</span></span>

<span data-ttu-id="fd2dd-112">Bu modül aşağıdaki durumlarda hataya neden:</span><span class="sxs-lookup"><span data-stu-id="fd2dd-112">This module can produce an error in the following cases:</span></span>

1. <span data-ttu-id="fd2dd-113">Etiket sütununda hatalı şekilde belirtildi.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-113">The Label column is specified incorrectly.</span></span> <span data-ttu-id="fd2dd-114">Bu, birden fazla sütun etiketi olarak seçilir ya da yanlış sütun dizini seçili meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-114">This can happen if either more than one column is selected as the Label or an incorrect column index is selected.</span></span> <span data-ttu-id="fd2dd-115">Örneğin, bir sütun dizini 30 yalnızca 25 sütunları olan bir giriş veri kümesi ile kullanılırsa, ikinci durum geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-115">For example, the second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="fd2dd-116">Veri kümesi herhangi bir özellik sütunu içermiyor.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-116">The dataset does not contain any Feature columns.</span></span> <span data-ttu-id="fd2dd-117">Örneğin, girdi veri kümesi etiket sütun işaretlendiğinden, yalnızca bir sütun varsa olurdu hangi model oluşturmak hiçbir özellik.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-117">For example, if the input dataset has only one column, which is marked as the Label column, there would be no features with which to build the model.</span></span> <span data-ttu-id="fd2dd-118">Bu durumda, [Train Model] [ train-model] modülünde bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-118">In this case, the [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="fd2dd-119">Girdi veri kümesi (özellikleri veya etiketi) sonsuz bir değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-119">The input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="fd2dd-120">Score Model modülünün hatalı sonuçlar üretir</span><span class="sxs-lookup"><span data-stu-id="fd2dd-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="fd2dd-122">Tipik bir eğitim ve sınama deneme denetimli öğrenme için de [bölünmüş veri] [ split] modülü iki bölüme özgün dataset böler: bir bölümü modeli eğitmek için kullanılır ve bir bölümü ne kadar iyi eğitilen model gerçekleştirir Puanlama amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-122">In a typical training/testing experiment for supervised learning, the [Split Data][split] module divides the original dataset into two parts: one part is used to train the model and one part is used to score how well the trained model performs.</span></span> <span data-ttu-id="fd2dd-123">Eğitim modeli sonra daha sonra sonuçları modelin doğruluğunu belirlemek için değerlendirilen test verileri Puanlama amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-123">The trained model is then used to score the test data, after which the results are evaluated to determine the accuracy of the model.</span></span>

<span data-ttu-id="fd2dd-124">[Score Model] [ score-model] modülü iki giriş gerektirir:</span><span class="sxs-lookup"><span data-stu-id="fd2dd-124">The [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="fd2dd-125">Eğitilen model çıktısını [Train Model] [ train-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-125">A trained model output from the [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="fd2dd-126">Modeli eğitmek için kullanılan veri kümesinden farklı bir Puanlama veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-126">A scoring dataset that is different from the dataset used to train the model.</span></span>

<span data-ttu-id="fd2dd-127">Rağmen deneme başarılı olduğunu, mümkünse [Score Model] [ score-model] modülü hatalı sonuçlar üretir.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-127">It's possible that even though the experiment succeeds, the [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="fd2dd-128">Bazı senaryolarda bu gerçekleşecek şekilde neden olabilir:</span><span class="sxs-lookup"><span data-stu-id="fd2dd-128">Several scenarios may cause this to happen:</span></span>

1. <span data-ttu-id="fd2dd-129">Belirtilen etiket kategorik ise ve bir regresyon modeli verileri eğitildi, hatalı bir çıktı tarafından üretilen [Score Model] [ score-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-129">If the specified Label is categorical and a regression model is trained on the data, an incorrect output would be produced by the [Score Model][score-model] module.</span></span> <span data-ttu-id="fd2dd-130">Regresyon sürekli yanıt değişkeni gerektirdiğinden budur.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="fd2dd-131">Bu durumda, bir sınıflandırma modelini kullanmak daha uygun olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-131">In this case, it would be more suitable to use a classification model.</span></span> 

2. <span data-ttu-id="fd2dd-132">Benzer şekilde, bir sınıflandırma modeli Etiket sütununda kayan nokta numarası olan bir veri kümesi üzerinde eğitildi, istenmeyen sonuçlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-132">Similarly, if a classification model is trained on a dataset having floating point numbers in the Label column, it may produce undesirable results.</span></span> <span data-ttu-id="fd2dd-133">Yalnızca bu aralık değerleri sınıfların sonlu ve genellikle biraz küçük, küme üzerinde veren bir ayrık yanıt değişken Sınıflandırmayı gerektirmiyor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="fd2dd-134">Puanlama veri kümesi modeli eğitmek için kullanılan tüm özellikleri içermiyorsa [Score Model] [ score-model] bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-134">If the scoring dataset does not contain all the features used to train the model, the [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="fd2dd-135">Puanlama kümesindeki bir satır eksik veya kendi özelliklerinden herhangi birini sonsuz bir değerini içeriyorsa [Score Model] [ score-model] ilgili satır için karşılık gelen herhangi bir çıktı oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-135">If a row in the scoring dataset contains a missing value or an infinite value for any of its features, the [Score Model][score-model] will not produce any output corresponding to that row.</span></span>

5. <span data-ttu-id="fd2dd-136">[Score Model] [ score-model] Puanlama kümesindeki tüm satırların aynı çıktıları üretebilir.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-136">The [Score Model][score-model] may produce identical outputs for all rows in the scoring dataset.</span></span> <span data-ttu-id="fd2dd-137">Bu, örneğin, örnekleri yaprak düğümü başına en az sayıda eğitim örnekleri kullanılabilir sayısından daha fazla olacak şekilde seçilirse karar ormanları kullanarak sınıflandırma çalışılırken gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="fd2dd-137">This could occur, for example, when attempting classification using Decision Forests if the minimum number of samples per leaf node is chosen to be more than the number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

