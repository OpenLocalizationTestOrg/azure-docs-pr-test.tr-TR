---
title: Azure Machine Learning ile aaaAnalyze veri | Microsoft Docs
description: "Azure Machine Learning toobuild Tahmine dayalı machine learning Azure SQL veri ambarında depolanan verileri temel alan modeli kullanın."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="9de90-103">Azure Machine Learning ile veri çözümleme</span><span class="sxs-lookup"><span data-stu-id="9de90-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9de90-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="9de90-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="9de90-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9de90-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="9de90-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9de90-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="9de90-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="9de90-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="9de90-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="9de90-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="9de90-109">Bu öğretici, Azure Machine Learning toobuild Tahmine dayalı machine learning Azure SQL veri ambarında depolanan verileri temel alan modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="9de90-109">This tutorial uses Azure Machine Learning toobuild a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="9de90-110">Özellikle, bu Adventure Works ' hello bisiklet satış mağazası için hedeflenen bir pazarlama kampanyası oluşturur, varsa tahmin ederek çalışmasını bir müşteri büyük olasılıkla toobuy bir bisiklet veya değil.</span><span class="sxs-lookup"><span data-stu-id="9de90-110">Specifically, this builds a targeted marketing campaign for Adventure Works, hello bike shop, by predicting if a customer is likely toobuy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9de90-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9de90-111">Prerequisites</span></span>
<span data-ttu-id="9de90-112">toostep Bu öğreticide, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="9de90-112">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="9de90-113">AdventureWorksDW örnek verileri önceden yüklenmiş bir SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9de90-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="9de90-114">tooprovision Bu, bkz: [SQL Data Warehouse oluşturma] [ Create a SQL Data Warehouse] ve tooload hello örnek verileri seçin.</span><span class="sxs-lookup"><span data-stu-id="9de90-114">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="9de90-115">Bir veri ambarınız olmasına karşın örnek verileriniz yoksa [örnek verileri elle yükleyebilirsiniz][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="9de90-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-hello-data"></a><span data-ttu-id="9de90-116">1. Merhaba Veri Al</span><span class="sxs-lookup"><span data-stu-id="9de90-116">1. Get hello data</span></span>
<span data-ttu-id="9de90-117">Merhaba hello AdventureWorksDW veritabanında hello bulunan dbo.vTargetMail görünümündeki verilerdir.</span><span class="sxs-lookup"><span data-stu-id="9de90-117">hello data is in hello dbo.vTargetMail view in hello AdventureWorksDW database.</span></span> <span data-ttu-id="9de90-118">tooread bu veriler:</span><span class="sxs-lookup"><span data-stu-id="9de90-118">tooread this data:</span></span>

1. <span data-ttu-id="9de90-119">[Azure Machine Learning Studio][Azure Machine Learning studio]'da oturum açıp denemelerim seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9de90-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="9de90-120">**+NEW (+YENİ)** düğmesine tıklayıp **Blank Experiment (Boş Deneme)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="9de90-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="9de90-121">Denemeniz için bir ad girin: Hedeflenen Pazarlama.</span><span class="sxs-lookup"><span data-stu-id="9de90-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="9de90-122">Sürükleme hello **okuyucu** hello modülleri hello tuvale bölmesine modülünden.</span><span class="sxs-lookup"><span data-stu-id="9de90-122">Drag hello **Reader** module from hello modules pane into hello canvas.</span></span>
5. <span data-ttu-id="9de90-123">SQL Data Warehouse veritabanınıza Hello ayrıntılarını hello Özellikler bölmesinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="9de90-123">Specify hello details of your SQL Data Warehouse database in hello Properties pane.</span></span>
6. <span data-ttu-id="9de90-124">Merhaba veritabanını belirtin **sorgu** tooread hello verileri.</span><span class="sxs-lookup"><span data-stu-id="9de90-124">Specify hello database **query** tooread hello data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="9de90-125">Tıklayarak Hello denemeyi çalıştırın **çalıştırmak** hello deneme tuvalinin altında.</span><span class="sxs-lookup"><span data-stu-id="9de90-125">Run hello experiment by clicking **Run** under hello experiment canvas.</span></span>
<span data-ttu-id="9de90-126">![Merhaba denemeyi çalıştırın][1]</span><span class="sxs-lookup"><span data-stu-id="9de90-126">![Run hello experiment][1]</span></span>

<span data-ttu-id="9de90-127">Hello denemeyi çalıştırma işlemi başarıyla sonlandıktan sonra hello okuyucu modülü hello sonundaki hello çıkış bağlantı noktasına tıklayın ve seçin **Görselleştir** toosee hello alınan veri.</span><span class="sxs-lookup"><span data-stu-id="9de90-127">After hello experiment finishes running successfully, click hello output port at hello bottom of hello Reader module and select **Visualize** toosee hello imported data.</span></span>
<span data-ttu-id="9de90-128">![İçeri aktarılan verileri görüntüleme][3]</span><span class="sxs-lookup"><span data-stu-id="9de90-128">![View imported data][3]</span></span>

## <a name="2-clean-hello-data"></a><span data-ttu-id="9de90-129">2. Temiz hello veri</span><span class="sxs-lookup"><span data-stu-id="9de90-129">2. Clean hello data</span></span>
<span data-ttu-id="9de90-130">tooclean hello veri hello modelle ilgili olmayan bazı sütunları bırakın.</span><span class="sxs-lookup"><span data-stu-id="9de90-130">tooclean hello data, drop some columns that are not relevant for hello model.</span></span> <span data-ttu-id="9de90-131">toodo bu:</span><span class="sxs-lookup"><span data-stu-id="9de90-131">toodo this:</span></span>

1. <span data-ttu-id="9de90-132">Sürükleme hello **proje sütunları** hello tuvale modüle.</span><span class="sxs-lookup"><span data-stu-id="9de90-132">Drag hello **Project Columns** module into hello canvas.</span></span>
2. <span data-ttu-id="9de90-133">Tıklatın **başlatma Sütun seçiciyi** hangi sütunların toodrop istediğiniz hello Özellikler bölmesinde toospecify içinde.</span><span class="sxs-lookup"><span data-stu-id="9de90-133">Click **Launch column selector** in hello Properties pane toospecify which columns you wish toodrop.</span></span>
   <span data-ttu-id="9de90-134">![Proje Sütunları][4]</span><span class="sxs-lookup"><span data-stu-id="9de90-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="9de90-135">Şu iki sütunu dışlayın: CustomerAlternateKey ve GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="9de90-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="9de90-136">![Gereksiz sütunları kaldırma][5]</span><span class="sxs-lookup"><span data-stu-id="9de90-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-hello-model"></a><span data-ttu-id="9de90-137">3. Merhaba model oluşturma</span><span class="sxs-lookup"><span data-stu-id="9de90-137">3. Build hello model</span></span>
<span data-ttu-id="9de90-138">Biz hello veri 80-20 bölecek: %80 tootrain machine learning modelini ve % 20 tootest hello modeli.</span><span class="sxs-lookup"><span data-stu-id="9de90-138">We will split hello data 80-20: 80% tootrain a machine learning model and 20% tootest hello model.</span></span> <span data-ttu-id="9de90-139">Yapacağız hello "İki sınıflı" algoritmalardan bu ikili sınıflandırma sorunu için kullanın.</span><span class="sxs-lookup"><span data-stu-id="9de90-139">We will make use of hello “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="9de90-140">Sürükleme hello **bölünmüş** hello tuvale modüle.</span><span class="sxs-lookup"><span data-stu-id="9de90-140">Drag hello **Split** module into hello canvas.</span></span>
2. <span data-ttu-id="9de90-141">Merhaba ilk çıkış veri kümesinde hello Özellikler bölmesinde bulunan satırlar için kesir değerini 0,8 girin.</span><span class="sxs-lookup"><span data-stu-id="9de90-141">Enter 0.8 for Fraction of rows in hello first output dataset in hello Properties pane.</span></span>
   <span data-ttu-id="9de90-142">![Verileri eğitim ve test kümesi olarak bölme][6]</span><span class="sxs-lookup"><span data-stu-id="9de90-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="9de90-143">Sürükleme hello **iki-Class Boosted karar ağacı** hello tuvale modüle.</span><span class="sxs-lookup"><span data-stu-id="9de90-143">Drag hello **Two-Class Boosted Decision Tree** module into hello canvas.</span></span>
4. <span data-ttu-id="9de90-144">Sürükleme hello **Train Model** hello modüle tuvale ve hello girişleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="9de90-144">Drag hello **Train Model** module into hello canvas and specify hello inputs.</span></span> <span data-ttu-id="9de90-145">Ardından **başlatma Sütun seçiciyi** hello Özellikler bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="9de90-145">Then, click **Launch column selector** in hello Properties pane.</span></span>
   * <span data-ttu-id="9de90-146">İlk giriş: ML algoritması</span><span class="sxs-lookup"><span data-stu-id="9de90-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="9de90-147">İkinci giriş: veri tootrain hello algoritması üzerinde.</span><span class="sxs-lookup"><span data-stu-id="9de90-147">Second input: Data tootrain hello algorithm on.</span></span>
     <span data-ttu-id="9de90-148">![Merhaba Train Model modülünü bağlama][7]</span><span class="sxs-lookup"><span data-stu-id="9de90-148">![Connect hello Train Model module][7]</span></span>
5. <span data-ttu-id="9de90-149">Select hello **BikeBuyer** sütun toopredict hello gibi sütun.</span><span class="sxs-lookup"><span data-stu-id="9de90-149">Select hello **BikeBuyer** column as hello column toopredict.</span></span>
   <span data-ttu-id="9de90-150">![Sütun toopredict seçin][8]</span><span class="sxs-lookup"><span data-stu-id="9de90-150">![Select Column toopredict][8]</span></span>

## <a name="4-score-hello-model"></a><span data-ttu-id="9de90-151">4. Puan hello modeli</span><span class="sxs-lookup"><span data-stu-id="9de90-151">4. Score hello model</span></span>
<span data-ttu-id="9de90-152">Şimdi, biz nasıl hello modeli test verileri üzerindeki işlevini test edeceğiz.</span><span class="sxs-lookup"><span data-stu-id="9de90-152">Now, we will test how hello model performs on test data.</span></span> <span data-ttu-id="9de90-153">Biz hello algoritması kendi Seçtiğimiz daha iyi gerçekleştiren farklı algoritma toosee ile karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="9de90-153">We will compare hello algorithm of our choice with a different algorithm toosee which performs better.</span></span>

1. <span data-ttu-id="9de90-154">Sürükleme **Score Model** hello tuvale modüle.</span><span class="sxs-lookup"><span data-stu-id="9de90-154">Drag **Score Model** module into hello canvas.</span></span>
    <span data-ttu-id="9de90-155">İlk giriş: eğitilmiş model ikinci giriş: Test verileri ![puan hello modeli][9]</span><span class="sxs-lookup"><span data-stu-id="9de90-155">First input: Trained model Second input: Test data ![Score hello model][9]</span></span>
2. <span data-ttu-id="9de90-156">Sürükleme hello **iki sınıflı Bayes noktası makinesi** hello deneme tuvalinin içine.</span><span class="sxs-lookup"><span data-stu-id="9de90-156">Drag hello **Two-Class Bayes Point Machine** into hello experiment canvas.</span></span> <span data-ttu-id="9de90-157">Bu algoritma karşılaştırma toohello iki-Class Boosted karar ağacı nasıl gerçekleştireceğini karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="9de90-157">We will compare how this algorithm performs in comparison toohello Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="9de90-158">Kopyala ve Yapıştır hello modülleri Train Model ve Score Model hello tuvale.</span><span class="sxs-lookup"><span data-stu-id="9de90-158">Copy and Paste hello modules Train Model and Score Model in hello canvas.</span></span>
4. <span data-ttu-id="9de90-159">Sürükleme hello **Evaluate Model** hello tuvale toocompare hello iki algoritmaları modüle.</span><span class="sxs-lookup"><span data-stu-id="9de90-159">Drag hello **Evaluate Model** module into hello canvas toocompare hello two algorithms.</span></span>
5. <span data-ttu-id="9de90-160">**Çalıştırma** hello deneme.</span><span class="sxs-lookup"><span data-stu-id="9de90-160">**Run** hello experiment.</span></span>
   <span data-ttu-id="9de90-161">![Merhaba denemeyi çalıştırın][10]</span><span class="sxs-lookup"><span data-stu-id="9de90-161">![Run hello experiment][10]</span></span>
6. <span data-ttu-id="9de90-162">Merhaba Evaluate Model modülünün hello altındaki Hello çıkış bağlantı noktasına tıklayın ve Görselleştir'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9de90-162">Click hello output port at hello bottom of hello Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="9de90-163">![Değerlendirme sonuçlarını görselleştirme][11]</span><span class="sxs-lookup"><span data-stu-id="9de90-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="9de90-164">Merhaba Metrikler hello ROC eğrisi, duyarlık geri çekme diyagramı olan ve eğri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9de90-164">hello metrics provided are hello ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="9de90-165">Bu ölçümlere bakarak, ikinci bir hello daha iyi gerçekleştirilen hello birinci modelin görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="9de90-165">Looking at these metrics, we can see that hello first model performed better than hello second one.</span></span> <span data-ttu-id="9de90-166">toolook ne first modeli tahmin Merhaba, hello Score Model çıkış bağlantı noktasına tıklayın ve Görselleştir tıklatın hello adresindeki.</span><span class="sxs-lookup"><span data-stu-id="9de90-166">toolook at hello what hello first model predicted, click on output port of hello Score Model and click Visualize.</span></span>
<span data-ttu-id="9de90-167">![Puanlama sonuçlarını görselleştirme][12]</span><span class="sxs-lookup"><span data-stu-id="9de90-167">![Visualize score results][12]</span></span>

<span data-ttu-id="9de90-168">İki sütun daha tooyour test veri eklenen görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9de90-168">You will see two more columns added tooyour test dataset.</span></span>

* <span data-ttu-id="9de90-169">Puanlanmış olasılıklar: hello bir müşterinin bir bisiklet alıcısı olma olasılığı.</span><span class="sxs-lookup"><span data-stu-id="9de90-169">Scored Probabilities: hello likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="9de90-170">Puanlanmış etiketler: hello modeliyle – bisiklet Alıcısı (1) gerçekleştirilip hello sınıflandırması (0).</span><span class="sxs-lookup"><span data-stu-id="9de90-170">Scored Labels: hello classification done by hello model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="9de90-171">Etiketleme bu olasılık eşiği too50% ayarlanır ve ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="9de90-171">This probability threshold for labeling is set too50% and can be adjusted.</span></span>

<span data-ttu-id="9de90-172">Merhaba sütununu BikeBuyer (gerçek) hello skoru etiketler (tahmin) ile karşılaştırarak, ne kadar iyi hello modeli verdiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9de90-172">Comparing hello column BikeBuyer (actual) with hello Scored Labels (prediction), you can see how well hello model has performed.</span></span> <span data-ttu-id="9de90-173">Sonraki adımlarda bu modeli toomake tahminleri yeni müşteriler için kullanın ve bu modeli bir web hizmeti olarak yayımlamak veya sonuçları geri tooSQL veri ambarı yazma.</span><span class="sxs-lookup"><span data-stu-id="9de90-173">As next steps, you can use this model toomake predictions for new customers and publish this model as a web service or write results back tooSQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9de90-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9de90-174">Next steps</span></span>
<span data-ttu-id="9de90-175">Tahmine dayalı makine öğrenimi modelleri oluşturma hakkında daha fazla toolearn başvurmak çok[giriş tooMachine Azure üzerinde öğrenme][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="9de90-175">toolearn more about building predictive machine learning models, refer too[Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
