---
<span data-ttu-id="9ecae-101">Başlık: aaa "Azure Analysis Services öğretici Ders 10: bölümleri oluşturma | Microsoft Docs"Açıklama: toocreate hello Azure Analysis Services öğretici projesinde nasıl bölümler açıklar.</span><span class="sxs-lookup"><span data-stu-id="9ecae-101">title: aaa"Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs" description: Describes how toocreate partitions in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="9ecae-102">Hizmetleri: analysis services documentationcenter: '' Yazar: minewiskan Yöneticisi: erikre Düzenleyicisi: '' etiketler: ''</span><span class="sxs-lookup"><span data-stu-id="9ecae-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="9ecae-103">MS.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get-makalesi ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="9ecae-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="9ecae-104">10. Ders: Bölüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ecae-104">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="9ecae-105">Bu ders, işlenen (yenilendi) bağımsız olarak diğer bölümler olabilecek daha küçük mantıksal parçalara bölümleri toodivide hello Factınternetsales tablosunda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ecae-105">In this lesson, you create partitions toodivide hello FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="9ecae-106">Varsayılan olarak, tüm Merhaba tablonun sütunları ve satırları içeren bir bölüm, modele dahil her tablo sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9ecae-106">By default, every table you include in your model has one partition, which includes all hello table’s columns and rows.</span></span> <span data-ttu-id="9ecae-107">Merhaba Factınternetsales tablosunda için yıla göre toodivide hello veri istiyoruz; bir bölüm her Merhaba tablonun beş yıl.</span><span class="sxs-lookup"><span data-stu-id="9ecae-107">For hello FactInternetSales table, we want toodivide hello data by year; one partition for each of hello table’s five years.</span></span> <span data-ttu-id="9ecae-108">Daha sonra her bölüm bağımsız olarak işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="9ecae-108">Each partition can then be processed independently.</span></span> <span data-ttu-id="9ecae-109">toolearn daha, fazla [bölümleri](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="9ecae-109">toolearn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="9ecae-110">Bu ders zaman toocomplete tahmini: **15 dakika**</span><span class="sxs-lookup"><span data-stu-id="9ecae-110">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="9ecae-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9ecae-111">Prerequisites</span></span>  
<span data-ttu-id="9ecae-112">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="9ecae-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="9ecae-113">Bu ders Hello görevleri gerçekleştirmeden önce hello önceki Ders tamamlandı: [Ders 9: hiyerarşileri oluşturma](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="9ecae-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="9ecae-114">Bölüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ecae-114">Create partitions</span></span>  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a><span data-ttu-id="9ecae-115">Merhaba Factınternetsales tablosunda toocreate bölümleri</span><span class="sxs-lookup"><span data-stu-id="9ecae-115">toocreate partitions in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="9ecae-116">Tablosal Model Gezgini’nde **Tablolar**’ı genişletin ve **FactInternetSales** > **Bölümler**’e sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ecae-116">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="9ecae-117">Bölüm Yöneticisi'nde **kopya**ve hello adını çok değiştirin**FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="9ecae-117">In Partition Manager, click **Copy**, and then change hello name too**FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="9ecae-118">Merhaba yıl 2010'da, belirli bir dönem içinde yalnızca bu satırları hello bölüm tooinclude istediğiniz çünkü hello sorgu ifadesi değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ecae-118">Because you want hello partition tooinclude only those rows within a certain period, for hello year 2010, you must modify hello query expression.</span></span>
  
4.  <span data-ttu-id="9ecae-119">Tıklatın **tasarım** tooopen sorgu Düzenleyicisi'ni ve hello ardından **FactInternetSales2010** sorgu.</span><span class="sxs-lookup"><span data-stu-id="9ecae-119">Click **Design** tooopen Query Editor, and then click hello **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="9ecae-120">Önizlemede hello aşağı hello tıklatın **OrderDate** sütun başlığını ve ardından **tarih filtreleri** > **arasında**.</span><span class="sxs-lookup"><span data-stu-id="9ecae-120">In preview, click hello down arrow in hello **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="9ecae-122">Hello filtre satırları iletişim kutusunda, **satırları göster: OrderDate**, bırakın **sonra veya eşittir**ve başlangıç tarihi alanına enter **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="9ecae-122">In hello Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in hello date field, enter **1/1/2010**.</span></span> <span data-ttu-id="9ecae-123">Hello bırakın **ve** seçili işleci seçip **önce**, başlangıç tarihi alanına enter **1/1/2011**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9ecae-123">Leave hello **And** operator selected, then select **is before**, then in hello date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="9ecae-125">Sorgu Düzenleyicisi’ndeki UYGULANAN ADIMLAR’da Filtrelenen Satırlar adlı başka bir adım göründüğüne dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9ecae-125">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="9ecae-126">Tooselect yalnızca sipariş tarihleri 2010'dan filtredir.</span><span class="sxs-lookup"><span data-stu-id="9ecae-126">This filter is tooselect only order dates from 2010.</span></span>

8.  <span data-ttu-id="9ecae-127">**İçeri Aktar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ecae-127">Click **Import**.</span></span>

    <span data-ttu-id="9ecae-128">Bölüm Yöneticisi'nde hello sorgu ifade artık ek bir satır filtre yan tümcesi içeriyorsa dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9ecae-128">In Partition Manager, notice hello query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="9ecae-130">Bu bölüm yalnızca hello veri hello OrderDate 2010 takvim yılı hello filtrelenmiş Satırları yan tümcesinde belirtilen hello olduğu bu satırı içermelidir bu bildirimi belirtir.</span><span class="sxs-lookup"><span data-stu-id="9ecae-130">This statement specifies this partition should include only hello data in those rows where hello OrderDate is in hello 2010 calendar year as specified in hello filtered rows clause.</span></span>  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a><span data-ttu-id="9ecae-131">toocreate hello 2011 yıl için bir bölüm</span><span class="sxs-lookup"><span data-stu-id="9ecae-131">toocreate a partition for hello 2011 year</span></span>  
  
1.  <span data-ttu-id="9ecae-132">Merhaba bölümleri listesinde hello tıklayın **FactInternetSales2010** bölüm oluşturduğunuz ve ardından **kopya**.</span><span class="sxs-lookup"><span data-stu-id="9ecae-132">In hello partitions list, click hello **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="9ecae-133">Merhaba bölüm adı çok değiştirme**FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="9ecae-133">Change hello partition name too**FactInternetSales2011**.</span></span> 

    <span data-ttu-id="9ecae-134">Sorgu Düzenleyici toocreate yeni bir filtre uygulanmış Satırları yan tümcesi toouse gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9ecae-134">You do not need toouse Query Editor toocreate a new filtered rows clause.</span></span> <span data-ttu-id="9ecae-135">Merhaba sorgu kopyasını 2010 için oluşturulduğundan toodo gereken tek şey hafif hello sorguda 2011 için değişiklik.</span><span class="sxs-lookup"><span data-stu-id="9ecae-135">Because you created a copy of hello query for 2010, all you need toodo is make a slight change in hello query for 2011.</span></span>
  
2.  <span data-ttu-id="9ecae-136">İçinde **sorgu ifadesi**için bu bölümü tooinclude yalnızca hello için satırları 2011 yıl sıralı, hello satırları filtre yan tümcesi ile Merhaba yıllarda değiştirin, **2011** ve **2012**, sırasıyla gibi:</span><span class="sxs-lookup"><span data-stu-id="9ecae-136">In **Query Expression**, in-order for this partition tooinclude only those rows for hello 2011 year, replace hello years in hello Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="9ecae-137">2012, 2013 ve 2014 için toocreate bölüm.</span><span class="sxs-lookup"><span data-stu-id="9ecae-137">toocreate partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="9ecae-138">2012, 2013 ve bu yıl hello yıl hello satırları filtre yan tümcesi tooinclude yalnızca satır içinde değiştirme 2014 bölümleri oluşturma hello önceki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="9ecae-138">Follow hello previous steps, creating partitions for 2012, 2013, and 2014, changing hello years in hello Filtered Rows clause tooinclude only rows for that year.</span></span> 
  

## <a name="delete-hello-factinternetsales-partition"></a><span data-ttu-id="9ecae-139">Merhaba Factınternetsales bölümü silin</span><span class="sxs-lookup"><span data-stu-id="9ecae-139">Delete hello FactInternetSales partition</span></span>
<span data-ttu-id="9ecae-140">Her yıl bölümleri sahip olduğunuza göre hello Factınternetsales bölüm silebilirsiniz; Çakışma işlem tüm bölümleri işlerken seçerken engelliyor.</span><span class="sxs-lookup"><span data-stu-id="9ecae-140">Now that you have partitions for each year, you can delete hello FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="toodelete-hello-factinternetsales-partition"></a><span data-ttu-id="9ecae-141">toodelete hello Factınternetsales bölümü</span><span class="sxs-lookup"><span data-stu-id="9ecae-141">toodelete hello FactInternetSales partition</span></span>
-  <span data-ttu-id="9ecae-142">Merhaba Factınternetsales bölüme tıklayın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="9ecae-142">Click hello FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="9ecae-143">İşlem bölümleri</span><span class="sxs-lookup"><span data-stu-id="9ecae-143">Process partitions</span></span>  
<span data-ttu-id="9ecae-144">Bölüm Yöneticisi'nde hello fark **son işlenen** sütun her hello yeni bölümler, oluşturduğunuz bu bölümler hiçbir zaman işlenen gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ecae-144">In Partition Manager, notice hello **Last Processed** column for each of hello new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="9ecae-145">Bölümler oluştururken, o bölümler bir işlem bölümleri veya işlem tablo işlemi toorefresh hello verileri çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ecae-145">When you create partitions, you should run a Process Partitions or Process Table operation toorefresh hello data in those partitions.</span></span>  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a><span data-ttu-id="9ecae-146">tooprocess hello Factınternetsales bölümleri</span><span class="sxs-lookup"><span data-stu-id="9ecae-146">tooprocess hello FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="9ecae-147">Tıklatın **Tamam** tooclose Bölüm Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="9ecae-147">Click **OK** tooclose Partition Manager.</span></span>  
  
2.  <span data-ttu-id="9ecae-148">Hello'ı tıklatın **Factınternetsales** tablo ve ardından hello **modeli** menü > **işlem** > **işlem bölümleri**.</span><span class="sxs-lookup"><span data-stu-id="9ecae-148">Click hello **FactInternetSales** table, then click hello **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="9ecae-149">Merhaba işlem bölümleri iletişim kutusunda doğrulayın **modu** çok ayarlanır**işlem varsayılan**.</span><span class="sxs-lookup"><span data-stu-id="9ecae-149">In hello Process Partitions dialog box, verify **Mode** is set too**Process Default**.</span></span>  
  
4.  <span data-ttu-id="9ecae-150">Hello Hello onay kutusunu seçin **işlem** her hello beş sütun bölümler oluşturduğunuz ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9ecae-150">Select hello checkbox in hello **Process** column for each of hello five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="9ecae-152">Kimliğe bürünme kimlik bilgilerini istenirse hello Windows kullanıcı adı ve parola Ders 2'de belirtilen girin.</span><span class="sxs-lookup"><span data-stu-id="9ecae-152">If you're prompted for Impersonation credentials, enter hello Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="9ecae-153">Merhaba **veri işleme** iletişim kutusu belirir ve her bölüm için işlem ayrıntılarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9ecae-153">hello **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="9ecae-154">Her bölüm için farklı sayıda satır aktarıldığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9ecae-154">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="9ecae-155">Her bölüm yalnızca bu satırları hello hello SQL deyimi WHERE yan tümcesinde belirtilen hello yıl içerir.</span><span class="sxs-lookup"><span data-stu-id="9ecae-155">Each partition includes only those rows for hello year specified in hello WHERE clause in hello SQL Statement.</span></span> <span data-ttu-id="9ecae-156">İşlem tamamlandığında, bir tane hello veri işleme iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="9ecae-156">When processing is finished, go ahead and close hello Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="9ecae-158">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="9ecae-158">What's next?</span></span>
<span data-ttu-id="9ecae-159">Git toohello sonraki Ders: [Ders 11: roller oluşturmak](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9ecae-159">Go toohello next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
