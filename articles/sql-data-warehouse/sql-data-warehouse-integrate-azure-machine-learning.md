---
title: SQL Data Warehouse ile Azure Machine Learning aaaUse | Microsoft Docs
description: "Çözüm geliştirmek üzere Azure SQL Data Warehouse ile Azure Machine Learning kullanma öğreticisi."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="d7862-103">SQL Data Warehouse ile Azure Machine Learning kullanın</span><span class="sxs-lookup"><span data-stu-id="d7862-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="d7862-104">Azure Machine Learning SQL Data Warehouse verilerinizi karşı toocreate Tahmine dayalı modelleri kullanın ve tüketmek hazır web Hizmetleri olarak yayımlama bir tam olarak yönetilen Tahmine dayalı analiz hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="d7862-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="d7862-105">Tahmine dayalı analiz hello temel bilgileri öğrenmek ve makine öğrenme okuyarak [giriş tooMachine Azure üzerinde öğrenme][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="d7862-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="d7862-106">Ardından nasıl toocreate, eğitme, Puanlama ve hello kullanarak bir makine öğrenimi modeline test öğrenebilirsiniz [oluşturma deneme öğretici][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="d7862-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="d7862-107">Bu makalede, öğreneceksiniz nasıl hello kullanarak aşağıdaki toodo hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="d7862-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="d7862-108">Veritabanı toocreate okuma verilerden eğitmek ve Tahmine dayalı bir modeli Puanlama</span><span class="sxs-lookup"><span data-stu-id="d7862-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="d7862-109">Veri tooyour veritabanı yazma</span><span class="sxs-lookup"><span data-stu-id="d7862-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="d7862-110">SQL veri ambarından veri okuma</span><span class="sxs-lookup"><span data-stu-id="d7862-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="d7862-111">Merhaba AdventureWorksDW veritabanında Ürün tablosundan biz verileri okur.</span><span class="sxs-lookup"><span data-stu-id="d7862-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="d7862-112">1. Adım</span><span class="sxs-lookup"><span data-stu-id="d7862-112">Step 1</span></span>
<span data-ttu-id="d7862-113">Tıklayarak yeni bir deneme başlatın + hello Machine Learning Studio penceresinin hello altındaki Yeni DENEMEYİ seçin ve ardından boş denemeler'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d7862-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="d7862-114">Select hello varsayılan hello tuvale hello başındaki ad denemeler ve toosomething anlamlı, örneğin, bir bisiklet fiyat tahmini yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="d7862-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="d7862-115">2. Adım</span><span class="sxs-lookup"><span data-stu-id="d7862-115">Step 2</span></span>
<span data-ttu-id="d7862-116">Veri kümelerinin hello paletindeki hello okuyucu modülü ve hello deneme tuvalinin hello solundaki modülleri arayın.</span><span class="sxs-lookup"><span data-stu-id="d7862-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="d7862-117">Merhaba modülü toohello deneme tuvaline sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="d7862-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="d7862-118">3. Adım</span><span class="sxs-lookup"><span data-stu-id="d7862-118">Step 3</span></span>
<span data-ttu-id="d7862-119">Merhaba okuyucu modülü seçin ve hello Özellikler bölmesinde doldurun.</span><span class="sxs-lookup"><span data-stu-id="d7862-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="d7862-120">Azure SQL veritabanı hello veri kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="d7862-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="d7862-121">Veritabanı sunucusu adı: tür hello sunucu adı.</span><span class="sxs-lookup"><span data-stu-id="d7862-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="d7862-122">Merhaba kullanabilirsiniz [Azure portal] [ Azure portal] toofind bu.</span><span class="sxs-lookup"><span data-stu-id="d7862-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="d7862-123">Veritabanı adı: yalnızca belirtilen hello sunucu bir veritabanı türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="d7862-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="d7862-124">Sunucu kullanıcı hesabı adı: hello veritabanı için erişim izinlerine sahip bir hesap türü hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="d7862-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="d7862-125">Sunucu kullanıcı hesabı parolası: sağlamak hello hello parolasını belirtilen kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="d7862-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="d7862-126">Herhangi bir sunucu sertifikayı kabul edin: tooskip verilerinizi okumadan önce hello site sertifikası gözden geçirmek istiyorsanız (daha az güvenli) bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="d7862-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="d7862-127">Veritabanı Sorgusu: tooread istediğiniz hello verileri tanımlayan bir SQL deyimi girin.</span><span class="sxs-lookup"><span data-stu-id="d7862-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="d7862-128">Bu durumda, biz sorgu aşağıdaki hello kullanarak Ürün tablosundan verileri okur.</span><span class="sxs-lookup"><span data-stu-id="d7862-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="d7862-129">4. Adım</span><span class="sxs-lookup"><span data-stu-id="d7862-129">Step 4</span></span>
1. <span data-ttu-id="d7862-130">Merhaba deneme tuvalinin altında Çalıştır tıklayarak Hello denemeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d7862-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="d7862-131">Merhaba deneme bittiğinde hello okuyucu modülü başarıyla tamamlandı yeşil onay işareti tooindicate sahip olur.</span><span class="sxs-lookup"><span data-stu-id="d7862-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="d7862-132">Ayrıca hello sağ üst köşesinde çalışma durumu tamamlandı hello dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d7862-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="d7862-133">toosee alınan verileri Merhaba, hello hello alt hello otomobil veri kümesinin çıkış bağlantı noktasına tıklayın ve görsel öğe seçin.</span><span class="sxs-lookup"><span data-stu-id="d7862-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="d7862-134">Oluşturmak, eğitmek ve bir modeli Puanlama</span><span class="sxs-lookup"><span data-stu-id="d7862-134">Create, train and score a model</span></span>
<span data-ttu-id="d7862-135">Şimdi bu veri kümesi için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d7862-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="d7862-136">Bir Model oluşturmak: verileri işlemek ve özellikleri tanımlar</span><span class="sxs-lookup"><span data-stu-id="d7862-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="d7862-137">Tren hello modeli: seçin ve bir öğrenme algoritmasını Uygula</span><span class="sxs-lookup"><span data-stu-id="d7862-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="d7862-138">Puan ve test hello modeli: yeni bir bisiklet fiyatını tahmin etme</span><span class="sxs-lookup"><span data-stu-id="d7862-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="d7862-139">toolearn nasıl toocreate, eğitme, Puanlama ve machine learning modelini kullanmak hello test hakkında daha fazla [oluşturma deneme öğretici][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="d7862-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="d7862-140">Veri tooAzure SQL veri ambarı yazma</span><span class="sxs-lookup"><span data-stu-id="d7862-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="d7862-141">Biz hello sonuç kümesi tooProductPriceForecast tablosundaki hello AdventureWorksDW veritabanında yazma.</span><span class="sxs-lookup"><span data-stu-id="d7862-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="d7862-142">1. Adım</span><span class="sxs-lookup"><span data-stu-id="d7862-142">Step 1</span></span>
<span data-ttu-id="d7862-143">Veri kümeleri hello paletini hello yazan modülünde ve hello deneme tuvalinin hello solundaki modülleri arayın.</span><span class="sxs-lookup"><span data-stu-id="d7862-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="d7862-144">Merhaba modülü toohello deneme tuvaline sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="d7862-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="d7862-145">2. Adım</span><span class="sxs-lookup"><span data-stu-id="d7862-145">Step 2</span></span>
<span data-ttu-id="d7862-146">Merhaba yazıcı modülü seçin ve hello Özellikler bölmesinde doldurun.</span><span class="sxs-lookup"><span data-stu-id="d7862-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="d7862-147">Azure SQL veritabanı veri hedef hello seçin.</span><span class="sxs-lookup"><span data-stu-id="d7862-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="d7862-148">Veritabanı sunucusu adı: tür hello sunucu adı.</span><span class="sxs-lookup"><span data-stu-id="d7862-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="d7862-149">Merhaba kullanabilirsiniz [Azure portal] [ Azure portal] toofind bu.</span><span class="sxs-lookup"><span data-stu-id="d7862-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="d7862-150">Veritabanı adı: yalnızca belirtilen hello sunucu bir veritabanı türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="d7862-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="d7862-151">Sunucu kullanıcı hesabı adı: hello veritabanı için yazma izinlerine sahip bir hesap türü hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="d7862-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="d7862-152">Sunucu kullanıcı hesabı parolası: sağlamak hello hello parolasını belirtilen kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="d7862-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="d7862-153">Herhangi bir sunucu sertifikası (güvensiz) kabul edin: tooview hello sertifika istemiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d7862-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="d7862-154">Kaydedilen sütunları toobe virgülle ayrılmış listesi: toooutput istediğiniz hello dataset ya da sonuç sütun listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7862-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="d7862-155">Veri tablosu adı: hello veri tablosu hello adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="d7862-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="d7862-156">Datatable sütunun virgülle ayrılmış listesini: hello yeni tabloda hello sütun adları toouse belirtin.</span><span class="sxs-lookup"><span data-stu-id="d7862-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="d7862-157">Merhaba sütun adları hello olanları hello kaynak veri kümesinde farklı olabilir, ancak liste gerekir hello hello çıkış tablosu için tanımladığınız aynı sayıda sütun burada.</span><span class="sxs-lookup"><span data-stu-id="d7862-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="d7862-158">SQL Azure işlem yazılan satır sayısı: Merhaba tooa SQL veritabanı tek bir işlemde yazılan satır sayısını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7862-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="d7862-159">3. Adım</span><span class="sxs-lookup"><span data-stu-id="d7862-159">Step 3</span></span>
1. <span data-ttu-id="d7862-160">Merhaba deneme tuvalinin altında Çalıştır tıklayarak Hello denemeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d7862-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="d7862-161">Merhaba deneme sona erdiğinde, tüm modüllerin başarıyla tamamlandı yeşil onay işareti tooindicate sahip olur.</span><span class="sxs-lookup"><span data-stu-id="d7862-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7862-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7862-162">Next steps</span></span>
<span data-ttu-id="d7862-163">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="d7862-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
