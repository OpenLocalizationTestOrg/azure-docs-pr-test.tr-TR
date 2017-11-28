---
<span data-ttu-id="d2659-101">Başlık: aaa "Azure Analysis Services öğretici Ders 2: veri alma | Microsoft Docs"Açıklama: Azure Analysis Services öğretici proje tooget ve içeri aktarma verileri nasıl hello açıklar.</span><span class="sxs-lookup"><span data-stu-id="d2659-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="d2659-102">Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''</span><span class="sxs-lookup"><span data-stu-id="d2659-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="d2659-103">MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="d2659-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="d2659-104">2. Ders: Verileri alma</span><span class="sxs-lookup"><span data-stu-id="d2659-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="d2659-105">Bu ders SSDT tooconnect toohello AdventureWorksDW2014 örnek veritabanı, verileri seçin, Önizleme ve filtre Veri Al kullanın ve sonra model çalışma alanınıza alın.</span><span class="sxs-lookup"><span data-stu-id="d2659-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="d2659-106">Verileri Al’ı kullanarak birçok farklı kaynaktaki verileri içeri aktarabilirsiniz: Azure SQL Veritabanı, Oracle, Sybase, OData Feed, Teradata, dosyalar ve daha fazlası.</span><span class="sxs-lookup"><span data-stu-id="d2659-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="d2659-107">Veriler bir Power Query M formül ifadesi kullanılarak da sorgulanabilir.</span><span class="sxs-lookup"><span data-stu-id="d2659-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="d2659-108">Bu ders zaman toocomplete tahmini: **10 dakika**</span><span class="sxs-lookup"><span data-stu-id="d2659-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="d2659-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d2659-109">Prerequisites</span></span>  
<span data-ttu-id="d2659-110">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="d2659-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="d2659-111">Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 1: yeni bir tablo modeli projesi oluşturmak](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="d2659-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="d2659-112">Bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d2659-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="d2659-113">toocreate bağlantı toohello AdventureWorksDW2014 veritabanı</span><span class="sxs-lookup"><span data-stu-id="d2659-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="d2659-114">Tablosal Model Gezgini'nde **Veri Kaynakları** > **Veri Kaynağından İçeri Aktar**’a sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d2659-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="d2659-115">Üzerinden bağlanan tooa veri kaynağına kılavuzları alma veri başlatır.</span><span class="sxs-lookup"><span data-stu-id="d2659-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="d2659-116">İçinde tablolu Model Gezgini görmüyorsanız, **Çözüm Gezgini**, çift **Model.bim** tooopen hello modeli hello Tasarımcısı'nda.</span><span class="sxs-lookup"><span data-stu-id="d2659-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="d2659-118">Verileri Al’da **Veritabanı** > **SQL Server Veritabanı** > **Bağlan**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d2659-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="d2659-119">Merhaba, **SQL Server veritabanı** iletişim, **Server**hello hello AdventureWorksDW2014 veritabanının yüklendiği hello sunucunun adını yazın ve ardından **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="d2659-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="d2659-120">İstendiğinde tooenter kimlik bilgileri, Analysis Services veri alırken ve verileri işlerken tooconnect toohello veri kaynağını kullanan toospecify hello kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="d2659-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="d2659-121">**Kimliğe Bürünme Modu**’nda **Hesap Kimliğine Bürün**’ü seçip kimlik bilgilerini girin ve **Bağlan**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d2659-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="d2659-122">Burada hello parola kullanım süresi sona ermiyor bir hesabı kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="d2659-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="d2659-124">Bir Windows kullanıcı hesabı ve parola kullanarak bağlanan tooa veri kaynağının hello en güvenli yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d2659-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="d2659-125">Merhaba Gezgini içinde seçin **AdventureWorksDW2014** veritabanı ve ardından **Tamam**. Merhaba bağlantı toohello veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d2659-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="d2659-126">Gezgini içinde tabloları aşağıdaki hello için onay kutusunu seçin hello: **DimCustomer**, **DimDate'i**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, ve **Factınternetsales**.</span><span class="sxs-lookup"><span data-stu-id="d2659-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="d2659-128">Tamam'a tıkladığınızda Sorgu Düzenleyicisi açılır.</span><span class="sxs-lookup"><span data-stu-id="d2659-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="d2659-129">Merhaba sonraki bölümde, yalnızca tooimport istediğiniz hello verileri seçin.</span><span class="sxs-lookup"><span data-stu-id="d2659-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="d2659-130">Merhaba tablo verileri filtreleme</span><span class="sxs-lookup"><span data-stu-id="d2659-130">Filter hello table data</span></span>  
<span data-ttu-id="d2659-131">Merhaba AdventureWorksDW2014 örnek veritabanındaki tablolarda modelinizde gerekli tooinclude olmayan veri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d2659-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="d2659-132">Mümkün olduğunda, gereksiz verileri toosave bellek içi alanı hello modeli tarafından kullanılan çıkış toofilter istiyor.</span><span class="sxs-lookup"><span data-stu-id="d2659-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="d2659-133">Bunu dağıtıldıktan sonra hello çalışma alanı veritabanı veya hello model veritabanı alındıktan olmayan bazı tablodan hello sütun filtre.</span><span class="sxs-lookup"><span data-stu-id="d2659-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="d2659-134">içe aktarmadan önce toofilter hello tablo verileri</span><span class="sxs-lookup"><span data-stu-id="d2659-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="d2659-135">Sorgu Düzenleyicisi'nde hello seçin **DimCustomer** tablo.</span><span class="sxs-lookup"><span data-stu-id="d2659-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="d2659-136">Bir görünümü hello veri kaynağı (AdventureWorksDWQ2014 örnek veritabanınızdaki) hello DimCustomer tablosunda yer alır.</span><span class="sxs-lookup"><span data-stu-id="d2659-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="d2659-137">Çoklu seçimi (Ctrl+tıklama) kullanarak **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**’ı seçin, sağ tıklayın ve **Sütunları Kaldır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d2659-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="d2659-139">Bu sütunlar için Hello değerleri değil ilgili tooInternet Satış Analiz olduğundan, bu sütunları yok gerek tooimport yoktur.</span><span class="sxs-lookup"><span data-stu-id="d2659-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="d2659-140">Gereksiz sütunların dışarıda bırakılması, modelinizin daha küçük ve daha verimli olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d2659-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="d2659-141">Her tablodaki sütunlar aşağıdaki hello kaldırarak tabloları kalan hello filtreleyin:</span><span class="sxs-lookup"><span data-stu-id="d2659-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="d2659-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="d2659-142">**DimDate**</span></span>
    
      |<span data-ttu-id="d2659-143">Sütun</span><span class="sxs-lookup"><span data-stu-id="d2659-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="d2659-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="d2659-144">DateKey</span></span>|  
      |<span data-ttu-id="d2659-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="d2659-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="d2659-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="d2659-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="d2659-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="d2659-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="d2659-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="d2659-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="d2659-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="d2659-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="d2659-150">Sütun</span><span class="sxs-lookup"><span data-stu-id="d2659-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="d2659-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="d2659-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="d2659-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="d2659-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="d2659-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="d2659-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="d2659-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="d2659-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="d2659-155">Sütun</span><span class="sxs-lookup"><span data-stu-id="d2659-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="d2659-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="d2659-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="d2659-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="d2659-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="d2659-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="d2659-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="d2659-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="d2659-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="d2659-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="d2659-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="d2659-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="d2659-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="d2659-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="d2659-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="d2659-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="d2659-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="d2659-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="d2659-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="d2659-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="d2659-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="d2659-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="d2659-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="d2659-167">Sütun</span><span class="sxs-lookup"><span data-stu-id="d2659-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="d2659-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="d2659-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="d2659-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="d2659-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="d2659-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="d2659-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="d2659-171">Sütun</span><span class="sxs-lookup"><span data-stu-id="d2659-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="d2659-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="d2659-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="d2659-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="d2659-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="d2659-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="d2659-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="d2659-175">Sütun</span><span class="sxs-lookup"><span data-stu-id="d2659-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="d2659-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="d2659-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="d2659-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="d2659-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="d2659-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="d2659-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="d2659-179"><a name="Import"></a>Seçili hello tablo ve sütun veri alın</span><span class="sxs-lookup"><span data-stu-id="d2659-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="d2659-180">Önizlemesi ve gereksiz verileri filtre göre hello kalan istediğiniz hello verileri içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2659-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="d2659-181">Merhaba sihirbaz tablolar arasındaki ilişkileri birlikte hello tablo verileri alır.</span><span class="sxs-lookup"><span data-stu-id="d2659-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="d2659-182">Yeni tablolar ve sütunlar hello modelinde oluşturulur ve filtre çıkışı verileri değil olması alınır.</span><span class="sxs-lookup"><span data-stu-id="d2659-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="d2659-183">Tablo ve sütun veri tooimport hello seçili</span><span class="sxs-lookup"><span data-stu-id="d2659-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="d2659-184">Seçimlerinizi gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="d2659-184">Review your selections.</span></span> <span data-ttu-id="d2659-185">Her şey yolundaysa **İçeri Aktar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d2659-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="d2659-186">Merhaba veri işleme iletişim, veri kaynağını çalışma veritabanınıza içeri aktarılan veriler hello durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d2659-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="d2659-188">**Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d2659-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="d2659-189">Model projenizi kaydetme</span><span class="sxs-lookup"><span data-stu-id="d2659-189">Save your model project</span></span>  
<span data-ttu-id="d2659-190">Toofrequently Kaydet modeli projenizi önemlidir.</span><span class="sxs-lookup"><span data-stu-id="d2659-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="d2659-191">toosave hello modeli projesi</span><span class="sxs-lookup"><span data-stu-id="d2659-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="d2659-192">**Dosya** > **Tümünü Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d2659-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="d2659-193">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="d2659-193">What's next?</span></span>
<span data-ttu-id="d2659-194">[3. Ders: Tarih Tablosu Olarak İşaretleme](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="d2659-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
