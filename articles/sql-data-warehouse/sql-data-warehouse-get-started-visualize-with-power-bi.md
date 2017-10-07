---
title: aaaVisualize SQL Data Warehouse verilerini Power BI Microsoft Azure ile
description: "Power BI ile SQL Data Warehouse verilerini görselleştirme"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="b99eb-103">Power BI ile verileri görselleştirme</span><span class="sxs-lookup"><span data-stu-id="b99eb-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b99eb-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="b99eb-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="b99eb-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b99eb-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="b99eb-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b99eb-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="b99eb-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="b99eb-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="b99eb-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="b99eb-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="b99eb-109">Bu öğretici şunların nasıl yapıldığını gösterir toouse Power BI tooconnect tooSQL veri ambarı ve birkaç temel görselleştirme oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="b99eb-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b99eb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b99eb-110">Prerequisites</span></span>
<span data-ttu-id="b99eb-111">toostep Bu öğreticide, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="b99eb-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="b99eb-112">SQL Data Warehouse hello AdventureWorksDW veritabanıyla önceden yüklendi.</span><span class="sxs-lookup"><span data-stu-id="b99eb-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="b99eb-113">tooprovision Bu, bkz: [SQL Data Warehouse oluşturma] [ Create a SQL Data Warehouse] ve tooload hello örnek verileri seçin.</span><span class="sxs-lookup"><span data-stu-id="b99eb-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="b99eb-114">Bir veri ambarınız olmasına karşın örnek verileriniz yoksa [örnek verileri elle yükleyebilirsiniz][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="b99eb-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="b99eb-115">1. Tooyour veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="b99eb-115">1. Connect tooyour database</span></span>
<span data-ttu-id="b99eb-116">Power BI tooopen ve tooyour AdventureWorksDW veritabanına bağlanın:</span><span class="sxs-lookup"><span data-stu-id="b99eb-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="b99eb-117">Merhaba içine oturum [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b99eb-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="b99eb-118">**SQL veritabanları** seçeneğine tıklayın ve AdventureWorks SQL Data Warehouse veritabanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="b99eb-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Veritabanınızı bulma][1]
3. <span data-ttu-id="b99eb-120">Merhaba 'Power bı'da Aç' düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b99eb-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Power BI düğmesi][2]
4. <span data-ttu-id="b99eb-122">Ardından veritabanınızın web adresinin görüntüleme hello SQL Data Warehouse bağlantı sayfası görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b99eb-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="b99eb-123">İleri'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b99eb-123">Click next.</span></span>
   
    ![Power BI bağlantısı][3]
5. <span data-ttu-id="b99eb-125">Azure SQL server kullanıcı adı ve parola girin ve tam olarak bağlı tooyour SQL Data Warehouse veritabanı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b99eb-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Power BI'da oturum açma][4]
6. <span data-ttu-id="b99eb-127">Power BI'da oturum açtıktan sonra sol dikey penceresinde hello hello AdventureWorksDW veri kümesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b99eb-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="b99eb-128">Bu hello veritabanı açar.</span><span class="sxs-lookup"><span data-stu-id="b99eb-128">This will open hello database.</span></span>
   
    ![Power BI AdventureWorksDW'yi açma][5]

## <a name="2-create-a-report"></a><span data-ttu-id="b99eb-130">2. Bir rapor oluşturun</span><span class="sxs-lookup"><span data-stu-id="b99eb-130">2. Create a report</span></span>
<span data-ttu-id="b99eb-131">Artık hazır toouse Power BI tooanalyze AdventureWorksDW örnek verilerinizi şunlardır.</span><span class="sxs-lookup"><span data-stu-id="b99eb-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="b99eb-132">tooperform hello analiz, AdventureWorksDW AggregateSales adlı bir görünüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b99eb-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="b99eb-133">Bu görünüm hello satış hello şirketin çözümlemek için anahtar ölçümleri hello bazılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="b99eb-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="b99eb-134">toocreate hello taraftaki alanlar bölmesinde toopostal kod göre satış tutarlarının bir haritasını hello AggregateSales görünümüne tooexpand'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b99eb-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="b99eb-135">Merhaba PostalCode ve SalesAmount sütunları tooselect tıklatın bunları.</span><span class="sxs-lookup"><span data-stu-id="b99eb-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![Power BI AggregateSales görünümünü seçme][6]
   
    <span data-ttu-id="b99eb-137">Power BI otomatik olarak bu verilerin coğrafi veriler olduğunu tanır ve verileri sizin için bir haritaya yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="b99eb-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Power BI haritası][7]
2. <span data-ttu-id="b99eb-139">Bu adımda müşteri geliri başına satış tutarını gösteren bir çubuk grafiği oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b99eb-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="b99eb-140">toocreate AggregateSales görünümüne gidin bu toohello genişletilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b99eb-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="b99eb-141">Merhaba SalesAmount alanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b99eb-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="b99eb-142">Merhaba Müşteri geliri alanını toohello sola sürükleyip eksene bırakın.</span><span class="sxs-lookup"><span data-stu-id="b99eb-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![Power BI eksen seçme][8]
   
    <span data-ttu-id="b99eb-144">Biz hello çubuk grafik hello sola taşındı.</span><span class="sxs-lookup"><span data-stu-id="b99eb-144">We moved hello bar chart over hello left.</span></span>
   
    ![Power BI çubuğu][9]
3. <span data-ttu-id="b99eb-146">Bu adımda, sipariş tarihi başına satış tutarını gösteren bir çizgi grafiği oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b99eb-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="b99eb-147">toocreate AggregateSales görünümüne gidin bu toohello genişletilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b99eb-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="b99eb-148">SalesAmount ve OrderDate öğelerine tıklayın</span><span class="sxs-lookup"><span data-stu-id="b99eb-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="b99eb-149">Merhaba görselleştirmeleri sütununda hello çizgi grafiği simgesine tıklayın; Bu hello ilk hello ikinci satırındaki içinde simgedir.</span><span class="sxs-lookup"><span data-stu-id="b99eb-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![Power BI çizgi grafiğini seçme][10]
   
    <span data-ttu-id="b99eb-151">Artık hello verilerin üç farklı görselleştirmesini gösteren bir rapora sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="b99eb-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![Power BI çizgi grafiği][11]

<span data-ttu-id="b99eb-153">**Dosya**'ya tıklayıp **Kaydet**'i seçerek ilerleme durumunuzu istediğiniz zaman kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b99eb-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b99eb-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b99eb-154">Next steps</span></span>
<span data-ttu-id="b99eb-155">Biz bazı zaman toowarm hello örnek verilerle verdiniz, nasıl çok bkz[geliştirmek][develop], [yük][load], veya [ geçiş][migrate].</span><span class="sxs-lookup"><span data-stu-id="b99eb-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="b99eb-156">Veya hello bakalım [Power BI Web sitesi][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="b99eb-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
