---
title: aaaDebug modelinizi Azure Machine Learning | Microsoft Docs
description: "Nasıl toodebug hataları Azure Machine Learning modüllerinin Train Model ve Score Model tarafından üretilen."
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
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="8af02-103">Azure Machine Learning’de Model Hatalarını Ayıklama</span><span class="sxs-lookup"><span data-stu-id="8af02-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="8af02-104">Bu makalede neden iki hataları aşağıdaki hello birini bir model çalıştırırken karşılaşılabilecek hello olası nedenleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="8af02-104">This article explains hello potential reasons why either of hello following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="8af02-105">Merhaba [Train Model] [ train-model] modülünde bir hata oluşturur</span><span class="sxs-lookup"><span data-stu-id="8af02-105">hello [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="8af02-106">Merhaba [Score Model] [ score-model] modülü hatalı sonuçlar üretir</span><span class="sxs-lookup"><span data-stu-id="8af02-106">hello [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="8af02-107">Train Model modülünün bir hata oluşturur</span><span class="sxs-lookup"><span data-stu-id="8af02-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="8af02-109">Merhaba [Train Model] [ train-model] modülü iki girdi bekliyor:</span><span class="sxs-lookup"><span data-stu-id="8af02-109">hello [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="8af02-110">Azure Machine Learning tarafından sağlanan modellerin hello koleksiyonundan makine öğrenimi modeline Hello türü.</span><span class="sxs-lookup"><span data-stu-id="8af02-110">hello type of machine learning model from hello collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="8af02-111">Merhaba eğitim verilerini belirten belirtilen etiket sütunu hello değişken toopredict (Merhaba diğer sütunları toobe özellikleri varsayılır).</span><span class="sxs-lookup"><span data-stu-id="8af02-111">hello training data with a specified Label column which specifies hello variable toopredict (hello other columns are assumed toobe Features).</span></span>

<span data-ttu-id="8af02-112">Bu modül durumları aşağıdaki hello hata oluşturabilir:</span><span class="sxs-lookup"><span data-stu-id="8af02-112">This module can produce an error in hello following cases:</span></span>

1. <span data-ttu-id="8af02-113">Merhaba etiket sütunu yanlış belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="8af02-113">hello Label column is specified incorrectly.</span></span> <span data-ttu-id="8af02-114">Bu etiket hello birden fazla sütun seçildi ya da yanlış sütun dizini seçili meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="8af02-114">This can happen if either more than one column is selected as hello Label or an incorrect column index is selected.</span></span> <span data-ttu-id="8af02-115">Örneğin, bir sütun dizini 30 yalnızca 25 sütunları olan bir giriş veri kümesi ile kullandıysanız hello ikinci durum geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="8af02-115">For example, hello second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="8af02-116">Merhaba veri kümesi herhangi bir özellik sütunu içermiyor.</span><span class="sxs-lookup"><span data-stu-id="8af02-116">hello dataset does not contain any Feature columns.</span></span> <span data-ttu-id="8af02-117">Örneğin, hello girdi veri kümesi hello etiket sütun işaretlendiğinden, yalnızca bir sütun varsa olurdu hangi toobuild hello modeliyle hiçbir özellik.</span><span class="sxs-lookup"><span data-stu-id="8af02-117">For example, if hello input dataset has only one column, which is marked as hello Label column, there would be no features with which toobuild hello model.</span></span> <span data-ttu-id="8af02-118">Bu durumda, hello [Train Model] [ train-model] modülünde bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8af02-118">In this case, hello [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="8af02-119">Merhaba girdi veri kümesi (özellikleri veya etiketi) sonsuz bir değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8af02-119">hello input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="8af02-120">Score Model modülünün hatalı sonuçlar üretir</span><span class="sxs-lookup"><span data-stu-id="8af02-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="8af02-122">Bir tipik eğitim ve sınama denemesinde denetimli öğrenme için hello [bölünmüş veri] [ split] modülü iki bölüme hello özgün dataset böler: bir parçasıdır kullanılan tootrain hello modeli ve bir bölümü kullanılır tooscore ne kadar iyi hello eğitilen model gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="8af02-122">In a typical training/testing experiment for supervised learning, hello [Split Data][split] module divides hello original dataset into two parts: one part is used tootrain hello model and one part is used tooscore how well hello trained model performs.</span></span> <span data-ttu-id="8af02-123">kullanılan tooscore hello sonra test verileri, sonra hello sonuçları değerlendirilen toodetermine hello hello modeli doğruluğunu olduğu hello eğitilen modelidir.</span><span class="sxs-lookup"><span data-stu-id="8af02-123">hello trained model is then used tooscore hello test data, after which hello results are evaluated toodetermine hello accuracy of hello model.</span></span>

<span data-ttu-id="8af02-124">Merhaba [Score Model] [ score-model] modülü iki giriş gerektirir:</span><span class="sxs-lookup"><span data-stu-id="8af02-124">hello [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="8af02-125">Merhaba eğitilen model çıktısını [Train Model] [ train-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="8af02-125">A trained model output from hello [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="8af02-126">Merhaba kümesinden farklı bir Puanlama dataset tootrain hello modeli kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8af02-126">A scoring dataset that is different from hello dataset used tootrain hello model.</span></span>

<span data-ttu-id="8af02-127">Merhaba deneme başarılı olsa bile hello olası kullanıcının [Score Model] [ score-model] modülü hatalı sonuçlar üretir.</span><span class="sxs-lookup"><span data-stu-id="8af02-127">It's possible that even though hello experiment succeeds, hello [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="8af02-128">Bazı senaryolarda bu toohappen neden olabilir:</span><span class="sxs-lookup"><span data-stu-id="8af02-128">Several scenarios may cause this toohappen:</span></span>

1. <span data-ttu-id="8af02-129">Merhaba etiket kategorik ve bir regresyon modeli hello verileri eğitildi belirtilmişse, hatalı bir çıktı hello tarafından üretilen [Score Model] [ score-model] modülü.</span><span class="sxs-lookup"><span data-stu-id="8af02-129">If hello specified Label is categorical and a regression model is trained on hello data, an incorrect output would be produced by hello [Score Model][score-model] module.</span></span> <span data-ttu-id="8af02-130">Regresyon sürekli yanıt değişkeni gerektirdiğinden budur.</span><span class="sxs-lookup"><span data-stu-id="8af02-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="8af02-131">Bu durumda, daha uygun toouse bir sınıflandırma modeli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8af02-131">In this case, it would be more suitable toouse a classification model.</span></span> 

2. <span data-ttu-id="8af02-132">Benzer şekilde, bir sınıflandırma modeli kayan nokta numarası hello etiket sütuna sahip bir veri kümesi üzerinde eğitildi, istenmeyen sonuçlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="8af02-132">Similarly, if a classification model is trained on a dataset having floating point numbers in hello Label column, it may produce undesirable results.</span></span> <span data-ttu-id="8af02-133">Yalnızca bu aralık değerleri sınıfların sonlu ve genellikle biraz küçük, küme üzerinde veren bir ayrık yanıt değişken Sınıflandırmayı gerektirmiyor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="8af02-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="8af02-134">Veri kümesi Puanlama hello tüm hello kullanılan özellikler tootrain hello modeli içermiyorsa hello [Score Model] [ score-model] bir hata oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8af02-134">If hello scoring dataset does not contain all hello features used tootrain hello model, hello [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="8af02-135">Veri kümesi Puanlama hello satırda eksik bir değer veya özelliklerinden birini sonsuz bir değer içeriyorsa, hello [Score Model] [ score-model] hiçbir çıktı karşılık gelen toothat satır oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="8af02-135">If a row in hello scoring dataset contains a missing value or an infinite value for any of its features, hello [Score Model][score-model] will not produce any output corresponding toothat row.</span></span>

5. <span data-ttu-id="8af02-136">Merhaba [Score Model] [ score-model] dataset Puanlama hello içindeki tüm satırların aynı çıktıları üretebilir.</span><span class="sxs-lookup"><span data-stu-id="8af02-136">hello [Score Model][score-model] may produce identical outputs for all rows in hello scoring dataset.</span></span> <span data-ttu-id="8af02-137">Bu, örneğin, örnekleri yaprak düğümü başına en az sayıda hello eğitim örnekleri kullanılabilir hello birden çok toobe sayısı seçilirse karar ormanları kullanarak sınıflandırma çalışılırken gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="8af02-137">This could occur, for example, when attempting classification using Decision Forests if hello minimum number of samples per leaf node is chosen toobe more than hello number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

