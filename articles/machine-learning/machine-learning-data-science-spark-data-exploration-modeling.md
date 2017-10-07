---
title: "aaaData araştırması ve Spark ile modelleme | Microsoft Docs"
description: "Veri keşfi ve modelleme yetenekleri azure'da hello Spark Mllib'i araç setini showcases hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="ad3eb-103">Spark ile veri keşfi ve modelleme</span><span class="sxs-lookup"><span data-stu-id="ad3eb-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="ad3eb-104">Bu kılavuzda Hdınsight Spark toodo veri keşfi kullanır ve ikili sınıflandırma ve görevleri hello NYC örneğinde modelleme regresyon Seyahat Ücreti 2013 dataset masrafları.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-104">This walkthrough uses HDInsight Spark toodo data exploration and binary classification and regression modeling tasks on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="ad3eb-105">Merhaba hello adımlarda size yol gösterir [veri bilimi işlemi](http://aka.ms/datascienceprocess)için Hdınsight Spark kullanarak uçtan, küme için işleme ve Azure BLOB'ların toostore hello veri ve hello modeller.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="ad3eb-106">Hello işlem bir Azure Storage Blobundan getirildi veri visualizes inceler ve ardından hello veri toobuild Tahmine dayalı modelleri hazırlar.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="ad3eb-107">Bu modeller hello Spark Mllib'i Araç Seti toodo ikili sınıflandırma ve görevleri modelleme regresyon kullanarak derlemesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-107">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="ad3eb-108">Merhaba **ikili sınıflandırma** görev gerekmediğini toopredict hello seyahat için ücretli bir ipucu.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-108">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="ad3eb-109">Merhaba **regresyon** toopredict hello diğer ipucu özelliklerini temel alarak hello ipucu miktarını bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-109">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="ad3eb-110">Merhaba modelleri kullanırız Lojistik ve doğrusal regresyon, rastgele ormanları ve gradyan boosted ağaçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-110">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="ad3eb-111">[Doğrusal regresyon SGD ile](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) Stokastik gradyan düşüşü (SGD) yöntemini kullanan doğrusal regresyon modeli ve en iyi duruma getirme ve özellik için toopredict hello ipucu tutarlar ölçeklendirme Ücretli.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="ad3eb-112">[LBFGS ile Lojistik regresyon](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) veya "logit" regresyon hello bağımlı değişken kategorik toodo veri sınıflandırması olduğunda kullanılabilen bir regresyon modeli.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="ad3eb-113">LBFGS sınırlı bir bilgisayarın bellek miktarını kullanarak hello Broyden – Fletcher'dan – Goldfarb – Shanno (BFGS) algoritması benzeyen ve machine learning'de yaygın olarak kullanılan bir yarı-Newton iyileştirme algoritması ' dir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-113">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="ad3eb-114">[Rastgele ormanlar](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) karar ağaçları ensembles şunlardır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="ad3eb-115">Bunlar, birçok karar ağaçları tooreduce hello riskini overfitting birleştirin.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-115">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="ad3eb-116">Rastgele ormanlar regresyon ve sınıflandırma için kullanılır ve kategorik özellikleri işleyebilir ve toohello çok sınıflı sınıflandırma ayarı genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-116">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="ad3eb-117">Bunlar, özellik ölçekleme ve bu mümkün toocapture sapmalar ve özellik etkileşimleri gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-117">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="ad3eb-118">Rastgele ormanlar hello en başarılı machine learning modellerini sınıflandırma ve regresyon biridir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-118">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="ad3eb-119">[Gradyan boosted ağaçları](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) olan karar ağaçları ensembles.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="ad3eb-120">GBTs tren karar tekrarlayarak toominimize kaybı işlevi ağaçları.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-120">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="ad3eb-121">GBTs regresyon ve sınıflandırma için kullanılır ve kategorik özellikleri işleyebilir, özellik ölçeklendirme gerektirmez ve mümkün toocapture sapmalar ve etkileşimleri özellik.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="ad3eb-122">Bir sınıflandırma veya çoklu sınıflar ayarında de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="ad3eb-123">Merhaba modelleme adımları ayrıca nasıl tootrain, değerlendirmek ve her türde bir model Kaydet gösteren kod içerir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-123">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="ad3eb-124">Python kullanılan toocode hello çözümü ve tooshow hello ilgili çizimleri olmuştur.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-124">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="ad3eb-125">Merhaba Spark Mllib'i Araç Seti büyük veri kümeleri üzerinde tasarlanmış toowork olsa da, nispeten küçük bir örnek (yaklaşık 30 170 K satır, yaklaşık hello özgün NYC dataset %0,1 kullanarak Mb) burada kolaylık sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-125">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="ad3eb-126">burada verilen hello alıştırma verimli bir şekilde (yaklaşık 10 dakika cinsinden) 2 çalışan düğümleri ile bir Hdınsight kümesi üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-126">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="ad3eb-127">Merhaba küçük değişiklikler içeren aynı kodu kullanılan tooprocess daha büyük veri-kümeleriyle, verileri bellekte önbelleğe alma ve hello küme boyutunu değiştirmek için uygun değişiklikleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-127">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ad3eb-128">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ad3eb-128">Prerequisites</span></span>
<span data-ttu-id="ad3eb-129">Bir Azure hesabı ve Spark 1.6 (veya Spark 2.0) ihtiyacınız Hdınsight küme toocomplete Bu izlenecek yol.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="ad3eb-130">Merhaba bkz [genel bakış, verileri Azure Hdınsight'ta Spark kullanmanın Bilim](machine-learning-data-science-spark-overview.md) yönelik yönergeler toosatisfy bu gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-130">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="ad3eb-131">Bu konu ayrıca açıklamasını hello burada kullanılan NYC 2013 ücreti verileri ve nasıl tooexecute kod hello Spark kümesinde Jupyter not defteri gelen yönergeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-131">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="ad3eb-132">Spark kümeleri ve dizüstü bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="ad3eb-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="ad3eb-133">Kurulum adımlarını ve kod bu kılavuzda bir Hdınsight Spark 1.6 kullanmak için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="ad3eb-134">Ancak Jupyter not defterleri Hdınsight Spark 1.6 ve Spark 2.0 kümeleri için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="ad3eb-135">Merhaba not defterlerini ve bağlantıları toothem açıklamasını hello sağlanan [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) bunları içeren hello GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-135">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="ad3eb-136">Ayrıca, hello kod burada ve bağlı hello not defterlerini geneldir ve tüm Spark kümesi üzerinde çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-136">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="ad3eb-137">Hdınsight Spark kullanmıyorsanız hello Küme kurulumu ve Yönetimi adımları ne burada gösterilenden biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-137">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="ad3eb-138">Kolaylık olması için Spark 1.6 (toobe hello Jupyter not defteri sunucu, hello pySpark Çekirdeği'nde çalıştırın) ve Spark 2. 0'ı (toobe hello pySpark3 Çekirdeği'nde hello Jupyter not defteri sunucu olarak çalıştır) için toohello Jupyter not defterleri hello bağlantılar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-138">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 (toobe run in hello pySpark kernel of hello Jupyter Notebook server) and  Spark 2.0 (toobe run in hello pySpark3 kernel of hello Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="ad3eb-139">Spark 1.6 dizüstü bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="ad3eb-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="ad3eb-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): ilgili bilgiler verilmektedir modelleme ve birkaç farklı algoritmalarıyla Puanlama tooperform veri keşfi,.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how tooperform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="ad3eb-141">Spark 2.0 dizüstü bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="ad3eb-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="ad3eb-142">bir Spark 2.0 kümesi kullanılarak uygulanan hello regresyon ve sınıflandırma görevler ayrı not defterlerinde ve farklı bir veri kümesi hello sınıflandırma dizüstü kullanır:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-142">hello regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and hello classification notebook uses a different data set:</span></span>

- <span data-ttu-id="ad3eb-143">[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Bu dosyayı nasıl tooperform veri keşfi, model oluşturma ve Spark 2. 0'Puanlama hello NYC ücreti seyahat kullanarak kümeleri hakkında bilgi sağlar. ve ücreti verileri-set açıklanan [burada](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="ad3eb-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="ad3eb-144">Bu Not hızlı bir şekilde Spark 2.0 için sağladık hello kod keşfetme için iyi bir başlangıç noktası olabilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-144">This notebook may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> <span data-ttu-id="ad3eb-145">Daha ayrıntılı bir not defteri hello NYC ücreti verileri analiz eder, bu listede hello sonraki not defteri bakın.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-145">For a more detailed notebook analyzes hello NYC Taxi data, see hello next notebook in this list.</span></span> <span data-ttu-id="ad3eb-146">Bu liste aşağıdaki bu dizüstü bilgisayarlar karşılaştırmak hello notlarına bakın.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-146">See hello notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="ad3eb-147">[Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): Bu dosyayı nasıl wrangling tooperform verileri (işlem), Spark SQL ve dataframe modelleme ve kullanarak Puanlama araştırması NYC ücreti seyahat ve açıklanan ücreti veri kümesi hello gösterir [ Burada](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="ad3eb-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="ad3eb-148">[Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): Bu dosyayı nasıl wrangling tooperform verileri (işlem), Spark SQL ve dataframe modelleme ve kullanarak Puanlama araştırması, iyi bilinen uçak zamanında ayrılma hello gösterir veri kümesi 2011 ve 2012.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="ad3eb-149">Bu hava durumu özellikleri hello modele dahil edilebilir biz hello uçak dataset hello havaalanı hava durumu verileri (örneğin windspeed, sıcaklık, yükseklik vb.) önceki toomodeling ile tümleşik.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-149">We integrated hello airline dataset with hello airport weather data (e.g. windspeed, temperature, altitude etc.) prior toomodeling, so these weather features can be included in hello model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="ad3eb-150">Merhaba uçak dataset toohello Spark 2.0 not defterlerini eklenen toobetter hello sınıflandırma algoritmalarının kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-150">hello airline dataset was added toohello Spark 2.0 notebooks toobetter illustrate hello use of classification algorithms.</span></span> <span data-ttu-id="ad3eb-151">Uçak zamanında ayrılma dataset ve hava durumu veri kümesi hakkında bilgi için bağlantılar aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-151">See hello following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="ad3eb-152">Uçak zamanında ayrılma veri: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="ad3eb-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="ad3eb-153">Havaalanı hava durumu verileri: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="ad3eb-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="ad3eb-154">Merhaba NYC ücreti Hello Spark 2.0 not defterlerini ve uçak uçuş gecikme veri kümeleri, 10 dakika veya daha fazla toorun (bağlı olarak, HDI kümesi boyutunu hello) alabilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-154">hello Spark 2.0 notebooks on hello NYC taxi and airline flight delay data-sets can take 10 mins or more toorun (depending on hello size of your HDI cluster).</span></span> <span data-ttu-id="ad3eb-155">Merhaba hello listesinin ilk not defteri gösterir pek çok görünüşünün hello veri keşfi, Görselleştirme ve ML model eğitim aşağı örneklenen NYC veri hangi hello ücreti ve ücreti dosyaları önceden birleştirilmiş kümesi, daha az zaman toorun götüren bir Not: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) bir çok daha kısa süre toofinish (2-3 dakika) bu not alır ve olması iyi bir başlangıç noktası hızla hello kod keşfetme için sahip olduğumuz Spark 2.0 için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-155">hello first notebook in hello above list shows many aspects of hello data exploration, visualization and ML model training in a notebook that takes less time toorun with down-sampled NYC data set, in which hello taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time toofinish (2-3 mins) and may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="ad3eb-156">Merhaba aşağıdaki ilgili toousing Spark 1.6 açıklamalardır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-156">hello descriptions below are related toousing Spark 1.6.</span></span> <span data-ttu-id="ad3eb-157">Spark 2.0 sürümleri için lütfen açıklanmıştır ve yukarıdaki bağlı hello not defterlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-157">For Spark 2.0 versions, please use hello notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="ad3eb-158">Kurulumu: Spark bağlam depolama konumları, kitaplıklar ve hello hazır</span><span class="sxs-lookup"><span data-stu-id="ad3eb-158">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="ad3eb-159">Spark mümkün tooread ve yazma tooAzure depolama blobu (WASB olarak da bilinir) olur.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-159">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="ad3eb-160">Bu nedenle depolanan mevcut verilerinizi Spark kullanarak işlenebilir ve depolanan yeniden WASB hello sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-160">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="ad3eb-161">toosave modelleri veya WASB dosyalarında, hello yolu düzgün belirtilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-161">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="ad3eb-162">Merhaba varsayılan kapsayıcı bağlı toohello Spark kümesi ile başlayan bir yol kullanarak başvurulabilir: "wasb: / / /".</span><span class="sxs-lookup"><span data-stu-id="ad3eb-162">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="ad3eb-163">Başka konumlara tarafından başvurulan "wasb: / /".</span><span class="sxs-lookup"><span data-stu-id="ad3eb-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="ad3eb-164">Dizin yolları için depolama konumları WASB ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ad3eb-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="ad3eb-165">Hello aşağıdaki kod örneği hello konumunu okuma hello veri toobe belirtir ve hello modeli depolama dizini toowhich hello modeli çıktı hello yolu kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-165">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="ad3eb-166">Kitaplıkları içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="ad3eb-166">Import libraries</span></span>
<span data-ttu-id="ad3eb-167">Ayarlama, ayrıca gerekli kitaplıkları içeri aktarma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="ad3eb-168">Spark bağlamını ayarlayın ve gerekli kitaplıkları ile koddan hello içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-168">Set spark context and import necessary libraries with hello following code:</span></span>

    # IMPORT LIBRARIES
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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="ad3eb-169">Spark bağlamını ve PySpark sihirler hazır</span><span class="sxs-lookup"><span data-stu-id="ad3eb-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="ad3eb-170">Jupyter not defterleri ile sağlanan hello PySpark tekrar önceden belirlenmiş bir içerik var.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="ad3eb-171">Geliştirdiğiniz Merhaba uygulaması ile çalışmaya başlamadan önce bu nedenle, tooset hello Spark veya Hive bağlamları açıkça gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="ad3eb-172">Bu içerikler varsayılan olarak sizin için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-172">These contexts are available for you by default.</span></span> <span data-ttu-id="ad3eb-173">Bu içerikler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-173">These contexts are:</span></span>

* <span data-ttu-id="ad3eb-174">SC - Spark</span><span class="sxs-lookup"><span data-stu-id="ad3eb-174">sc - for Spark</span></span> 
* <span data-ttu-id="ad3eb-175">sqlContext - Hive için</span><span class="sxs-lookup"><span data-stu-id="ad3eb-175">sqlContext - for Hive</span></span>

<span data-ttu-id="ad3eb-176">Merhaba PySpark çekirdeği bazı önceden tanımlanmış "sihirleri" ile çağırabilir özel komutlar olduğu sağlar %%.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="ad3eb-177">Bu kod örneklerinde kullanılan olan iki komut vardır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="ad3eb-178">**%% yerel** sonraki satırların hello kodda yerel olarak yürütülen toobe olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="ad3eb-179">Kod geçerli Python kodu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="ad3eb-180">**%% sql -o <variable name>**  hello sqlContext bir Hive sorgusu yürütür.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="ad3eb-181">Merhaba -o parametre aktarılırsa hello hello sorgunun sonucu hello kalıcı %% Pandas DataFrame olarak yerel Python bağlamı.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="ad3eb-182">Hello tekrar Jupyter not defterlerini ve önceden tanımlanmış hello hakkında daha fazla bilgi "magics için" sağladıkları, bkz: [Jupyter not defterlerinde kullanılabilen çekirdekler Hdınsight Spark Linux kümeleri Hdınsight'ta](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="ad3eb-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="ad3eb-183">Ortak blob gelen veri alımı</span><span class="sxs-lookup"><span data-stu-id="ad3eb-183">Data ingestion from public blob</span></span>
<span data-ttu-id="ad3eb-184">Merhaba ilk hello veri bilimi işlemi adımdır kaynaklardan analiz tooingest hello veri toobe nerede olduğunu veri keşfi ve modelleme ortamınıza yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="ad3eb-185">Merhaba Spark bu kılavuzda ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-185">hello environment is Spark in this walkthrough.</span></span> <span data-ttu-id="ad3eb-186">Bu bölümde hello kod toocomplete bir dizi görev içerir:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="ad3eb-187">Merhaba veri örnek toobe Modellenen alma</span><span class="sxs-lookup"><span data-stu-id="ad3eb-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="ad3eb-188">(.tsv dosyası olarak depolanır) hello girdi veri kümesi okuyun</span><span class="sxs-lookup"><span data-stu-id="ad3eb-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="ad3eb-189">Biçim ve temiz hello verileri</span><span class="sxs-lookup"><span data-stu-id="ad3eb-189">format and clean hello data</span></span>
* <span data-ttu-id="ad3eb-190">oluşturma ve nesneleri (RDDs veya veri çerçevelerini) bellekte önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="ad3eb-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="ad3eb-191">SQL bağlam tabloda geçici olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="ad3eb-192">Veri alımı için hello kod aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-192">Here is hello code for data ingestion.</span></span>

    # INGEST DATA

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


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="ad3eb-193">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-193">**OUTPUT:**</span></span>

<span data-ttu-id="ad3eb-194">Hücre tooexecute geçen süre: 51.72 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-194">Time taken tooexecute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="ad3eb-195">Veri keşfi & Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="ad3eb-195">Data exploration & visualization</span></span>
<span data-ttu-id="ad3eb-196">Hello veri Spark alındıktan sonra hello sonraki hello veri bilimi işlemi hello veri keşfi ve görselleştirme aracılığıyla daha derin anlayış toogain adımdır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="ad3eb-197">Bu bölümde, SQL sorguları ve çizim hello hedef değişkenleri ve olası özellikleri için görsel denetleme kullanarak hello ücreti verileri inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="ad3eb-198">Özellikle, yolcu sayıları ücreti dönüşleri, ipucu tutarlar hello sıklığını ve nasıl ipuçları ödeme tutar ve türüne göre farklılık hello sıklığını çizmek.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="ad3eb-199">Histogram yolcu sayısı frekansların ücreti dönüşleri hello örnekteki Çiz</span><span class="sxs-lookup"><span data-stu-id="ad3eb-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="ad3eb-200">Bu kodu ve sonraki parçacıkları SQL Sihirli tooquery hello örnek ve yerel Sihirli tooplot hello verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="ad3eb-201">**SQL Sihirli (`%%sql`)** hello Hdınsight PySpark çekirdeği kolay satır içi HiveQL sorguları hello sqlContext karşı destekler.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="ad3eb-202">Merhaba (-o deðiþken_adý) bağımsız değişkeni devam ederse hello SQL sorgusu hello çıktısını hello Jupyter sunucuda Pandas DataFrame olarak.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="ad3eb-203">Bu, hello yerel modda kullanılabilir olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="ad3eb-204">Merhaba  **`%%local` Sihirli** olan toorun kod hello headnode hello Hdınsight kümesinin olduğu hello Jupyter sunucu üzerinde yerel olarak kullanılan.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="ad3eb-205">Genellikle, kullandığınız `%%local` hello birlikte Sihirli `%%sql` - o parametresiyle Sihirli.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-205">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="ad3eb-206">Merhaba -o parametresi yerel olarak hello SQL sorgusu hello çıktısını kalıcı ve ardından %% yerel Sihirli hello sonraki kod parçacığını toorun yerel olarak yerel olarak kalıcı hello çıktı hello SQL sorgularının karşı kümesini tetiklemek</span><span class="sxs-lookup"><span data-stu-id="ad3eb-206">hello -o parameter would persist hello output of hello SQL query locally and then %%local magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally</span></span>

<span data-ttu-id="ad3eb-207">Merhaba kod çalıştırdıktan sonra hello çıkış otomatik olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-207">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="ad3eb-208">Bu sorgu hello dönüşleri yolcu sayısına göre alır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-208">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="ad3eb-209">Bu kod bir yerel veri çerçevesi hello sorgu çıktısı oluşturur ve hello veri çizer.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-209">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="ad3eb-210">Merhaba `%%local` Sihirli oluşturur çerçeve, yerel veri `sqlResults`, kullanılabileceği ile matplotlib çizdirmek için.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-210">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="ad3eb-211">Bu PySpark Sihirli birden çok kez bu kılavuzda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="ad3eb-212">Merhaba miktarda veri büyükse, toocreate yerel belleğe sığması bir veri-çerçeve örnek.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-212">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="ad3eb-213">Sayıları tarafından yolcu hello kod tooplot hello dönüşleri İşte</span><span class="sxs-lookup"><span data-stu-id="ad3eb-213">Here is hello code tooplot hello trips by passenger counts</span></span>

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="ad3eb-214">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-214">**OUTPUT:**</span></span>

![Yolcu sayısına göre seyahat sıklığı](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="ad3eb-216">Hello kullanarak birkaç farklı türde görselleştirmeleri (tablo, pasta, çizgi, alan veya çubuğu) arasında seçebilirsiniz **türü** menü düğmelerini hello Not.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="ad3eb-217">Merhaba çubuğu çizim burada gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-217">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="ad3eb-218">Çizim histogram ipucu tutarlar ve nasıl ipucu tutar yolcu sayısı ve ücreti tutarlar göre değişir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="ad3eb-219">Bir SQL sorgusu toosample verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-219">Use a SQL query toosample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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


<span data-ttu-id="ad3eb-220">Bu kod hücresini hello SQL sorgu toocreate üç çizimleri hello verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-220">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


<span data-ttu-id="ad3eb-221">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-221">**OUTPUT:**</span></span> 

![İpucu tutar dağıtımı](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Yolcu sayısına göre ipucu tutar](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![İpucu tutar ücreti miktar](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="ad3eb-225">Modelleme mühendislik, dönüştürme ve veri hazırlığı özelliği</span><span class="sxs-lookup"><span data-stu-id="ad3eb-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="ad3eb-226">Bu bölümde açıklar ve ML modelleme kullanmak için tooprepare veri hello kod yordamları için kullanılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-226">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="ad3eb-227">Bunu nasıl toodo hello aşağıdaki görevleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-227">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="ad3eb-228">Yeni bir özellik tarafından binning saatleri trafiği zaman demet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="ad3eb-229">Dizin ve kategorik özellikleri kodlama</span><span class="sxs-lookup"><span data-stu-id="ad3eb-229">Index and encode categorical features</span></span>
* <span data-ttu-id="ad3eb-230">ML işlevleri giriş etiketli noktası nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad3eb-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="ad3eb-231">Rastgele bir alt örnekleme hello veri oluşturun ve eğitim ve test kümesi olarak bölme</span><span class="sxs-lookup"><span data-stu-id="ad3eb-231">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="ad3eb-232">Ölçeklendirme özelliği</span><span class="sxs-lookup"><span data-stu-id="ad3eb-232">Feature scaling</span></span>
* <span data-ttu-id="ad3eb-233">Bellek önbelleği nesneleri</span><span class="sxs-lookup"><span data-stu-id="ad3eb-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="ad3eb-234">Yeni bir özellik tarafından binning saatleri trafiği zaman demet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="ad3eb-235">Bu kodu nasıl toocreate saatleri trafiği zamanına binning tarafından yeni bir özellik aralıkları ve sonra nasıl toocache hello bellek ortaya çıkan veri çerçevede gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-235">This code shows how toocreate a new feature by binning hours into traffic time buckets and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="ad3eb-236">Esnek Dağıtılmış veri kümeleri (RDDs) ve veri çerçevelerini art arda kullanıldığı önbelleğe alma tooimproved yürütme sürelerinin yol açar.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="ad3eb-237">Buna göre biz RDDs ve veri çerçevelerini hello izlenecek çeşitli aşamalarında önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-237">Accordingly, we cache RDDs and data-frames at several stages in hello walkthrough.</span></span> 

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

<span data-ttu-id="ad3eb-238">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-238">**OUTPUT:**</span></span> 

<span data-ttu-id="ad3eb-239">126050</span><span class="sxs-lookup"><span data-stu-id="ad3eb-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="ad3eb-240">Dizin ve işlevleri modelleme içine girişi için kategorik özellikleri kodlama</span><span class="sxs-lookup"><span data-stu-id="ad3eb-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="ad3eb-241">Bu bölümde gösterilmiştir nasıl tooindex veya İşlevler modelleme hello giriş için kategorik özellikleri kodlayın.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-241">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="ad3eb-242">Modelleme hello ve Mllib'i işlevlerini kategorik giriş verisi toobe özelliklerle dizine veya önceki toouse kodlanmış gerektiren tahmin etmek.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-242">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="ad3eb-243">Merhaba modeline bağlı olarak tooindex gerekir veya farklı şekillerde kodlamak:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-243">Depending on hello model, you need tooindex or encode them in different ways:</span></span>  

* <span data-ttu-id="ad3eb-244">**Ağaç tabanlı modelleme** sayısal değerleri olarak kodlanmış kategorileri toobe gerektirir (örneğin, üç kategoride özelliğiyle kodlanması 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="ad3eb-244">**Tree-based modeling** requires categories toobe encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="ad3eb-245">Bu Mllib'i tarafından 's sağlanan [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) işlevi.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="ad3eb-246">Bu işlev bir dize sütunu etiketlerini tooa sütununun etiket sıklıklarını tarafından sıralanan etiket dizinlerini kodlar.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-246">This function encodes a string column of labels tooa column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="ad3eb-247">Giriş ve veri işleme için sayısal değerleri içeren dizine rağmen hello ağaç tabanlı algoritmalar belirtilen tootreat olabilir bunları uygun şekilde kategorileri olarak.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-247">Although indexed with numerical values for input and data handling, hello tree-based algorithms can be specified tootreat them appropriately as categories.</span></span> 
* <span data-ttu-id="ad3eb-248">**Lojistik ve doğrusal regresyon modeli** bir hot kodlaması, gerektiren nerede, örneğin, üç kategoriye sahip bir özellik içeren her 0 veya 1 bir gözlem hello kategorisine bağlı olarak üç özellik sütunlara genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="ad3eb-249">Mllib'i sağlar [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) bir hot toodo kodlama işlev.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="ad3eb-250">Bu Kodlayıcı sütununun etiket dizinlerini tooa ikili vektörler, en çok bir değerle tek bir-bir sütun eşler.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-250">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="ad3eb-251">Bu kodlama Lojistik regresyon gibi sayısal değerli özellikleri beklediğiniz algoritmalarına olanak uygulanan toobe toocategorical özellikleri.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="ad3eb-252">Kategorik özellikleri kodlanacağını ve kod tooindex hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-252">Here is hello code tooindex and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

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

<span data-ttu-id="ad3eb-253">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-253">**OUTPUT:**</span></span>

<span data-ttu-id="ad3eb-254">Hücre tooexecute geçen süre: 1.28 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-254">Time taken tooexecute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="ad3eb-255">ML işlevleri giriş etiketli noktası nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad3eb-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="ad3eb-256">Bu bölümde nasıl tooindex kategorik metin verileri etiketli noktası verileri olarak yazın ve böylece bu kullanılan tootrain ve test Mllib'i Lojistik regresyon ve diğer sınıflandırma modelleri olabilir kodlamak gösterir kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-256">This section contains code that shows how tooindex categorical text data as a labeled point data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="ad3eb-257">Etiketli noktası, esnek Dağıtılmış veri kümeleri (RDD) girdi verisi olarak Mllib'i ML algoritmalara çoğu tarafından gerektiği şekilde biçimlendirilmiş nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="ad3eb-258">A [noktası etiketli](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) yerel bir vektör, yoğun veya seyrek, etiket/yanıt ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="ad3eb-259">Bu bölüm gösteren kodu içerir nasıl tooindex kategorik metin verileri olarak bir [noktası etiketli](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) veri türü ve kullanılan tootrain ve test Mllib'i Lojistik regresyon ve diğer sınıflandırma modelleri olabilmesi kodlayın.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-259">This section contains code that shows how tooindex categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="ad3eb-260">Etiketli noktası, esnek Dağıtılmış veri kümeleri (RDD) bir etiket (hedef/yanıt değişken) ve özellik vektör oluşan nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="ad3eb-261">Bu biçim Mllib'i içinde birçok ML algoritması tarafından giriş olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="ad3eb-262">İşte kod tooindex hello ve ikili sınıflandırma için metin özellikleri kodlayın.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-262">Here is hello code tooindex and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="ad3eb-263">Doğrusal regresyon çözümlemesi için tooencode ve dizin kategorik metin özelliklerinden hello kod aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-263">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="ad3eb-264">Rastgele bir alt örnekleme hello veri oluşturun ve eğitim ve test kümesi olarak bölme</span><span class="sxs-lookup"><span data-stu-id="ad3eb-264">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="ad3eb-265">Bu kod bir rastgele örnekleme (% 25 burada kullanılır) hello veri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-265">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="ad3eb-266">Bu örneğin hello kümesinin toohello boyutu nedeniyle gerekli olmamasına rağmen bilmesi nasıl, burada örnek oluşturabilirsiniz göstermek nasıl toouse gerektiğinde kendi sorunu için.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-266">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample here so you know how toouse it for your own problem when needed.</span></span> <span data-ttu-id="ad3eb-267">Örnekleri büyük olduğunda bu eğitim modelleri sırasında önemli zamandan tasarruf edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="ad3eb-268">Sonraki biz hello örnek eğitim bölümü (burada %75) ve bir test bölümü (% 25 burada) toouse sınıflandırma ve regresyon modelleme bölün.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-268">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

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

<span data-ttu-id="ad3eb-269">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-269">**OUTPUT:**</span></span>

<span data-ttu-id="ad3eb-270">Hücre tooexecute geçen süre: 0.24 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-270">Time taken tooexecute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="ad3eb-271">Ölçeklendirme özelliği</span><span class="sxs-lookup"><span data-stu-id="ad3eb-271">Feature scaling</span></span>
<span data-ttu-id="ad3eb-272">Özellik ölçeklendirme, veri normalleştirme da bilinen, yaygın olarak yapılan değerlerle özellikleri olan belirli bir aşırı tartmanız olduğunu hello hedefi işlevinde oluşturmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="ad3eb-273">Merhaba özelliği ölçeklendirmeye yönelik kodu kullanan hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello özellikleri toounit farkı.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-273">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="ad3eb-274">Doğrusal regresyon ile Stokastik gradyan düşüşü (SGD), diğer machine learning modellerini regularized gerileme veya destek vektör makineler (SVM) gibi çeşitli eğitim için yaygın olarak kullanılan bir algoritma kullanmak için Mllib'i tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="ad3eb-275">Merhaba LinearRegressionWithSGD algoritması toobe hassas toofeature ölçeklendirme bulduk.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-275">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>
> 
> 

<span data-ttu-id="ad3eb-276">Merhaba kod tooscale değişkenlerinin regularized hello doğrusal SGD algoritması ile kullanmak için aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-276">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

    # FEATURE SCALING

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

<span data-ttu-id="ad3eb-277">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-277">**OUTPUT:**</span></span>

<span data-ttu-id="ad3eb-278">Hücre tooexecute geçen süre: 13.17 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-278">Time taken tooexecute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="ad3eb-279">Bellek önbelleği nesneleri</span><span class="sxs-lookup"><span data-stu-id="ad3eb-279">Cache objects in memory</span></span>
<span data-ttu-id="ad3eb-280">Eğitim ve ML algoritmalardan test etme için sınıflandırma, regresyon, kullanılan hello giriş verisi çerçeve nesneleri önbelleğe alarak azaltılabilir için harcanan hello süre ve özellikleri ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-280">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression, and scaled features.</span></span>

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

<span data-ttu-id="ad3eb-281">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-281">**OUTPUT:**</span></span> 

<span data-ttu-id="ad3eb-282">Hücre tooexecute geçen süre: 0,15 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-282">Time taken tooexecute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="ad3eb-283">Bir ipucu ile ikili sınıflandırma modelleri Ücretli olsun veya olmasın tahmin etme</span><span class="sxs-lookup"><span data-stu-id="ad3eb-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="ad3eb-284">Bu bölümde, bir ipucu ücreti seyahat için ücretli olup olmadığına bakılmaksızın kullanım üç tahmin etmeye hello ikili sınıflandırma görevi için nasıl modeller gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-284">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="ad3eb-285">sunulan hello model şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-285">hello models presented are:</span></span>

* <span data-ttu-id="ad3eb-286">Regularized Lojistik regresyon</span><span class="sxs-lookup"><span data-stu-id="ad3eb-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="ad3eb-287">Rastgele orman modeli</span><span class="sxs-lookup"><span data-stu-id="ad3eb-287">Random forest model</span></span>
* <span data-ttu-id="ad3eb-288">Gradyan artırma ağaçları</span><span class="sxs-lookup"><span data-stu-id="ad3eb-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="ad3eb-289">Her model kod bölümünde oluşturma adımları ayrılır:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="ad3eb-290">**Eğitim modeli** bir parametre kümesi ile verileri</span><span class="sxs-lookup"><span data-stu-id="ad3eb-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="ad3eb-291">**Model değerlendirme** ölçümlerle sınama veri kümesi üzerinde</span><span class="sxs-lookup"><span data-stu-id="ad3eb-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="ad3eb-292">**Model kaydetme** gelecekteki tüketimi için blob içinde</span><span class="sxs-lookup"><span data-stu-id="ad3eb-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="ad3eb-293">Sınıflandırma Lojistik regresyon kullanma</span><span class="sxs-lookup"><span data-stu-id="ad3eb-293">Classification using logistic regression</span></span>
<span data-ttu-id="ad3eb-294">Bu bölümdeki Hello kod gösterir nasıl tootrain, değerlendirmek ve lojistik regresyon modeli ile Kaydet [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) tahmin bir ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-294">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="ad3eb-295">**MS ve hyperparameter Süpürme kullanarak hello Lojistik regresyon modelini eğitme**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-295">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="ad3eb-296">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-296">**OUTPUT:**</span></span> 

<span data-ttu-id="ad3eb-297">Katsayısını: [0.0082065285375-0.0223675576104,-0.0183812028036, - 3.48124578069e-05-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="ad3eb-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="ad3eb-298">Intercept:-0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="ad3eb-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="ad3eb-299">Hücre tooexecute geçen süre: 14.43 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-299">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="ad3eb-300">**Standart ölçümlerle Hello ikili sınıflandırma modelini değerlendir**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-300">**Evaluate hello binary classification model with standard metrics**</span></span>

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

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


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="ad3eb-301">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-301">**OUTPUT:**</span></span> 

<span data-ttu-id="ad3eb-302">PR alanında 0.985297691373 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="ad3eb-303">ROC alanında 0.983714670256 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="ad3eb-304">Özet istatistikleri</span><span class="sxs-lookup"><span data-stu-id="ad3eb-304">Summary Stats</span></span>

<span data-ttu-id="ad3eb-305">Duyarlık 0.984304060189 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="ad3eb-306">Geri çağırma 0.984304060189 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="ad3eb-307">F1 Puan 0.984304060189 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="ad3eb-308">Hücre tooexecute geçen süre: 57.61 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-308">Time taken tooexecute above cell: 57.61 seconds</span></span>

<span data-ttu-id="ad3eb-309">**Merhaba ROC eğrisi çizme.**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-309">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="ad3eb-310">Merhaba *predictionAndLabelsDF* bir tablo olarak kayıtlı *tmp_results*, hello önceki hücrenin.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-310">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="ad3eb-311">*tmp_results* kullanılan toodo sorgu ve sonuçları çerçevesine hello sqlResults verileri-çizdirmek için çıktı.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-311">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="ad3eb-312">Merhaba kod aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-312">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="ad3eb-313">İşte, hello kod toomake Öngörüler ve çizim hello ROC eğrisi.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-313">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


<span data-ttu-id="ad3eb-314">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-314">**OUTPUT:**</span></span>

![Lojistik regresyon ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="ad3eb-316">Rastgele orman sınıflandırma</span><span class="sxs-lookup"><span data-stu-id="ad3eb-316">Random forest classification</span></span>
<span data-ttu-id="ad3eb-317">Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın tahmin rastgele orman modeli kaydedin gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-317">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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

<span data-ttu-id="ad3eb-318">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-318">**OUTPUT:**</span></span>

<span data-ttu-id="ad3eb-319">ROC alanında 0.985297691373 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="ad3eb-320">Hücre tooexecute geçen süre: 31.09 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-320">Time taken tooexecute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="ad3eb-321">Gradyan artırma ağaçları sınıflandırma</span><span class="sxs-lookup"><span data-stu-id="ad3eb-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="ad3eb-322">Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın tahmin bir gradyan artırma ağaçları modeli kaydedin gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-322">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
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


<span data-ttu-id="ad3eb-323">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-323">**OUTPUT:**</span></span>

<span data-ttu-id="ad3eb-324">ROC alanında 0.985297691373 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="ad3eb-325">Hücre tooexecute geçen süre: 19.76 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-325">Time taken tooexecute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="ad3eb-326">Regresyon modellerle ücreti dönüşleri ipucu tutarlarının tahmin etme</span><span class="sxs-lookup"><span data-stu-id="ad3eb-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="ad3eb-327">Bu bölümde, nasıl diğer ipucu özelliklerini temel alarak ücreti seyahat için ücretli hello ipucu hello miktarı tahmin etmeye hello regresyon görev için üç kullanım modelleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-327">This section shows how use three models for hello regression task of predicting hello amount of hello tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="ad3eb-328">sunulan hello model şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-328">hello models presented are:</span></span>

* <span data-ttu-id="ad3eb-329">Regularized doğrusal regresyon</span><span class="sxs-lookup"><span data-stu-id="ad3eb-329">Regularized linear regression</span></span>
* <span data-ttu-id="ad3eb-330">Rastgele orman</span><span class="sxs-lookup"><span data-stu-id="ad3eb-330">Random forest</span></span>
* <span data-ttu-id="ad3eb-331">Gradyan artırma ağaçları</span><span class="sxs-lookup"><span data-stu-id="ad3eb-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="ad3eb-332">Bu modeller hello girişte açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-332">These models were described in hello introduction.</span></span> <span data-ttu-id="ad3eb-333">Her model kod bölümünde oluşturma adımları ayrılır:</span><span class="sxs-lookup"><span data-stu-id="ad3eb-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="ad3eb-334">**Eğitim modeli** bir parametre kümesi ile verileri</span><span class="sxs-lookup"><span data-stu-id="ad3eb-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="ad3eb-335">**Model değerlendirme** ölçümlerle sınama veri kümesi üzerinde</span><span class="sxs-lookup"><span data-stu-id="ad3eb-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="ad3eb-336">**Model kaydetme** gelecekteki tüketimi için blob içinde</span><span class="sxs-lookup"><span data-stu-id="ad3eb-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="ad3eb-337">Doğrusal regresyon SGD ile</span><span class="sxs-lookup"><span data-stu-id="ad3eb-337">Linear regression with SGD</span></span>
<span data-ttu-id="ad3eb-338">Merhaba kod bu bölümdeki toouse özellikleri tootrain iyileştirme için stokastik gradyan düşüşü (SGD) kullanan bir doğrusal regresyon nasıl ölçeklendirilmesi gösterir ve tooscore, değerlendirmek ve Azure Blob Storage (WASB) hello modeli kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-338">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="ad3eb-339">Deneyimi bizim LinearRegressionWithSGD modellerin hello yakınsama sorunları olabilir ve parametreleri değiştirilen/dikkatle geçerli bir model almak için en iyi duruma getirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-339">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="ad3eb-340">Değişkenleri önemli ölçüde ölçeklendirmeyi yakınsama yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

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

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="ad3eb-341">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-341">**OUTPUT:**</span></span>

<span data-ttu-id="ad3eb-342">Katsayısını: [0.00457675809917,-0.0226314167349,-0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981,-0.000987181489428,-0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995,-0.00990211159703,-0.00637410344522, 0.545083566179,-0.536756072402, 0.0105762393099,-0.0130117577055, 0.0129304737772,-0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="ad3eb-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="ad3eb-343">Intercept: 0.853872718283</span><span class="sxs-lookup"><span data-stu-id="ad3eb-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="ad3eb-344">RMSE 1.24190115863 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="ad3eb-345">R sqr 0.608017146081 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="ad3eb-346">Hücre tooexecute geçen süre: 58.42 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-346">Time taken tooexecute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="ad3eb-347">Rastgele orman regresyon</span><span class="sxs-lookup"><span data-stu-id="ad3eb-347">Random Forest regression</span></span>
<span data-ttu-id="ad3eb-348">Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve hello NYC ücreti seyahat veri ipucu tutarını tahmin rastgele orman regresyon kaydedin gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-348">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts tip amount for hello NYC taxi trip data.</span></span>

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
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

<span data-ttu-id="ad3eb-349">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-349">**OUTPUT:**</span></span>

<span data-ttu-id="ad3eb-350">RMSE 0.891209218139 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="ad3eb-351">R sqr 0.759661334921 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="ad3eb-352">Hücre tooexecute geçen süre: 49.21 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-352">Time taken tooexecute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="ad3eb-353">Gradyan artırma ağaçları regresyon</span><span class="sxs-lookup"><span data-stu-id="ad3eb-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="ad3eb-354">Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve hello NYC ücreti seyahat veri ipucu tutarını tahmin bir gradyan artırma ağaçları modeli kaydedin gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-354">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="ad3eb-355">** Eğitme ve değerlendirme **</span><span class="sxs-lookup"><span data-stu-id="ad3eb-355">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="ad3eb-356">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-356">**OUTPUT:**</span></span>

<span data-ttu-id="ad3eb-357">RMSE 0.908473148639 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="ad3eb-358">R sqr 0.753835096681 =</span><span class="sxs-lookup"><span data-stu-id="ad3eb-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="ad3eb-359">Hücre tooexecute geçen süre: 34.52 saniye</span><span class="sxs-lookup"><span data-stu-id="ad3eb-359">Time taken tooexecute above cell: 34.52 seconds</span></span>

<span data-ttu-id="ad3eb-360">**Çizim**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-360">**Plot**</span></span>

<span data-ttu-id="ad3eb-361">*tmp_results* hello önceki hücre Hive tablo olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-361">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="ad3eb-362">Merhaba tablodan sonuçlar hello içine çıkarılır *sqlResults* çizdirmek için veri çerçeve.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-362">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="ad3eb-363">Merhaba kod aşağıdadır</span><span class="sxs-lookup"><span data-stu-id="ad3eb-363">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="ad3eb-364">Merhaba Jupyter server kullanarak hello kod tooplot hello verilerini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-364">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


<span data-ttu-id="ad3eb-365">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-365">**OUTPUT:**</span></span>

![Fiili-vs-tahmin-ipucu-tutarlar](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="ad3eb-367">Bellek nesneleri Temizle</span><span class="sxs-lookup"><span data-stu-id="ad3eb-367">Clean up objects from memory</span></span>
<span data-ttu-id="ad3eb-368">Kullanım `unpersist()` toodelete nesneleri bellekte önbelleğe alınmış.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-368">Use `unpersist()` toodelete objects cached in memory.</span></span>

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a><span data-ttu-id="ad3eb-369">Kullanım ve puanlama yönelik hello modellerinin kayıt depolama konumları</span><span class="sxs-lookup"><span data-stu-id="ad3eb-369">Record storage locations of hello models for consumption and scoring</span></span>
<span data-ttu-id="ad3eb-370">bağımsız bir veri kümesini tooconsume ve puanı hello açıklanan [puanı ve Spark yerleşik machine learning modellerini değerlendirme](machine-learning-data-science-spark-model-consumption.md) konu, gereksinim duyduğunuz toocopy ve bu dosya adları içeren kaydedilmiş hello modelleri burada hello oluşturulan Yapıştır Tüketim Jupyter not defteri.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-370">tooconsume and score an independent dataset described in hello [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need toocopy and paste these file names containing hello saved models created here into hello Consumption Jupyter notebook.</span></span> <span data-ttu-id="ad3eb-371">Burada, hello kod tooprint var. gerek duyduğunuz hello yolları toomodel dosyaları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-371">Here is hello code tooprint out hello paths toomodel files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="ad3eb-372">**ÇIKTI**</span><span class="sxs-lookup"><span data-stu-id="ad3eb-372">**OUTPUT**</span></span>

<span data-ttu-id="ad3eb-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="ad3eb-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="ad3eb-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="ad3eb-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="ad3eb-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="ad3eb-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="ad3eb-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="ad3eb-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="ad3eb-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="ad3eb-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="ad3eb-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="ad3eb-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="ad3eb-379">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="ad3eb-379">What's next?</span></span>
<span data-ttu-id="ad3eb-380">Spark Mllib'i hello ile regresyon ve sınıflandırma modelleri oluşturduğunuza göre hazır toolearn nasıl olan tooscore ve bu modeller değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-380">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span> <span data-ttu-id="ad3eb-381">Gelişmiş Veri keşfi ve çapraz doğrulama, hyper-parametre de dahil olmak üzere içine not defteri çekecek daha derin modelleme hello yerleştirmez ve değerlendirme model.</span><span class="sxs-lookup"><span data-stu-id="ad3eb-381">hello advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="ad3eb-382">**Model tüketimi:** toolearn nasıl tooscore ve bu konuda oluşturulan hello sınıflandırma ve regresyon modelleri değerlendirmek, bkz: [puanı ve Spark yerleşik makine öğrenimi modellerini değerlendirme](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="ad3eb-382">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="ad3eb-383">**Çapraz doğrulama ve hyperparameter Süpürme**: bkz [veri keşfi ve modelleme Spark ile Gelişmiş](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) modelleri nasıl olabilir üzerinde çapraz doğrulama ve parametre hyper Süpürme kullanılarak eğitilmiş</span><span class="sxs-lookup"><span data-stu-id="ad3eb-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

