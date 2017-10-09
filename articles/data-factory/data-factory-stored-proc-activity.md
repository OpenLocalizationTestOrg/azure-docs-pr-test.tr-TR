---
title: "aaaSQL sunucu saklı yordam etkinliği"
description: "Merhaba SQL Server saklı yordam etkinliği tooinvoke bir saklı yordam bir Azure SQL Database veya Azure SQL veri ambarı Data Factory işlem hattı nasıl kullanabileceğinizi öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="9985b-103">SQL Server saklı yordam etkinliği</span><span class="sxs-lookup"><span data-stu-id="9985b-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="9985b-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="9985b-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="9985b-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="9985b-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="9985b-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="9985b-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="9985b-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="9985b-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="9985b-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="9985b-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="9985b-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9985b-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="9985b-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9985b-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="9985b-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9985b-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="9985b-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="9985b-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="9985b-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="9985b-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="9985b-114">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9985b-114">Overview</span></span>
<span data-ttu-id="9985b-115">Veri fabrikasında veri dönüştürme etkinlikleri kullanma [ardışık düzen](data-factory-create-pipelines.md) Öngörüler ve öngörü içine tootransform ve işlem ham verileri.</span><span class="sxs-lookup"><span data-stu-id="9985b-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) tootransform and process raw data into predictions and insights.</span></span> <span data-ttu-id="9985b-116">Merhaba saklı yordam etkinliği, veri fabrikası destekleyen hello dönüştürme etkinlikleri biridir.</span><span class="sxs-lookup"><span data-stu-id="9985b-116">hello Stored Procedure Activity is one of hello transformation activities that Data Factory supports.</span></span> <span data-ttu-id="9985b-117">Bu makale üzerinde hello derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve veri fabrikası'nda desteklenen hello dönüştürme etkinliklerinin genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="9985b-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="9985b-118">Kuruluşunuzdaki veya bir Azure sanal makinesini (VM) bir saklı yordam veri aşağıdaki hello birinde depolar hello saklı yordam etkinliği tooinvoke kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9985b-118">You can use hello Stored Procedure Activity tooinvoke a stored procedure in one of hello following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="9985b-119">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9985b-119">Azure SQL Database</span></span>
- <span data-ttu-id="9985b-120">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="9985b-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="9985b-121">SQL Server veritabanı.</span><span class="sxs-lookup"><span data-stu-id="9985b-121">SQL Server Database.</span></span>  <span data-ttu-id="9985b-122">SQL Server kullanıyorsanız, veri yönetimi ağ geçidi üzerinde aynı ana veritabanı hello veya ayrı bir makineye erişim toohello veritabanı olan makine hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9985b-122">If you are using SQL Server, install Data Management Gateway on hello same machine that hosts hello database or on a separate machine that has access toohello database.</span></span> <span data-ttu-id="9985b-123">Veri Yönetimi ağ geçidi, veri bağlayan bir bileşen şirket içi/açma Azure VM bulut Hizmetleri ile güvenli ve yönetilen bir şekilde kaynakları ' dir.</span><span class="sxs-lookup"><span data-stu-id="9985b-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="9985b-124">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="9985b-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9985b-125">Azure SQL Database veya SQL Server veri kopyalama işlemi sırasında hello yapılandırabilirsiniz **SqlSink** kopyalama etkinliği tooinvoke hello kullanarak bir saklı yordam içinde **sqlWriterStoredProcedureName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9985b-125">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="9985b-126">Daha fazla bilgi için bkz: [çağırma kopyalama etkinliği bir saklı yordamdan](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="9985b-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="9985b-127">Bağlayıcı makaleler hello özelliği hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9985b-127">For details about hello property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="9985b-128">Kopyalama etkinliği kullanarak bir Azure SQL Data Warehouse'a veri kopyalama sırasında bir saklı yordam çağırma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9985b-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="9985b-129">Ancak SQL Data Warehouse hello saklı yordam etkinliği tooinvoke bir saklı yordam kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9985b-129">But, you can use hello stored procedure activity tooinvoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="9985b-130">Azure SQL Database veya SQL Server veya Azure SQL Data Warehouse veri kopyalama işlemi sırasında yapılandırabileceğiniz **SqlSource** kopyalama etkinliği tooinvoke bir saklı yordam tooread veri hello kullanarak hello kaynak veritabanından içinde  **sqlReaderStoredProcedureName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9985b-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="9985b-131">Bağlayıcı makaleler hello daha fazla bilgi için bkz: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL veri ambarı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="9985b-131">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="9985b-132">izlenecek yol kullandığı aşağıdaki hello ardışık düzen tooinvoke bir Azure SQL veritabanındaki bir saklı yordam içinde saklı yordam etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="9985b-132">hello following walkthrough uses hello Stored Procedure Activity in a pipeline tooinvoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="9985b-133">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="9985b-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="9985b-134">Örnek tablo ve saklı yordam</span><span class="sxs-lookup"><span data-stu-id="9985b-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="9985b-135">Merhaba aşağıdaki oluşturma **tablo** SQL Server Management Studio veya tanımanız başka bir araç kullanarak, Azure SQL veritabanındaki.</span><span class="sxs-lookup"><span data-stu-id="9985b-135">Create hello following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="9985b-136">Merhaba datetimestamp hello tarih ve saat hello karşılık gelen kimliği oluşturulduğunda bir sütundur.</span><span class="sxs-lookup"><span data-stu-id="9985b-136">hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="9985b-137">Kimliği tanımlanan hello benzersiz ve hello datetimestamp sütun hello tarih ve saat hello karşılık gelen kimliği ne zaman oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9985b-137">Id is hello unique identified and hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>
    
    ![Örnek veriler](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="9985b-139">Bu örnekte, depolanan hello bir Azure SQL veritabanı'nda bir yordamdır.</span><span class="sxs-lookup"><span data-stu-id="9985b-139">In this sample, hello stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="9985b-140">Merhaba yaklaşım Hello saklı yordamı bir Azure SQL Data Warehouse hem de SQL Server veritabanı varsa, benzer.</span><span class="sxs-lookup"><span data-stu-id="9985b-140">If hello stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, hello approach is similar.</span></span> <span data-ttu-id="9985b-141">SQL Server veritabanı için yüklemeniz gereken bir [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="9985b-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="9985b-142">Merhaba aşağıdaki oluşturma **saklı yordamı** toohello içinde veri ekleyen **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="9985b-142">Create hello following **stored procedure** that inserts data in toohello **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="9985b-143">**Ad** ve **büyük/küçük harf** Merhaba parametre (Bu örnekte DateTime) hello ardışık düzen/JSON etkinliğinde belirtilen parametresi eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="9985b-143">**Name** and **casing** of hello parameter (DateTime in this example) must match that of parameter specified in hello pipeline/activity JSON.</span></span> <span data-ttu-id="9985b-144">İçinde saklı yordamı tanımı Merhaba, emin  **@**  hello parametresi için bir önek olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9985b-144">In hello stored procedure definition, ensure that **@** is used as a prefix for hello parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="9985b-145">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="9985b-145">Create a data factory</span></span>
1. <span data-ttu-id="9985b-146">Çok oturum[Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9985b-146">Log in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9985b-147">Tıklatın **yeni** hello sol menüsünde **Intelligence + analiz**, tıklatıp **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="9985b-147">Click **NEW** on hello left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Yeni veri fabrikası](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="9985b-149">Merhaba, **yeni data factory** dikey penceresinde girin **SProcDF** hello adı için.</span><span class="sxs-lookup"><span data-stu-id="9985b-149">In hello **New data factory** blade, enter **SProcDF** for hello Name.</span></span> <span data-ttu-id="9985b-150">Azure Data Factory adları **genel benzersiz**.</span><span class="sxs-lookup"><span data-stu-id="9985b-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="9985b-151">Sizin adınızla tooenable hello başarılı oluşturulmasını hello Fabrika hello veri fabrikasının tooprefix hello adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="9985b-151">You need tooprefix hello name of hello data factory with your name, tooenable hello successful creation of hello factory.</span></span>

   ![Yeni veri fabrikası](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="9985b-153">Seçin, **Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="9985b-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="9985b-154">İçin **kaynak grubu**, aşağıdaki adımları hello birini yapın:</span><span class="sxs-lookup"><span data-stu-id="9985b-154">For **Resource Group**, do one of hello following steps:</span></span>
   1. <span data-ttu-id="9985b-155">Tıklatın **Yeni Oluştur** ve hello kaynak grubu için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="9985b-155">Click **Create new** and enter a name for hello resource group.</span></span>
   2. <span data-ttu-id="9985b-156">Tıklatın **var olanı kullan** ve varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="9985b-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="9985b-157">Select hello **konumu** hello veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="9985b-157">Select hello **location** for hello data factory.</span></span>
7. <span data-ttu-id="9985b-158">Seçin **PIN toodashboard** böylece hello panosunda oturum sonraki açışınızda hello veri fabrikası görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9985b-158">Select **Pin toodashboard** so that you can see hello data factory on hello dashboard next time you log in.</span></span>
8. <span data-ttu-id="9985b-159">Tıklatın **oluşturma** hello üzerinde **yeni data factory** dikey.</span><span class="sxs-lookup"><span data-stu-id="9985b-159">Click **Create** on hello **New data factory** blade.</span></span>
9. <span data-ttu-id="9985b-160">Hello oluşturulmakta hello veri fabrikası gördüğünüz **Pano** hello Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9985b-160">You see hello data factory being created in hello **dashboard** of hello Azure portal.</span></span> <span data-ttu-id="9985b-161">Merhaba veri fabrikası başarıyla oluşturulduktan sonra gösterir hello veri fabrikası sayfasına bakın hello hello data Factory içeriği.</span><span class="sxs-lookup"><span data-stu-id="9985b-161">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![Data Factory giriş sayfası](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="9985b-163">Bir Azure SQL bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="9985b-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="9985b-164">Merhaba veri fabrikası oluşturduktan sonra içeren hello sampletable tablo ve sp_sample depolanan yordamı, tooyour veri fabrikası Azure SQL veritabanınızı bağlanan Azure SQL bağlı hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9985b-164">After creating hello data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains hello sampletable table and sp_sample stored procedure, tooyour data factory.</span></span>

1. <span data-ttu-id="9985b-165">Tıklatın **yazar ve dağıtma** hello üzerinde **Data Factory** dikey **SProcDF** toolaunch hello Data Factory Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="9985b-165">Click **Author and deploy** on hello **Data Factory** blade for **SProcDF** toolaunch hello Data Factory Editor.</span></span>
2. <span data-ttu-id="9985b-166">Tıklatın **yeni veri deposu** hello komut çubuğu ve seçin **Azure SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="9985b-166">Click **New data store** on hello command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="9985b-167">Hizmeti hello Düzenleyicisi'nde hello Azure SQL oluşturmak için JSON betiği bağlı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9985b-167">You should see hello JSON script for creating an Azure SQL linked service in hello editor.</span></span>

   ![Yeni veri deposu](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="9985b-169">Hello JSON betiği, aşağıdaki değişiklikler hello olun:</span><span class="sxs-lookup"><span data-stu-id="9985b-169">In hello JSON script, make hello following changes:</span></span>

   1. <span data-ttu-id="9985b-170">Değiştir `<servername>` Azure SQL veritabanı sunucunuzun hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="9985b-170">Replace `<servername>` with hello name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="9985b-171">Değiştir `<databasename>` içinde oluşturduğunuz hello tablo ve hello hello veritabanıyla saklı yordamı.</span><span class="sxs-lookup"><span data-stu-id="9985b-171">Replace `<databasename>` with hello database in which you created hello table and hello stored procedure.</span></span>
   3. <span data-ttu-id="9985b-172">Değiştir `<username@servername>` hello kullanıcı erişimi toohello veritabanı olan bir hesap ile.</span><span class="sxs-lookup"><span data-stu-id="9985b-172">Replace `<username@servername>` with hello user account that has access toohello database.</span></span>
   4. <span data-ttu-id="9985b-173">Değiştir `<password>` hello hello kullanıcı hesabının parolasını ile.</span><span class="sxs-lookup"><span data-stu-id="9985b-173">Replace `<password>` with hello password for hello user account.</span></span>

      ![Yeni veri deposu](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="9985b-175">toodeploy Merhaba bağlantılı hizmeti,'ı tıklatın **dağıtma** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="9985b-175">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="9985b-176">Merhaba solda görüntülemek hello AzureSqlLinkedService hello ağacında gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="9985b-176">Confirm that you see hello AzureSqlLinkedService in hello tree view on hello left.</span></span>

    ![bağlantılı hizmet bulunduğu ağaç görünümü](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="9985b-178">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9985b-178">Create an output dataset</span></span>
<span data-ttu-id="9985b-179">Merhaba saklı yordamı olsa bile bir çıkış veri kümesi için bir saklı yordam etkinliği herhangi bir veri üretmez belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9985b-179">You must specify an output dataset for a stored procedure activity even if hello stored procedure does not produce any data.</span></span> <span data-ttu-id="9985b-180">Buna ait hello hello zamanlama hello etkinlik (ne sıklıkta hello etkinlik - saatlik çalıştırılır, günlük, vb.) sürücüleri veri kümesi çıkışını olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="9985b-180">That's because it's hello output dataset that drives hello schedule of hello activity (how often hello activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="9985b-181">Merhaba çıktı veri kümesi kullanmalısınız bir **bağlantılı hizmeti** tooan Azure SQL Database veya bir Azure SQL Data Warehouse veya SQL Server veritabanı istediğiniz saklı yordam toorun hello başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="9985b-181">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="9985b-182">Merhaba çıktı veri kümesi hello saklı yordamın sonraki işleme biçimini toopass hello sonuç olarak başka bir etkinlik tarafından kullanılabileceği ([etkinlikleri zincirleme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello ardışık düzeninde.</span><span class="sxs-lookup"><span data-stu-id="9985b-182">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="9985b-183">Ancak, veri fabrikası otomatik olarak bir saklı yordam toothis dataset hello çıktısını yazmaz.</span><span class="sxs-lookup"><span data-stu-id="9985b-183">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="9985b-184">Bu, çıktı veri kümesi noktalarına hello o yazma tooa SQL tablosu hello saklı yordamı olur.</span><span class="sxs-lookup"><span data-stu-id="9985b-184">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="9985b-185">Bazı durumlarda, hello çıktı veri kümesi olabilir bir **kukla dataset** (gerçekten hello çıktısını tutmaz tooa tablo işaret eden bir veri kümesi saklı yordamı).</span><span class="sxs-lookup"><span data-stu-id="9985b-185">In some cases, hello output dataset can be a **dummy dataset** (a dataset that points tooa table that does not really hold output of hello stored procedure).</span></span> <span data-ttu-id="9985b-186">Hello çalıştırmak için toospecify hello zamanlama depolanan yordam etkinliği yalnızca kukla bu veri kümesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9985b-186">This dummy dataset is used only toospecify hello schedule for running hello stored procedure activity.</span></span> 

1. <span data-ttu-id="9985b-187">Düğmeyi görmüyorsanız araç çubuğunda **... Daha fazla** hello araç çubuğundan, **yeni veri kümesi**, tıklatıp **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="9985b-187">Click **... More** on hello toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="9985b-188">**Yeni veri kümesi** hello komut çubuğu ve select **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="9985b-188">**New dataset** on hello command bar and select **Azure SQL**.</span></span>

    ![bağlantılı hizmet bulunduğu ağaç görünümü](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="9985b-190">JSON betiği toohello JSON Düzenleyicisi'nde aşağıdaki hello kopyalayıp yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="9985b-190">Copy/paste hello following JSON script in toohello JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="9985b-191">toodeploy dataset Merhaba, tıklatın **dağıtma** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="9985b-191">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="9985b-192">Merhaba dataset hello ağaç görünümünde gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="9985b-192">Confirm that you see hello dataset in hello tree view.</span></span>

    ![Bağlı hizmetlerin bulunduğu ağaç görünümü](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="9985b-194">SqlServerStoredProcedure etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9985b-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="9985b-195">Şimdi, saklı yordam etkinliği ile işlem hattı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="9985b-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="9985b-196">Merhaba aşağıdaki özelliklere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="9985b-196">Notice hello following properties:</span></span> 

- <span data-ttu-id="9985b-197">Merhaba **türü** özelliği çok ayarlanmış**SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="9985b-197">hello **type** property is set too**SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="9985b-198">Merhaba **storedProcedureName** türü özellikleri ayarlanmış çok**sp_sample** (Merhaba adını saklı yordamı).</span><span class="sxs-lookup"><span data-stu-id="9985b-198">hello **storedProcedureName** in type properties is set too**sp_sample** (name of hello stored procedure).</span></span>
- <span data-ttu-id="9985b-199">Merhaba **storedProcedureParameters** bölüm adlı bir parametre içeren **saniyeyi tarih /**.</span><span class="sxs-lookup"><span data-stu-id="9985b-199">hello **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="9985b-200">Ad ve büyük/küçük harf hello parametresinin json'da hello adını ve büyük/küçük harf hello saklı yordamı tanımında hello parametresinin eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="9985b-200">Name and casing of hello parameter in JSON must match hello name and casing of hello parameter in hello stored procedure definition.</span></span> <span data-ttu-id="9985b-201">Bir parametre için null başarılı olursa hello sözdizimini kullanın: `"param1": null` (tüm küçük harf).</span><span class="sxs-lookup"><span data-stu-id="9985b-201">If you need pass null for a parameter, use hello syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="9985b-202">Düğmeyi görmüyorsanız araç çubuğunda **... Daha fazla** hello komut çubuğu ve tıklatın **yeni işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="9985b-202">Click **... More** on hello command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="9985b-203">JSON parçacığı aşağıdaki hello kopyalayıp yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="9985b-203">Copy/paste hello following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="9985b-204">toodeploy hello ardışık tıklatın **dağıtma** hello araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="9985b-204">toodeploy hello pipeline, click **Deploy** on hello toolbar.</span></span>  

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="9985b-205">Merhaba işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="9985b-205">Monitor hello pipeline</span></span>
1. <span data-ttu-id="9985b-206">Tıklatın **X** tooclose Data Factory Düzenleyici dikey toonavigate toohello Data Factory dikey penceresine geri tıklatın ve **diyagramı**.</span><span class="sxs-lookup"><span data-stu-id="9985b-206">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Diyagram kutucuğu](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="9985b-208">Merhaba, **diyagram görünümü**hello ardışık düzen özetini görmek ve kullanılan veri kümelerine Bu öğretici.</span><span class="sxs-lookup"><span data-stu-id="9985b-208">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Diyagram kutucuğu](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="9985b-210">Merhaba dataset Hello diyagram görünümü, çift `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="9985b-210">In hello Diagram View, double-click hello dataset `sprocsampleout`.</span></span> <span data-ttu-id="9985b-211">Merhaba dilimi hazır durumda bakın.</span><span class="sxs-lookup"><span data-stu-id="9985b-211">You see hello slices in Ready state.</span></span> <span data-ttu-id="9985b-212">Merhaba başlangıç zamanı ve bitiş saati başlangıç JSON öğesinden arasındaki her bir saat dilimi oluşturduğundan beş dilimler olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9985b-212">There should be five slices because a slice is produced for each hour between hello start time and end time from hello JSON.</span></span>

    ![Diyagram kutucuğu](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="9985b-214">Bir dilim olduğunda **hazır** Çalıştır durumunda, bir `select * from sampletable` veri hello hello Azure SQL veritabanı tooverify sorgusu toohello tabloda hello saklı yordamı tarafından eklenir.</span><span class="sxs-lookup"><span data-stu-id="9985b-214">When a slice is in **Ready** state, run a `select * from sampletable` query against hello Azure SQL database tooverify that hello data was inserted in toohello table by hello stored procedure.</span></span>

   ![Çıktı verileri](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="9985b-216">Bkz: [hello işlem hattını izleme](data-factory-monitor-manage-pipelines.md) Azure Data Factory işlem hatlarını izleme hakkında ayrıntılı bilgi.</span><span class="sxs-lookup"><span data-stu-id="9985b-216">See [Monitor hello pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="9985b-217">Bir giriş veri kümesi belirtin</span><span class="sxs-lookup"><span data-stu-id="9985b-217">Specify an input dataset</span></span>
<span data-ttu-id="9985b-218">Merhaba kılavuzda saklı yordam etkinliği herhangi bir giriş veri kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="9985b-218">In hello walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="9985b-219">Bir giriş veri kümesi belirtirseniz, girdi veri kümesi hello dilimin (hazır durumda) kullanılabilir hale gelene kadar hello saklı yordam etkinliği çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9985b-219">If you specify an input dataset, hello stored procedure activity does not run until hello slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="9985b-220">Merhaba veri kümesi, dış bir veri kümesini olabilir (değil üretilen hello başka bir etkinliğin tarafından aynı ardışık düzen) ya da bir Yukarı Akış etkinliği (Bu etkinlik önce çalışır hello etkinliği) tarafından üretilen bir iç veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="9985b-220">hello dataset can be an external dataset (that is not produced by another activity in hello same pipeline) or an internal dataset that is produced by an upstream activity (hello activity that runs before this activity).</span></span> <span data-ttu-id="9985b-221">Merhaba saklı yordam etkinliği için birden çok giriş veri kümesi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9985b-221">You can specify multiple input datasets for hello stored procedure activity.</span></span> <span data-ttu-id="9985b-222">Bunu yaparsanız, yalnızca tüm hello girdi veri kümesi dilimleri (hazır durumda) kullanılabilir hello saklı yordam etkinliği çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="9985b-222">If you do so, hello stored procedure activity runs only when all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="9985b-223">Merhaba girdi veri kümesi hello saklı yordama parametre olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9985b-223">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="9985b-224">Başlangıç hello saklı yordam etkinliği önce yalnızca kullanılan toocheck hello bağımlılık vardır.</span><span class="sxs-lookup"><span data-stu-id="9985b-224">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="9985b-225">Diğer etkinliklerle zincirleme</span><span class="sxs-lookup"><span data-stu-id="9985b-225">Chaining with other activities</span></span>
<span data-ttu-id="9985b-226">Toochain bu etkinliği olmayan bir Yukarı Akış etkinliği istiyorsanız, bu etkinliğin bir giriş olarak hello Yukarı Akış etkinliği hello çıktısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="9985b-226">If you want toochain an upstream activity with this activity, specify hello output of hello upstream activity as an input of this activity.</span></span> <span data-ttu-id="9985b-227">Bunu yaptığınızda hello saklı yordam etkinliği hello Yukarı Akış etkinliği tamamlar ve hello çıkış veri kümesi hello Yukarı Akış etkinliği (hazır durumunda) kullanılabilir kadar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9985b-227">When you do so, hello stored procedure activity does not run until hello upstream activity completes and hello output dataset of hello upstream activity is available (in Ready status).</span></span> <span data-ttu-id="9985b-228">Birden çok Yukarı Akış etkinliği çıkış kümelerini hello saklı yordam etkinliği giriş veri kümeleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9985b-228">You can specify output datasets of multiple upstream activities as input datasets of hello stored procedure activity.</span></span> <span data-ttu-id="9985b-229">Yalnızca tüm hello girdi veri kümesi dilimler kullanılabilir hello saklı yordam etkinliği bunu yaptığınızda çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="9985b-229">When you do so, hello stored procedure activity runs only when all hello input dataset slices are available.</span></span>  

<span data-ttu-id="9985b-230">Aşağıdaki örneğine hello hello hello Kopyala etkinliğinin çıkışıdır: hello girişidir OutputDataset saklı yordam etkinliği.</span><span class="sxs-lookup"><span data-stu-id="9985b-230">In hello following example, hello output of hello copy activity is: OutputDataset, which is an input of hello stored procedure activity.</span></span> <span data-ttu-id="9985b-231">Bu nedenle, hello saklı yordam etkinliği hello kopyalama etkinliği tamamlar ve hello OutputDataset dilim (hazır durumda) kullanılabilir oluncaya kadar çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9985b-231">Therefore, hello stored procedure activity does not run until hello copy activity completes and hello OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="9985b-232">Birden çok giriş veri kümeleri belirtirseniz, tüm hello girdi veri kümesi dilimleri (hazır durumda) kullanılabilir oluncaya kadar hello saklı yordam etkinliği çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9985b-232">If you specify multiple input datasets, hello stored procedure activity does not run until all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="9985b-233">Merhaba giriş veri kümeleri doğrudan parametreleri toohello saklı yordam etkinliği kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9985b-233">hello input datasets cannot be used directly as parameters toohello stored procedure activity.</span></span> 

<span data-ttu-id="9985b-234">Etkinlikler zincirleme daha fazla bilgi için bkz: [bir ardışık düzende birden çok etkinlik](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="9985b-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="9985b-235">Benzer şekilde, toolink hello deposu yordam etkinliği ile **aşağı akış etkinlikleri** (Merhaba saklı yordam etkinliği tamamlandıktan sonra çalıştırılan hello etkinlikleri) belirtin hello çıkış veri kümesi hello saklı yordam etkinliği bir Merhaba ardışık düzen hello aşağı akış etkinliğinde giriş.</span><span class="sxs-lookup"><span data-stu-id="9985b-235">Similarly, toolink hello store procedure activity with **downstream activities** (hello activities that run after hello stored procedure activity completes), specify hello output dataset of hello stored procedure activity as an input of hello downstream activity in hello pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9985b-236">Azure SQL Database veya SQL Server veri kopyalama işlemi sırasında hello yapılandırabilirsiniz **SqlSink** kopyalama etkinliği tooinvoke hello kullanarak bir saklı yordam içinde **sqlWriterStoredProcedureName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9985b-236">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="9985b-237">Daha fazla bilgi için bkz: [çağırma kopyalama etkinliği bir saklı yordamdan](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="9985b-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="9985b-238">Bağlayıcı makaleler hello hello özelliği hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9985b-238">For details about hello property, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="9985b-239">Azure SQL Database veya SQL Server veya Azure SQL Data Warehouse veri kopyalama işlemi sırasında yapılandırabileceğiniz **SqlSource** kopyalama etkinliği tooinvoke bir saklı yordam tooread veri hello kullanarak hello kaynak veritabanından içinde  **sqlReaderStoredProcedureName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="9985b-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="9985b-240">Bağlayıcı makaleler hello daha fazla bilgi için bkz: [Azure SQL veritabanı](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL veri ambarı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="9985b-240">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="9985b-241">JSON biçimi</span><span class="sxs-lookup"><span data-stu-id="9985b-241">JSON format</span></span>
<span data-ttu-id="9985b-242">Bir saklı yordam etkinliği tanımlamak için hello JSON biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9985b-242">Here is hello JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="9985b-243">Aşağıdaki tablonun hello bu JSON özelliklerini açıklamaktadır:</span><span class="sxs-lookup"><span data-stu-id="9985b-243">hello following table describes these JSON properties:</span></span>

| <span data-ttu-id="9985b-244">Özellik</span><span class="sxs-lookup"><span data-stu-id="9985b-244">Property</span></span> | <span data-ttu-id="9985b-245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9985b-245">Description</span></span> | <span data-ttu-id="9985b-246">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9985b-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9985b-247">ad</span><span class="sxs-lookup"><span data-stu-id="9985b-247">name</span></span> | <span data-ttu-id="9985b-248">Merhaba etkinlik adı</span><span class="sxs-lookup"><span data-stu-id="9985b-248">Name of hello activity</span></span> |<span data-ttu-id="9985b-249">Evet</span><span class="sxs-lookup"><span data-stu-id="9985b-249">Yes</span></span> |
| <span data-ttu-id="9985b-250">açıklama</span><span class="sxs-lookup"><span data-stu-id="9985b-250">description</span></span> |<span data-ttu-id="9985b-251">Hangi hello etkinliği için kullanılan açıklayan metin</span><span class="sxs-lookup"><span data-stu-id="9985b-251">Text describing what hello activity is used for</span></span> |<span data-ttu-id="9985b-252">Hayır</span><span class="sxs-lookup"><span data-stu-id="9985b-252">No</span></span> |
| <span data-ttu-id="9985b-253">type</span><span class="sxs-lookup"><span data-stu-id="9985b-253">type</span></span> | <span data-ttu-id="9985b-254">Ayarlanmalıdır: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="9985b-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="9985b-255">Evet</span><span class="sxs-lookup"><span data-stu-id="9985b-255">Yes</span></span> |
| <span data-ttu-id="9985b-256">Girişleri</span><span class="sxs-lookup"><span data-stu-id="9985b-256">inputs</span></span> | <span data-ttu-id="9985b-257">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="9985b-257">Optional.</span></span> <span data-ttu-id="9985b-258">Bir giriş veri kümesi belirtirseniz, ('Hazır' durumunda) kullanılabilir olmalıdır Merhaba depolanan yordam etkinliği toorun.</span><span class="sxs-lookup"><span data-stu-id="9985b-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="9985b-259">Merhaba girdi veri kümesi hello saklı yordama parametre olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9985b-259">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="9985b-260">Başlangıç hello saklı yordam etkinliği önce yalnızca kullanılan toocheck hello bağımlılık vardır.</span><span class="sxs-lookup"><span data-stu-id="9985b-260">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> |<span data-ttu-id="9985b-261">Hayır</span><span class="sxs-lookup"><span data-stu-id="9985b-261">No</span></span> |
| <span data-ttu-id="9985b-262">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="9985b-262">outputs</span></span> | <span data-ttu-id="9985b-263">Bir çıkış veri kümesi için bir saklı yordam etkinliği belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9985b-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="9985b-264">Çıktı veri kümesi belirtir hello **zamanlama** hello için saklı yordam etkinliği (saatlik, haftalık, aylık, vb.).</span><span class="sxs-lookup"><span data-stu-id="9985b-264">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="9985b-265">Merhaba çıktı veri kümesi kullanmalısınız bir **bağlantılı hizmeti** tooan Azure SQL Database veya bir Azure SQL Data Warehouse veya SQL Server veritabanı istediğiniz saklı yordam toorun hello başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="9985b-265">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <br/><br/><span data-ttu-id="9985b-266">Merhaba çıktı veri kümesi hello saklı yordamın sonraki işleme biçimini toopass hello sonuç olarak başka bir etkinlik tarafından kullanılabileceği ([etkinlikleri zincirleme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello ardışık düzeninde.</span><span class="sxs-lookup"><span data-stu-id="9985b-266">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="9985b-267">Ancak, veri fabrikası otomatik olarak bir saklı yordam toothis dataset hello çıktısını yazmaz.</span><span class="sxs-lookup"><span data-stu-id="9985b-267">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="9985b-268">Bu, çıktı veri kümesi noktalarına hello o yazma tooa SQL tablosu hello saklı yordamı olur.</span><span class="sxs-lookup"><span data-stu-id="9985b-268">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <br/><br/><span data-ttu-id="9985b-269">Bazı durumlarda, hello çıktı veri kümesi olabilir bir **kukla dataset**, toospecify hello zamanlama hello çalıştırmak için depolanan yordam etkinliği yalnızca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9985b-269">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span> |<span data-ttu-id="9985b-270">Evet</span><span class="sxs-lookup"><span data-stu-id="9985b-270">Yes</span></span> |
| <span data-ttu-id="9985b-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="9985b-271">storedProcedureName</span></span> |<span data-ttu-id="9985b-272">Hello Azure SQL veritabanı veya çıktı tablosu kullanır hello hello bağlantılı hizmeti tarafından temsil edilen Azure SQL Data Warehouse veya SQL Server veritabanında depolanan hello yordamı Hello adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="9985b-272">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="9985b-273">Evet</span><span class="sxs-lookup"><span data-stu-id="9985b-273">Yes</span></span> |
| <span data-ttu-id="9985b-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="9985b-274">storedProcedureParameters</span></span> |<span data-ttu-id="9985b-275">Saklı yordam parametreleri için değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="9985b-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="9985b-276">Toopass parametresi için null ihtiyacınız varsa, hello sözdizimini kullanın: "param1": null (tüm küçük harf).</span><span class="sxs-lookup"><span data-stu-id="9985b-276">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="9985b-277">Bu özellik kullanma hakkında örnek toolearn aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="9985b-277">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="9985b-278">Hayır</span><span class="sxs-lookup"><span data-stu-id="9985b-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="9985b-279">Statik değer geçirme</span><span class="sxs-lookup"><span data-stu-id="9985b-279">Passing a static value</span></span>
<span data-ttu-id="9985b-280">Şimdi, şimdi 'örnek belge' adlı bir statik değeri içeren hello tabloda 'Senaryo' adlı başka bir sütun eklemeyi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9985b-280">Now, let’s consider adding another column named ‘Scenario’ in hello table containing a static value called ‘Document sample’.</span></span>

![Örnek veri 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="9985b-282">**Tablo:**</span><span class="sxs-lookup"><span data-stu-id="9985b-282">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="9985b-283">**Saklı yordam:**</span><span class="sxs-lookup"><span data-stu-id="9985b-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="9985b-284">Şimdi, hello geçirmek **senaryo** hello parametre ve hello değerinden saklı yordam etkinliği.</span><span class="sxs-lookup"><span data-stu-id="9985b-284">Now, pass hello **Scenario** parameter and hello value from hello stored procedure activity.</span></span> <span data-ttu-id="9985b-285">Merhaba **typeProperties** hello parçacığını aşağıdaki hello örnek görülüyor önceki bölümde:</span><span class="sxs-lookup"><span data-stu-id="9985b-285">hello **typeProperties** section in hello preceding sample looks like hello following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="9985b-286">**Data Factory veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="9985b-286">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="9985b-287">**Data Factory işlem hattı**</span><span class="sxs-lookup"><span data-stu-id="9985b-287">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```