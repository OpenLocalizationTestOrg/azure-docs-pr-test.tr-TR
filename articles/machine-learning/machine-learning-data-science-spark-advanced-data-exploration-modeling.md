---
title: "aaaAdvanced veri keşfi ve Spark ile modelleme | Microsoft Docs"
description: "Çapraz doğrulama ve hyperparameter en iyi duruma getirme kullanarak ikili sınıflandırma ve regresyon modeli eğitmek ve Hdınsight Spark toodo veri keşfi kullanın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="788fb-103">Spark ile gelişmiş veri keşfi ve modelleme</span><span class="sxs-lookup"><span data-stu-id="788fb-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="788fb-104">Bu kılavuzda Hdınsight Spark toodo veri keşfi ve tren ikili sınıflandırma ve çapraz doğrulama kullanarak regresyon modeli kullanır ve hyperparameter en iyi duruma getirilmesi bir örneği hello NYC Seyahat Ücreti 2013 dataset masrafları.</span><span class="sxs-lookup"><span data-stu-id="788fb-104">This walkthrough uses HDInsight Spark toodo data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="788fb-105">Merhaba hello adımlarda size yol gösterir [veri bilimi işlemi](http://aka.ms/datascienceprocess)için Hdınsight Spark kullanarak uçtan, küme için işleme ve Azure BLOB'ların toostore hello veri ve hello modeller.</span><span class="sxs-lookup"><span data-stu-id="788fb-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="788fb-106">Hello işlem bir Azure Storage Blobundan getirildi veri visualizes inceler ve ardından hello veri toobuild Tahmine dayalı modelleri hazırlar.</span><span class="sxs-lookup"><span data-stu-id="788fb-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="788fb-107">Python kullanılan toocode hello çözümü ve tooshow hello ilgili çizimleri olmuştur.</span><span class="sxs-lookup"><span data-stu-id="788fb-107">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span> <span data-ttu-id="788fb-108">Bu modeller hello Spark Mllib'i Araç Seti toodo ikili sınıflandırma ve görevleri modelleme regresyon kullanarak derlemesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="788fb-108">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="788fb-109">Merhaba **ikili sınıflandırma** görev gerekmediğini toopredict hello seyahat için ücretli bir ipucu.</span><span class="sxs-lookup"><span data-stu-id="788fb-109">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="788fb-110">Merhaba **regresyon** toopredict hello diğer ipucu özelliklerini temel alarak hello ipucu miktarını bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="788fb-110">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="788fb-111">Merhaba modelleme adımları ayrıca nasıl tootrain, değerlendirmek ve her türde bir model Kaydet gösteren kod içerir.</span><span class="sxs-lookup"><span data-stu-id="788fb-111">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="788fb-112">Merhaba konu aynı yerde hello hello bazıları kapsar [veri keşfi ve modelleme Spark ile](machine-learning-data-science-spark-data-exploration-modeling.md) konu.</span><span class="sxs-lookup"><span data-stu-id="788fb-112">hello topic covers some of hello same ground as hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="788fb-113">Ancak "de en iyi şekilde doğru sınıflandırma ve regresyon modeli tootrain yerleştirmez hyperparameter ile çapraz doğrulama kullandığından, daha gelişmiş".</span><span class="sxs-lookup"><span data-stu-id="788fb-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping tootrain optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="788fb-114">**Çapraz doğrulama (MS)** ne kadar iyi bilinen bir veri kümesi üzerinde eğitilmiş model üzerinde eğitilmedi veri kümeleri toopredicting hello özelliklerini genelleştirir değerlendirir bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="788fb-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes toopredicting hello features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="788fb-115">Burada kullanılan yaygın olarak görülen bir uygulama toodivide K Katlama içine bir veri kümesidir ve bir hepsini şekilde hello Katlama biri dışındaki tüm hello modeli eğitmek.</span><span class="sxs-lookup"><span data-stu-id="788fb-115">A common implementation used here is toodivide a dataset into K folds and then train hello model in a round-robin fashion on all but one of hello folds.</span></span> <span data-ttu-id="788fb-116">Merhaba bağımsız veri kümesi bu kullanılmayan Katlama tootrain hello modelde karşı doğru bir şekilde test edildiğinde hello modeli tooprediction Hello yeteneklerini uygunluk.</span><span class="sxs-lookup"><span data-stu-id="788fb-116">hello ability of hello model tooprediction accurately when tested against hello independent dataset in this fold not used tootrain hello model is assessed.</span></span>

<span data-ttu-id="788fb-117">**Hyperparameter iyileştirme** kümesiyle bir ölçü bağımsız bir veri kümesi üzerinde hello algoritması'nın performansını en iyi duruma getirme genellikle hello amacı hyperparameters bir öğrenme algoritması seçme hello sorunudur.</span><span class="sxs-lookup"><span data-stu-id="788fb-117">**Hyperparameter optimization** is hello problem of choosing a set of hyperparameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="788fb-118">**Hyperparameters** hello model eğitim yordamı dışında belirtilmelidir değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="788fb-118">**Hyperparameters** are values that must be specified outside of hello model training procedure.</span></span> <span data-ttu-id="788fb-119">Bu değerler hakkında varsayımlar hello esneklik ve hello modelleri doğruluğunu etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-119">Assumptions about these values can impact hello flexibility and accuracy of hello models.</span></span> <span data-ttu-id="788fb-120">Karar ağaçları gibi Hello derinliği ve hello ağacında bırakır sayısı istenen hyperparameters, örneğin, sahip.</span><span class="sxs-lookup"><span data-stu-id="788fb-120">Decision trees have hyperparameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="788fb-121">Destek vektör makinelerin (SVMs) misclassification cezası terim ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="788fb-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="788fb-122">Burada kullanılan bir ortak yolu tooperform hyperparameter iyileştirme bir kılavuz arama değil veya **parametresi tarama**.</span><span class="sxs-lookup"><span data-stu-id="788fb-122">A common way tooperform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="788fb-123">Bu ayrıntılı aramasını hello değerleri aracılığıyla hello hyperparameter alanı belirtilen bir alt bir öğrenme algoritması kümeleri oluşur.</span><span class="sxs-lookup"><span data-stu-id="788fb-123">This consists of performing an exhaustive search through hello values a specified subset of hello hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="788fb-124">Çapraz doğrulama performans ölçüm toosort hello kılavuz arama algoritması tarafından üretilen hello verimle çıkışı sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-124">Cross validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="788fb-125">MS hello modeli korur hello kapasite tooapply toohello genel hangi hello eğitim verileri ayıklandı veri kümesi bir model tootraining verileri overfitting gibi sınırı sorunları hyperparameter sakınımlı yardımcı ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="788fb-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model tootraining data so that hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

<span data-ttu-id="788fb-126">Merhaba modelleri kullanırız Lojistik ve doğrusal regresyon, rastgele ormanları ve gradyan boosted ağaçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="788fb-126">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="788fb-127">[Doğrusal regresyon SGD ile](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) Stokastik gradyan düşüşü (SGD) yöntemini kullanan doğrusal regresyon modeli ve en iyi duruma getirme ve özellik için toopredict hello ipucu tutarlar ölçeklendirme Ücretli.</span><span class="sxs-lookup"><span data-stu-id="788fb-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="788fb-128">[LBFGS ile Lojistik regresyon](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) veya "logit" regresyon hello bağımlı değişken kategorik toodo veri sınıflandırması olduğunda kullanılabilen bir regresyon modeli.</span><span class="sxs-lookup"><span data-stu-id="788fb-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="788fb-129">LBFGS sınırlı bir bilgisayarın bellek miktarını kullanarak hello Broyden – Fletcher'dan – Goldfarb – Shanno (BFGS) algoritması benzeyen ve machine learning'de yaygın olarak kullanılan bir yarı-Newton iyileştirme algoritması ' dir.</span><span class="sxs-lookup"><span data-stu-id="788fb-129">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="788fb-130">[Rastgele ormanlar](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) karar ağaçları ensembles şunlardır.</span><span class="sxs-lookup"><span data-stu-id="788fb-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="788fb-131">Bunlar, birçok karar ağaçları tooreduce hello riskini overfitting birleştirin.</span><span class="sxs-lookup"><span data-stu-id="788fb-131">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="788fb-132">Rastgele ormanlar regresyon ve sınıflandırma için kullanılır ve kategorik özellikleri işleyebilir ve toohello çok sınıflı sınıflandırma ayarı genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-132">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="788fb-133">Bunlar, özellik ölçekleme ve bu mümkün toocapture sapmalar ve özellik etkileşimleri gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="788fb-133">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="788fb-134">Rastgele ormanlar hello en başarılı machine learning modellerini sınıflandırma ve regresyon biridir.</span><span class="sxs-lookup"><span data-stu-id="788fb-134">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="788fb-135">[Gradyan boosted ağaçları](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) olan karar ağaçları ensembles.</span><span class="sxs-lookup"><span data-stu-id="788fb-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="788fb-136">GBTs tren karar tekrarlayarak toominimize kaybı işlevi ağaçları.</span><span class="sxs-lookup"><span data-stu-id="788fb-136">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="788fb-137">GBTs regresyon ve sınıflandırma için kullanılır ve kategorik özellikleri işleyebilir, özellik ölçeklendirme gerektirmez ve mümkün toocapture sapmalar ve etkileşimleri özellik.</span><span class="sxs-lookup"><span data-stu-id="788fb-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="788fb-138">Bir sınıflandırma veya çoklu sınıflar ayarında de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="788fb-139">MS ve Hyperparameter kullanan örnekler modelleme tarama gösterildiğinden hello ikili sınıflandırma sorunu için.</span><span class="sxs-lookup"><span data-stu-id="788fb-139">Modeling examples using CV and Hyperparameter sweep are shown for hello binary classification problem.</span></span> <span data-ttu-id="788fb-140">Daha basit örnekler (olmadan parametre dağılımlarında) regresyon görevleri için ana konudaki hello sunulur.</span><span class="sxs-lookup"><span data-stu-id="788fb-140">Simpler examples (without parameter sweeps) are presented in hello main topic for regression tasks.</span></span> <span data-ttu-id="788fb-141">Ancak hello ekte esnek net doğrusal regresyon ve MS için parametre tarama için rastgele orman regresyon ile kullanarak doğrulama da sunulur.</span><span class="sxs-lookup"><span data-stu-id="788fb-141">But in hello appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="788fb-142">Merhaba **esnek net** regularized regresyon yöntemi doğrusal regresyon sığdırma, doğrusal olarak modeller için birleştirir hello L1 ve L2 ölçümleri hello cezaları olan [Serbest Şekil](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) ve [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="788fb-142">hello **elastic net** is a regularized regression method for fitting linear regression models that linearly combines hello L1 and L2 metrics as penalties of hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="788fb-143">Merhaba Spark Mllib'i Araç Seti büyük veri kümeleri üzerinde tasarlanmış toowork olsa da, nispeten küçük bir örnek (yaklaşık 30 170 K satır, yaklaşık hello özgün NYC dataset %0,1 kullanarak Mb) burada kolaylık sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="788fb-143">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="788fb-144">burada verilen hello alıştırma verimli bir şekilde (yaklaşık 10 dakika cinsinden) 2 çalışan düğümleri ile bir Hdınsight kümesi üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="788fb-144">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="788fb-145">Merhaba küçük değişiklikler içeren aynı kodu kullanılan tooprocess daha büyük veri-kümeleriyle, verileri bellekte önbelleğe alma ve hello küme boyutunu değiştirmek için uygun değişiklikleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-145">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="788fb-146">Kurulum: Spark kümeleri ve dizüstü bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="788fb-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="788fb-147">Kurulum adımlarını ve kod bu kılavuzda bir Hdınsight Spark 1.6 kullanmak için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="788fb-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="788fb-148">Ancak Jupyter not defterleri Hdınsight Spark 1.6 ve Spark 2.0 kümeleri için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="788fb-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="788fb-149">Merhaba not defterlerini ve bağlantıları toothem açıklamasını hello sağlanan [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) bunları içeren hello GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="788fb-149">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="788fb-150">Ayrıca, hello kod burada ve bağlı hello not defterlerini geneldir ve tüm Spark kümesi üzerinde çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="788fb-150">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="788fb-151">Hdınsight Spark kullanmıyorsanız hello Küme kurulumu ve Yönetimi adımları ne burada gösterilenden biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-151">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="788fb-152">Kolaylık olması için Spark 1.6 ve 2.0 toobe hello pyspark Çekirdeği'nde hello Jupyter not defteri sunucu, çalıştırmak için hello bağlantılar toohello Jupyter not defterleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="788fb-152">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 and 2.0 toobe run in hello pyspark kernel of hello Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="788fb-153">Spark 1.6 dizüstü bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="788fb-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="788fb-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Not Defteri #1 ve hyperparameter ayarlama ve çapraz doğrulama kullanarak modeli geliştirme konuları içerir.</span><span class="sxs-lookup"><span data-stu-id="788fb-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="788fb-155">Spark 2.0 dizüstü bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="788fb-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="788fb-156">[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Bu dosyayı nasıl tooperform veri keşfi, model oluşturma ve Spark 2. 0'Puanlama kümeleri hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="788fb-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="788fb-157">Kurulumu: Spark bağlam depolama konumları, kitaplıklar ve hello hazır</span><span class="sxs-lookup"><span data-stu-id="788fb-157">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="788fb-158">Spark mümkün tooread ve yazma tooAzure depolama blobu (WASB olarak da bilinir) olur.</span><span class="sxs-lookup"><span data-stu-id="788fb-158">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="788fb-159">Bu nedenle depolanan mevcut verilerinizi Spark kullanarak işlenebilir ve depolanan yeniden WASB hello sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="788fb-159">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="788fb-160">toosave modelleri veya WASB dosyalarında, hello yolu düzgün belirtilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="788fb-160">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="788fb-161">Merhaba varsayılan kapsayıcı bağlı toohello Spark kümesi ile başlayan bir yol kullanarak başvurulabilir: "wasb: / / /".</span><span class="sxs-lookup"><span data-stu-id="788fb-161">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="788fb-162">Başka konumlara tarafından başvurulan "wasb: / /".</span><span class="sxs-lookup"><span data-stu-id="788fb-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="788fb-163">Dizin yolları için depolama konumları WASB ayarlayın</span><span class="sxs-lookup"><span data-stu-id="788fb-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="788fb-164">Hello aşağıdaki kod örneği hello konumunu okuma hello veri toobe belirtir ve hello modeli depolama dizini toowhich hello modeli çıktı hello yolu kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="788fb-164">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="788fb-165">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-165">**OUTPUT**</span></span>

<span data-ttu-id="788fb-166">DateTime.DateTime (2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="788fb-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="788fb-167">Kitaplıkları içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="788fb-167">Import libraries</span></span>
<span data-ttu-id="788fb-168">Gerekli kitaplıkları ile koddan hello içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="788fb-168">Import necessary libraries with hello following code:</span></span>

    # LOAD PYSPARK LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="788fb-169">Spark bağlamını ve PySpark sihirler hazır</span><span class="sxs-lookup"><span data-stu-id="788fb-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="788fb-170">Jupyter not defterleri ile sağlanan hello PySpark tekrar önceden belirlenmiş bir içerik var.</span><span class="sxs-lookup"><span data-stu-id="788fb-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="788fb-171">Geliştirdiğiniz Merhaba uygulaması ile çalışmaya başlamadan önce bu nedenle, tooset hello Spark veya Hive bağlamları açıkça gerekmez.</span><span class="sxs-lookup"><span data-stu-id="788fb-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="788fb-172">Bu içerikler varsayılan olarak sizin için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-172">These contexts are available for you by default.</span></span> <span data-ttu-id="788fb-173">Bu içerikler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="788fb-173">These contexts are:</span></span>

* <span data-ttu-id="788fb-174">SC - Spark</span><span class="sxs-lookup"><span data-stu-id="788fb-174">sc - for Spark</span></span> 
* <span data-ttu-id="788fb-175">sqlContext - Hive için</span><span class="sxs-lookup"><span data-stu-id="788fb-175">sqlContext - for Hive</span></span>

<span data-ttu-id="788fb-176">Merhaba PySpark çekirdeği bazı önceden tanımlanmış "sihirleri" ile çağırabilir özel komutlar olduğu sağlar %%.</span><span class="sxs-lookup"><span data-stu-id="788fb-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="788fb-177">Bu kod örneklerinde kullanılan olan iki komut vardır.</span><span class="sxs-lookup"><span data-stu-id="788fb-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="788fb-178">**%% yerel** sonraki satırların hello kodda yerel olarak yürütülen toobe olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="788fb-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="788fb-179">Kod geçerli Python kodu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="788fb-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="788fb-180">**%% sql -o <variable name>**  hello sqlContext bir Hive sorgusu yürütür.</span><span class="sxs-lookup"><span data-stu-id="788fb-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="788fb-181">Merhaba -o parametre aktarılırsa hello hello sorgunun sonucu hello kalıcı %% Pandas DataFrame olarak yerel Python bağlamı.</span><span class="sxs-lookup"><span data-stu-id="788fb-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="788fb-182">Hello tekrar Jupyter not defterlerini ve önceden tanımlanmış hello hakkında daha fazla bilgi "magics için" sağladıkları, bkz: [Jupyter not defterlerinde kullanılabilen çekirdekler Hdınsight Spark Linux kümeleri Hdınsight'ta](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="788fb-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="788fb-183">Veri alımı ortak blob gelen:</span><span class="sxs-lookup"><span data-stu-id="788fb-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="788fb-184">Merhaba ilk hello veri bilimi işlemi tooingest hello veri toobe veri keşfi ve modelleme ortamınıza bulunduğu kaynaklardan analiz adımdır.</span><span class="sxs-lookup"><span data-stu-id="788fb-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="788fb-185">Bu Spark bu kılavuzda ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="788fb-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="788fb-186">Bu bölümde hello kod toocomplete bir dizi görev içerir:</span><span class="sxs-lookup"><span data-stu-id="788fb-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="788fb-187">Merhaba veri örnek toobe Modellenen alma</span><span class="sxs-lookup"><span data-stu-id="788fb-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="788fb-188">(.tsv dosyası olarak depolanır) hello girdi veri kümesi okuyun</span><span class="sxs-lookup"><span data-stu-id="788fb-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="788fb-189">Biçim ve temiz hello verileri</span><span class="sxs-lookup"><span data-stu-id="788fb-189">format and clean hello data</span></span>
* <span data-ttu-id="788fb-190">oluşturma ve nesneleri (RDDs veya veri çerçevelerini) bellekte önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="788fb-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="788fb-191">SQL bağlam tabloda geçici olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="788fb-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="788fb-192">Veri alımı için hello kod aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="788fb-192">Here is hello code for data ingestion.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="788fb-193">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-193">**OUTPUT**</span></span>

<span data-ttu-id="788fb-194">Hücre tooexecute geçen süre: 276.62 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-194">Time taken tooexecute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="788fb-195">Veri keşfi & Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="788fb-195">Data exploration & visualization</span></span>
<span data-ttu-id="788fb-196">Hello veri Spark alındıktan sonra hello sonraki hello veri bilimi işlemi hello veri keşfi ve görselleştirme aracılığıyla daha derin anlayış toogain adımdır.</span><span class="sxs-lookup"><span data-stu-id="788fb-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="788fb-197">Bu bölümde, SQL sorguları ve çizim hello hedef değişkenleri ve olası özellikleri için görsel denetleme kullanarak hello ücreti verileri inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="788fb-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="788fb-198">Özellikle, yolcu sayıları ücreti dönüşleri, ipucu tutarlar hello sıklığını ve nasıl ipuçları ödeme tutar ve türüne göre farklılık hello sıklığını çizmek.</span><span class="sxs-lookup"><span data-stu-id="788fb-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="788fb-199">Histogram yolcu sayısı frekansların ücreti dönüşleri hello örnekteki Çiz</span><span class="sxs-lookup"><span data-stu-id="788fb-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="788fb-200">Bu kodu ve sonraki parçacıkları SQL Sihirli tooquery hello örnek ve yerel Sihirli tooplot hello verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="788fb-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="788fb-201">**SQL Sihirli (`%%sql`)** hello Hdınsight PySpark çekirdeği kolay satır içi HiveQL sorguları hello sqlContext karşı destekler.</span><span class="sxs-lookup"><span data-stu-id="788fb-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="788fb-202">Merhaba (-o deðiþken_adý) bağımsız değişkeni devam ederse hello SQL sorgusu hello çıktısını hello Jupyter sunucuda Pandas DataFrame olarak.</span><span class="sxs-lookup"><span data-stu-id="788fb-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="788fb-203">Bu, hello yerel modda kullanılabilir olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="788fb-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="788fb-204">Merhaba  **`%%local` Sihirli** olan toorun kod hello headnode hello Hdınsight kümesinin olduğu hello Jupyter sunucu üzerinde yerel olarak kullanılan.</span><span class="sxs-lookup"><span data-stu-id="788fb-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="788fb-205">Genellikle, kullandığınız `%%local` hello sonra Sihirli `%%sql -o` Sihirli olduğu kullanılan toorun bir sorgu.</span><span class="sxs-lookup"><span data-stu-id="788fb-205">Typically, you use `%%local` magic after hello `%%sql -o` magic is used toorun a query.</span></span> <span data-ttu-id="788fb-206">Merhaba -o parametresi yerel olarak hello SQL sorgusu hello çıktısını kalıcı.</span><span class="sxs-lookup"><span data-stu-id="788fb-206">hello -o parameter would persist hello output of hello SQL query locally.</span></span> <span data-ttu-id="788fb-207">Ardından hello `%%local` Sihirli Tetikleyicileri hello kod parçacıkları toorun yerel olarak yerel olarak kalıcı hello çıktı hello SQL sorgularının karşı sonraki kümesi.</span><span class="sxs-lookup"><span data-stu-id="788fb-207">Then hello `%%local` magic triggers hello next set of code snippets toorun locally against hello output of hello SQL queries that has been persisted locally.</span></span> <span data-ttu-id="788fb-208">Merhaba kod çalıştırdıktan sonra hello çıkış otomatik olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="788fb-208">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="788fb-209">Bu sorgu hello dönüşleri yolcu sayısına göre alır.</span><span class="sxs-lookup"><span data-stu-id="788fb-209">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="788fb-210">Bu kod bir yerel veri çerçevesi hello sorgu çıktısı oluşturur ve hello veri çizer.</span><span class="sxs-lookup"><span data-stu-id="788fb-210">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="788fb-211">Merhaba `%%local` Sihirli oluşturur çerçeve, yerel veri `sqlResults`, kullanılabileceği ile matplotlib çizdirmek için.</span><span class="sxs-lookup"><span data-stu-id="788fb-211">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="788fb-212">Bu PySpark Sihirli birden çok kez bu kılavuzda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="788fb-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="788fb-213">Merhaba miktarda veri büyükse, toocreate yerel belleğe sığması bir veri-çerçeve örnek.</span><span class="sxs-lookup"><span data-stu-id="788fb-213">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="788fb-214">Sayıları tarafından yolcu hello kod tooplot hello dönüşleri İşte</span><span class="sxs-lookup"><span data-stu-id="788fb-214">Here is hello code tooplot hello trips by passenger counts</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="788fb-215">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-215">**OUTPUT**</span></span>

![Dönüş yolcu sayısına göre sıklığı](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="788fb-217">Hello kullanarak birkaç farklı türde görselleştirmeleri (tablo, pasta, çizgi, alan veya çubuğu) arasında seçebilirsiniz **türü** menü düğmelerini hello Not.</span><span class="sxs-lookup"><span data-stu-id="788fb-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="788fb-218">Merhaba çubuğu çizim burada gösterilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-218">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="788fb-219">Çizim histogram ipucu tutarlar ve nasıl ipucu tutar yolcu sayısı ve ücreti tutarlar göre değişir.</span><span class="sxs-lookup"><span data-stu-id="788fb-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="788fb-220">Bir SQL sorgusu toosample verileri kullanmak...</span><span class="sxs-lookup"><span data-stu-id="788fb-220">Use a SQL query toosample data..</span></span>

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


<span data-ttu-id="788fb-221">Bu kod hücresini hello SQL sorgu toocreate üç çizimleri hello verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="788fb-221">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


<span data-ttu-id="788fb-222">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="788fb-222">**OUTPUT:**</span></span> 

![İpucu tutar dağıtımı](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Yolcu sayısına göre ipucu tutar](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Tutarı Tutar ücreti tarafından İpucu](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="788fb-226">Modelleme mühendislik, dönüştürme ve veri hazırlığı özelliği</span><span class="sxs-lookup"><span data-stu-id="788fb-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="788fb-227">Bu bölümde açıklar ve ML modelleme kullanmak için tooprepare veri hello kod yordamları için kullanılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="788fb-227">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="788fb-228">Bunu nasıl toodo hello aşağıdaki görevleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="788fb-228">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="788fb-229">Yeni bir özellik saatleri trafiği zaman depo bölümleme tarafından oluşturma</span><span class="sxs-lookup"><span data-stu-id="788fb-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="788fb-230">Dizin ve üzerinde hot kategorik özellikleri kodlama</span><span class="sxs-lookup"><span data-stu-id="788fb-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="788fb-231">ML işlevleri giriş etiketli noktası nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="788fb-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="788fb-232">Rastgele bir alt örnekleme hello veri oluşturun ve eğitim ve test kümesi olarak bölme</span><span class="sxs-lookup"><span data-stu-id="788fb-232">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="788fb-233">Ölçeklendirme özelliği</span><span class="sxs-lookup"><span data-stu-id="788fb-233">Feature scaling</span></span>
* <span data-ttu-id="788fb-234">Bellek önbelleği nesneleri</span><span class="sxs-lookup"><span data-stu-id="788fb-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="788fb-235">Depo trafiği kez bölümleme tarafından yeni bir özellik oluşturma</span><span class="sxs-lookup"><span data-stu-id="788fb-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="788fb-236">Bu kod toocreate trafiği bölümleme tarafından yeni bir özellik depo nasıl zaman ve ardından nasıl toocache hello bellek ortaya çıkan veri çerçevede gösterir.</span><span class="sxs-lookup"><span data-stu-id="788fb-236">This code shows how toocreate a new feature by partitioning traffic times into bins and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="788fb-237">Tooimproved yürütme süresi, önbelleğe alma dayanıklı Dağıtılmış veri kümeleri (RDDs) ve veri çerçevelerini art arda kullanıldığı yol açar.</span><span class="sxs-lookup"><span data-stu-id="788fb-237">Caching leads tooimproved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="788fb-238">Bu nedenle, biz RDDs ve veri çerçevelerini bu kılavuz çeşitli aşamalarında önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="788fb-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="788fb-239">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-239">**OUTPUT**</span></span>

<span data-ttu-id="788fb-240">126050</span><span class="sxs-lookup"><span data-stu-id="788fb-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="788fb-241">Dizini oluşturmak ve bir hot kategorik özellikleri kodlama</span><span class="sxs-lookup"><span data-stu-id="788fb-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="788fb-242">Bu bölümde gösterilmiştir nasıl tooindex veya İşlevler modelleme hello giriş için kategorik özellikleri kodlayın.</span><span class="sxs-lookup"><span data-stu-id="788fb-242">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="788fb-243">Modelleme hello ve Mllib'i işlevlerini kategorik giriş verisi özelliklerle dizine veya kodlanmış dikkat gerektiren tahmin önceki toouse.</span><span class="sxs-lookup"><span data-stu-id="788fb-243">hello modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior toouse.</span></span> 

<span data-ttu-id="788fb-244">Merhaba modeline bağlı olarak farklı şekillerde kodlamak olmak veya tooindex gerekir.</span><span class="sxs-lookup"><span data-stu-id="788fb-244">Depending on hello model, you need tooindex or encode them in different ways.</span></span> <span data-ttu-id="788fb-245">Örneğin, Logistic ve doğrusal regresyon modeli bir hot kodlama, burada gerektirir, örneğin, üç kategoriye sahip bir özellik içeren her 0 veya 1 bir gözlem hello kategorisine bağlı olarak üç özellik sütunlara genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="788fb-246">Mllib'i sağlar [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) bir hot toodo kodlama işlev.</span><span class="sxs-lookup"><span data-stu-id="788fb-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="788fb-247">Bu Kodlayıcı sütununun etiket dizinlerini tooa ikili vektörler, en çok bir değerle tek bir-bir sütun eşler.</span><span class="sxs-lookup"><span data-stu-id="788fb-247">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="788fb-248">Bu kodlama Lojistik regresyon gibi sayısal değerli özellikleri beklediğiniz algoritmalarına olanak uygulanan toobe toocategorical özellikleri.</span><span class="sxs-lookup"><span data-stu-id="788fb-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="788fb-249">Kategorik özellikleri kodlanacağını ve kod tooindex hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="788fb-249">Here is hello code tooindex and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="788fb-250">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-250">**OUTPUT**</span></span>

<span data-ttu-id="788fb-251">Hücre tooexecute geçen süre: 3.14 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-251">Time taken tooexecute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="788fb-252">ML işlevleri giriş etiketli noktası nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="788fb-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="788fb-253">Bu bölüm, etiketlenmiş noktası veri olarak tooindex kategorik metin veri türü nasıl ve ne gösteren kod içerir tooencode onu.</span><span class="sxs-lookup"><span data-stu-id="788fb-253">This section contains code that shows how tooindex categorical text data as a labeled point data type and how tooencode it.</span></span> <span data-ttu-id="788fb-254">Bu, kullanılan toobe tootrain ve test Mllib'i Lojistik regresyon ve diğer sınıflandırma modelleri hazırlar.</span><span class="sxs-lookup"><span data-stu-id="788fb-254">This prepares it toobe used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="788fb-255">Etiketli noktası, esnek Dağıtılmış veri kümeleri (RDD) girdi verisi olarak Mllib'i ML algoritmalara çoğu tarafından gerektiği şekilde biçimlendirilmiş nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="788fb-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="788fb-256">A [noktası etiketli](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) yerel bir vektör, yoğun veya seyrek, etiket/yanıt ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="788fb-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="788fb-257">İşte kod tooindex hello ve ikili sınıflandırma için metin özellikleri kodlayın.</span><span class="sxs-lookup"><span data-stu-id="788fb-257">Here is hello code tooindex and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="788fb-258">Doğrusal regresyon çözümlemesi için tooencode ve dizin kategorik metin özelliklerinden hello kod aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="788fb-258">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="788fb-259">Rastgele bir alt örnekleme hello veri oluşturun ve eğitim ve test kümesi olarak bölme</span><span class="sxs-lookup"><span data-stu-id="788fb-259">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="788fb-260">Bu kod bir rastgele örnekleme (% 25 burada kullanılır) hello veri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="788fb-260">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="788fb-261">Bu örneğin hello kümesinin toohello boyutu nedeniyle gerekli olmamasına karşın, burada hello verileri nasıl örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="788fb-261">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample hello data here.</span></span> <span data-ttu-id="788fb-262">Bildiğiniz sonra nasıl toouse gerekirse kendi sorunu için.</span><span class="sxs-lookup"><span data-stu-id="788fb-262">Then you know how toouse it for your own problem if needed.</span></span> <span data-ttu-id="788fb-263">Örnekleri büyük olduğunda bu eğitim modelleri sırasında önemli zamandan tasarruf edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="788fb-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="788fb-264">Sonraki biz hello örnek eğitim bölümü (burada %75) ve bir test bölümü (% 25 burada) toouse sınıflandırma ve regresyon modelleme bölün.</span><span class="sxs-lookup"><span data-stu-id="788fb-264">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="788fb-265">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-265">**OUTPUT**</span></span>

<span data-ttu-id="788fb-266">Hücre tooexecute geçen süre: 0.31 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-266">Time taken tooexecute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="788fb-267">Ölçeklendirme özelliği</span><span class="sxs-lookup"><span data-stu-id="788fb-267">Feature scaling</span></span>
<span data-ttu-id="788fb-268">Özellik ölçeklendirme, veri normalleştirme da bilinen, yaygın olarak yapılan değerlerle özellikleri olan belirli bir aşırı tartmanız olduğunu hello hedefi işlevinde oluşturmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="788fb-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="788fb-269">Merhaba özelliği ölçeklendirmeye yönelik kodu kullanan hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello özellikleri toounit farkı.</span><span class="sxs-lookup"><span data-stu-id="788fb-269">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="788fb-270">Doğrusal regresyon ile Stokastik gradyan düşüşü (SGD) kullanmak için Mllib'i tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="788fb-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="788fb-271">SGD diğer machine learning modellerini regularized gerileme veya destek vektör makineler (SVM) gibi çeşitli eğitim için yaygın olarak kullanılan bir algoritmadır.</span><span class="sxs-lookup"><span data-stu-id="788fb-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="788fb-272">Merhaba LinearRegressionWithSGD algoritması toobe hassas toofeature ölçeklendirme bulduk.</span><span class="sxs-lookup"><span data-stu-id="788fb-272">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>   
> 
> 

<span data-ttu-id="788fb-273">Merhaba kod tooscale değişkenlerinin regularized hello doğrusal SGD algoritması ile kullanmak için aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="788fb-273">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="788fb-274">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-274">**OUTPUT**</span></span>

<span data-ttu-id="788fb-275">Hücre tooexecute geçen süre: 11.67 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-275">Time taken tooexecute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="788fb-276">Bellek önbelleği nesneleri</span><span class="sxs-lookup"><span data-stu-id="788fb-276">Cache objects in memory</span></span>
<span data-ttu-id="788fb-277">Eğitim ve ML algoritmalardan sınamak için harcanan hello süre nesneleri için sınıflandırma, regresyon kullanılan ve özellikleri ölçeklendirilmiş hello giriş verisi çerçeve önbelleğe alarak azaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-277">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression and, scaled features.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="788fb-278">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-278">**OUTPUT**</span></span> 

<span data-ttu-id="788fb-279">Hücre tooexecute geçen süre: 0,13 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-279">Time taken tooexecute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="788fb-280">Bir ipucu ile ikili sınıflandırma modelleri Ücretli olsun veya olmasın tahmin etme</span><span class="sxs-lookup"><span data-stu-id="788fb-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="788fb-281">Bu bölümde, bir ipucu ücreti seyahat için ücretli olup olmadığına bakılmaksızın kullanım üç tahmin etmeye hello ikili sınıflandırma görevi için nasıl modeller gösterir.</span><span class="sxs-lookup"><span data-stu-id="788fb-281">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="788fb-282">sunulan hello model şunlardır:</span><span class="sxs-lookup"><span data-stu-id="788fb-282">hello models presented are:</span></span>

* <span data-ttu-id="788fb-283">Lojistik regresyon</span><span class="sxs-lookup"><span data-stu-id="788fb-283">Logistic regression</span></span> 
* <span data-ttu-id="788fb-284">Rastgele orman</span><span class="sxs-lookup"><span data-stu-id="788fb-284">Random forest</span></span>
* <span data-ttu-id="788fb-285">Gradyan artırma ağaçları</span><span class="sxs-lookup"><span data-stu-id="788fb-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="788fb-286">Her model kod bölümünde oluşturma adımları ayrılır:</span><span class="sxs-lookup"><span data-stu-id="788fb-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="788fb-287">**Eğitim modeli** bir parametre kümesi ile verileri</span><span class="sxs-lookup"><span data-stu-id="788fb-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="788fb-288">**Model değerlendirme** ölçümlerle sınama veri kümesi üzerinde</span><span class="sxs-lookup"><span data-stu-id="788fb-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="788fb-289">**Model kaydetme** gelecekteki tüketimi için blob içinde</span><span class="sxs-lookup"><span data-stu-id="788fb-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="788fb-290">Gösteriyoruz nasıl toodo çapraz doğrulama (MS) iki yolla yerleştirmez parametresiyle:</span><span class="sxs-lookup"><span data-stu-id="788fb-290">We show how toodo cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="788fb-291">Kullanarak **genel** uygulanan tooany algoritması Mllib'i ve tooany parametresinde olabilen özel kod bir algoritma ayarlar.</span><span class="sxs-lookup"><span data-stu-id="788fb-291">Using **generic** custom code which can be applied tooany algorithm in MLlib and tooany parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="788fb-292">Hello kullanarak **pySpark CrossValidator ardışık düzen işlevi**.</span><span class="sxs-lookup"><span data-stu-id="788fb-292">Using hello **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="788fb-293">Not CrossValidator Spark 1.5.0 için birkaç sınırlamalara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="788fb-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="788fb-294">Gelecekteki tüketimi için kaydedilen/kalıcı ardışık düzen modelleri olamaz.</span><span class="sxs-lookup"><span data-stu-id="788fb-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="788fb-295">Bir modeldeki her parametre için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="788fb-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="788fb-296">Her Mllib'i algoritması için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="788fb-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="788fb-297">Doğrulama ve ikili sınıflandırma hello Lojistik regresyon algoritması ile kullanılan hyperparameter Süpürme çapraz genel</span><span class="sxs-lookup"><span data-stu-id="788fb-297">Generic cross validation and hyperparameter sweeping used with hello logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="788fb-298">Bu bölümdeki Hello kod gösterir nasıl tootrain, değerlendirmek ve lojistik regresyon modeli ile Kaydet [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) tahmin bir ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın.</span><span class="sxs-lookup"><span data-stu-id="788fb-298">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="788fb-299">Merhaba model doğrulama (MS) ve Mllib'i algoritmalara öğrenme Merhaba, uygulanan tooany olabilir özel kod ile uygulanan hyperparameter Süpürme çapraz kullanarak eğitildi.</span><span class="sxs-lookup"><span data-stu-id="788fb-299">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied tooany of hello learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="788fb-300">Bu özel MS kod Hello yürütmeyi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-300">hello execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="788fb-301">**MS ve hyperparameter Süpürme kullanarak hello Lojistik regresyon modelini eğitme**</span><span class="sxs-lookup"><span data-stu-id="788fb-301">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="788fb-302">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-302">**OUTPUT**</span></span>

<span data-ttu-id="788fb-303">Katsayısını: [0.0082065285375-0.0223675576104,-0.0183812028036, - 3.48124578069e-05-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="788fb-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="788fb-304">Intercept:-0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="788fb-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="788fb-305">Hücre tooexecute geçen süre: 14.43 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-305">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="788fb-306">**Standart ölçümlerle Hello ikili sınıflandırma modelini değerlendir**</span><span class="sxs-lookup"><span data-stu-id="788fb-306">**Evaluate hello binary classification model with standard metrics**</span></span>

<span data-ttu-id="788fb-307">Bu bölümdeki Hello kodunu nasıl tooevaluate Lojistik regresyon modeli test verileri-hello ROC eğrisi, bir çizim dahil olmak üzere küme karşı gösterir.</span><span class="sxs-lookup"><span data-stu-id="788fb-307">hello code in this section shows how tooevaluate a logistic regression model against a test data-set, including a plot of hello ROC curve.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="788fb-308">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-308">**OUTPUT**</span></span>

<span data-ttu-id="788fb-309">PR alanında 0.985336538462 =</span><span class="sxs-lookup"><span data-stu-id="788fb-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="788fb-310">ROC alanında 0.983383274312 =</span><span class="sxs-lookup"><span data-stu-id="788fb-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="788fb-311">Özet istatistikleri</span><span class="sxs-lookup"><span data-stu-id="788fb-311">Summary Stats</span></span>

<span data-ttu-id="788fb-312">Duyarlık 0.984174341679 =</span><span class="sxs-lookup"><span data-stu-id="788fb-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="788fb-313">Geri çağırma 0.984174341679 =</span><span class="sxs-lookup"><span data-stu-id="788fb-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="788fb-314">F1 Puan 0.984174341679 =</span><span class="sxs-lookup"><span data-stu-id="788fb-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="788fb-315">Hücre tooexecute geçen süre: 2.67 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-315">Time taken tooexecute above cell: 2.67 seconds</span></span>

<span data-ttu-id="788fb-316">**Merhaba ROC eğrisi çizme.**</span><span class="sxs-lookup"><span data-stu-id="788fb-316">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="788fb-317">Merhaba *predictionAndLabelsDF* bir tablo olarak kayıtlı *tmp_results*, hello önceki hücrenin.</span><span class="sxs-lookup"><span data-stu-id="788fb-317">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="788fb-318">*tmp_results* kullanılan toodo sorgu ve sonuçları çerçevesine hello sqlResults verileri-çizdirmek için çıktı.</span><span class="sxs-lookup"><span data-stu-id="788fb-318">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="788fb-319">Merhaba kod aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="788fb-319">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="788fb-320">İşte, hello kod toomake Öngörüler ve çizim hello ROC eğrisi.</span><span class="sxs-lookup"><span data-stu-id="788fb-320">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="788fb-321">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-321">**OUTPUT**</span></span>

![Lojistik regresyon ROC eğrisi genel yaklaşım için](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="788fb-323">**Gelecekte kullanım için bir blob modelinde Sürdür**</span><span class="sxs-lookup"><span data-stu-id="788fb-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="788fb-324">Bu bölümdeki Hello kodu nasıl toosave hello Lojistik regresyon modeli tüketimi için gösterilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-324">hello code in this section shows how toosave hello logistic regression model for consumption.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="788fb-325">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-325">**OUTPUT**</span></span>

<span data-ttu-id="788fb-326">Hücre tooexecute geçen süre: 34.57 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-326">Time taken tooexecute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="788fb-327">Lojistik regresyon (esnek regresyon) modeliyle Mllib'i'nın CrossValidator ardışık düzen işlevini kullanın</span><span class="sxs-lookup"><span data-stu-id="788fb-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="788fb-328">Bu bölümdeki Hello kod gösterir nasıl tootrain, değerlendirmek ve lojistik regresyon modeli ile Kaydet [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) tahmin bir ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın.</span><span class="sxs-lookup"><span data-stu-id="788fb-328">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="788fb-329">Çapraz doğrulama (MS) kullanarak Hello modeli eğitildi ve hyperparameter Süpürme ile Merhaba Mllib'i CrossValidator ardışık düzen işlevi için MS parametre tarama ile uygulanan.</span><span class="sxs-lookup"><span data-stu-id="788fb-329">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with hello MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="788fb-330">Bu Mllib'i MS kod Hello yürütmeyi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-330">hello execution of this MLlib CV code can take several minutes.</span></span>
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="788fb-331">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-331">**OUTPUT**</span></span>

<span data-ttu-id="788fb-332">Hücre tooexecute geçen süre: 107.98 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-332">Time taken tooexecute above cell: 107.98 seconds</span></span>

<span data-ttu-id="788fb-333">**Merhaba ROC eğrisi çizme.**</span><span class="sxs-lookup"><span data-stu-id="788fb-333">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="788fb-334">Merhaba *predictionAndLabelsDF* bir tablo olarak kayıtlı *tmp_results*, hello önceki hücrenin.</span><span class="sxs-lookup"><span data-stu-id="788fb-334">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="788fb-335">*tmp_results* kullanılan toodo sorgu ve sonuçları çerçevesine hello sqlResults verileri-çizdirmek için çıktı.</span><span class="sxs-lookup"><span data-stu-id="788fb-335">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="788fb-336">Merhaba kod aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="788fb-336">Here is hello code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="788fb-337">Merhaba kod tooplot hello ROC eğrisi aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="788fb-337">Here is hello code tooplot hello ROC curve.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="788fb-338">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-338">**OUTPUT**</span></span>

![Mllib'i'nın CrossValidator kullanarak Lojistik regresyon ROC eğrisi](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="788fb-340">Rastgele orman sınıflandırma</span><span class="sxs-lookup"><span data-stu-id="788fb-340">Random forest classification</span></span>
<span data-ttu-id="788fb-341">Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın tahmin rastgele orman regresyon kaydedin gösterir.</span><span class="sxs-lookup"><span data-stu-id="788fb-341">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="788fb-342">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-342">**OUTPUT**</span></span>

<span data-ttu-id="788fb-343">ROC alanında 0.985336538462 =</span><span class="sxs-lookup"><span data-stu-id="788fb-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="788fb-344">Hücre tooexecute geçen süre: 26.72 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-344">Time taken tooexecute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="788fb-345">Gradyan artırma ağaçları sınıflandırma</span><span class="sxs-lookup"><span data-stu-id="788fb-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="788fb-346">Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın tahmin bir gradyan artırma ağaçları modeli kaydedin gösterir.</span><span class="sxs-lookup"><span data-stu-id="788fb-346">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="788fb-347">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-347">**OUTPUT**</span></span>

<span data-ttu-id="788fb-348">ROC alanında 0.985336538462 =</span><span class="sxs-lookup"><span data-stu-id="788fb-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="788fb-349">Hücre tooexecute geçen süre: 28.13 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-349">Time taken tooexecute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="788fb-350">İpucu tutar (MS kullanarak değil) regresyon modelleriyle tahmin etme</span><span class="sxs-lookup"><span data-stu-id="788fb-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="788fb-351">Bu bölümde nasıl hello regresyon görev için üç kullanım modelleri gösterir: tahmin diğer ipucu özelliklerini temel alarak ücreti seyahat için ücretli hello ipucu tutar.</span><span class="sxs-lookup"><span data-stu-id="788fb-351">This section shows how use three models for hello regression task: predict hello tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="788fb-352">sunulan hello model şunlardır:</span><span class="sxs-lookup"><span data-stu-id="788fb-352">hello models presented are:</span></span>

* <span data-ttu-id="788fb-353">Regularized doğrusal regresyon</span><span class="sxs-lookup"><span data-stu-id="788fb-353">Regularized linear regression</span></span>
* <span data-ttu-id="788fb-354">Rastgele orman</span><span class="sxs-lookup"><span data-stu-id="788fb-354">Random forest</span></span>
* <span data-ttu-id="788fb-355">Gradyan artırma ağaçları</span><span class="sxs-lookup"><span data-stu-id="788fb-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="788fb-356">Bu modeller hello girişte açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="788fb-356">These models were described in hello introduction.</span></span> <span data-ttu-id="788fb-357">Her model kod bölümünde oluşturma adımları ayrılır:</span><span class="sxs-lookup"><span data-stu-id="788fb-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="788fb-358">**Eğitim modeli** bir parametre kümesi ile verileri</span><span class="sxs-lookup"><span data-stu-id="788fb-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="788fb-359">**Model değerlendirme** ölçümlerle sınama veri kümesi üzerinde</span><span class="sxs-lookup"><span data-stu-id="788fb-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="788fb-360">**Model kaydetme** gelecekteki tüketimi için blob içinde</span><span class="sxs-lookup"><span data-stu-id="788fb-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="788fb-361">AZURE Not: Bu hello Lojistik regresyon modelleri için ayrıntılı gösterildi olduğundan çapraz doğrulama hello üç regresyon modeli, bu bölümde ile kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="788fb-361">AZURE NOTE: Cross-validation is not used with hello three regression models in this section, since this was shown in detail for hello logistic regression models.</span></span> <span data-ttu-id="788fb-362">Merhaba, bu konunun ek toouse MS esnek Net ile doğrusal regresyon için nasıl sağlandığını gösteren bir örnek.</span><span class="sxs-lookup"><span data-stu-id="788fb-362">An example showing how toouse CV with Elastic Net for linear regression is provided in hello Appendix of this topic.</span></span>
> 
> <span data-ttu-id="788fb-363">AZURE Not: deneyimi bizim olabilir yakınsama LinearRegressionWithSGD modellerin ile ilgili sorunları ve parametreleri değiştirilen/dikkatle geçerli bir model almak için en iyi duruma getirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="788fb-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="788fb-364">Değişkenleri önemli ölçüde ölçeklendirmeyi yakınsama yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="788fb-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="788fb-365">Merhaba ek toothis konuda gösterilen esnek net regresyon de LinearRegressionWithSGD yerine kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-365">Elastic net regression, shown in hello Appendix toothis topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="788fb-366">Doğrusal regresyon SGD ile</span><span class="sxs-lookup"><span data-stu-id="788fb-366">Linear regression with SGD</span></span>
<span data-ttu-id="788fb-367">Merhaba kod bu bölümdeki toouse özellikleri tootrain iyileştirme için stokastik gradyan düşüşü (SGD) kullanan bir doğrusal regresyon nasıl ölçeklendirilmesi gösterir ve tooscore, değerlendirmek ve Azure Blob Storage (WASB) hello modeli kaydedin.</span><span class="sxs-lookup"><span data-stu-id="788fb-367">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="788fb-368">Deneyimi bizim LinearRegressionWithSGD modellerin hello yakınsama sorunları olabilir ve parametreleri değiştirilen/dikkatle geçerli bir model almak için en iyi duruma getirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="788fb-368">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="788fb-369">Değişkenleri önemli ölçüde ölçeklendirmeyi yakınsama yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="788fb-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="788fb-370">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-370">**OUTPUT**</span></span>

<span data-ttu-id="788fb-371">Katsayısını: [0.0141707753435,-0.0252930927087,-0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092,-0.00456498588241,-0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632,-0.00289545676449,-0.00791124681938, 0.54396316518,-0.536293513569, 0.0119076553369,-0.0173039244582, 0.0119632796147, 0.00146764882502]</span><span class="sxs-lookup"><span data-stu-id="788fb-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="788fb-372">Intercept: 0.854507624459</span><span class="sxs-lookup"><span data-stu-id="788fb-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="788fb-373">RMSE 1.23485131376 =</span><span class="sxs-lookup"><span data-stu-id="788fb-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="788fb-374">R sqr 0.597963951127 =</span><span class="sxs-lookup"><span data-stu-id="788fb-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="788fb-375">Hücre tooexecute geçen süre: 38.62 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-375">Time taken tooexecute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="788fb-376">Rastgele orman regresyon</span><span class="sxs-lookup"><span data-stu-id="788fb-376">Random Forest regression</span></span>
<span data-ttu-id="788fb-377">Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve hello NYC ücreti seyahat veri ipucu tutarını tahmin rastgele orman modeli kaydedin gösterir.</span><span class="sxs-lookup"><span data-stu-id="788fb-377">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts tip amount for hello NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="788fb-378">Çapraz doğrulama özel kod kullanarak yerleştirmez parametresiyle hello ekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="788fb-378">Cross-validation with parameter sweeping using custom code is provided in hello appendix.</span></span>
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="788fb-379">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-379">**OUTPUT**</span></span>

<span data-ttu-id="788fb-380">RMSE 0.931981967875 =</span><span class="sxs-lookup"><span data-stu-id="788fb-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="788fb-381">R sqr 0.733445485802 =</span><span class="sxs-lookup"><span data-stu-id="788fb-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="788fb-382">Hücre tooexecute geçen süre: 25.98 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-382">Time taken tooexecute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="788fb-383">Gradyan artırma ağaçları regresyon</span><span class="sxs-lookup"><span data-stu-id="788fb-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="788fb-384">Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve hello NYC ücreti seyahat veri ipucu tutarını tahmin bir gradyan artırma ağaçları modeli kaydedin gösterir.</span><span class="sxs-lookup"><span data-stu-id="788fb-384">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="788fb-385">** Eğitme ve değerlendirme **</span><span class="sxs-lookup"><span data-stu-id="788fb-385">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="788fb-386">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-386">**OUTPUT**</span></span>

<span data-ttu-id="788fb-387">RMSE 0.928172197114 =</span><span class="sxs-lookup"><span data-stu-id="788fb-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="788fb-388">R sqr 0.732680354389 =</span><span class="sxs-lookup"><span data-stu-id="788fb-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="788fb-389">Hücre tooexecute geçen süre: 20.9 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-389">Time taken tooexecute above cell: 20.9 seconds</span></span>

<span data-ttu-id="788fb-390">**Çizim**</span><span class="sxs-lookup"><span data-stu-id="788fb-390">**Plot**</span></span>

<span data-ttu-id="788fb-391">*tmp_results* hello önceki hücre Hive tablo olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-391">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="788fb-392">Merhaba tablodan sonuçlar hello içine çıkarılır *sqlResults* çizdirmek için veri çerçeve.</span><span class="sxs-lookup"><span data-stu-id="788fb-392">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="788fb-393">Merhaba kod aşağıdadır</span><span class="sxs-lookup"><span data-stu-id="788fb-393">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="788fb-394">Merhaba Jupyter server kullanarak hello kod tooplot hello verilerini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="788fb-394">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Fiili-vs-tahmin-ipucu-tutarlar](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="788fb-396">Ek: çapraz doğrulama parametresi dağılımlarında ile kullanarak ek gerileme görevleri</span><span class="sxs-lookup"><span data-stu-id="788fb-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="788fb-397">Bu ek kod gösteren içeren nasıl doğrusal regresyon ve nasıl toodo MS parametresiyle sweep rastgele orman regresyon için özel kod kullanarak için esnek net kullanarak toodo MS.</span><span class="sxs-lookup"><span data-stu-id="788fb-397">This appendix contains code showing how toodo CV using Elastic net for linear regression and how toodo CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="788fb-398">Doğrulama için doğrusal regresyon esnek net kullanarak arası</span><span class="sxs-lookup"><span data-stu-id="788fb-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="788fb-399">Bu bölümdeki Hello kod nasıl toodo çapraz doğrulama için doğrusal regresyon esnek net kullanarak ve nasıl tooevaluate hello modeline göre test verilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="788fb-399">hello code in this section shows how toodo cross validation using Elastic net for linear regression and how tooevaluate hello model against test data.</span></span>

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="788fb-400">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-400">**OUTPUT**</span></span>

<span data-ttu-id="788fb-401">Hücre tooexecute geçen süre: 161.21 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-401">Time taken tooexecute above cell: 161.21  seconds</span></span>

<span data-ttu-id="788fb-402">**R SQR Metrik değerlendir**</span><span class="sxs-lookup"><span data-stu-id="788fb-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="788fb-403">*tmp_results* hello önceki hücre Hive tablo olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="788fb-403">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="788fb-404">Merhaba tablodan sonuçlar hello içine çıkarılır *sqlResults* çizdirmek için veri çerçeve.</span><span class="sxs-lookup"><span data-stu-id="788fb-404">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="788fb-405">Merhaba kod aşağıdadır</span><span class="sxs-lookup"><span data-stu-id="788fb-405">Here is hello code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="788fb-406">Merhaba kod toocalculate R sqr aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="788fb-406">Here is hello code toocalculate R-sqr.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="788fb-407">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-407">**OUTPUT**</span></span>

<span data-ttu-id="788fb-408">R sqr 0.619184907088 =</span><span class="sxs-lookup"><span data-stu-id="788fb-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="788fb-409">Rastgele orman regresyon için özel kod kullanarak parametre tarama ile doğrulama arası</span><span class="sxs-lookup"><span data-stu-id="788fb-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="788fb-410">Bu bölümdeki Hello kod nasıl toodo çapraz doğrulama rastgele orman regresyon için özel kod kullanarak parametre tarama ile ve nasıl tooevaluate hello modeline göre test verilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="788fb-410">hello code in this section shows how toodo cross validation with parameter sweep using custom code for random forest regression and how tooevaluate hello model against test data.</span></span>

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="788fb-411">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-411">**OUTPUT**</span></span>

<span data-ttu-id="788fb-412">RMSE 0.906972198262 =</span><span class="sxs-lookup"><span data-stu-id="788fb-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="788fb-413">R sqr 0.740751197012 =</span><span class="sxs-lookup"><span data-stu-id="788fb-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="788fb-414">Hücre tooexecute geçen süre: 69.17 saniye</span><span class="sxs-lookup"><span data-stu-id="788fb-414">Time taken tooexecute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="788fb-415">Bellek ve yazdırma modeli konumları nesneleri Temizle</span><span class="sxs-lookup"><span data-stu-id="788fb-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="788fb-416">Kullanım `unpersist()` toodelete nesneleri bellekte önbelleğe alınmış.</span><span class="sxs-lookup"><span data-stu-id="788fb-416">Use `unpersist()` toodelete objects cached in memory.</span></span>

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


<span data-ttu-id="788fb-417">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-417">**OUTPUT**</span></span>

<span data-ttu-id="788fb-418">PythonRDD [122] RDD PythonRDD.scala adresindeki adresindeki: 43</span><span class="sxs-lookup"><span data-stu-id="788fb-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="788fb-419">** Çıktının yolu toomodel hello tüketim not defterinde kullanılan toobe dosyaları.</span><span class="sxs-lookup"><span data-stu-id="788fb-419">**Printout path toomodel files toobe used in hello consumption notebook.</span></span> <span data-ttu-id="788fb-420">** tooconsume ve puanı bağımsız veri kümesi, toocopy gerekir ve bu dosya adları hello "Tüketim dizüstü" yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="788fb-420">** tooconsume and score an independent data-set, you need toocopy and paste these file names in hello "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="788fb-421">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="788fb-421">**OUTPUT**</span></span>

<span data-ttu-id="788fb-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="788fb-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="788fb-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="788fb-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="788fb-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="788fb-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="788fb-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="788fb-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="788fb-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="788fb-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="788fb-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="788fb-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="788fb-428">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="788fb-428">What's next?</span></span>
<span data-ttu-id="788fb-429">Spark Mllib'i hello ile regresyon ve sınıflandırma modelleri oluşturduğunuza göre hazır toolearn nasıl olan tooscore ve bu modeller değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="788fb-429">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span>

<span data-ttu-id="788fb-430">**Model tüketimi:** toolearn nasıl tooscore ve bu konuda oluşturulan hello sınıflandırma ve regresyon modelleri değerlendirmek, bkz: [puanı ve Spark yerleşik makine öğrenimi modellerini değerlendirme](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="788fb-430">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

